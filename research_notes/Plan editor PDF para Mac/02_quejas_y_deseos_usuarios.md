# Voice of the customer: PDF editing on Mac (2024–2026)

> **Method and limits (read first).** Research done 2026-10-24 with WebSearch only. In this environment **Reddit was blocked** (the search API refuses reddit.com, and fetches failed), and **WebFetch/curl could not reach any page** (DNS/proxy errors on news.ycombinator.com, forums.macrumors.com, discussions.apple.com, hn.algolia.com). So every quote below comes from **search-result snippets and summaries**. It was **not checked against the full page**, and wording may be slightly paraphrased. Before using a quote in marketing, open the link and confirm it. Thread dates are given when the search result showed them. Apple Community thread IDs give a rough age: 2555xxxx–2559xxxx is about 2024–25, 2560xxxx–2562xxxx is about 2025–26, and below 2540xxxx is pre-2023. Counts like "X of Y threads" refer only to the ~90 distinct results in my ~25 searches. They are **not** a statistically valid sample. Reddit sentiment (r/macapps etc.) is a **gap**.

## 1. What PDF tasks Mac users most often ask about, and which features they request most

### Takeaway
Most of the volume is about **fixing Preview's failures**, not about editing in depth. The top problems are: (1) form data or annotations lost or flattened on save, (2) "Reduce File Size" ruining scans, (3) slowness and hangs with large or scanned PDFs, (4) signing, including certificate signing for Spanish speakers, (5) redaction and Bates numbering for legal work, and (6) XFA government forms that will not open. "Edit existing text" is the feature the reviews use to separate "real editors" from Preview. The plan deliberately leaves that out.

### Cited Findings
**Forms losing data or getting flattened in Preview (the most persistent theme: 6 Apple Community threads plus 2 Adobe/expert posts, spanning 2008–2025)**
- Apple Community, "PDFs self flatten when saved in Preview" (thread 256096563, about 2025). A responder tested on **macOS Sequoia 15.5**: text annotations survived a save and reopen, but "Adding text annotations with Apple's Preview is not creating the missing Adobe PDF form fields." In other words, users mix up filling over a flat PDF with real AcroForm fields. — [Apple Community](https://discussions.apple.com/thread/256096563)
- Old but often cited (about 2008): "When 'Save As...' is selected, the file is saved, but any information entered within the fields is lost from both the original and saved copy." — [Apple Community 1433382](https://discussions.apple.com/thread/1433382)
- Form filled in Preview "does not display" in other viewers. Fields that look filled in Preview show up blank in Acrobat/Reader. — [Apple Community 3255797](https://discussions.apple.com/thread/3255797) (old). A vendor blog says the cause is that Preview "frequently fail[s] to generate standard PDF Appearance Streams." That is a commercial source. — [imagepdf.tools](https://imagepdf.tools/blog/why-do-my-pdf-form-fields-disappear-after-saving-in-mac-preview)
- A LibreOffice-made form: "the problem occurs with radio buttons – all other editable fields work fine". The choices were visible in print preview but lost on save. — [Apple Community 254545912](https://discussions.apple.com/thread/254545912) (this thread is my best guess from the snippet)
- Sonoma: form fields drop characters and ignore font changes. Posters blame Preview's lack of Acrobat JavaScript support. — [Apple Community 255536704](https://discussions.apple.com/thread/255536704) (about 2024)
- A long-standing expert view, from Adobe forum regular Karl Heinz Kremer: "Preview.app – Killer of PDF Files" (2013). The advice repeated in Adobe forums is to avoid opening PDFs in Preview at all. — [KHKonsulting](http://khkonsulting.com/2013/06/preview-app-killer-of-pdf-files/); [Adobe Community](https://community.adobe.com/questions-9/saving-filled-forms-1308396)

**Annotations vanishing in Preview (at least 9 Apple Community threads, several from 2022–2025)**
- On Sonoma 14.1, a user lost most of their annotations after saving and reopening, and older versions of the file "seemed to come back." — [Apple Community 255282944](https://discussions.apple.com/thread/255282944)
- Highlights and text boxes vanish from long or large PDFs. — [Apple Community 253675313](https://discussions.apple.com/thread/253675313); "Why does Preview forget annotations?" (LaTeX/Overleaf PDFs) — [255428351](https://discussions.apple.com/thread/255428351); Preview and Acrobat annotations not visible in each other — [256271825](https://discussions.apple.com/thread/256271825) (about 2025–26); others: [253093013](https://discussions.apple.com/thread/253093013), [253798752](https://discussions.apple.com/thread/253798752), [8191023](https://discussions.apple.com/thread/8191023) (old)
- Workarounds users rely on: re-export with the "Create Generic PDFX-3" Quartz filter, re-save in Acrobat Reader, or a GitHub repair script. — [255282944](https://discussions.apple.com/thread/255282944), [253093013](https://discussions.apple.com/thread/253093013)

**macOS Tahoe 26 regressions in Preview (2025–2026: 5 threads plus 1 article)**
- Highlighting fails or shows up as "odd blue boxes," especially in table-heavy PDFs such as **bank statements** (macReports, April 2026). The usual workaround is printing to a new PDF, which "doesn't always help." — [macReports](https://macreports.com/cant-highlight-pdfs-in-macos-tahoe-26-heres-how-to-fix/)
- In Tahoe 26.3/26.3.1, users cannot highlight or select text inside table cells. — [Apple Community 256257514](https://discussions.apple.com/thread/256257514). Text cannot be selected or copied after the upgrade. — [256142433](https://discussions.apple.com/thread/256142433)
- Thumbnail arrow-key scrolling makes pages drift to the left (26.0). — [256143817](https://discussions.apple.com/thread/256143817). "Preview Down bug after macOS Tahoe Update." — [256140291](https://discussions.apple.com/thread/256140291)
- In Illustrator-made PDFs, beige backgrounds and faint text disappear in Preview on 26.0.1 (October 2025). The workaround offered was Acrobat. — [Adobe Community](https://community.adobe.com/questions-9/macos-tahoe-26-0-1-pdfs-from-illustrator-showing-missing-beige-backgrounds-faint-text-in-preview-1305086)

**Compression ("how to compress PDF on Mac")**
- Apple itself warns: "when compressed, the PDF may be of lower quality than the original." — [Apple Support](https://support.apple.com/guide/preview/reduce-the-size-of-a-pdf-prvw1509/mac)
- The filter is fixed, with hardcoded parameters "you cannot see, adjust, or vary." On text-only PDFs it "barely reduces the file size at all," and there is no target-size option. One source claims the setting is JPEG 0.70 at 144 DPI, but that is a single vendor source and unverified. — [Smol](https://smolmac.com/blog/preview-reduce-file-size-mac); [Basalt](https://basaltformac.com/blog/compress-pdf-mac/)
- Demand signal: **at least 7 commercial pages** compete for this one query (Smallpdf, Compresto, Mainspring, Smol, Basalt, Utilitly, Lynote). — [Smallpdf](https://smallpdf.com/blog/reduce-pdf-file-size-mac-preview), [Compresto](https://compresto.app/blog/compress-pdf-size-mac), [Mainspring](https://trymainspring.com/blog/reduce-pdf-file-size-mac), [Utilitly](https://utilitly.com/blog/how-to-compress-a-pdf-on-mac), [Lynote](https://lynote.ai/blog/reduce-pdf-size-preview)

**Large or scanned PDFs: slowness**
- Search hangs: Preview "begins searching after one character, which means it must find thousands of results, and then it hangs and beachballs." — [Apple Community 255383222](https://discussions.apple.com/thread/255383222) (about 2024)
- On Sequoia, zooming a large scanned file is very slow in Preview, while Quick Look is smooth. — [Apple Community 255922303](https://discussions.apple.com/thread/255922303) (about 2024–25)
- PDF Expert "opens 6000+ page PDFs immediately, but searching through it is slow." — (same group of Apple Community results; see [6625952](https://discussions.apple.com/thread/6625952), older)
- Explanation from a vendor blog: in scans "every page … is a JPEG that has to be decoded," and turning the sidebar off helps. — [Basalt](https://basaltformac.com/blog/large-pdf-preview-slow/)

**Editing existing text**
- Review sites consistently name "Preview cannot edit the existing text inside a PDF or run OCR on scanned documents" as its two limits. — [MacHow2](https://machow2.com/best-pdf-mac/); Apple's own guide confirms that you cannot edit PDF text in Preview. — [Apple Support](https://support.apple.com/guide/preview/annotate-a-pdf-prvw11580/mac)

### Inferences
- The plan's core (forms, sign, organize, OCR, compress) matches the real pain well. The most valuable promise is "**your form data and annotations will still be there, and visible in Acrobat, after you save**." That is a reliability promise, not a feature. Tahoe regressions keep this pain alive in 2025–26.
- Compression with **visible quality and size control** (a preview of the result, a target size such as "under 5 MB for a portal") is a real differentiator against Preview's single black-box filter.
- Big-file performance (thumbnails and search on 500+ page scans) should go into the test suite as a selling point.

### Gaps
- I could not measure relative search volume (no Google Trends or keyword tool access). The ranking above is by how many forum threads and SEO pages I found, not by query volume.
- I could not get Reddit's r/mac, r/MacOS, or r/macapps threads (blocked).

## 2. Top complaints about each major app

### Takeaway
- **Acrobat:** subscription cost and cancellation fees (now an FTC/DOJ lawsuit), AI Assistant pop-ups that won't stay off, bloat, slowness, sign-in prompts.
- **PDF Expert:** "lifetime" doesn't include major versions, plus the forced account and subscription switch.
- **Wondershare:** refund and auto-renew traps, bot-only support.
- **UPDF:** the Mac App Store build lacks OCR, plus bugs and AI upsells.
- **PDFgear:** "free, but why?", closed source, weak AI.
- **Preview:** reliability (see section 1).
- **Nitro:** I found almost no consumer sentiment.

### Cited Findings
**Adobe Acrobat**
- FTC and DOJ sued Adobe in June 2024. The early termination fee is "50 per cent of the remaining payments" when you cancel in year 1, hidden in fine print. Online cancellation means clicking through many pages, and phone cancellations get dropped. — [Silicon UK](https://www.silicon.co.uk/e-regulation/ftc-adobe-suit-568368), [Computing](https://computing.co.uk/news/4324811/us-government-sues-adobe-concealing-fees-complicating-cancellations). In May 2025 Adobe's motion to dismiss was **denied**. — [Bloomberg Law](https://news.bloomberglaw.com/litigation/adobe-fails-to-escape-ftc-suit-over-subscription-cancellations). Later outcome: not found (gap).
- AI Assistant: "The AI Assistant pop-up when I try to search is incredibly annoying and covers part of the page… There's no X to close it out." — [Acrobat UserVoice](https://acrobat.uservoice.com/forums/931921-adobe-acrobat-in-browsers/suggestions/48325505-ai-assistant-is-annoying)
- "unclicking the Generative AI preference continues to put it back on every time I open up another pdf." Another user: disabling it "does NOT remove the botton from the tool bar." — [Adobe Community](https://community.adobe.com/questions-9/remove-ai-assistant-button-from-acrobat-1290490); "Acrobat: I don't want any AI in my Adobe Apps. Can AI be turned off?" — [Adobe Community](https://community.adobe.com/questions-9/acrobat-i-don-t-want-any-ai-in-my-adobe-apps-can-ai-be-turned-off-1290342)
- On privacy and performance: "I do not want your AI analyzing my personal documents"; it "causes noticeable lag issues, even when I've 'disabled' it." — (same group of Adobe Community and UserVoice threads: [1](https://acrobat.uservoice.com/forums/590923-acrobat-for-windows-and-mac/suggestions/50322765-remove-ai-assistance), [2](https://acrobat.uservoice.com/forums/914680-acrobat-reader-for-ios/suggestions/48914369-turn-off-ai-assistant), [3](https://community.adobe.com/t5/acrobat-discussions/stop-with-the-ai-user-prompts-in-acrobat-it-s-getting-ridiculous/m-p/15153169) "Stop with the AI user prompts in Acrobat, it's getting ridiculous")
- There was enough volume that Adobe staff posted "**We Heard You: Full Control Over AI Features in Acrobat**." — [Adobe Community](https://community.adobe.com/questions-9/we-heard-you-full-control-over-ai-features-in-acrobat-1305625)
- Bloat: "Bloated Acrobat app" — [Adobe Community](https://community.adobe.com/questions-9/bloated-acrobat-app-1625997); "bloated inefficient product, cancelling subscription" (a long-time user who cancelled over AI features, February 2025) — [Adobe Community](https://community.adobe.com/questions-9/bloated-inefficient-product-cancelling-subscription-1300380); the Reader installer is about 2 GB on Windows (November 2025) — same group of results; HN "The Size of Adobe Reader Installers Through the Years" — [HN 45012931](https://news.ycombinator.com/item?id=45012931)
- HN thread "Acrobat is intrusive, slow and non-customizable." A commenter said Reader asked them to sign in to an account and pay to open a PDF (platform not confirmed). — [HN 45598776](https://news.ycombinator.com/item?id=45598776)
- Mac Reader "lagging, slow and unusable" on Ventura. The fix was disabling "new Acrobat." — [Adobe Community](https://community.adobe.com/questions-12/adobe-reader-lagging-slow-and-unusable-macos-ventura-13-2-1-1527226)
- What Acrobat still wins on, per MacRumors posters: preflight, form **creation**, print production. — [MacRumors 2471049](https://forums.macrumors.com/threads/is-there-an-alternative-to-acrobat.2471049/), [MacRumors 2421548](https://forums.macrumors.com/threads/is-there-a-solid-option-against-adobe-acrobat.2421548/) (about 2024–25; exact dates not verified)

**PDF Expert (Readdle)**
- When it moved to subscription, it forced account creation "even if paid V2 customer." A user: Readdle "lied about the 'lifetime'". The Readdle rep's reply: "Lifetime PDF Expert users will get all minor updates… a major release such as PDF Expert 4 won't be included in the Lifetime access." Another user: doc-to-PDF conversion "used to work in V2 but this new version wants me to buy the subscription." — [MacRumors 2350184](https://forums.macrumors.com/threads/pdf-expert-switching-to-subscription-model-forces-account-creation-even-if-paid-v2-customer.2350184/page-2) (**2022, older**, but it explains why people distrust "lifetime" today)
- App Store: "introduced payment for everyone rendering your previous purchase worthless"; features they had bought were moved behind a subscription. — [App Store reviews](https://apps.apple.com/us/app/pdf-expert-editor-reader/id743974925?see-all=reviews) (mixed dates, some 2019 or earlier)
- Reliability: "prone to crashing when you have 3 or 4 pdfs open simultaneously," and a PDF corrupted twice during annotation (the reviewer dropped from 3 stars to 1); "files tend to get corrupted for no good reason if you have synced with cloud services"; "random crashes… loss of last few minutes of annotations." — [App Store](https://apps.apple.com/us/app/pdf-expert-editor-reader/id743974925?see-all=reviews), [JustUseApp](https://justuseapp.com/en/app/743974925/pdf-expert-pdf-editor-reader/reviews)
- Trustpilot: a user charged for a £39.99 yearly plan they say they did not subscribe to; the scanner crashes repeatedly. — [Trustpilot Readdle](https://www.trustpilot.com/review/pdfexpert.com)
- Positive: on MacRumors and in review sites it is still "the best PDF editor for most Mac users," with a "genuinely Mac-friendly interface." — [MacHow2](https://machow2.com/best-pdf-mac/). One MacRumors poster paid about $25 by buying outside the App Store. — [MacRumors 2421548](https://forums.macrumors.com/threads/is-there-a-solid-option-against-adobe-acrobat.2421548/)

**PDFelement / Wondershare**
- Trustpilot PDFelement (about 3,100 reviews): support is bot-only; a lifetime-license buyer was told to "purchase another package before a refund would be issued"; a refund was denied the same day as purchase; "cancelled twice" and still charged. — [Trustpilot PDFelement](https://www.trustpilot.com/review/pdf.wondershare.com), [CA page 2](https://ca.trustpilot.com/review/pdf.wondershare.com?page=2)
- Wondershare company page (about 567 reviews): unwanted yearly renewals, refunds denied the same day, a renewal charged after cancelling. — [Trustpilot Wondershare](https://www.trustpilot.com/review/www.wondershare.com)
- PissedConsumer: 1.5 stars from 129 reviews, 82% unfavorable, "deceptive renewal practices." — [PissedConsumer](https://wondershare.pissedconsumer.com/review.html)
- App Store (2021): after an update, saving without a watermark asked them to buy a new plan, even though they already had a yearly subscription. — [App Store PDFelement](https://apps.apple.com/us/app/pdfelement-pdf-editor-viewer/id1516765045?see-all=reviews). A 2026 review warns that the AI add-on trial renews at an annual price, so "set a reminder to cancel before day seven." — [max-productive.ai](https://max-productive.ai/ai-tools/wondershare-pdfelement/)
- Counterpoint: the Mac App Store rating is about 4.5 from about 2.1K ratings (secondary source, not verified). — same results as above

**UPDF**
- The Mac App Store build **lacks OCR**, and Intel Macs get no OCR at all. UPDF support: "at this time, we do not have a solution for offering OCR support for users on Intel-based Mac devices." — [How-To Geek, "Feature-Packed but Buggy"](https://www.howtogeek.com/855530/updf-for-mac-review-feature-packed-but-buggy/) (about 2022); [AppSumo Q&A](https://appsumo.com/products/updf/questions/the-ocr-button-seems-to-be-missing-1210683/). This confirms the plan's premise, but I could not confirm the 2026 status.
- Capterra: "very slow load times and the software signing me out frequently"; a reviewer wants the AI pricing split so they pay only for what they use. — [Capterra UPDF](https://www.capterra.com/p/255423/UPDF/reviews/). Trustpilot summary: concerns about "certain features being automatically added as paid subscriptions." — [Trustpilot UPDF](https://uk.trustpilot.com/review/updf.com?page=7). An App Store reviewer avoids the AI because it is a subscription. — [App Store UPDF](https://apps.apple.com/us/app/updf-ai-pdf-editor-converter/id1619925971?mt=12&see-all=reviews&platform=mac)
- Claims of aggressive marketing or astroturfing: **I found no evidence** in the searchable results (Reddit, where these claims usually appear, was blocked).

**PDFgear (free)**
- Praised as free, with no watermark, and it edits existing text. — [PCWorld](https://www.pcworld.com/article/702374/best-free-pdf-editors.html), [Trustpilot about 9,878 reviews](https://ie.trustpilot.com/review/pdfgear.com) ("clean, user friendly and free!")
- The "catch" comments: "the AI makes things up constantly"; closed source, no Linux; a review says "lacks OCR functionality," which conflicts with other sources that list OCR (unresolved). A guide notes a paid version "may be introduced in the future." — [AlternativeTo](https://www.alternativeto.net/software/pdfgear/about/); [Wikipedia](https://en.wikipedia.org/wiki/PDFgear)

**Nitro PDF Pro**: it appears in MacRumors alternative lists and Spanish review sites ("can be expensive for some users"), but I found no substantive Mac user complaints. — [MacRumors 2421548](https://forums.macrumors.com/threads/is-there-a-solid-option-against-adobe-acrobat.2421548/)

**Free / open-source sentiment (HN)**
- Ask HN "Is there a good open-source alternative to Adobe Acrobat?" (about January 2026). The answers recommend combinations: Okular + qpdf, "**Preview + qpdf**" on macOS, Stirling-PDF (self-hosted), PDF24, pdftk, and Foxit "very good." — [HN 46764607](https://news.ycombinator.com/item?id=46764607)
- 2025–26 has seen a flood of "Show HN" free PDF editors, met with skepticism about licensing (BreezePDF and the MuPDF AGPL). — [HN 47555636](https://news.ycombinator.com/item?id=47555636), [HN 47563103](https://news.ycombinator.com/item?id=47563103), [HN 47556134](https://news.ycombinator.com/item?id=47556134), [HN 46675231](https://news.ycombinator.com/item?id=46675231), [HN 44901683](https://news.ycombinator.com/item?id=44901683) (EmbedPDF "doesn't fully handle XFA")

### Inferences
- The three trust killers are: (a) "lifetime" that isn't, (b) renewals and refund traps, and (c) AI forced into the UI. The plan's "no account, no cloud, no AI, pay once" answers all three. The marketing should say exactly what "forever" covers (for example, "all 1.x and 2.x updates"), because PDF Expert's case shows people read "lifetime" as including major versions.
- Free competitors (PDFgear, browser tools, Show HN projects) put a lid on prices for basic tasks. A $29.99 app has to win on **trust, being native, reliability, and privacy**, not on features.
- Watch out: Basalt (basaltformac.com) appears again and again with SEO content on exactly the plan's themes: compression, slow large PDFs, Bates numbering, redaction for law firms, perpetual license. It looks like a direct indie competitor. The pricing researcher should check it.

### Gaps
- Nitro and PDFgear: little substantive user sentiment found.
- There is no reliable 2026 status for UPDF App Store OCR or for the outcome of the Adobe FTC case.

## 3. Willingness to pay, and attitudes to subscriptions, AI, watermarks, and privacy

### Takeaway
Mac users clearly prefer one-time licenses (36% vs 30% for any subscription in the one Mac survey I found, which is dated and from a vendor). There is active backlash against AI in PDF apps. Privacy concern about upload-based tools is real and is already being used as a marketing angle. I found **no direct evidence of a specific price point** like "$29.99" from users (gap).

### Cited Findings
- Setapp survey of Mac users: **36% prefer one-time lifetime licenses, 17% annual subscriptions, 13% monthly.** The source is about 2022 and sponsored by a subscription vendor. — [TechRepublic](https://www.techrepublic.com/article/survey-reveals-mac-app-purchasing-trends/)
- Distrust of "one-time": some apps "claim to be 'one-time' but pop up again for upgrades." — [Setapp](https://setapp.com/how-to/track-and-optimize-mac-app-spending). A perpetual current-version license "lets you keep the version you purchased, but a future major release may cost extra." — [Daytactic](https://daytactic.com/blog/best-one-time-purchase-mac-apps/)
- MacRumors posters value PDFpen for "no forced upgrades," an education discount, and a license instead of a subscription. — [MacRumors 2421548](https://forums.macrumors.com/threads/is-there-a-solid-option-against-adobe-acrobat.2421548/)
- Counter-view: "whether the price is high or low is orthogonal to whether it's a subscription." — [Kartick Substack](https://kartick.substack.com/p/subscriptions-are-the-right-way-to-16-06-11)
- AI: the user request on Acrobat UserVoice is for a clear setting to turn it off completely and keep the app "simple, fast, and private." — [UserVoice](https://acrobat.uservoice.com/forums/590923-acrobat-for-windows-and-mac/suggestions/50322765-remove-ai-assistance). A long-time user cancelled Acrobat over AI. — [Adobe Community](https://community.adobe.com/questions-9/bloated-inefficient-product-cancelling-subscription-1300380). UPDF reviewers avoid or object to the AI subscriptions. — [Capterra](https://www.capterra.com/p/255423/UPDF/reviews/)
- Watermarks: free trials (PDFelement) stamp watermarks on exports and limit conversion and compression; the 2021 App Store complaint was about a watermark showing up after an update. — [Fixthephoto](https://fixthephoto.com/pdfelement-review.html), [App Store](https://apps.apple.com/us/app/pdfelement-pdf-editor-viewer/id1516765045?see-all=reviews). PDFgear's "no watermark" is a headline reason people recommend it. — [PCWorld](https://www.pcworld.com/article/702374/best-free-pdf-editors.html)
- Privacy: iLovePDF deletes uploads within 2 h and Smallpdf within 1 h (their own claims), yet reviewers say that for "contracts, medical records, financial statements, or anything covered by professional secrecy, the upload model itself is the risk," and advise "use a local tool that never uploads the file." — [iLovePDF legal](https://www.ilovepdf.com/help/legal), [Smallpdf](https://smallpdf.com/blog/is-smallpdf-safe), [gethonestpdf](https://www.gethonestpdf.com/blog/is-smallpdf-safe-2026), [RaptorPDF](https://www.raptorpdf.com/is-ilovepdf-safe) (competitor sources, not neutral)

### Inferences
- "No AI" can be stated outright as a feature ("your documents never leave your Mac, no AI reads them"). That matches the Acrobat backlash and the professional-secrecy concern.
- **Risk to the plan's free tier:** putting watermarks on signing, OCR, and compression copies the pattern users resent in PDFelement, and it competes badly with PDFgear and Preview, which have no watermarks. A better option may be a time-limited full trial, or a page or document limit, instead of watermarks. At minimum, say clearly up front what gets watermarked.

### Gaps
- No user posts were found that name a price they would pay for a simple Mac PDF app. Reddit was blocked, and this is where such posts usually are.
- No independent 2024–26 survey on subscription vs one-time for Mac utilities.

## 4. Pain points by professional segment, including Spanish speakers

### Takeaway
- **Lawyers:** redaction and Bates numbering are the two things free tools (Preview) cannot do, and they are the main reason lawyers stay on Acrobat.
- **Spain:** certificate signing (FNMT/DNIe) is effectively mandatory for professionals and for many students (TFG). Preview cannot do it. Users are pushed to Acrobat Reader (free) or AutoFirma, both of which break often on macOS.
- **XFA government forms:** they cannot be opened in Preview or most non-Adobe viewers.
- **Students, accountants, real estate:** little segment-specific Mac sentiment found.

### Cited Findings
**Lawyers**
- "Redaction and Bates numbering are the two features that free PDF software typically lacks." — [Missouri Bar News](https://news.mobar.org/what-tricks-can-free-pdf-software-do/)
- "macOS ships nothing that does it. Preview cannot, Automator's PDF actions cannot" (Bates). The advice: stamp Bates numbers before redacting, and keep the number in the page content rather than as an annotation. — [Basalt (vendor)](https://basaltformac.com/blog/bates-numbering-mac/), [Basalt redaction workflow](https://basaltformac.com/blog/pdf-redaction-for-law-firms/)
- Free browser redaction tools are marketed as "No Adobe, No Preview Workaround," which implies users try to redact in Preview by drawing black boxes. That is unsafe because the text stays underneath. — [WildAndFreeTools](https://wildandfreetools.com/blog/redact-pdf-mac-free-no-adobe-preview/); LawNext keeps a whole "Redaction" software category for lawyers. — [LawNext](https://directory.lawnext.com/categories/redaction/)

**Spanish speakers: certificate signing**
- Applesfera tutorial: Acrobat Reader can sign with a digital certificate and **Vista Previa (Preview) cannot**. — [Applesfera](https://www.applesfera.com/tutoriales/como-firmar-pdf-certificado-digital-macos). This conflicts with Tenorshare, which lists Preview as an option. That is likely wrong, because Preview only adds image signatures. — [Tenorshare ES](https://www.tenorshare.es/edit-pdf/firmar-pdf-con-certificado-digital-en-mac.html)
- The Madrid Bar Association (ICAM) publishes a guide "Cómo firmar digitalmente documentos PDF con Adobe Reader DC en Mac" (How to digitally sign PDFs with Adobe Reader DC on Mac). The Universidad de La Rioja publishes signing instructions for TFG (final-year thesis) submissions. These show institutions require certificate signatures from lawyers and students. — [ICAM PDF](https://web.icam.es/bucket/firmar%20digitalmente%20pdf%20MAC%20Acrobat%20DC.pdf), [UniRioja](https://www.unirioja.es/facultades_escuelas/fct/TFG/Instrucciones_firmarPDFs.pdf)
- AutoFirma on macOS Ventura opens but finds no FNMT certificate in the Keychain. Suggested fixes: Java 8, Full Disk Access, Safari, restart. — [Comunidad de Apple 253744732](https://communities.apple.com/es/thread/253744732). Universidad de Málaga FAQ: on Mac you have to pick "almacén de claves del sistema" (the system keystore) in AutoFirma. — [UMA FAQ](https://cau.sci.uma.es/faq/index.php?action=artikel&cat=32&id=333&artlang=es). "Solución a que AutoFirma no te muestre ningún certificado digital o no funcione con DNIe" (Fix for AutoFirma not showing any digital certificate or not working with DNIe). — [JASoft](https://www.jasoft.org/Blog/post/solucion-a-que-autofirma-no-te-muestre-ningun-certificado-digital)
- "Problema al firmar con los nuevos certificados de la FNMT" (Problem signing with the new FNMT certificates) in Acrobat. The fix offered (request a new certificate) was called tedious. — [Adobe Community ES](https://community.adobe.com/t5/acrobat-discussions/problema-al-firmar-con-los-nuevos-certificados-de-la-fnmt/td-p/13297711); "error al firmar con certificado electrónico de la FNMT" (error signing with an FNMT electronic certificate): credential invalid; allowing the certificate in Preferences > Signatures did not fix it for one user. — [Adobe Community](https://community.adobe.com/questions-9/error-al-firmar-con-certificado-electronico-de-la-fnmt-1264102)
- Count: **6 of the 9** Spanish-language results on certificate signing were troubleshooting pages for failures. That suggests frequent friction.

**Spanish speakers: XFA forms**
- "Formularios XFA PDF dinámicos en Mac y Safari" (dynamic XFA PDF forms on Mac and Safari) — [AppleAyuda](https://www.appleayuda.com/pregunta/95239/formularios-xfa-pdf-dinamicos-en-mac-y-safari). XFA forms show a blank page, an error, or "Please wait..." outside Acrobat/Reader, and browsers don't support them. — [files.co](https://files.co/es/blog/formularios-pdf-rellenables/), [Adobe Community](https://community.adobe.com/questions-12/unable-to-open-xfa-dynamic-pdf-in-ios-mac-and-android-1521299) (2020). Even PDF Expert has a help page "XFA is not supported." — [Expert PDF support](https://support.expert-pdf.com/hc/en-us/articles/14228998817556-XFA-is-not-supported-How-to-open-and-edit-this-PDF-file)

**Mexico/LatAm (SAT e.firma)**
- I found nothing specific. e.firma uses .cer/.key files, not .p12. I could not confirm how Mac users sign PDFs with it. — gap

**Students**
- Only generic guides: Preview is "the easiest answer… for quick PDF markup" but has "limited annotation options"; Skim is popular with academics but has no mobile sync or OCR. — [Setapp](https://setapp.com/how-to/annotate-pdf-on-mac), [Carleton guide](https://gouldguides.carleton.edu/c.php?g=147129&p=963781). Tahoe's highlight bugs (section 1) hit students directly.

### Inferences
- For Spanish professionals (abogados, gestores, asesores fiscales, funcionarios) and TFG students, **PAdES certificate signing with Keychain/FNMT/DNIe is close to a must-have**. The plan puts it in v1.5/v2. Free Acrobat Reader + AutoFirma do cover it, so it is not a reason to buy unless it is far easier. "Sign with your FNMT certificate in 2 clicks, no Java, no AutoFirma" could be the strongest hook for the Spanish market. It is worth testing as an early v1.x feature, since Apple's Security framework can access identities in the Keychain.
- XFA: PDFKit cannot render it. The plan's "detect and warn" approach is right. The message should tell people the form needs Acrobat Reader, which is free, so they don't blame the app.
- Redaction is high-intensity for lawyers but carries liability. Leaving it out of v1 is reasonable. The app should then actively *prevent* fake redaction (a black box over text) or warn about it, because users try it.

### Gaps
- No accountant- or real-estate-specific Mac PDF sentiment found (beyond generic signing and forms).
- I don't know which specific Spanish government portals still serve XFA in 2026 (AEAT, SEPE, and the Seguridad Social mostly use web forms; not verified).
- e.firma (SAT) on Mac: no data.

## 5. Common dealbreakers in 1–2 star reviews

### Takeaway
The recurring 1-star triggers are: **file corruption or lost annotations**, **crashes with several or large files**, **paid features taken away or moved behind a subscription**, **unwanted renewals or refunds refused**, **watermarks appearing after an update**, and **forced sign-in or account**.

### Cited Findings
- Corruption and crashes: PDF Expert reviews ("corrupted twice," "crashing when you have 3 or 4 pdfs open," cloud sync corrupting files). — [App Store](https://apps.apple.com/us/app/pdf-expert-editor-reader/id743974925?see-all=reviews), [JustUseApp](https://justuseapp.com/en/app/743974925/pdf-expert-pdf-editor-reader/reviews)
- Bait and switch: "rendering your previous purchase worthless." — [App Store PDF Expert](https://apps.apple.com/us/app/pdf-expert-editor-reader/id743974925?see-all=reviews); a watermark after an update despite paying. — [App Store PDFelement](https://apps.apple.com/us/app/pdfelement-pdf-editor-viewer/id1516765045?see-all=reviews)
- Billing: "cancelled twice" and still charged; refunds refused the same day. — [Trustpilot PDFelement](https://www.trustpilot.com/review/pdf.wondershare.com); a charge for a yearly plan the user did not subscribe to. — [Trustpilot Readdle](https://www.trustpilot.com/review/pdfexpert.com)
- Account and sign-in: PDF Expert forced account creation (2022). — [MacRumors](https://forums.macrumors.com/threads/pdf-expert-switching-to-subscription-model-forces-account-creation-even-if-paid-v2-customer.2350184/page-2); UPDF "signing me out frequently." — [Capterra](https://www.capterra.com/p/255423/UPDF/reviews/)
- Missing promised features: the UPDF App Store build has no OCR. — [How-To Geek](https://www.howtogeek.com/855530/updf-for-mac-review-feature-packed-but-buggy/)

### Inferences
- The plan's "always write to a copy, then replace" plus a 30+ real-PDF regression suite targets the number-one dealbreaker. Mention it in the App Store description ("never overwrites your original until the save succeeds").
- Avoid any change after launch that moves paid features into a new tier. Users punish this with 1-star reviews years later.

### Gaps
- I could not scrape App Store reviews in bulk (fetch blocked), so there are no counts by category.

## 6. Unmet needs and "I wish there was an app that…"

### Takeaway
The clearest unmet need is: **a Preview that doesn't break files**. That means trustworthy forms and annotations that show up in Acrobat, controllable compression, fast on huge scans, and easy certificate signing (Spain), with no account, no AI, and no subscription. Power users currently piece this together (Preview + qpdf, Stirling-PDF, PDF24 online).

### Cited Findings
- HN users on macOS combine "Preview + qpdf" for encryption and quick edits, and Stirling-PDF for complex jobs. That suggests no single trusted Mac app covers the middle ground. — [HN 46764607](https://news.ycombinator.com/item?id=46764607)
- Older HN: "Ask HN: How is there not a full-featured open-source PDF editor/viewer?"; scanned-PDF cleanup "still lacks a single good tool"; LibreOffice Draw "mangles fonts" on re-export. — [HN 18762856](https://news.ycombinator.com/item?id=18762856) (2018, older), [HN 37995726](https://news.ycombinator.com/item?id=37995726) (2023)
- An Acrobat user's wish: keep the app "simple, fast, and private." — [UserVoice](https://acrobat.uservoice.com/forums/590923-acrobat-for-windows-and-mac/suggestions/50322765-remove-ai-assistance)
- Users want **pay only for what they use**, for example AI search vs summary split out. — [Capterra UPDF](https://www.capterra.com/p/255423/UPDF/reviews/)
- Many new indie "simple PDF" tools launched on HN in 2025–26. Demand exists, but so does crowding. — [HN 47555636](https://news.ycombinator.com/item?id=47555636), [HN 47563103](https://news.ycombinator.com/item?id=47563103), [HN 46675231](https://news.ycombinator.com/item?id=46675231)

### Inferences
- Possible positioning: "**The PDF app that doesn't lose your work**." Lead with reliability and compatibility with Acrobat (appearance streams for filled fields), then compression with a target size, then OCR. Lead with "No AI, no account, no cloud" as the trust line.
- For the Spanish-speaking market, "firma con certificado FNMT/DNIe" (signing with an FNMT/DNIe certificate) is the feature most likely to turn a free-Preview user into a buyer. It should be reconsidered for an early v1.x release.

### Gaps
- Explicit "I wish there was an app that…" posts live mostly on Reddit (r/macapps, r/mac), which I could not reach. A follow-up pass with Reddit access is strongly recommended to collect verbatim wishes, price expectations, and UPDF astroturfing claims.
