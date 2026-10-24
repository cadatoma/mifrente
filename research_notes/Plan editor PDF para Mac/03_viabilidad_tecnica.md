# Technical feasibility of a sandboxed Mac App Store PDF editor on Apple frameworks only (PDFKit, Vision, Core Graphics, ImageIO, Keychain), as of October 2026

Scope note: the plan being checked is `00_plan_original.txt` (19 Oct 2026, Rafael Vasquez). It says v1.0 needs 8–10 weeks part-time because "Apple ya resuelve la parte difícil (PDFKit y Vision)", targets macOS 14+, and uses no paid libraries. Context found during research: **macOS 27 has shipped by Oct 2026.** One plugin README refers to "macOS 27 Golden Gate" ([OCRmyPDF-AppleOCR](https://github.com/mkyt/OCRmyPDF-AppleOCR)), and an Apple Developer Forums thread discusses iOS 27.0 and a 27.2 beta ([thread 851708](https://developer.apple.com/forums/thread/851708)). Some sites could not be reached from this environment: macscripter.net, mjtsai.com, eclecticlight.co, telemetrydeck.com, qpdf.readthedocs.io and pdfium.googlesource.com. For those pages, only search-result snippets were available, and this is flagged where it matters.

---

## 1. OCR: producing a searchable PDF with an invisible text layer using Vision

### Takeaway
OCR in the sandbox is clearly feasible. The recognition step is the easy part. The hard part is building the invisible text layer correctly: per-word placement, horizontal scaling, rotated pages, and keeping annotations and links on rewritten pages. That is real engineering work, and Apple does not provide it as a public, documented API. PDFKit has an undocumented `saveTextFromOCROption` write option (macOS 13+). Prototype it first, because it could replace most of the custom work.

### Cited Findings
- **APIs available by OS version:**
  - `RecognizeTextRequest`, the new Swift-native Vision API, needs macOS 15.0+ ([Apple docs](https://developer.apple.com/documentation/vision/recognizetextrequest.md)).
  - `RecognizeDocumentsRequest` needs macOS 26.0+ ([Apple docs](https://developer.apple.com/documentation/vision/recognizedocumentsrequest.md)).
  - On macOS 14, the only option is the older `VNRecognizeTextRequest`. mac-ocr uses it and states a macOS 10.15+ requirement ([mac-ocr](https://github.com/privatenumber/mac-ocr)).
- **What `RecognizeDocumentsRequest` returns:** an array of `DocumentObservation` objects that give "document's structure grouped by words, lines, or paragraphs", plus tables and lists. It has `textRecognitionOptions` and `supportedRecognitionLanguages` ([Apple docs](https://developer.apple.com/documentation/vision/recognizedocumentsrequest.md); [WWDC25 session 272 "Read documents using the Vision framework"](https://developer.apple.com/videos/play/wwdc2025/272/)).
- **`RecognizeTextRequest` options:** `recognitionLevel` (accurate vs fast), `recognitionLanguages` ("in priority order"), `automaticallyDetectsLanguage`, `usesLanguageCorrection`, `customWords` and `minimumTextHeightFraction` ([Apple docs](https://developer.apple.com/documentation/vision/recognizetextrequest.md)).
- **Spanish support:** Spanish is supported. The revision 2 header comments say the accurate level supports "English, Chinese, Portuguese, French, Italian, German and Spanish", and the fast level supports the same list without Chinese. Apple recommends querying `supportedRecognitionLanguages(for:revision:)` at runtime instead of hard-coding the list ([Apple Developer Forums 121048](https://developer.apple.com/forums/thread/121048); [Apple "Recognizing text in images"](https://developer.apple.com/documentation/vision/recognizing-text-in-images.md)).
- **Multilingual and language-detection limits:** the OCRmyPDF-AppleOCR plugin documents the language list "as of macOS 27". It says OCR "for multilingual documents is **not supported**", and that automatic language detection (`und`) is not supported in `livetext` mode. It describes Apple Vision as having "excellent accuracy and speed compared to other on-device OCR engines such as Tesseract" ([OCRmyPDF-AppleOCR](https://github.com/mkyt/OCRmyPDF-AppleOCR)).
- **Text-layer pitfall shown by a real implementation:** the same plugin says OCRmyPDF's `fpdf2` renderer places the invisible layer wrongly on rotated text. On an ~8° rotated sample it produced "~147 pt font where `sandwich` uses ~15 pt". It also collapses vertical CJK lines. The recommended "sandwich" renderer keeps "rotation, text extent and font size … correct on skewed and rotated pages" ([OCRmyPDF-AppleOCR](https://github.com/mkyt/OCRmyPDF-AppleOCR)).
- **Open-source Swift reference (MIT):** mac-ocr is a native Swift CLI built on `VNRecognizeTextRequest`. It writes "invisible text drawn with Core Graphics + Core Text, placed word by word where Vision found each word". Other details from its README:
  - "Vision can miss small labels when it analyzes a full high-resolution page at once", so the tool adds a "partitioned" pass that splits large pages into regions. That pass is slower because Vision processes the regions serially.
  - Pages that already contain text are skipped by default.
  - Output goes to a temp file and is then replaced atomically.
  - Images without DPI metadata fall back to 72 DPI.

  ([mac-ocr](https://github.com/privatenumber/mac-ocr))
- **Built-in PDFKit OCR-on-save:** `PDFDocumentWriteOption.saveTextFromOCROption` exists and is available on macOS 13.0+. Apple's page has no description text ([Apple docs](https://developer.apple.com/documentation/pdfkit/pdfdocumentwriteoption/savetextfromocroption.md)). A MacScripter post says it is missing from the Objective-C docs but works from AppleScriptObjC. The same post says Preview on Sonoma/Sequoia exposes this as an "Embed text" export option. This comes from a search snippet; the page itself could not be fetched ([MacScripter](https://www.macscripter.net/t/how-to-ocr-scanned-pdf-using-pdfkit-on-macos-sonoma-or-sequoia/76915)).

### Inferences
- **Recommended pipeline (macOS 14/15 compatible):** for each page with no text layer:
  1. Rasterize the page at about 300 dpi, or extract its single image.
  2. Run `VNRecognizeTextRequest` / `RecognizeTextRequest` at `.accurate`, with `recognitionLanguages = [es-ES, en-US]` and language correction on.
  3. Use `VNRecognizedText.boundingBox(for:)` per word to get word boxes.
  4. Write a new page through a `CGContext` PDF context: draw the original page with `drawPDFPage`, which keeps vectors; set `textDrawingMode = .invisible` (PDF `Tr 3`); then draw each word with Core Text. Scale each word horizontally (text matrix or `Tz`) so its advance width matches the Vision box, and rotate the text matrix by the angle of the box's baseline.

  Map Vision's normalized, bottom-left-origin coordinates to the page's `mediaBox`/`cropBox`, and account for the page's `/Rotate`. This is a well-known source of bugs.
- **Accents:** these should work if Core Text embeds a subset font with a ToUnicode map, which Core Graphics normally does. Verify it with an automated test: copy text out of `PDFDocument.string` and compare "ñ, á, ü". No source confirms ToUnicode behaviour.
- **Hidden cost:** rebuilding a page through `CGContext` drops its annotations, links and widgets. The forum thread on stripped link annotations shows this pattern ([Apple Developer Forums 711925](https://developer.apple.com/forums/thread/711925)). The OCR pass must re-add them or leave such pages alone. Scanned pages rarely have annotations, which reduces the risk.
- **Multi-column text:** order matters only for copy/paste and search across lines, not for placement. Word-level placement is position-correct whatever the column layout. `RecognizeDocumentsRequest` (macOS 26+) gives paragraph grouping, which can improve reading order, but it rules out macOS 14/15.
- **Spike first:** prototype `saveTextFromOCROption` in week 1. If it produces a good text layer for Spanish and English, OCR effort drops from about 2–3 weeks to under one week. Being undocumented, it gives no control over languages, confidence, progress or cancellation, and it may change between OS releases.
- **Effort/risk:** custom layer: Medium effort (2–3 weeks part-time including tests), Medium risk. Recognition quality itself is low risk. No third-party library is needed.

### Gaps
- No benchmark was found for seconds per page (accurate vs fast, Apple Silicon vs Intel) or for memory use in batch runs. Measure it in the spike.
- There are no published Spanish accuracy numbers. Only claims of quality relative to Tesseract were found.
- What `saveTextFromOCROption` actually does (which languages, whether it OCRs every image-only page, behaviour in the sandbox) is undocumented by Apple. It was confirmed only through a forum snippet.
- Whether PDFKit preserves an invisible `Tr 3` text layer through later `PDFDocument.write` calls was not confirmed by any source. It should hold, since text is page content, but test it.

---

## 2. Compression: real approaches when PDFKit cannot recompress embedded images directly

### Takeaway
"Compression with levels" is the most underestimated module in the plan. Apple offers three blunt tools:
- the PDFKit write options `saveImagesAsJPEGOption` and `optimizeImagesForScreenOption`, which are toggles, not levels;
- Quartz filters, whose defaults are notorious for damaging quality;
- rasterizing pages, which destroys text and vectors.

Proper per-image downsampling and re-encoding, the approach behind competitive "PDF Squeezer"-class results, requires a PDF object-level writer. Apple has none (CGPDF is read-only). The realistic permissive choice is **qpdf (Apache-2.0)** combined with ImageIO for decoding and encoding. MuPDF and Ghostscript are AGPL and do not fit a closed-source app without a paid licence.

### Cited Findings
- **PDFKit write options:** `PDFDocumentWriteOption` includes `optimizeImagesForScreenOption`, `saveImagesAsJPEGOption`, `burnInAnnotationsOption` and `saveTextFromOCROption`, alongside the password and permissions options. Apple documents none of them beyond their names ([Apple docs](https://developer.apple.com/documentation/pdfkit/pdfdocumentwriteoption.md)).
- **Matching Preview options:** Preview's export dialog has "Optimize images for screen… to reduce file size" and "Save images as JPEG", and Apple warns that a compressed PDF "may be of lower quality than the original" ([Apple Preview User Guide](https://support.apple.com/guide/preview/prvw1509)).
- **Quartz filter quality:** the built-in "Reduce File Size" Quartz filter limits images to a maximum of 512 px by default, which "explains why you are getting poor quality PDFs". Users create custom filters in ColorSync Utility (for example 150 dpi and JPEG ~85% for scanned A4). Already-optimized PDFs can even grow in size ([OWC/MacSales blog](https://blog.macsales.com/63995-reduce-pdf-size-control-quality-for-free/); [Apple Community thread](https://discussions.apple.com/thread/252514993)).
- **Problems with whole-document re-interpretation:** for Ghostscript `-dPDFSETTINGS=/screen`, the author of pdf-optimizer reports that it "flattened color to DeviceRGB, dropped the ICC profile, and re-baked masks and vectors".
- **What good output looks like:** pdf-optimizer's own approach recompresses only raster image streams in place and leaves "vectors, masks, text, the ICC profile, and document structure" untouched. Its main techniques:
  - photos re-encoded as JPEG, flat images re-deflated;
  - downsampling by effective on-page DPI;
  - keeping a new stream only if it is smaller;
  - passing soft masks, Indexed, Separation, Lab and CMYK images through untouched.

  Its README reports 302.8 MB reduced to 38.9 MB. It is MIT-licensed, but it uses **MuPDF** to read and write PDF objects ([mattdesl/pdf-optimizer](https://github.com/mattdesl/pdf-optimizer)).
- **qpdf licence and scope:** qpdf is "Licensed under the Apache License, Version 2.0" (Artistic 2.0 before version 7). It depends on zlib and libjpeg, plus GnuTLS or OpenSSL depending on the crypto provider, and "does not render PDFs or perform text extraction" ([qpdf README](https://github.com/qpdf/qpdf/blob/main/README.md)).
- **qpdf compression and cleanup options:**
  - `--optimize-images`: "Attempt to use DCT (JPEG) compression for images that fall within certain constraints", with `--oi-min-width` and related limits;
  - `--recompress-flate` and `--compression-level` (1–9);
  - `--object-streams` and `--linearize`;
  - `--remove-metadata` and `--remove-info`;
  - `--flatten-annotations` and `--generate-appearances`.

  ([qpdf CLI manual source](https://raw.githubusercontent.com/qpdf/qpdf/main/manual/cli.rst))
- **MuPDF licence:** MuPDF is AGPL or commercial. Under the AGPL, "your entire application that uses MuPDF must be distributed under the GNU AGPL". A maintainer has called this licence incompatible with the App Store, and the alternative is a commercial licence from Artifex ([MuPDF license docs](https://mupdf.readthedocs.io/en/1.27.0/license.html); [MuPDF Explored, licensing](https://ghostscript.com/~robin/mupdf_explored/mupdf_exploredse159.html)).
- **Ghostscript licence:** Ghostscript is AGPL (since 9.07, February 2013) or commercial through Artifex ([Artifex licensing](https://ghostscript.com/licensing); [Wikipedia](https://en.wikipedia.org/wiki/Ghostscript)).
- **PDF Squeezer:** the vendor describes "a sophisticated compression process that uses numerous methods" with presets, with no detail on its engine ([Witt Software](https://www.witt-software.com/pdfsqueezer-windows/); [Macworld review](https://macworld.com/article/3583678/pdf-squeezer-4-review.html)). A Go project with the same name bundles qpdf, Ghostscript and veraPDF as optional tools ([hawkff/pdf-squeezer](https://pkg.go.dev/github.com/hawkff/pdf-squeezer)), but it is unrelated to the commercial app.

### Inferences
- **The CGPDF gap:** `CGPDFDocument`/`CGPDFPage`/`CGPDFStream` can read image XObjects and their raw data, but Core Graphics has no API to replace one object and re-serialize the file. Any "re-encode images, keep everything else" approach therefore needs an object-level writer. qpdf is the permissive option. PDFium is believed to be BSD-licensed and has image-object APIs, but it is a much heavier Chromium-style build.
- **Recommended approach for v1.0:**
  - **Level "Light":** qpdf structural optimization, i.e. `--object-streams=generate`, `--recompress-flate`, `--compression-level=9`, and dropping unused objects. This is lossless and safe.
  - **Levels "Medium"/"Strong":** walk image XObjects with qpdf, decode DeviceRGB/DeviceGray DCT and Flate images with ImageIO/CGImage, downsample to a target effective DPI (for example 150/100), re-encode with `CGImageDestination` as JPEG at a quality setting, write the new stream back through qpdf, and keep it only if smaller. Skip CMYK/Indexed/ICC-based/SMask/JBIG2/JPX images, or handle them carefully. This is the pdf-optimizer model ported to qpdf plus ImageIO.
  - **Fallback for the first beta:** expose the PDFKit `saveImagesAsJPEG` + `optimizeImagesForScreen` options as a single "Reduce size" switch, and test them, since their DPI and quality are undocumented.
- **Building qpdf for the sandbox:** it is C++17 and would be wrapped as an XCFramework behind a small Objective-C++ or C shim. Apple platforms provide zlib, but libjpeg must be built too, or qpdf compiled to skip its own DCT path while ImageIO does the image work. Plan 3–5 days for build and CI setup alone.
- **Effort/risk:** High effort (3–4 weeks part-time for a solid level-based engine and a regression suite), High risk (colour shifts, masks, odd colour spaces). This is the module most likely to blow the schedule. Consider moving "Strong" compression to v1.1.

### Gaps
- The PDFium licence text could not be fetched (googlesource was unreachable). Commonly known as BSD-3-Clause with some Apache-2.0 parts; verify before relying on it.
- The DPI and JPEG quality that `optimizeImagesForScreenOption` and `saveImagesAsJPEGOption` use are undocumented, and their per-option macOS availability page was not fetched. They are probably macOS 13+, like their sibling options.
- Exactly how qpdf's `--optimize-images` behaves (whether it downsamples) is not confirmed. The manual snippet mentions only "DCT compression … within certain constraints".
- No evidence was found about which engine the commercial PDF Squeezer uses.
- The public `QuartzFilter` class (Quartz framework) can apply a custom filter to a `CGContext`, but it was not researched in depth here.

---

## 3. PDFKit known bugs and limitations, 2023–2026

### Takeaway
PDFKit has a long, ongoing record of **save-path regressions** around forms, widgets and annotations. Several of these are open in 2026 on macOS 26 and iOS 27. The plan's mitigation ("detect and warn" plus a test bank of about 30 PDFs) is the right idea but too small. Expect to write workarounds around PDFKit's writer and to keep re-testing on every macOS point release.

### Cited Findings
- **Radio buttons on macOS 26.3 (FB22167174, March 2026, no Apple response):** building a radio group with `PDFAnnotation` and saving through `dataRepresentation()` keeps only the first-added button's state; all others are written as `/AS /Off`. Serialization even changes in-memory `buttonWidgetState`. The poster's workaround is to add the selected widget first ([Apple Developer Forums 818162](https://developer.apple.com/forums/thread/818162)).
- **Radio buttons in Preview on macOS 12–13 (FB9978281):** incremental updates moved `/V`, `/T`, `/FT` into the kid widget, removed `/Parent`, and never updated the parent field, so selections were lost on reopen. The reporter says it was fixed in macOS 14 and iOS 17 ([Apple Developer Forums 735073](https://developer.apple.com/forums/thread/735073)).
- **Duplicated field text on iOS/iPadOS 17.2+:** after a `dataRepresentation()` → `PDFDocument(data:)` round trip, filled text field content is duplicated when the file is printed or shared. Users still reported it on iOS 18.4.1 in April 2025. One user could not reproduce it on macOS 15.0, and noted that iOS writes PDF 1.4 while macOS writes PDF 1.3 ([Apple Developer Forums 743379](https://developer.apple.com/forums/thread/743379)).
- **iOS/iPadOS 27.0 annotation image corruption (FB25195006):** `dataRepresentation()` and `write(to:)` write corrupt PDFs when a custom `PDFAnnotation` subclass that overrides `draw(with:in:)` draws a 16-bit-per-component image. Only half of the image data is written, and Acrobat reports "Insufficient data for an image". The bug was still present in the 27.2 beta.
  - DTS workaround: copy pages into a fresh `PDFDocument` before annotating. DTS notes this drops `documentAttributes`, which must be copied back, and did not verify that outlines survive.
  - Related iOS 27 regressions: FB24882188, FB24843022.

  ([Apple Developer Forums 851708](https://developer.apple.com/forums/thread/851708))
- **Push-button captions:** captions are not reliably written to the file on save ([Apple Developer Forums 778817](https://developer.apple.com/forums/thread/778817)).
- **Lost links when drawing pages:** drawing pages through `CGContext` (`page.draw(with:to:)`) produces output without the original link annotations ([Apple Developer Forums 711925](https://developer.apple.com/forums/thread/711925)).
- **"Append" save mode (DEVONthink staff):** "a known bug in the PDFkit framework of macOS when saving PDFs using the fast 'Append' mode", also affecting Preview. Users also report annotations becoming corrupt across Preview, Skim, Highlights and DEVONthink after editing metadata ([DEVONthink forum](https://discourse.devontechnologies.com/t/devonthink-corrupting-pdf-annotations/67074); [DEVONthink forum, 3.91 thread](https://discourse.devontechnologies.com/t/dt-3-91-editing-pdf-documents-not-working-anymore/75915?page=3)).
- **Highlights on iOS:** macOS-made highlights reportedly "not compliant to the official PDF standard" and do not show on iOS ([DEVONthink forum](https://discourse.devontechnologies.com/t/pdf-highlights-not-synching-to-devonthink-to-go/25108)).
- **Large files:** a DEVONthink user found file size mattered more than page count. A ~4.7 MB, 500-page file lagged little; a ~27 MB, ~500-page file lagged a lot. A developer blamed PDFKit's save path ([DEVONthink forum](https://discourse.devontechnologies.com/t/devonthink-and-large-pdfs/65727)).
- **Memory growth (older report):** in Skim, which uses PDFKit, memory grew from ~50 MB to 726 MB while paging through a 189-page PDF ([macosx-tex list, 2015](https://email.esm.psu.edu/pipermail/macosx-tex/2015-October/054308.html)).
- **XFA:** built-in macOS support in PDFKit and Quartz 2D does not include XFA forms, and its AcroForm support is limited ([Eclectic Light, "The nightmare of forms" (search snippet; page not reachable)](https://eclecticlight.co/2019/06/18/pdf-without-adobe-23-the-nightmare-of-forms/)).
  - A form that does not appear is likely an XFA form ([Nutrient guide](https://www.nutrient.io/guides/ios/rendering-issues/pspdfkit-doesnt-show-the-pdf-form/)).
  - XFA/LiveCycle was removed from PDF 2.0 ([Apryse FAQ](https://docs.apryse.com/ios/faq/xfa-lifecycle-support)).
- **JavaScript:** Acrobat Reader and Preview on Mac "do not support JavaScript actions", according to one support note, so script-calculated fields will not compute ([Mainspring FAQ](https://answers.gomainspring.com/knowledge/faq-when-using-a-mac-my-customer-form-data-is-not-being-saved)).

### Inferences
- **XFA detection:** open the file with `CGPDFDocument`, take the catalog → `/AcroForm` dictionary → check for an `/XFA` key. If `/NeedsRendering true` is also set (dynamic XFA), warn that the form cannot be filled. If the file has only an `/XFA` key next to normal AcroForm fields (hybrid), the AcroForm fields can be filled, but warn that the XFA data will be stale. This comes from the PDF specification, not from a found source.
- **JavaScript detection:** scan for `/JS` or `/AA` actions on fields and for `/Names /JavaScript` in the catalog, then show a "calculations will not update" banner.
- **Defensive design:**
  - Never use incremental or "append" saves; always do a full rewrite into a temp file.
  - After saving, reopen the output and compare field values, page count, annotation count and outline count with the in-memory model. Refuse to replace the original if anything differs.
  - Do not override `draw(with:in:)` with wide-colour images. Use 8-bpc sRGB for signature stamps; the iOS 27 bug hits exactly this pattern, and macOS 27 behaviour is unknown.
- **Performance:** for 500+ pages or 200 MB, avoid `PDFThumbnailView` for big documents. Generate thumbnails lazily on a background queue with `PDFPage.thumbnail(of:for:)` and keep a bounded cache. Do merge and split on a background task with progress.
- **Effort/risk:** the PDFKit-bug tax is roughly 20–30% of total schedule (inference). Forms are High risk.

### Gaps
- No public macOS 27 PDFKit regression reports were found yet (the 16-bpc bug is confirmed only on iOS 27).
- No specific source was found on page insertion corrupting outlines or links. The DTS note that outline preservation was "not verified" when copying pages hints at this.
- No authoritative source covers signature/stamp appearance streams written by PDFKit on macOS 26/27.

---

## 4. Flattening and true redaction (v1.5)

### Takeaway
Flattening is cheap: PDFKit's `burnInAnnotationsOption` (macOS 13+) does it, and qpdf `--flatten-annotations` is an alternative. True redaction is not possible with PDFKit alone, because PDFKit cannot delete the underlying text, images or vectors in a page's content stream. The only all-Apple route is to rasterize the affected page and then OCR it again.

### Cited Findings
- **PDFKit flattening:** `burnInAnnotationsOption` is available on macOS 13.0+, with no description in Apple's docs ([Apple docs](https://developer.apple.com/documentation/pdfkit/pdfdocumentwriteoption/burninannotationsoption.md)).
- **qpdf flattening:** "--flatten-annotations: This option collapses annotations into the pages' contents with special handling for form fields"; `--generate-appearances` regenerates appearance streams ([qpdf manual](https://raw.githubusercontent.com/qpdf/qpdf/main/manual/cli.rst)).
- **What true redaction requires:** the industry approach is two steps, mark and then apply, where the apply step permanently deletes "the content within the regions". Annotations and form fields must be flattened first, or they escape redaction ([ComPDF redaction guide](https://compdf.com/guides/pdf-sdk/ios/redaction/redact-pdfs); [Qoppa KB](https://kbpdfstudio.qoppa.com/?p=2656)).

### Inferences
- **v1.5 redaction without a commercial SDK:**
  - **(a) Rasterize:** render each page that has redactions at 300 dpi, paint the boxes black, and replace the page with the image. Then re-OCR the non-redacted text with the section 1 pipeline. Also remove the `/Metadata` stream, the document info, embedded files and JavaScript. This is safe but loses vector and text fidelity on those pages.
  - **(b) Edit content streams with qpdf:** parse each page's content stream, drop text-showing operators whose glyph boxes intersect a redaction rectangle, and clip images. This is a research-grade task; do not promise it for v1.5.
- **Marketing:** call (a) "redacción segura (rasteriza la página)". Never ship a black-box annotation as "redaction".

### Gaps
- No source showed how `burnInAnnotationsOption` handles widgets, meaning whether form fields are flattened or dropped. Test it.

---

## 5. Password protection and metadata scrubbing

### Takeaway
PDFKit can set user and owner passwords and permissions. However, the Core Graphics encryption layer underneath documents key lengths **only up to 128 bits**, so AES-256 (PDF 2.0, R6) output through Apple frameworks is unlikely. Clearing `documentAttributes` does not reliably remove the XMP `/Metadata` stream. qpdf provides both 256-bit AES and full metadata removal.

### Cited Findings
- **PDFKit password options:** `ownerPasswordOption` ("required for encryption"), `userPasswordOption` ("optional for encryption") and `accessPermissionsOption` ([Apple docs](https://developer.apple.com/documentation/pdfkit/pdfdocumentwriteoption.md)).
- **Core Graphics key length:** `kCGPDFContextEncryptionKeyLength` must be "a multiple of 8 between 40 and 128, inclusive. If this key is absent or invalid, the encryption key length defaults to 40 bits", and the description refers to the PDF 1.5 reference ([Apple docs](https://developer.apple.com/documentation/coregraphics/kcgpdfcontextencryptionkeylength.md)).
- **Preview's cipher (unconfirmed):** secondary blogs claim Preview encrypts with AES-128. No Apple document confirms this ([peony.ink](https://www.peony.ink/blog/password-protect-pdf-without-adobe); [techpp](https://techpp.com/2021/03/12/password-protect-pdf-on-mac/)).
- **qpdf encryption:** qpdf advises "Use 256-bit encryption unless you have a specific reason to use an insecure format", and offers `--remove-metadata` ("Exclude metadata from the output file") and `--remove-info` ([qpdf manual](https://raw.githubusercontent.com/qpdf/qpdf/main/manual/cli.rst); [qpdf encryption docs](https://qpdf.readthedocs.io/en/12.2/encryption.html)).
- **Older metadata-write regression:** a 2017 report describes a `writeToFile:withOptions:` metadata regression on High Sierra, showing that the write path has broken before ([Apple Developer Forums 94884](https://developer.apple.com/forums/thread/94884)).

### Inferences
- **Encryption:** if the app already embeds qpdf for compression, use it for "Proteger" as well: AES-256 (R6), permissions, and `--remove-metadata --remove-info`. Otherwise, PDFKit encryption is acceptable for v1.0 but should be described as "AES-128/compatible", not "AES-256". Run `qpdf --show-encryption` on PDFKit output in CI to find out what it actually writes.
- **Metadata:** PDFKit exposes only the Info dictionary (`documentAttributes`); there is no public API for the catalog `/Metadata` XMP stream. A PDFKit-only scrub therefore leaves XMP (creator tool, original author, history), and also leaves embedded files, page-piece dictionaries and per-image XMP. For an "abogados" (lawyers) feature this is a real liability unless the app uses qpdf.
- **Effort/risk:** with qpdf: Low–Medium effort (about 1 week). PDFKit-only: Low effort but medium "false promise" risk.

### Gaps
- The cipher PDFKit actually writes on macOS 14–27 (RC4-128 vs AES-128) is not documented. Verify it empirically.
- Whether PDFKit preserves or drops XMP when it rewrites a file was not confirmed by any source.

---

## 6. Signatures: storage and annotation approach

### Takeaway
Feasible with low risk. Draw, type or import the signature, store it as a small 8-bpc PNG, and place it as a stamp annotation, or burn it into the page content on export. Keychain storage of a few KB of data is technically possible. A file in the app container, encrypted with a CryptoKit key kept in the Keychain, is a cleaner design. Avoid the `draw(with:in:)`-override pattern with 16-bpc images.

### Cited Findings
- **Bug matching the signature-stamp pattern:** on iOS 27, a `PDFAnnotation` subclass that overrides `draw(with:in:)` to draw a 16-bpc image produces corrupt PDFs. The workaround is 8-bpc sRGB rendering, or copying pages into a new document before annotating ([Apple Developer Forums 851708](https://developer.apple.com/forums/thread/851708)).
- **Appearance dictionaries:** push-button and appearance-dictionary data was not written reliably on save in one report ([Apple Developer Forums 778817](https://developer.apple.com/forums/thread/778817)).

### Inferences
- **Placement:** either (a) use a stamp `PDFAnnotation` while editing and flatten with `burnInAnnotationsOption` on "Finish and share", so the signature cannot be lifted out easily; or (b) draw the image into page content through a `CGContext`, with the side effects noted in sections 1 and 3.
- **Storage:** use Keychain items (`kSecClassGenericPassword` with `kSecAttrAccessibleWhenUnlocked`, not synchronizable unless the user opts in) for small blobs. For several signatures with high-resolution images, store encrypted files in `Application Support` instead.
- **Effort/risk:** Low–Medium (about 1 week).

### Gaps
- No source states Keychain item size limits or Apple guidance against storing images there.
- Legal aspects of simple electronic signatures were not researched, as instructed.

---

## 7. Continuity Camera / "Import from iPhone" and document scanning in a sandboxed SwiftUI/AppKit app

### Takeaway
Supported and essentially free. Use the `NSMenuItem.importFromDeviceIdentifier` menu item, or SwiftUI's `ImportFromDevicesCommands()`, with an `NSServicesMenuRequestor` responder. VisionKit's `VNDocumentCameraViewController` is iOS-only. The Mac receives the scan from the iPhone. There are SwiftUI quirks, so budget time to debug the responder chain.

### Cited Findings
- **Apple's guidance:**
  - Continuity Camera has been available since macOS 10.14. `NSTextView` gets it automatically.
  - Other views must override `validRequestor(forSendType:returnType:)` and implement `readSelection(from:)` (`NSServicesMenuRequestor`) to read the image from the pasteboard.
  - The menu item is added with identifier `NSMenuItem.importFromDeviceIdentifier`, for example in `applicationWillFinishLaunching`. AppKit adds the item to contextual menus automatically.

  ([Apple: Supporting Continuity Camera in Your Mac App](https://developer.apple.com/documentation/appkit/supporting-continuity-camera-in-your-mac-app.md))
- **SwiftUI:** add `.commands { ImportFromDevicesCommands() }` on the scene, or use `.importsItemProviders` on a view ([Apple Developer Forums 750367](https://developer.apple.com/forums/thread/750367)).
- **SwiftUI Toggle bug (2024, isolated case):** if any view in the active window contains a `Toggle`, even a hidden one, all "Import from iPhone or iPad" items are disabled ([Michael Tsai blog, Aug 2024 (search snippet)](https://mjtsai.com/blog/2024/08/30/swiftui-breaks-continuity-camera/)).
- **Error report:** `ImportFromDevicesCommands` produced Cocoa error 66563 in one thread ([Apple Developer Forums 695137](https://developer.apple.com/forums/thread/695137)).

### Inferences
- **Pasteboard types:** a document scan most likely arrives as a PDF or an image on the pasteboard. Accept `.pdf` plus `NSImage.imageTypes`, then run OCR (section 1) automatically.
- **Sandbox:** no special entitlement is mentioned in Apple's guide, so no extra entitlement appears to be needed.
- **Hosting:** host the receiving `NSResponder` in an AppKit `NSViewRepresentable`/`NSViewController` inside the SwiftUI window, to avoid the SwiftUI responder-chain bugs.
- **Effort/risk:** Low effort (2–4 days), Low–Medium risk because of the SwiftUI quirks.

### Gaps
- No source confirms the exact pasteboard UTI for "Scan Documents" (PDF vs multi-image).
- No source confirms whether the Toggle bug still exists on macOS 26/27.

---

## 8. Sandbox, document architecture, safe save and large files

### Takeaway
Use an **AppKit `NSDocument` subclass**, hosted in SwiftUI views if desired. `NSDocument` already implements crash-safe writing (`writeSafely`), autosave and versions. SwiftUI `DocumentGroup` with `FileDocument` reads the file into memory and is a poor fit for 200 MB PDFs and for strict control of the save path.

### Cited Findings
- **`NSDocument.writeSafely(to:ofType:for:)`:** it "is responsible for doing document writing in a way that minimizes the danger of leaving the disk … in an inconsistent state in the event of an app crash, system crash, hardware failure, power outage". It calls `write(to:ofType:for:originalContentsURL:)` and preserves file attributes, and `keepBackupFile` controls backups ([Apple docs](https://developer.apple.com/documentation/appkit/nsdocument/writesafely(to:oftype:for:).md)).
- **Atomic-replace pattern in practice:** mac-ocr writes to a temp file, then replaces the destination atomically, and warns that a `.<name>.<uuid>.tmp` file can be left behind if the process is killed ([mac-ocr](https://github.com/privatenumber/mac-ocr)).

### Inferences
- **Save sequence:**
  1. Write with `PDFDocument.write(to: tempURL, withOptions:)` into the `NSDocument`-provided URL, which sits in a temporary or replacement directory on the same volume.
  2. Validate the output: reopen it, compare counts and field values (section 3), and optionally run qpdf's check API.
  3. Only then let `NSDocument` move it into place.
- **Autosave:** keep `autosavesInPlace` false, or use explicit "Save as copy" semantics. Autosave-in-place with Versions on 200 MB PDFs is slow and multiplies disk use. Expose Duplicate and Revert instead.
- **Sandbox entitlements:** `com.apple.security.files.user-selected.read-write`, and security-scoped bookmarks (`com.apple.security.files.bookmarks.app-scope`) for recent files, batch output folders and watch folders. Merging files that the user drags in works through the drag's implicit grant.
- **Effort/risk:** Medium (1–1.5 weeks); this is the foundation for everything else.

### Gaps
- No 2025–2026 source compares `DocumentGroup` and `NSDocument` specifically for large PDFs; the recommendation is an engineering inference.

---

## 9. Minimum macOS version (14 vs 15 vs 26)

### Takeaway
Move the minimum from macOS 14 to **macOS 15**, or consider **macOS 26**. Adoption data suggests few paying customers remain on macOS 14 by late 2026. Requiring macOS 15 unlocks the Swift `RecognizeTextRequest` API, and macOS 26 adds `RecognizeDocumentsRequest` and the native Liquid Glass look. macOS 27 has already shipped, so even macOS 26 is "one version back".

### Cited Findings
- **TelemetryDeck (data to late April 2026, updated 2026-05-03):** macOS 26.4 was the most-used version at ~47%, macOS 26.3 was ~20%, and macOS 15.6 had dropped to ~3.6% ([TelemetryDeck survey (search snippet; page not reachable)](https://telemetrydeck.com/survey/apple/macOS/versions/)).
- **Secondary article (Aug 2026):** Tahoe on ~86% of tracked macOS installs in the week of 27 July 2026, and Sequoia at 12.2%. Unverified against TelemetryDeck ([aboutchromebooks.com](https://www.aboutchromebooks.com/?p=33929)).
- **API floors:** `RecognizeTextRequest` needs macOS 15+; `RecognizeDocumentsRequest` needs macOS 26+ ([Apple docs](https://developer.apple.com/documentation/vision/recognizetextrequest.md); [Apple docs](https://developer.apple.com/documentation/vision/recognizedocumentsrequest.md)).
- **macOS 27 is out (Oct 2026)** ([OCRmyPDF-AppleOCR](https://github.com/mkyt/OCRmyPDF-AppleOCR); [Apple Developer Forums 851708](https://developer.apple.com/forums/thread/851708)).

### Inferences
- **macOS 15 minimum:** keeps a small Sequoia tail and lets OCR use one modern async Vision API. The cost is minimal.
- **macOS 26 minimum:** simplifies the UI (Liquid Glass without fallbacks), `RecognizeDocumentsRequest`, and App Intents/Foundation Models, if those are ever wanted. Given ~86% Tahoe share in mid-2026 plus macOS 27, the cost looks small, but verify with current TelemetryDeck data.
- **Testing burden:** every supported major version multiplies the PDFKit regression matrix (section 3). Fewer versions means fewer save-path bugs to chase.

### Gaps
- No verified Oct 2026 share figures for macOS 14 or macOS 27.
- No data on the macOS version mix of PDF-utility buyers specifically.

---

## 10. Testing strategy for "never corrupt a PDF"

### Takeaway
A 30-file folder is not enough. Combine:
- public corpora: the veraPDF corpus (CC-BY-4.0, 1,500+ files), the pdf.js test suite and govdocs1;
- the user's 30+ real files;
- automated round-trip invariants;
- external validators run in CI on a Mac runner: qpdf's check mode and the veraPDF Arlington-model checker.

### Cited Findings
- **veraPDF corpus:** covers PDF/A and PDF/UA with over 1,500 files under CC-BY-4.0, complementing the Isartor and Bavaria suites, and is used industry-wide, Adobe included ([InfraFinder / veraPDF](https://infrafinder.investinopen.org/solutions/verapdf); [PDF Association](https://www.pdfa.org/first-set-of-candidate-verapdf-corpus-files-delivered/)).
- **veraPDF tooling:** veraPDF built an open-source checker based on the Arlington PDF Model that analyses files against the full PDF 2.0 specification. Full Arlington checking was released in September 2024. veraPDF 1.28 came out in April/May 2025; the sources differ on the month ([PDF Days Europe 2025 poster](https://pdfa.org/download-area/posters/PDFDaysEurope2025-TechnicalPoster-DualLab.pdf); [RIMPA](https://www.rimpa.com.au/resource/development-preview-pdf-file-checker-based-on-the-arlington-pdf-model.html)).

### Inferences
- **Round-trip invariants per test file and operation** (open → op → save → reopen):
  - page count and page sizes and rotations are as expected;
  - `PDFDocument.string` is unchanged or a superset (OCR);
  - the set of annotations and fields and their values is equal;
  - the outline and links resolve;
  - the file opens in PDFKit, `CGPDFDocument` and qpdf without errors.
- **Visual check:** render each page to a bitmap before and after, and diff with a tolerance.
- **Fuzzing:** randomized operation sequences (insert, rotate, delete, fill, annotate, save, compress) on corpus files, asserting the invariants after every step. Add mutated or truncated files to check that the app fails gracefully and never overwrites the original.
- **Per-OS runs:** run the suite on each supported macOS major and the current beta, which matters given the recurring regressions in section 3.
- **Licences:** veraPDF and the pdf.js corpora are only test inputs or tools, not shipped code, so their licences do not affect the closed-source app.

### Gaps
- Licence and terms for govdocs1 and the pdf.js test PDFs were not checked.
- qpdf `--check` documentation sits in the unread part of the manual. It is a well-known qpdf feature, but no citation was gathered.

---

## 11. Overall: is 8–10 weeks part-time realistic, and which modules are highest risk?

### Takeaway
No. The plan's premise that "Apple already solves the hard part" holds only for viewing, page organization, basic annotation and the raw OCR engine. Compression with levels, a correctly placed OCR text layer, reliable form saving, real metadata scrubbing and AES-256 all fall outside what PDFKit does well, or need a third-party writer (qpdf). A realistic part-time estimate for a v1.0 that does not damage files is about **16–24 weeks**. Alternatively, keep 10 weeks by cutting scope: compression as a single PDFKit toggle, OCR via `saveTextFromOCROption` if it proves good, and redaction and AES-256 deferred.

### Cited Findings
- The forum and DTS reports above document live save-path regressions in 2026 on macOS 26.3 and iOS 27.0, plus older form bugs ([818162](https://developer.apple.com/forums/thread/818162); [851708](https://developer.apple.com/forums/thread/851708); [735073](https://developer.apple.com/forums/thread/735073); [743379](https://developer.apple.com/forums/thread/743379)).
- Ghostscript/MuPDF-class compression is AGPL-only without a commercial licence, while qpdf is Apache-2.0 ([MuPDF license](https://mupdf.readthedocs.io/en/1.27.0/license.html); [Artifex licensing](https://ghostscript.com/licensing); [qpdf README](https://github.com/qpdf/qpdf/blob/main/README.md)).
- Core Graphics encryption documents keys only up to 128 bits ([Apple docs](https://developer.apple.com/documentation/coregraphics/kcgpdfcontextencryptionkeylength.md)).

### Inferences
All ratings and week counts below are estimates by this researcher, not sourced figures.

| Module | Recommended approach / APIs | Known pitfalls | Effort (part-time) | Risk | Third-party lib? |
|---|---|---|---|---|---|
| Base: document, viewer, safe save | `NSDocument` + `PDFView`, lazy thumbnails, temp-write → validate → replace | Large files, autosave/Versions cost, sandbox bookmarks | 1.5–2 wk | Medium | No |
| Organize (merge/split/reorder/rotate/insert/delete) | `PDFDocument.insert/removePage/exchangePage`, `PDFPage.rotation` | Outlines/links after insertion (unverified), memory on merge | 1–1.5 wk | Low–Medium | No |
| Annotate | PDFKit annotations (highlight, underline, note, freeText, ink, shapes) | iOS 27 draw-override bug; highlights compatibility with other viewers; "Append" save bug | 1–1.5 wk | Medium | No |
| Forms | PDFKit widgets; XFA/JS detection via `CGPDFDocument` catalog; verify after save | Radio bug FB22167174 (macOS 26.3), duplicated values (iOS 17.2+), appearance streams, no XFA/JS | 1.5–2.5 wk | **High** | No (qpdf `--generate-appearances` optional) |
| Signature | 8-bpc PNG stamp annotation, flatten on export; storage in Keychain or encrypted container file | 16-bpc corruption bug; appearance streams | 0.5–1 wk | Low–Medium | No |
| OCR | Vision `VNRecognizeTextRequest` / `RecognizeTextRequest` + Core Text `.invisible` per word with scaling and rotation; spike `saveTextFromOCROption` first | Coordinates and `/Rotate`, small text (partitioning), multilingual pages, losing annotations when rebuilding a page | 2–3 wk (≤1 wk if built-in option suffices) | Medium | No (mac-ocr MIT for reference) |
| Compress (levels) | qpdf (Apache-2.0) structural + per-image ImageIO downsample and re-encode; PDFKit JPEG/screen options as fallback | Quartz filter quality; colour spaces, SMasks, ICC; CGPDF read-only | 3–4 wk | **High** | **Yes: qpdf** (or accept weak PDFKit toggles) |
| Protect | PDFKit passwords (≤128-bit per CG docs) or qpdf AES-256; qpdf `--remove-metadata --remove-info` | XMP not reachable from PDFKit; "AES-256" claim not deliverable without qpdf | 0.5–1 wk | Medium | Recommended: qpdf |
| Scanner (iPhone) | `ImportFromDevicesCommands` / `importFromDeviceIdentifier` + `NSServicesMenuRequestor` in an AppKit-hosted view | SwiftUI responder-chain bugs (Toggle) | 0.5 wk | Low–Medium | No |
| Test infrastructure | Corpora + invariants + veraPDF/qpdf checks + per-OS CI | Needs Mac CI runners and per-OS matrix | 1.5–2 wk (ongoing) | — | Tools only (not shipped) |
| Payments, trial, watermark, beta, launch | StoreKit 2, watermark via flattened annotation | — | 2–3 wk | Low–Medium | No |

- **Sum:** roughly **15–22 weeks** part-time before buffer.
- **Highest risk, in order:** compression with levels, then forms reliability, then the OCR text layer, then "Proteger" promises (AES-256 and XMP).
- **The plan's "no external libraries" claim:** realistically it becomes "one permissive library, qpdf (Apache-2.0)". Include its Apache-2.0 NOTICE and licence text in the app's acknowledgements.
- **The plan's selling point "OCR works in the sandbox":** confirmed. The OCR engine is the least risky part of the OCR module; the text-layer writer carries the risk.

### Gaps
- No public developer post-mortems (from PDF Squeezer, PDF Search or Skim developers) giving real effort figures for comparable apps were found.
- The effort numbers above are inferences, not sourced estimates.
