# UX best practices and differentiation for a simple, native Mac PDF app (as of 2026-10-24)

Scope: product design, UX patterns, macOS integration, onboarding/free tier, trust signals, and feature prioritization for the $29.99 one-time "everything Preview can't do" app described in `00_plan_original.txt`. Pricing, competitor matrices, user complaints and low-level feasibility are covered by other researchers.

Research caveat (applies to all sections): web search in this session returned few primary reviews from MacStories, 9to5Mac or The Sweet Setup, and no Reddit r/macapps threads. Several fetches of macworld.com and coyotetracks.org failed with DNS errors. Much of the "what users praise" evidence below comes from secondary or affiliate-style blogs and is flagged as such. Effort estimates (low/medium/high, for a solo developer using Claude Code) are the researcher's own judgment, not sourced facts.

---

## 1. What reviewers and users praise in the UX of the best Mac PDF apps (PDF Expert, Preview, Skim, PDF Squeezer)

### Takeaway
Praise clusters around three things: **speed on large files** (no hangs when opening or scrolling), a **native, uncluttered UI** that doesn't overwhelm despite many tools, and, for single-purpose tools like PDF Squeezer, **drop-a-file, see-the-result immediacy** (before/after size, nothing saved until you confirm). Mac power users also reward "Mac-assed" conventions: real menus, a real Settings window, keyboard shortcuts and system integration.

### Cited Findings
- PDF Expert is called "the smoothest, most Mac-native experience" of the alternatives tested. It handled documents "without the brief hangs I saw in Preview when opening large files" — [Medium: 4 Mac Preview alternatives](https://medium.com/data-science-in-your-pocket/4-mac-preview-alternatives-i-tried-for-pdfs-images-1980c7db94e1) (single blogger, anecdotal)
- PDF Expert is described as having "a minimalist, modern, Apple-native user interface" with "extremely fast loading and rendering", and a layout where "four main tabs keep things simple"; one reviewer "did not feel that it was overwhelming" despite the many tools — [The Business Dive review 2026](https://thebusinessdive.com/pdf-expert-review); [pdnob roundup](https://www.pdnob.com/pdf-editor/best-pdf-reader-for-mac.html) (affiliate-style sources, weak)
- Counterpoint: pdnob notes PDF Expert's interface "occasionally required an extra click or two to access less common tools", and some advanced tools cost extra — [pdnob](https://www.pdnob.com/pdf-editor/best-pdf-reader-for-mac.html)
- A Mac buyer said PDF Expert is "almost as good as Adobe Acrobat but much lighter on your Mac" — [PDF Expert listing on the App Store](https://apps.apple.com/app/pdf-expert/id743974925) / reseller page (anecdotal)
- Older (El Capitan-era) Cult of Mac review framed PDF Expert as "the lightweight, powerful viewer your Mac needs" — [Cult of Mac](https://www.cultofmac.com/398539/pdf-expert-mac-review/) (over 10 years old)
- Preview remains "more convenient for signing, form filling" and is free; TechRadar calls it the best Apple PDF reader but notes it lacks advanced editing — [Medium](https://medium.com/data-science-in-your-pocket/4-mac-preview-alternatives-i-tried-for-pdfs-images-1980c7db94e1); [TechRadar](https://www.techradar.com/best/best-pdf-reader-for-mac)
- Skim is praised for reading and marking up long documents: reading bar, snapshots, magnifier, bookmarks and a searchable notes pane, plus AppleScript support. Others call it "not as polished" — [Medium](https://medium.com/data-science-in-your-pocket/4-mac-preview-alternatives-i-tried-for-pdfs-images-1980c7db94e1); [AlternativeTo: Skim](https://alternativeto.net/software/skim/?p=2)
- A reviewer noticed small details: in one app search hits are listed in document order, while "With Preview… the hits seem to appear in a more or less random order" — [Medium](https://medium.com/data-science-in-your-pocket/4-mac-preview-alternatives-i-tried-for-pdfs-images-1980c7db94e1)
- **PDF Squeezer (Macworld review):** files dropped onto the window "are processed immediately with the chosen profile". The sidebar shows the compression achieved and a comparison of original vs new size. It offers three presets (Light/Medium/Strong) plus custom profiles. Files stay unchanged until you click Save, and the originals then go to the Trash. Its Finder Quick Action (compress from Finder, Touch Bar or Services) was the reviewer's favorite automation — [Macworld: PDF Squeezer 4 review](https://www.macworld.com/article/234641/pdf-squeezer-4-review.html)
- PDF Squeezer drawbacks: Medium/Strong presets made some image-based text unreadable, and the Quick Action needed laborious setup (enable via Automator, then install in preferences). MacG called it "more laborious to activate" than the share extension it replaced — [Macworld](https://www.macworld.com/article/234641/pdf-squeezer-4-review.html); [MacG](https://www.macg.co/logiciels/2020/06/pdf-squeezer-4-compresse-encore-mieux-les-pdf-114465). PDF Squeezer 4 sells for $19.99 on the App Store — [App Store](https://apps.apple.com/app/id1502111349)
- "Mac-assed Mac app" (Brent Simmons, crediting Collin Donnell) means apps that are "unapologetically Mac apps… not trying to wow us with all their custom not-Mac-like UI (which often isn't very accessible)" — [inessential](https://inessential.com/2020/03/19/proxyman); [Daring Fireball](https://daringfireball.net/linked/2020/03/20/mac-assed-mac-apps)
- Gruber's qualities of such apps include following the HIG, doing things "the Mac way" so they are easy to learn, and craft — [Daring Fireball: Sketch / Mac apps](https://daringfireball.net/2020/11/sketch_mac_app_mac_apps). In July 2026 Gruber wrote that "truly native, idiomatically correct Mac-assed Mac apps are resurgent", and praised an app for having "a Settings window that is … a window" — [Daring Fireball, 2026-07-04](https://daringfireball.net/linked/2026/07/04/from-the-archive-electron-decline-of-native-apps)
- Caution on tooling: Paulo Andrade (linked by Gruber, July 2026) argues SwiftUI "does not make it easy to create great Mac apps" — [Daring Fireball, 2026-07-12](https://daringfireball.net/linked/2026/07/12/andrade-swiftui)

### Inferences
- Perceived speed is the number-one "feels Mac-like" signal. Concrete decisions: lazy thumbnail rendering, opening a 500-page PDF to page 1 instantly, and never blocking the main thread during OCR or compression (progress shown in a sidebar or toolbar, with work cancellable). Effort: **medium** (PDFKit handles rendering; the discipline is async work plus testing on large files).
- Copy PDF Squeezer's "drop → instant preview of result → explicit Save" loop for every transform action (compress, OCR, merge). It is the best-reviewed UX pattern in the category for single tasks. Effort: **low–medium**.
- Avoid PDF Squeezer's mistake: make the Finder Quick Action work with zero setup. App Intents and an Action/Share extension are discovered automatically on modern macOS (see section 3).
- Hybrid SwiftUI + AppKit is the safe path. PDFView is AppKit (NSView) anyway, so wrap it, and use SwiftUI for inspectors and sheets. Andrade's critique suggests not forcing pure SwiftUI for the document window. Effort: inherent to the build.
- "Mac-assed" checklist to adopt, nearly free: full menu bar with every command, standard shortcuts (⌘O/⌘S/⌘⇧S/⌘P/⌘F/⌘Z/⌘⇧Z, ⌘+/⌘−, ⌥⌘1 sidebar), a real Settings window (⌘,), window state restoration, Recent Documents, Services, AppleScript/App Intents, and full VoiceOver labels. Effort: **low** if done from day one, **high** to retrofit.

### Gaps
- No primary MacStories, 9to5Mac, The Sweet Setup or Macworld PDF Expert reviews could be retrieved this session (macworld.com DNS failures). No Reddit r/macapps threads surfaced. Highlights and Nitro UX praise was not found.
- No quantitative data (e.g. App Store review text mining) on which UI decisions drive ratings.

---

## 2. Task-first hub ("What do you want to do?") vs document-first (Preview-style)

### Takeaway
No public A/B data was found comparing task-hub and document-first landing screens for PDF tools. Web tools (iLovePDF, Smallpdf) are task-first because they have no file context. Even iLovePDF's own iOS app moved toward a **homepage with recent files plus tools**. The best fit for a Mac app is a hybrid: document-first when a file is opened (Finder double-click, drag to Dock), plus a lightweight **Welcome / "Tools" window** shown when the app launches without a document.

### Cited Findings
- iLovePDF redesigned its iOS app from a landing screen "which took you straight to a list of files to import" to one that "acts more like a real homepage", with a recent-files carousel, favorites and storage categories. The developer said "Redesigning the home screen was a question of reorganization". No metrics were published — [iLovePDF blog: new iLovePDF for iOS](https://ilovepdf.com/blog/new-ilovepdf-for-ios)
- A G2 reviewer (UI/UX designer) praises iLovePDF because merging, splitting and converting take "just a few clicks" — [G2: iLovePDF](https://www.g2.com/products/ilovepdf) (anecdotal)
- PDF Squeezer is effectively a single-task "drop zone" app, and reviewers liked that dropped files are processed immediately — [Macworld](https://www.macworld.com/article/234641/pdf-squeezer-4-review.html)

### Inferences
- Recommended pattern (effort **low–medium**):
  1. **No document open** → a Welcome window (like Xcode or Pages) with 6–8 large tiles: *Fill & Sign, Compress, Make Searchable (OCR), Combine Files, Organize Pages, Scan from iPhone, Protect, Images → PDF*. Recent files sit underneath, and the whole window is a drop target. A file dropped onto a tile runs that task.
  2. **Document open** → document-first window (thumbnails sidebar, page view, inspector). A **"Tools" toolbar menu / ⌘K command palette** offers the same task verbs, so the hub vocabulary carries through.
  3. Task tiles map 1:1 to App Intents / Quick Actions (section 3), so the same verbs show up in Finder, Spotlight and Shortcuts.
- Why the hybrid: macOS users arrive mostly by double-clicking a PDF, so the app must be a good default PDF viewer to win "Open With" status. Many target users (freelancers, small offices) think in tasks ("I need to sign this", "I need it under 10 MB"), and the task tiles also show off the feature set to trial users.
- Opening to a hub every time a file is double-clicked would feel un-Mac-like and slow. Show the hub only when there is no document.

### Gaps
- No conversion or retention data comparing the two approaches was found (no Smallpdf case study, no UX teardowns with metrics). Treat the recommendation as a reasoned design choice, not evidence-backed.

---

## 3. Cheap, highly visible macOS integration opportunities

### Takeaway
In macOS 26 Tahoe, **App Intents are the single highest-leverage integration**. One implementation exposes actions in Shortcuts, **Spotlight (Actions tab, with user-assignable Quick Keys)**, Siri/Apple Intelligence, and the new **Mac folder automations** ("run when a file is added to a folder"). Add a Finder Quick Action/Share extension and a Dock/window drop target, and the app is present everywhere a user touches a PDF.

### Cited Findings
- WWDC25 "Develop for Shortcuts and Spotlight with App Intents": apps can run App Intents **directly from Spotlight on Mac**, and adopting App Intents for Shortcuts also makes actions available in Spotlight. For an intent to appear in Spotlight, its parameter summary must include all required parameters without defaults — [WWDC25 session 260](https://developer.apple.com/videos/play/wwdc2025/260/)
- Same session: **personal automations come to Mac**, with Mac-specific types including **folder and external-drive automations**. Example: an "invoice processing shortcut… runs every time I add a new invoice to a specific folder". Any intent available on macOS can be used in Mac automations — [WWDC25 session 260](https://developer.apple.com/videos/play/wwdc2025/260/)
- Same session: the Shortcuts **"Use Model" action** (on-device model, Private Cloud Compute or ChatGPT) can take an app's entities as input. Content from your app is passed to the model as JSON — [WWDC25 session 260](https://developer.apple.com/videos/play/wwdc2025/260/)
- Spotlight and Visual Intelligence are new clients of App Intents in 2025, and App Intents is described as the app's route into Apple Intelligence — [WWDC25 session 275](https://developer.apple.com/videos/play/wwdc2025/275/); [WWDC25 session 244](https://developer.apple.com/videos/play/wwdc2025/244/)
- macOS Tahoe Spotlight has an Actions section (⌘3). Actions from installed apps' App Intents "are automatically included", and users can "Add Quick Keys" (e.g. "sm" → Send Message). Spotlight is context-aware and can filter files by type, including PDFs — [AppleInsider](https://appleinsider.com/inside/macos-tahoe/tips/spotlight-got-a-huge-upgrade-in-macos-tahoe-heres-how-to-use-it); [OWC/MacSales](https://eshop.macsales.com/blog/98115-spotlight-gets-supercharged-in-macos-tahoe-your-complete-guide-to-getting-more-out-of-the-default-mac-launcher/); [TWiT](https://twit.tv/posts/tech/mastering-spotlight-actions-macos-tahoe)
- macOS 27 "Golden Gate" (WWDC26, June 2026) roundups list "Faster PDF saving" and "More document formats in Preview" and "better PDF editing" among its changes, plus a new Siri AI and Liquid Glass tweaks — [Basic Apple Guy: macOS wall of text](https://basicappleguy.com/haberdashery/macoswalloftext); [TechRadar macOS 27](https://www.techradar.com/computing/mac-os/macos-27-golden-gate-announced-at-wwdc-2026-heres-everything-you-need-to-know); [Macworld macOS 27 guide](https://www.macworld.com/article/3139330/macos-27-mac-features-siri-apple-intelligence-release-date-compatibility.html) (secondary; Apple's own WWDC26 macOS guide: [developer.apple.com](https://developer.apple.com/wwdc26/guides/macos/))
- PDF Squeezer's Quick Action (Finder, Touch Bar, Services) was its reviewer's favorite automation, but setup friction was criticized — [Macworld](https://www.macworld.com/article/234641/pdf-squeezer-4-review.html); [MacG](https://www.macg.co/logiciels/2020/06/pdf-squeezer-4-compresse-encore-mieux-les-pdf-114465)

### Inferences (with effort)
Priority-ordered integration list:

| # | Integration | What the user sees | Effort | Notes |
|---|---|---|---|---|
| 1 | **App Intents** for Compress, Make Searchable (OCR), Combine, Images→PDF, Remove Metadata, Add Password, Rotate, Extract Pages | Shortcuts actions, Spotlight Actions with Quick Keys ("cmp" → Compress PDF), Siri, folder automations ("every PDF dropped in ~/Scans gets OCR'd") | **Low–Medium** | One codebase feeds 4+ surfaces. Make every parameter optional/defaulted so actions appear in Spotlight (per session 260). Requires the macOS 26 SDK; Spotlight actions only on 26+. |
| 2 | **Finder Quick Action / Action extension** ("Compress PDF", "Make Searchable", "Combine into PDF") on right-click > Quick Actions and the Finder preview pane | Visible every time they right-click a PDF | **Low–Medium** | Must work out of the box. Avoid PDF Squeezer's Automator-setup friction. Verify that App Intents with file inputs also appear as Finder Quick Actions on macOS 26 (unconfirmed this session). |
| 3 | **Drag & drop everywhere**: Dock icon, Welcome tiles, thumbnail sidebar (drop PDFs or images to insert pages), drag pages *out* to Finder to extract them | Feels magical, zero learning | **Low** | Dock drop = `application(_:open:)`. Dragging thumbnails out as files is the standout delight. |
| 4 | **Continuity Camera scan** (File > Import from iPhone > Scan Documents) | Already in plan | **Low** | NSMenu item via `NSServicesMenuRequestor` / Continuity Camera API. |
| 5 | **Share menu / Share extension** ("Compress for email", then share via Mail) | Medium visibility | **Low–Medium** | |
| 6 | **Batch window**: drop a folder → choose action → output folder, with a per-file before/after table | Small offices love it | **Medium** | Same engine as the intents. |
| 7 | **Services menu** entries | Power users | **Low** | Mostly superseded by Quick Actions/App Intents. |
| 8 | **Quick Look** | — | Skip | macOS already Quick Looks PDFs. Only relevant if the app had a custom format. |
| 9 | **Spotlight indexing** | — | Skip / Low | macOS already indexes PDF text. The value is that OCR'd output becomes Spotlight-searchable, which is a marketing point ("make your scans findable in Spotlight"). |
| 10 | **Menu-bar droplet** | Niche | **Low–Medium** | Optional v1.x. Folder automations via App Intents cover the "watch folder" need natively. |
| 11 | **Handoff / iCloud Drive** | — | Low priority | Document-based app gets iCloud Drive file access for free. Handoff has little value without an iOS app. |

- Apple Intelligence / Siri: positioning is "no AI", but exposing App Intents lets *users* chain the app into Apple's on-device "Use Model" action if they want to. The app itself never sends data anywhere. This is a privacy-safe way to be "AI-compatible" without shipping AI features. Effort: **free** once intents exist.
- **Platform-floor conflict with plan:** the plan targets macOS 14+. Spotlight actions, Mac automations and Liquid Glass are macOS 26 features. Recommendation: build with the macOS 26 SDK, keep a 14+ deployment target if desired, and light up 26-only integrations with `#available`. Alternatively, consider raising the floor to macOS 15 to cut test matrix. (Researcher's judgment; check with feasibility researcher.)

### Gaps
- Could not confirm from a primary source whether App Intents taking `IntentFile` inputs automatically appear as Finder Quick Actions in macOS 26/27. Session 260's page summary didn't cover file-based intents.
- No primary WWDC26 session details retrieved on new App Intents or Siri capabilities in macOS 27 (only secondary roundups). Release date of macOS 27 not confirmed here (macworld.com fetch failed).
- Usage data on how many users actually use Quick Actions or Shortcuts was not found.

---

## 4. Design language: Liquid Glass, HIG for document apps, keyboard, accessibility (including accessible output PDFs)

### Takeaway
Liquid Glass (macOS 26) belongs to the **navigation/controls layer** (toolbar, sidebar, inspectors), never the document canvas. Use standard AppKit/SwiftUI toolbars and controls to get it mostly for free. Accessibility of the *app* (VoiceOver, keyboard) is cheap if done from the start. Producing **tagged/accessible output PDFs is not supported by PDFKit** and should be excluded from v1.0 claims.

### Cited Findings
- Apple describes Liquid Glass as a translucent material that "reflects and refracts light" and says the new design "establishes a common foundation for the look and feel of Mac apps", with refreshed materials and controls system-wide. Session code shows removing glass from a toolbar item, tinting a toolbar control, prominent toolbar item style (`.prominent`), and badges — [WWDC25 session 310](https://developer.apple.com/videos/play/wwdc2025/310/)
- Third-party (non-Apple) HIG summary: use Liquid Glass for sidebars, toolbars and navigation chrome, and avoid it in primary content areas (documents, media) — [skills.sh macos-hig-designer](https://skills.sh/designnotdrum/skills/macos-hig-designer) (unofficial; Apple's HIG Materials page could not be fetched this session)
- macOS 27 includes "Liquid Glass tweaks" — [TechRadar macOS 27](https://www.techradar.com/computing/mac-os/macos-27-golden-gate-announced-at-wwdc-2026-heres-everything-you-need-to-know)
- "Mac-assed" apps avoid custom non-Mac UI, which "often isn't very accessible" — [inessential](https://inessential.com/2020/03/19/proxyman)
- PDFKit tagging: a developer on the Swift forums found "hardly any documentation" on generating accessibility-tagged PDFs with PDFKit. Another developer studying the latest PDFKit docs found "no mention of semantic tagging, read order or the PDF/UA format". Tagging is available via Adobe's Auto-Tag API or Foxit SDK (third-party, paid/cloud) — [Swift Forums](https://forums.swift.org/t/dynamic-pdfs-with-accessibility-tags-using-pdfkit/67419); [Adobe Community](https://community.adobe.com/t5/acrobat-sdk-discussions/generate-pdfs-with-accessibility-tags-dynamically-using-pdfkit-in-swift/m-p/14101856)
- On macOS 26+, Vision can extract structured paragraphs, tables and lists from documents (via a wrapper project) — [mac-ocr on GitHub](https://github.com/privatenumber/mac-ocr)

### Inferences (with effort)
- **Liquid Glass:** use the system `NSToolbar`/SwiftUI `.toolbar`, `NavigationSplitView` sidebar and inspector. Keep the PDF canvas an opaque, neutral background. One `.prominent` toolbar button for the primary action in context (e.g. "Sign", "Save Compressed"). Avoid custom glass panels over the page. Effort: **low** (mostly free with the macOS 26 SDK; test the macOS 14/15 appearance too).
- **Document-app conventions:** NSDocument / DocumentGroup behaviors (autosave, Versions via File > Revert To > Browse All Versions, Duplicate, Rename in the title bar, proxy icon drag). These are both "native" signals and trust signals (section 6). Effort: **low–medium** (PDFKit + NSDocument; autosave for PDFs needs care to avoid rewriting large files constantly).
- **Keyboard:** single-key tool switching when not editing text (e.g. H highlight, T text, S sign, A arrow/select), ⌘K command palette for all tasks, arrow keys plus Delete in the thumbnail grid, ⌘⌥R rotate, and the full shortcut list in the Help menu. Effort: **low**.
- **App accessibility:** label every toolbar or custom control for VoiceOver, support Dynamic Type equivalents in sidebar/inspector, respect Reduce Transparency (Liquid Glass falls back automatically with system controls), and keep the signature pad keyboard-reachable (typed signature option). Effort: **low** if built in.
- **Output accessibility:** do NOT claim tagged/PDF/UA output in v1.0. PDFKit can't author structure trees. The honest win is that OCR adds a real text layer, so screen readers and search can read scans that were previously images-only. That is a genuine accessibility improvement worth stating. Tagging could be a v2 research item (macOS 26 structured Vision output plus a custom structure-tree writer = **high** effort).

### Gaps
- Apple's official HIG pages (Materials / Liquid Glass, Toolbars, Document-based apps) could not be fetched. Specific official wording on "don't use glass in content" is unverified from Apple directly.
- No confirmation whether macOS 27 PDFKit added tagging APIs.

---

## 5. Onboarding & free-tier design that converts without feeling scammy

### Takeaway
Users in this category most resent **"free" that collapses at export** (surprise watermarks on the output). The plan's current free tier (sign, OCR and compress *with watermark*) is risky: a watermarked signature or compressed contract is useless, so it reads as bait. A clearer model is **free forever for viewing/annotating/organizing, plus either a full-featured time-limited trial or a small number of free "pro" exports, with no watermark**, and a single honest one-time unlock screen.

### Cited Findings
- Watermark resentment across PDF editors: Master PDF Editor's free version "will inject a watermark. $50 for the un marked version", and a reviewer called the developer "misleading". An Icecream PDF Editor user complained of "a watermark every time I edit files". A G2 reviewer disliked having to upgrade to remove the trial watermark — [AlternativeTo: Master PDF Editor](https://alternativeto.net/software/master-pdf-editor/about); [Software Advice: Icecream PDF Editor](https://www.softwareadvice.com.au/software/224197/icecream-pdf-editor); [G2: AceThinker PDF Writer](https://www.g2.com/products/acethinker-pdf-writer/reviews)
- Icecream reviewers also objected to a "lifetime" licence that required another purchase after two major upgrades — [Software Advice](https://www.softwareadvice.com.au/software/224197/icecream-pdf-editor). This is relevant to how "pay once" is worded.
- A vendor blog (UPDF, biased) claims r/pdf complaints show how quickly "free" promises collapse at the export stage — [UPDF blog](https://updf.com/edit-pdf/online-pdf-editor-free-without-watermark/)
- RevenueCat 2026 (115k+ mostly mobile subscription apps): hard paywalls have a median Day-35 conversion of 10.7% vs 2.1% for freemium. Revenue per install at Day 60 is $3.09 vs $0.38. Year-one retention is similar (27% vs 28%). Over 60% of conversions happen within the first week, and about a third on Day 0. Freemium "remains the right call when free users drive word of mouth" — [RevenueCat: 2026 benchmarks](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026); [RevenueCat: hard paywall vs freemium](https://www.revenuecat.com/blog/growth/hard-paywall-vs-freemium) (subscription/mobile data; applicability to a $29.99 one-time Mac app is limited)
- Mac App Store trials for non-subscription apps: make the app free and add a **$0 non-consumable IAP named "XX-day Trial"**. Before the trial, the app must state its duration, what becomes unavailable, and the price of full functionality — [9to5Mac](https://9to5mac.com/2018/06/10/app-store-free-trials-more/); [Cult of Mac](https://www.cultofmac.com/553297/apple-finally-brings-free-trials-to-app-store/)
- Developer criticism: Daniel Jalkut (MarsEdit) said the app becomes "essentially useless" after the trial and that paid-turned-free apps rank oddly in charts. Banktivity's developer reported Family Sharing problems with the unlock-IAP approach (2019) — [Cult of Mac on Jalkut](https://www.cultofmac.com/news/macos-developer-explains-problems-with-app-stores-free-trials); [IGG Software](https://www.iggsoftware.com/blog/2019/01/no-good-deed-goes-left-unpunished/)

### Inferences (with effort)
- **Recommended free tier (effort: low–medium, StoreKit 2):**
  - Free forever: open/view, search, annotate, organize pages (merge/split/reorder/rotate/delete), fill interactive forms. This makes the app a good *default PDF viewer*, which keeps it on the Mac, drives word of mouth, and gives the paywall many chances to be seen.
  - Pro (one-time $29.99): Sign, OCR, Compress, Protect/Metadata, iPhone scan to searchable PDF, batch, Quick Actions/Shortcuts.
  - Trial mechanics: **7-day full trial via $0 "7-day Trial" IAP**, or (alternative) **"3 free Pro exports"** with a visible counter ("2 of 3 free exports left"). Either way, **no watermarks on output**. Users accept limits they can see up front. They resent surprises at export time.
  - If watermarks are kept anyway, show them **live in the preview before export** (not only in the saved file), and never on signatures.
- **Paywall UX that earns respect:** one sheet, shown in context when a Pro action is chosen ("Compress is part of PDF X Pro"), showing: the price once, "Pay once. Yours forever on all your Macs", "No account, no subscription, files never leave your Mac", a Restore Purchase button, and a "Not now" button that returns to the document. Don't show the paywall at first launch, since users arriving via a double-clicked PDF need to see value first. The RevenueCat finding that most conversions happen in week one argues for a visible but non-blocking "Unlock Pro" toolbar item during the trial.
- **Lifetime wording:** say "includes all 1.x updates" or define what "forever" means explicitly. Vague "lifetime" claims drew complaints (Icecream).
- **Onboarding:** no multi-screen tour. A Welcome window (section 2) is the onboarding. Add contextual empty states and one-time coach marks, e.g. "Tip: right-click any PDF in Finder > Quick Actions > Compress PDF", plus a Settings button to verify the extension is enabled. Effort: **low**.

### Gaps
- No data specific to Mac one-time-purchase apps comparing trial vs watermark vs usage-limit conversion. RevenueCat data is subscription/mobile.
- Current (2026) state of Apple's $0 trial IAP guideline wording and Family Sharing behavior not re-verified (sources are 2018–2019).

---

## 6. Trust & safety signals ("your files never leave your Mac", never corrupt files)

### Takeaway
Trust in a PDF app is earned by **visible reversibility** and **showing results before committing**. PDF Squeezer's "nothing changes until Save, originals to Trash" plus before/after sizes is the model. Preview's compression is known to degrade quality silently, which is an opening for an app that shows exactly what will happen.

### Cited Findings
- Apple's own guide warns that compressing in Preview "can lower its quality" and that results depend on the options chosen. The Quartz filter's settings are not exposed — [Apple Support: Preview reduce file size](https://support.apple.com/guide/preview/prvw1509)
- Smallpdf (competitor, biased) says Preview "often reduces image quality quite aggressively". A MacSales commenter said the built-in filter made a document unreadable, and users resort to hand-made Quartz filters (150/100 dpi) — [Smallpdf blog](https://smallpdf.com/blog/reduce-pdf-file-size-mac-preview); [OWC/MacSales](https://eshop.macsales.com/blog/53900-how-to-reduce-the-file-size-of-a-pdf-in-macos/)
- A July 2026 Microsoft Tech Community thread asks how to shrink mixed text/vector/scan PDFs on Mac without losing sharpness. Suggested Print → Save as PDF workarounds reportedly strip form fields and interactivity — [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/windows-10/how-to-minimize-pdf-file-size-on-mac-without-losing-quality/m-p/4541353) (claim not independently verified)
- PDF Squeezer: files stay unchanged until Save, originals go to Trash, and before/after size is shown. But Medium/Strong presets made some image text unreadable — [Macworld](https://www.macworld.com/article/234641/pdf-squeezer-4-review.html)

### Inferences (with effort)
- **Compression:** preview pane with original vs compressed side by side at 100% zoom on the page with the smallest text, the estimated output size *before* saving, and a "target size" mode ("Under 10 MB for email", "Under 2 MB for portals") that searches DPI/JPEG quality and picks the best quality that fits. Warn if text becomes unreadable (e.g. if OCR confidence on the compressed version drops versus the original). Never strip form fields or links (unlike Print→PDF). Effort: **medium** (target-size search is a loop over existing compression; the readability check reuses Vision).
- **OCR:** show recognized text highlighted on the page after OCR (toggle "Show text layer"), language auto-detect with override (Spanish/English), and a "Select text to verify" hint. Effort: **low–medium**.
- **Never corrupt:** write to temp, validate by re-opening with PDFKit (page count, form field count, and that it renders), then atomically replace. Support Versions (Browse All Versions) and multi-level Undo across page operations. For destructive transforms (compress, OCR, flatten), default to **"Save as new file" named `contract (compressed).pdf`** beside the original, with an option to replace. Effort: **medium**. Already partly in plan; the validation step is the addition.
- **Privacy as UI, not just marketing:** a small "On this Mac" lock badge in the status area during OCR/compress, an App Store privacy label of "Data Not Collected", no network entitlement at all in the sandbox (verifiable claim), and a one-line Settings note "This app has no network access". Effort: **low**. Removing `com.apple.security.network.client` is a strong, checkable trust signal. Note that this conflicts with any web-licensing (Paddle) build, which would need network for activation, so plan the MAS build without network.
- **Detect-and-warn for limits** (XFA forms, signed PDFs whose signatures would be invalidated by edits, encrypted files): clear banner explaining what can't be done, rather than silent failure. Already in the plan risk table. UX effort: **low**.

### Gaps
- No user-research data quantifying how much "offline/no account" messaging lifts conversion in this category.

---

## 7. Feature prioritization, small delights, and what to exclude

### Takeaway
The highest perceived value per effort comes from **Compress (with target size + before/after)**, **Fill & Sign as one flow with saved snippets**, **OCR "Make Searchable"**, and **page organization via drag & drop of thumbnails/files**. All map to Preview's documented weak spots. Small, cheap delights (target-size compression, reusable form snippets, initials, date stamp, images/clipboard → PDF, drag pages out to extract) differentiate more than big features. Exclude anything that breaks "simple": text editing, conversion to Office, AI, cloud, collaboration and certificate signatures.

### Cited Findings
- Preview compression lacks control and degrades quality (see section 6) — [Apple Support](https://support.apple.com/guide/preview/prvw1509); [OWC/MacSales](https://eshop.macsales.com/blog/53900-how-to-reduce-the-file-size-of-a-pdf-in-macos/)
- Users who mainly need signing and forms find Preview "more convenient", so the bar for Fill & Sign is "at least as easy as Preview" — [Medium](https://medium.com/data-science-in-your-pocket/4-mac-preview-alternatives-i-tried-for-pdfs-images-1980c7db94e1)
- Preview hangs briefly on large files, and alternative apps are praised for smooth large-document handling — [Medium](https://medium.com/data-science-in-your-pocket/4-mac-preview-alternatives-i-tried-for-pdfs-images-1980c7db94e1)
- A $19.99 single-purpose compressor (PDF Squeezer) exists and is reviewed well, so compression alone has proven willingness to pay — [App Store](https://apps.apple.com/app/id1502111349); [Macworld](https://www.macworld.com/article/234641/pdf-squeezer-4-review.html)
- macOS 27 Preview gets "better PDF editing" and faster saving, so Preview's baseline is rising — [Basic Apple Guy](https://basicappleguy.com/haberdashery/macoswalloftext); [TechRadar](https://www.techradar.com/computing/mac-os/macos-27-golden-gate-announced-at-wwdc-2026-heres-everything-you-need-to-know)

### Inferences (with effort)
**MVP features ranked by perceived value ÷ effort (researcher judgment):**

| Rank | Feature | Perceived value | Effort | Key UX decision |
|---|---|---|---|---|
| 1 | Compress | Very high (constant forum ask; portals/email limits) | Medium | Target-size presets ("Email ≤ 10 MB", "Portal ≤ 2 MB", "Custom"), before/after size and visual preview, never strip forms |
| 2 | Fill & Sign | Very high (reason people open Acrobat) | Medium | One "Fill & Sign" mode: auto-detect fields, click anywhere on flat PDFs to type, Tab between fields, signature/initials/date one click away |
| 3 | OCR "Make Searchable" | High (clear Acrobat Standard gap per plan) | Low–Medium (Vision) | Single button, auto language, batch, Spotlight-findable output messaging |
| 4 | Organize pages | High | Low–Medium (PDFKit) | Thumbnail grid with drag-reorder, drop files/images to insert, drag pages out to extract, ⌘-click multi-select then rotate/delete |
| 5 | iPhone scan | Medium–High (very visible, demo-able) | Low | Scan → auto-OCR → save, in one step |
| 6 | Protect / metadata | Medium (offices, lawyers) | Low | "Remove personal info" one-click plus inspector showing what metadata exists |
| 7 | Annotate | Expected baseline (Preview does it) | Medium | Don't over-invest; parity with Preview plus single-key tools |

**Low-cost delights to add (v1.0 or v1.1):**
- **Compress to target size** ("make it under X MB"). Effort **low–medium** on top of compression. Top differentiator vs Preview.
- **Reusable form snippets / "My Info"** (name, address, email, phone, tax ID, today's date in local format) as a popover or autocomplete when clicking a field. Stored locally in the Keychain or app container. Effort **low**. High delight for freelancers filling recurring government forms.
- **Initials + date stamp** next to the signature in the signature palette. Effort **low**.
- **Images / clipboard → PDF** (File > New from Clipboard ⌘⌥N; drop JPG/PNG/HEIC to the Welcome window). Effort **low**.
- **Drag thumbnails out to Finder** to extract pages as a new PDF. Effort **low**.
- **Page numbers / simple text watermark / Bates numbering**. Effort **low–medium**. Bates appeals to the lawyer segment in the plan; consider v1.1.
- **Flatten form** ("Make final") so filled forms can't be altered. Effort **low**.
- **"Share compressed"** in the Share menu (compress to email size, then hand to Mail). Effort **low**.
- **Batch window** (folder in, folder out). Effort **medium**.
- Side-by-side compare: effort **high** for real diffing. Exclude from v1, or offer only "open two documents side by side" (free via window tiling).

**Explicitly exclude to stay simple** (aligns with plan's out-of-scope list): editing original PDF text, conversion to Word/Excel, certified redaction (risky to claim, since a fake redaction is a liability), certificate-based digital signatures, AI chat/summaries, cloud sync/accounts, collaboration/comments sync, form *authoring*, PDF/A or PDF/UA compliance claims, and tagged-PDF generation (section 4). Also avoid "tabs of tools" bloat: keep the toolbar to roughly 6 primary items with the rest in menus and ⌘K.

### Gaps
- No quantitative survey ranking these features by user demand was found this session. The ranking is inferred from Preview's documented weaknesses and proven paid niches (PDF Squeezer). The "user complaints" researcher may have better demand evidence.

---

## 8. App naming/branding patterns and localization

### Takeaway
No reliable sources were found this session on naming or localization performance in the PDF category. The recommendations below are inferences only. The plan already calls for an App Store–searchable name containing "PDF".

### Cited Findings
- Category names observed in this research all embed "PDF" with a benefit or persona word: "PDF Expert: Editor & Converter", "PDF Squeezer 4", "PDFelement", "UPDF" — [PDF Expert App Store](https://apps.apple.com/app/pdf-expert/id743974925); [PDF Squeezer App Store](https://apps.apple.com/app/id1502111349)
- PDF Expert's App Store title is localized per storefront (e.g. German "PDF Expert: Dateien bearbeiten") — [App Store CH](https://apps.apple.com/ch/app/pdf-expert-dateien-bearbeiten/id743974925)

### Inferences
- Naming pattern: short brandable word + "PDF" in the 30-character App Store name, with keywords in the subtitle. For example "<Name> PDF: Fill, Sign, Compress" (EN) and "<Name> PDF: Firmar, Llenar, OCR" (ES). Localize the subtitle and keywords per storefront like PDF Expert does. Effort: **low**.
- Avoid names that imply Adobe/Acrobat or Apple's Preview, which risk trademark rejection.
- Localization: Spanish + English from day one costs little with String Catalogs (Xcode) plus Claude Code translation, given a small UI surface (~300 strings). Vision OCR language support matters more than UI language for OCR value. Next candidates by Mac App Store market size would plausibly be German, French, Japanese and Portuguese (BR). Effort per language: **low** for UI, plus **low–medium** for App Store screenshots and metadata. Verify with market data from the pricing/market researcher.

### Gaps
- No data on App Store search volume for "PDF" variants, or on conversion lift from localization in this category. No Product Hunt launch analyses of PDF tools were retrieved.
