# Voice of the customer: what photographers want from AI denoise/upscale/sharpen on Mac, and what they complain about (2024–2026)

> **Method note (read first):** Research date 2026-10-24. In this environment, direct page fetching was blocked for every domain tried (dpreview.com, community.topazlabs.com, fstoppers.com, medium.com, alex-kunz.com, focus-on-photography-forum.net, thomasfitzgeraldphotography.com), and reddit.com is blocked for both search and fetch. So **no Reddit threads were read**, and quotes below come from search-engine extracts of the pages, not from full page reads. Quotes in "double quotes" are text the search tool returned as verbatim; everything else is paraphrased. Frequency rankings are qualitative: they count how many independent sources/threads raised a theme in about 35 searches, not a statistical sample. Items older than 2025 are marked **[older]**.

---

## Ranked map (summary for the report writer)

| # | Pain point / desire | Intensity | Frequency in sources | What it means for the $59 Mac app |
|---|---|---|---|---|
| 1 | Subscription anger at Topaz (Sept/Oct 2025) and fear of what Adobe will do (deal announced June 25, closed Sept 23, 2026) | Very high | Very high (DPReview, Topaz forum 50+ page transition thread, TalkPhotography, Focus-on-Photography, blogs) | The core thesis holds, but angry users mostly **stay on frozen perpetual Topaz versions** or move to **DxO PureRAW / Lightroom Denoise**, not to new unknown apps |
| 2 | Artifacts / over-processing: checkerboard/grid patterns, "waxy skin", detail smeared by aggressive Autopilot defaults, uncanny face recovery, wrecked fine feathers on heavy crops | High | High (Topaz forum bug threads, Nikonites, BCG, BirdForum, CaptureLandscapes, TechRadar) | A natural look, adjustable strength and a blend with the original are what people want; "no AI look" is a selling point |
| 3 | RAW round-trip problems: "fake" DNGs (TIFF in a DNG wrapper), missing camera profile in Lightroom, color shifts (Nikon reds), wrong color spaces | High for pros | Medium-high (Topaz forum, Lightroom Queen, Adobe community, DxO forum, DPReview) | Plan outputs JPEG/TIFF16/PNG only, with **no linear DNG**. That is a major workflow gap for the Lightroom/Capture One crowd |
| 4 | Batch speed and blocking UI: Lightroom Denoise locks the app (14.4–15.2), batch 5x slower than single image, old DNG workflow made 90–250 MB files | High for wedding/event | High (Adobe community, Lightroom Queen, Fitzgerald, Tim Grey) | Fast, background, overnight batch is a real differentiator **if** quality is close to DxO/Lightroom |
| 5 | Paid upgrade policies: DxO upgrade costs ($80–90 every ~year), Topaz renewal going $99 to $199, Skylum "Upgrade Pass" pressure | Medium-high | Medium (DxO forum, Topaz forum, Fstoppers on Skylum, Trustpilot) | A $29/yr "upgrade pass" echoes the model people already resent; it needs very clear "keep what you have" wording |
| 6 | Crashes and slowness on Mac (Topaz Photo AI 3.x on Sequoia, Intel Macs, large upscales, generative models) | Medium | Medium (Topaz forum, reviews, App Store listings) | Stability on Apple Silicon and a predictable time per image matter |
| 7 | Cloud credits / generative upscale: Gigapixel inside Adobe uses 10–20 credits per image, fails while still charging credits, face hallucination fears | Medium, rising | Medium (Adobe community, Adobe FAQ, reviews) | "On-device, no credits, no hallucinated faces" is a credible message after the Adobe deal |
| 8 | Wanting non-RAW input (JPEG, TIFF, HEIC, scans): PureRAW is RAW-only, and new Lightroom Denoise won't run on JPEG/HEIC/TIFF | Medium | Medium | The plan's JPEG/HEIC/PNG/TIFF input fills a real gap that PureRAW and Lightroom leave |
| 9 | Deblur (motion/lens) and face recovery as next features | Low-medium | Low (few explicit requests found) | Fine for v1.5, not a v1 requirement |
| 10 | Spanish-speaking market: same DxO-first advice, euro pricing (PureRAW €129.99, Adobe ~€12/month) | Low distinct signal | Low (few real forums surfaced) | No distinct needs found beyond localization and euro pricing |

---

## 1. Reaction to Topaz going subscription-only and to the Adobe acquisition; are photographers looking for alternatives, and which ones?

### Takeaway
Reaction to both moves was strongly negative and loud. But the most common responses are (a) "I'll keep my frozen perpetual Topaz version as long as it works", and (b) moving to tools people already know: **DxO PureRAW** (most recommended), **Lightroom's built-in Denoise** (for people already paying Adobe), **ON1 NoNoise** (cheapest one-time) and DxO PhotoLab. Brand-new, unknown one-time apps are almost never mentioned. Aiarty is promoted mainly by its own vendor content.

### Cited Findings
**Timeline (confirmed):**
- Topaz stopped selling and renewing perpetual licenses on **Sept 16, 2025**. Coverage said all Topaz software would be subscription-only from **Oct 3, 2025**. — [Topaz community transition thread p.50](https://community.topazlabs.com/t/topaz-studio-transition-questions/95039?page=50); [CG Channel, Sept 2025](https://www.cgchannel.com/2025/09/topaz-labs-to-end-perpetual-licenses-of-its-software/)
- The Topaz Studio transition Q&A thread on Topaz's own forum runs to **at least 51 pages**, which shows how intense the reaction was. — [Topaz community p.51](https://community.topazlabs.com/t/topaz-studio-transition-questions/95039?page=51)
- Adobe's acquisition of Topaz was announced **June 25, 2026** and **closed Sept 23, 2026**. SEC filings put the price at **$340M**. Topaz stays a standalone brand. — [Forbes, 2026-09-23](https://www.forbes.com/sites/dbloom/2026/09/23/adobe-closes-topaz-labs-deal-adds-ai-video--image-enhancement-tools/); [PhotographyTalk](https://www.photographytalk.com/adobe-owns-topaz-labs/); [Camera Jabber](https://camerajabber.com/photography-news/adobe-completes-topaz-labs-acquisition-topaz-stays-a-standalone-brand/)
- Adobe says Topaz products stay available as standalone offerings through Topaz's site. It has **not** said which features will run locally and which will use credits, or whether Topaz subscribers will get Adobe entitlements. — [Camera Times](https://cameratimes.org/adobe-topaz-labs-acquisition-complete-what-changes/); [remio.ai analysis](https://www.remio.ai/post/adobe-topaz-labs-acquisition-closes-but-independence-is-the-real-test); [CineD](https://www.cined.com/adobe-to-acquire-topaz-labs-ai-upscaling-and-image-enhancement-on-device-models-standalone-apps-to-continue/)

**Sentiment on the subscription move:**
- DPReview "Topaz Labs Apps are now Subscription only": a user whose Gigapixel, Photo AI and Video AI licenses had lapsed said they would not send Topaz more money. Another described a "severe subscription allergy" and said they would keep using Photo AI "as long as it works" but would not "jump on the subscription train". — [DPReview forum](https://www.dpreview.com/forums/threads/topaz-labs-apps-are-now-subscription-only.4824377/)
- Same thread: a user said the recent Topaz standalone titles and the subscription trials were "not significantly better than the On1 equivalents". Another said Topaz sharpening had reached "good enough", so new updates had little value to them. — [DPReview forum](https://www.dpreview.com/forums/threads/topaz-labs-apps-are-now-subscription-only.4824377/)
- Some perpetual owners were offered only the frozen "Photo AI 3" version, with a Studio renewal at $99 as the upgrade path. Frozen perpetual installs keep working, and cancelling Studio stops the Studio apps. — [DPReview "Topaz Going Subscription" p.3](https://www.dpreview.com/forums/threads/topaz-going-subscription.4815340/page-3); [Topaz community](https://community.topazlabs.com/t/education-studio-photo-license-upgrade/98810)
- A Topaz forum thread titled "Annual Topaz Photo AI – should I cancel?" shows subscribers weighing whether to cancel. — [Topaz community](https://community.topazlabs.com/t/discussion-annual-topaz-photo-ai-should-i-cancel/96575)
- PhotoWorkout calls the subscription "the main friction point": fair for power users, harder to recommend for people who need it a few times a month. — [PhotoWorkout review](https://www.photoworkout.com/topaz-photo-ai-review/)
- Silent Peak Photo's review headline: "Subscription Hurts Value". — [Silent Peak Photo](https://silentpeakphoto.com/photo-editing-apps/photo-editing-app-reviews/topaz-photo-ai-review/)
- Current Topaz pricing reported by reviewers conflicts: Topaz Photo at **$199/yr** after a first-year discount ([Topaz pricing page](https://www.topazlabs.com/pricing)); "$17–$39/month" ([CaptureLandscapes 2026](https://www.capturelandscapes.com/topaz-photo-ai/)); "$399/year via Topaz Studio" ([Capture the Atlas ES](https://capturetheatlas.com/es/programas-para-reducir-el-ruido/)). The prices conflict across sources.

**Sentiment on the Adobe acquisition:**
- Topaz's forum thread "Adobe to Acquire Topaz Labs" is mostly negative. Posters predicted the end of local processing and cited past Adobe acquisitions they had abandoned. One long-time user wrote they "could forfeit the ability to use either if Adobe tightens the screws on us" and called subscription costs too expensive. Another was "deeply disappointed by this move". — [Topaz community p.1](https://community.topazlabs.com/t/adobe-to-acquire-topaz-labs/103761); [p.2](https://community.topazlabs.com/t/adobe-to-acquire-topaz-labs/103761?page=2)
- Fstoppers (opinion) framed it as Adobe buying "one of the last good things in photo editing", arguing that Topaz's independence was its appeal. — [Fstoppers](https://fstoppers.com/originals/adobe-buying-one-last-good-things-photo-editing-903215)
- Anthony Morganti, a popular photography educator: "Adobe Is Acquiring Topaz Labs. Photographers Want Answers". — [Medium](https://medium.com/@anthonymorganti/adobe-is-acquiring-topaz-labs-photographers-want-answers-f1fe265acb10); Thomas Fitzgerald: "Adobe strikes again" — [blog, June 2026](https://blog.thomasfitzgeraldphotography.com/blog/2026/6/adobe-strikes-again-buys-topaz-labs)
- Counterpoint: some noted that Topaz had already gone subscription in Sept 2025, so the deal felt less like a sudden betrayal. One commentator noted that many video pros who rely on Topaz don't use Adobe as their main tool. — [search summary of Medium/Designtography coverage](https://medium.com/designtography-magazine/adobe-strikes-again-buys-topaz-labs-130f20244d81)

**What people recommend to each other:**
- On a Topaz-alternatives thread in Adobe's community, DxO PureRAW was recommended as attractively priced. — [Adobe community](https://community.adobe.com/questions-712/topaz-photo-ai-alternatives-1553656)
- On BirdForum, a user who dropped Topaz found Lightroom's built-in Denoise "roughly on par with DXO PR 5" until late 2025. Another member says PureRAW 6 is "generally a touch ahead" of Adobe Denoise in speed and quality. — [BirdForum (2025)](https://www.birdforum.net/threads/what-is-your-post-processing-image-software.470510/)
- A forum user: "use DxO PhotoLab for everything as [they] didn't want to go down the subscription route". — [BirdForum Topaz vs PhotoLab](https://www.birdforum.net/threads/thought-on-topaz-photo-ai-vs-dxo-photolab.448384/)
- On BCG Forums, a user said PureRAW recovered a soft face with strong sharpening and none of Topaz's artifacts. — [BCG forums](https://bcgforums.com/threads/topaz-ai-products.40122/); see also [BCG "Switching to DXO Pure Raw 6 from LrC and/or Topaz Photo AI 4.0.4?"](https://bcgforums.com/threads/switching-to-dxo-pure-raw-6-from-lightroom-classic-and-or-topaz-photo-ai-v-4-0-4.52926/page-2)
- 2026 reviewer roundups converge on DxO PureRAW for the hardest high-ISO files, Lightroom Denoise if you already pay for Adobe, and **ON1 NoNoise AI as "the cheapest one-off price"**. — [Finding the Universe 2026](https://www.findingtheuniverse.com/best-noise-reduction-software/)
- Other one-time options mentioned: Pixelmator Pro (Mac, $49.99), Upscayl (free, open source, local), Aiarty (perpetual; mostly self-promoted), Luminar Neo (one-time; prices of $149 and $249 conflict). — [AlternativeTo](https://alternativeto.net/software/topaz-photo-ai/about); [Aiarty (vendor)](https://www.aiarty.com/ai-image-enhancer/topaz-labs-alternative.htm)

### Inferences
- The plan's premise ("they left Topaz and want a one-time alternative") is directionally right about the **emotion**. But the observed **behavior** is staying on frozen versions or moving to established names (DxO, Lightroom, ON1). A new $59 app has to beat the default answer "just use PureRAW / Lightroom Denoise" with proof: side-by-side samples, speed numbers and a free trial.
- Upscaling (Gigapixel) is where Topaz is still seen as best-in-class, and where one-time alternatives are weakest. The upscale side may be a bigger opening than denoise, where DxO is the community default.
- Fear about the Adobe deal centers on **local processing ending and credits being metered**. That supports "100% on-device, no credits" as the lead message.

### Gaps
- No Reddit data (blocked). It could not be measured how often r/photography or r/WeddingPhotography mention specific alternatives.
- No reliable figure for how many Topaz users actually cancelled or switched.

---

## 2. Complaints about specific tools

### Takeaway
- **Topaz:** artifacts (grid/checkerboard, zigzags from sharpening), over-aggressive defaults and Autopilot, uncanny faces, Mac crashes, and subscription value.
- **Lightroom Denoise:** speed in batch, a blocked UI, huge DNGs in the old workflow, and RAW-only.
- **DxO PureRAW:** upgrade pricing, RAW-only, camera/lens support limits, and color-space issues.
- **Luminar:** upgrade-pass pressure, demos that oversell, and generative tools.
- **Pixelmator:** stagnation fears after Apple bought it.
- **ON1:** little signal found.

### Cited Findings
**Topaz Photo AI / Gigapixel**
- Faint checkerboard artifacts in dark backgrounds that show up when lifted later. A responder said the squares are a known issue, but the suggested fix (v2.3.1) didn't help the poster. — [Nikonites](https://nikonites.com/forum/threads/anyone-having-trouble-with-checkerboard-artifacts-in-the-backgrounds-with-topaz-ai.48274/) **[older]**
- Pixelated square artifacts in about **20% of images** in one user's Lightroom round trip over two days. — [Topaz community bug](https://community.topazlabs.com/t/one-or-more-pixelated-square-artifacts-in-output-tif-from-photo-ai/76597) **[older]**
- Colored zigzag pixel effects on scanned 4x5 film, traced to the sharpening model. — [Topaz community](https://community.topazlabs.com/t/weird-artefacts-at-pixel-level-using-photo-ai/51007) **[older]**
- "Photo AI artefacts, new version worse than before": complaints of artifacts and over-sharpening (late 2024). — [Topaz community](https://community.topazlabs.com/t/photo-ai-artefacts-new-version-worse-than-before/83199)
- BCG Forums: the AI products produce many artifacts, "particularly in backgrounds". — [BCG](https://bcgforums.com/threads/topaz-ai-products.40122/)
- BirdForum on heavily cropped bird record shots: Topaz output "looks ok until you zoom in ever so slightly". — [BirdForum](https://www.birdforum.net/threads/what-is-your-post-processing-image-software.470510/)
- CaptureLandscapes (2026): with Autopilot or default noise reduction, the software removes noise but also significant detail. The reviewer prefers PureRAW and finds Lightroom AI Denoise better than Topaz. — [CaptureLandscapes](https://www.capturelandscapes.com/topaz-photo-ai/)
- TechRadar lists as a con: face recovery "can look uncanny". — [TechRadar](https://www.techradar.com/computing/creative-software/topaz-photo-ai-review-image-correction-with-artificial-intelligence)
- Amateur Photographer's test: Topaz was fastest (25 s for a TIFF, against 85 s for PureRAW 3 and 94 s for Lightroom) but the **least good** of the three on quality. — [Amateur Photographer](https://amateurphotographer.com/software/adobe-lightrooms-denoise-tool-how-does-it-compare/) **[older, 2023]**
- Crash right after Autopilot analysis when clicking Apply (v3.3.0, macOS Sequoia, Oct 2024), and a crash on launch. — [Topaz community](https://community.topazlabs.com/t/crash-macos-sequoia-15-0-1/80340)
- Super Focus took about 25 min on an older Mac laptop. Intel Macs run it "just horribly slowly". Apple Silicon is "quite fast". — [Topaz community "Incredibly slow performance"](https://community.topazlabs.com/t/incredibly-slow-performance/58059); [Topaz community hardware thread](https://community.topazlabs.com/t/photo-ai-running-slowly-some-hardware-advice-please/62090); [VideoProc review](https://www.videoproc.com/resource/topaz-photo-ai-review.htm)
- DPReview: support response has become "too often... a poor or no response at all". — [DPReview Photo AI 4 review thread](https://www.dpreview.com/forums/threads/topaz-photo-ai-4-review.4804409/)
- Gigapixel generative upscale in Adobe apps: a generic failure while Firefly worked (Dec 2025), and credits deducted with no result. — [Adobe community](https://community.adobe.com/questions-712/topaz-gigapixel-for-generative-upscale-giving-error-message-we-have-encountered-an-issue-1619230); [Adobe bug report](https://community.adobe.com/bug-reports-403/p-firefly-won-t-upscale-images-but-it-still-takes-credits-1626948/index3.html)
- DPReview generative upscale comparison: Gigapixel "was better, but it still messed up the cars in the scene". — [DPReview](https://www.dpreview.com/forums/threads/comparison-of-photoshops-new-generative-upscale.4820479/)

**Lightroom Denoise**
- Old DNG workflow **[2023]**: about 2 min per 20 MB Olympus file with Lightroom locked; one Windows user saw about 6.5 min per image; output DNGs of 90 MB from 20 MB originals; a blogger saw 150–250 MB per image. — [Lightroom Queen "Rendering DNG using Denoise SLOW!"](https://www.lightroomqueen.com/community/threads/rendering-dng-using-denoise-slow.47654/); [Adobe community large DNG](https://community.adobe.com/t5/lightroom-classic-discussions/large-dng-files-in-lr-12-3/m-p/13919915); [Paolo Sartori 2025](https://www.paolosartoriphotography.com/blog/2025/6/game-changer-lightroom-ai-denoise-no-longer-creates-dng-files-heres-why-that-matters)
- 14.4 (mid-2025) applies Denoise in place without a DNG. Many welcomed it ("game changer"), but batches now run in a **modal dialog that locks Lightroom**. Fitzgerald: "One of the biggest complaints I received... when batch processing Denoise with the new method, it no longer updates in the background." — [Fitzgerald Aug 2025](https://blog.thomasfitzgeraldphotography.com/blog/2025/8/how-to-background-process-denoise-in-lightroom-classic-144-and-other-ai-settings); [Adobe idea "Bring back the ability of Enhance to run in the background"](https://community.adobe.com/t5/lightroom-classic-ideas/p-bring-back-the-ability-of-enhance-to-run-in-the-background-lrc/idi-p/15374596/page/11) (11+ pages of votes and comments); [Tim Grey Oct 2025](https://asktimgrey.com/2025/10/20/denoise-without-dng/)
- Mac: "Denoise on M1 MacBook Air is incredibly slow now". After a batch, switching photos and moving sliders is sluggish until metadata is saved (a reported bug). One user went from 15 min per image on Windows to **15 s on an M4 Pro**. — [Lightroom Queen "Speeding up LR Denoise?"](https://www.lightroomqueen.com/community/threads/speeding-up-lr-denoise.53507/); [Adobe community 14.4/14.5 issues](https://community.adobe.com/t5/lightroom-classic-discussions/issues-with-denoise-in-14-4-14-5/td-p/15484581)
- Feb 2026, LrC 15.2 on a Mac mini M4 Pro: a single image took 5–7 s, but in a batch the second image took 38–40 s ("five times longer in batch mode"). — [Adobe community](https://community.adobe.com/questions-675/denoise-takes-five-times-longer-in-batch-mode-than-single-image-1551176)
- One guide says batches run in the background again since **15.3 (April 2026)**. Single source, not checked against Adobe's release notes. — [lightroom-tools.com](https://lightroom-tools.com/blog/lightroom-classic-ai-denoise)
- Denoise now won't run on JPEG, HEIC or TIFF (RAW/linear DNG only). — [lightroom-tools.com](https://lightroom-tools.com/blog/lightroom-classic-ai-denoise); see also the Adobe idea [AI Denoise output to TIFF option vs DNG](https://community.adobe.com/t5/lightroom-classic-ideas/p-ai-denoise-output-to-tiff-option-vs-dng/idi-p/13912500/page/2)
- Wedding guide warning: pushed too far, denoise "waxes skin". — [findme.photo 2026](https://findme.photo/blog/ai-photo-editing-stack-wedding-photographers-2026)

**DxO PureRAW**
- Upgrade pricing: the v5 upgrade was only $10 below a new license on Black Friday ("greedy"; about $45 suggested as fair). And: "I bought PureRAW 2 three weeks ago and DxO says I need to pay $29 for the version 3 upgrade! I will no longer consider DxO for any products." — [DxO forum "Customer unfriendly upgrade policy"](https://forum.dxo.com/t/customer-unfriendly-upgrade-policy/49285)
- PureRAW 6 costs $139.99 (€129.99 in Spain) new, or about $89.99 to upgrade from v4/5. One year of camera/lens updates is included. — [Amateur Photographer PR6 review](https://amateurphotographer.com/review/dxo-pureraw-6-review/); [Silent Peak](https://silentpeakphoto.com/photo-editing-apps/photo-editing-app-reviews/dxo-pureraw-review/)
- It feels restrictive when your camera/lens combo isn't supported. Fuji X-Trans support came in stages (beta in v5, broader in v6). — [Silent Peak](https://silentpeakphoto.com/photo-editing-apps/photo-editing-app-reviews/dxo-pureraw-review/); [Amateur Photographer](https://amateurphotographer.com/review/dxo-pureraw-6-review/)
- RAW-only input, so no TIFF/JPEG. — [DxO forum "Pure Raw and Tiff?"](https://forum.dxo.com/t/pure-raw-and-tiff/25516)
- "PureRAW 4 useless due to wrong color spaces for DNG and JPG" (multi-page thread). Linear DNGs never embed ICC profiles. — [DxO forum](https://forum.dxo.com/t/pureraw-4-useless-due-to-wrong-color-spaces-for-dng-and-jpg/42175?page=3)

**Luminar Neo (Skylum)**
- Fstoppers critic: Skylum forces "re-purchase to get updates (Luminar 4, Luminar AI, Luminar Neo)" or pushes "Upgrade Passes", and feature demos work "nowhere near close to what they show". After complaints, Skylum "pretty much killed the subscription model" but replaced it with "confusing pricing". — [Fstoppers fall update review](https://fstoppers.com/artificial-intelligence/review-luminar-neo-fall-update-winner-some-powerful-new-tools-715721)
- DPReview thread verdict: "RAW tools: good. Generative AI: tragic. Masking: still allergic to edges." — [DPReview](https://www.dpreview.com/forums/threads/andy-reviews-skylums-luminar-neo-fall-update-and-praises-lightroom.4822169/)
- Trustpilot: an Ecosystem Pass bought under a different email couldn't be merged ("we don't have the time to do that now"). Reports of freezes and features not working. Support is otherwise praised. — [Trustpilot](https://www.trustpilot.com/review/skylum.com?page=2)

**Pixelmator Pro / Photomator**
- Apple completed the purchase in Feb 2025. Users fear asset-stripping (like Dark Sky) and slower development ("the change log has gone dead"). — [AppleInsider](https://appleinsider.com/articles/25/02/11/apple-makes-first-change-to-pixelmator-pro-with-a-new-splash-screen); [MacRumors forum](https://forums.macrumors.com/threads/so-whats-happening-with-pixelmator-and-photomator.2458589/)

### Inferences
- The most repeated **quality** complaint across tools is over-processing (waxy skin, smeared feathers, grid artifacts) rather than "not enough denoise". A default that leans natural, a strength slider and an "original blend" control (already in the plan as "mezclable") directly address it.
- Lightroom's speed and blocking pain is real but shrinking (in-place Denoise in 2025, background batch possibly back in April 2026). Competing on "faster than Lightroom" alone is fragile.

### Gaps
- ON1 NoNoise/Photo RAW complaints: not enough signal found.
- Pixelmator ML Super Resolution/Denoise quality complaints: none found.
- Topaz quality complaints are mostly 2023–2024 (v2–v3). Little was found on 2026 Topaz Studio "Photo" quality.

---

## 3. Workflow must-haves

### Takeaway
Pros live in Lightroom Classic/Capture One. The workflow they defend is **RAW in, cleaned *linear DNG* out, keep editing white balance and profile**. TIFF works but "bakes" white balance and profile. Wedding/event shooters want unattended whole-shoot batch runs, with PureRAW as the "batch everything" tool and Topaz for the hard frames. Non-RAW input (JPEG/TIFF) is a real gap in PureRAW and new Lightroom Denoise.

### Cited Findings
- **DNG/TIFF round trip:** "Topaz DNG files are simply tiff files in a dng wrapper." With TIFF, white balance and the raw profile are set before sending and "cannot be adjusted any more on return." — [Lightroom Queen "LRC and Topaz Denoise RAW Files"](https://www.lightroomqueen.com/community/threads/lrc-and-topaz-denoise-raw-files.44527/)
- "Missing Camera Profile" in Lightroom after the Photo AI plug-in round trip. The workaround was Edit In to TIFF. — [Topaz community](https://community.topazlabs.com/t/missing-camera-profile-in-lightroom-after-photo-ai-plug-in-edit-of-raw-file/52977); [Adobe community, yellowish tint DNG](https://community.adobe.com/t5/lightroom-classic-discussions/missing-camera-profile-after-importing-dng-from-topaz-denoise-ai/m-p/13113537) **[older]**
- Photo AI 3.0.0 plugin exported TIFF instead of DNG and users pushed back ("Resolved in 3.0.2"). Users treat DNG output as a must. — [Topaz community](https://community.topazlabs.com/t/plugin-exports-tiff-instead-of-dng-v3-0-0/67466?page=3)
- Color: Topaz "will often ruin the red colors for Nikon Z8/Z9 raw files sent as DNG" (single user). ORF color profile disappears in Photo AI. — [DPReview ORF thread](https://www.dpreview.com/forums/threads/color-profile-of-orf-file-disappears-in-topaz-photo-ai-how-to-fix-that.4782707/); [photoartfromscience color shift](https://www.photoartfromscience.com/single-post/how-to-fix-topaz-photo-ai-color-shift-problems); [Topaz "Export Color Profile"](https://community.topazlabs.com/t/export-color-profile/18828)
- Batch from Lightroom Classic loads only a few files ("Topaz support insist that it is a bug in Lightroom"). — [Adobe community](https://community.adobe.com/questions-675/topaz-denoise-ai-plug-in-problem-with-lightroom-classic-959493)
- The Lightroom cloud app doesn't support plugins at all, only Classic. — [Adobe community](https://community.adobe.com/t5/lightroom-ecosystem-cloud-based-discussions/can-i-install-topaz-denoise-in-adobe-lightroom-on-mac-version-i-am-using-is-not-lightroom-classic/m-p/13027487/highlight/true)
- Wedding practice: PureRAW for the whole shoot, Topaz for hard frames, Lightroom Denoise for dark reception frames. Test skin at 100% before batching. — [findme.photo 2026](https://findme.photo/blog/ai-photo-editing-stack-wedding-photographers-2026); [Finding the Universe](https://www.findingtheuniverse.com/best-noise-reduction-software/)
- Pre-processing pattern ("PureRAW first, then Lightroom") is the norm, including in Spanish-language forums. — [AI Photography Training](https://aiphotographytraining.substack.com/p/why-we-use-dxo-pureraw-as-a-pre-processor); [Fujistas foro](https://fujistas.com/foro/threads/experiencias-y-opiniones-sobre-dxo-pure-raw.69993/)
- **Speed benchmarks on Apple Silicon (PureRAW 6):**
  - M1 Max: about 30 s per Nikon Z9 file with DeepPRIME XD3. Canon R5 45 MP: 27 files in 11:46 (about 26 s per file).
  - M2 Mac Studio: 40 GFX 100 MP files in 5:54 with DeepPRIME 3 (about 9 s per file) against 28:10 with XD3 (about 42 s per file).
  - M2 Pro: 12 R5 files in 3:22 (about 17 s per file).
  - XD3 is about 2x slower than DeepPRIME 3.

  Sources: [Photography Life PR6](https://photographylife.com/dxo-pureraw-6-review-amazing-compression); [Shotkit PR6](https://shotkit.com/dxo-pureraw-6/); [PetaPixel 2026-04](https://petapixel.com/2026/04/09/dxo-pureraw-6-the-ultimate-beginners-guide/); [Julie Edwards](https://julieedwards-x.blog/2026/03/16/a-deep-dive-into-dxo-pureraw-6/)
- Lightroom Denoise: 5–7 s per image single on an M4 Pro (batch was slower until a fix). — [Adobe community](https://community.adobe.com/questions-675/denoise-takes-five-times-longer-in-batch-mode-than-single-image-1551176)
- Old reviewer advice: run large PureRAW batches overnight. — [Photography Life PureRAW 2](https://photographylife.com/reviews/dxo-pureraw-2) **[older]**
- Topaz is valued because it can denoise already-edited TIFF/JPEG, unlike PureRAW. — [Finding the Universe](https://www.findingtheuniverse.com/best-noise-reduction-software/)
- Event volume: Lightroom Denoise is called the "speed champ" and "good enough" for event volume. — [PhotoWorkout 2026](https://www.photoworkout.com/best-noise-reduction-software/)

### Inferences
- **Speed target:** to be competitive on M1–M4, about **5–15 s per 24–45 MP image** at "standard" quality puts a 2,000-image wedding at about 3–8 hours, so overnight. PureRAW XD3 at 26–42 s per image is the quality benchmark people accept for a slower "max quality" mode.
- **Linear DNG output is the single biggest workflow gap in the v1.0 plan.** Without it, wedding/event pros using Lightroom/Capture One treat the app as a JPEG/TIFF finisher, not a RAW pre-processor. Also, denoising *after* demosaic on a rendered RGB image generally can't match RAW-domain tools (DxO, Lightroom) at extreme ISO. That is an inference worth testing in the week-2 go/no-go.
- Metadata and color-profile preservation (already in the plan) responds to real, recurring complaints. Proper ICC tagging of TIFF16 output should be verified.
- A Lightroom Classic "Edit In" external-editor entry costs little, and it avoids the plugin-DNG headaches. Even though plugins are out of scope for v1, supporting Edit In (TIFF in, TIFF out, same folder, same name with a suffix) is a cheap win.

### Gaps
- No direct data on how fast photographers expect support for brand-new cameras. Only DxO's model ("support included for one year") was found.
- No M3/M4-specific PureRAW numbers. No Topaz 2026 speed numbers on M-series.
- No sources found on phone-JPEG or old-scan use cases specifically among pros. (The Topaz 4x5 scan artifact thread shows scan users exist.)

---

## 4. Features most wanted next

### Takeaway
Explicit requests found were sparse. The signals point to (1) **background/queued batch**, the most voted Lightroom idea in this area; (2) **non-RAW input**; (3) **natural face handling** (uncanny face recovery is a complaint, not a wish); and (4) **motion/lens deblur**, which Topaz and ON1 already sell. Generative upscale draws suspicion, not demand.

### Cited Findings
- Adobe idea "Bring back the ability of Enhance to run in the background" (11+ pages). — [Adobe community ideas](https://community.adobe.com/t5/lightroom-classic-ideas/p-bring-back-the-ability-of-enhance-to-run-in-the-background-lrc/idi-p/15374596/page/8)
- Adobe idea "AI Denoise output to TIFF option vs DNG". — [Adobe community](https://community.adobe.com/t5/lightroom-classic-ideas/p-ai-denoise-output-to-tiff-option-vs-dng/idi-p/13912500/page/2)
- "Paste settings from previous denoises again" (users want to reuse the same denoise settings across shots, like presets per ISO). — [Adobe community](https://community.adobe.com/t5/lightroom-classic-bugs/p-paste-settings-from-previous-denoises-again/idc-p/15397145)
- Deblur exists in competitors: Topaz "Unblur Image" (motion + lens blur), ON1 "Tack Sharp AI" with Deblur. — [Topaz](https://www.topazlabs.com/tools/unblur-image); [photoartfromscience on ON1](https://www.photoartfromscience.com/single-post/on1-photo-raw-2023-deblur-for-motion-blur-repair)
- Face hallucination warnings for generative upscale: faces with only a few usable pixels "may receive plausible but inaccurate features". — [itechguides](https://www.itechguides.com/photoshop-brings-low-res-images-back-to-life-with-generative-upscale/); [Media.io](https://www.media.io/comparison/topaz-labs-image-upscaler-review.html)

### Inferences
- A good v1.5 candidate is **presets per camera/ISO with "apply to all similar"**, which wedding shooters ask for implicitly through "paste settings". It is cheaper than face models, which need licenses (CodeFormer is non-commercial, as the plan notes).
- Deblur is in demand but hard. Promising it risks the "demo vs reality" backlash Skylum gets.

### Gaps
- No ranked feature-request data (Reddit polls and the Topaz feature-request board were unreachable). Video, astro and similar wishes could not be quantified.

---

## 5. Willingness to pay

### Takeaway
There is strong, repeated hostility to subscriptions and to "forced" paid upgrades. But people **do pay $80–$140 one-time** for DxO and paid $99/yr for Topaz upgrades for years. The breaking points were $199 renewals and subscription-only access. Prices people mention: $29 (resented as a surprise upgrade fee), about $45 (called a "fair" upgrade), $49.99 (Pixelmator), $79.99/€79.99 (old Topaz DeNoise), $89.99 (DxO upgrade), $99 (Topaz renewal, tolerated), $129–$139.99 (PureRAW 6 new), $199/yr ("highway robbery"). Watermark-gated trials are the norm on Mac upscalers. Local processing gets praise in the context of the Adobe-credit fears.

### Cited Findings
- Topaz upgrade history: "$49 for one product and $99 for multiple products" when yearly upgrades began. Later, renewal notices of about $199 were called "highway robbery". A thread is titled "Appalled at the cost of year subscription". — [Topaz community renewal licenses](https://community.topazlabs.com/t/renewal-licenses/59515); [Photo AI pricing](https://community.topazlabs.com/t/photo-ai-pricing/78645); [Appalled](https://community.topazlabs.com/t/appalled-at-the-cost-of-year-subscription/77755); [TalkPhotography "Topaz subscription renewal. What?????"](https://www.talkphotography.co.uk/threads/topaz-subscription-renewal-what.771872/)
- DxO upgrade anger (the $29 and about $45 "fair" quotes above). — [DxO forum](https://forum.dxo.com/t/customer-unfriendly-upgrade-policy/49285)
- Skylum Upgrade Pass backlash. Perpetual licenses with only one year of updates make a "lifetime's use" unlikely. — [Fstoppers](https://fstoppers.com/artificial-intelligence/review-luminar-neo-fall-update-winner-some-powerful-new-tools-715721); [Digital Camera World via search summary](https://tech.yahoo.com/computing/articles/skylum-luminar-neo-review-140040649.html)
- Subscription fatigue commentary: Fstoppers "Someone Please Save Us Photographers From All These Subscriptions" and "Why Creatives Are Abandoning Adobe in 2025"; Creative Bloq "2026 will be the breaking point". Survey figures cited by vendor blogs (45%, 52%, "62% Photofocus 2025") **could not be traced to originals and should not be used**. — [Fstoppers](https://fstoppers.com/business/someone-please-save-us-photographers-all-these-subscriptions-649634); [Fstoppers 2025](https://fstoppers.com/post-production/end-adobes-monopoly-why-creatives-are-switching-708358); [Creative Bloq](https://www.creativebloq.com/art/digital-art/subscription-fatigue-is-real-and-2026-will-be-the-breaking-point-for-artists)
- Watermark trials: most paid Mac upscalers let you preview but charge to export or to remove the watermark. Low-rated App Store apps draw 1-star reviews for crashes on the free version ($3.99 to remove the watermark), and one buyer asked for a **$90 refund** over slow, crashing, poor results. — [iDownloadBlog 2024](https://www.idownloadblog.com/2024/06/05/how-to-upscale-images-mac/) **[older]**; [App Store: Upscale AI](https://apps.apple.com/us/app/upscale-ai-photo-enhancer-4k/id6753763810?mt=12); [App Store: Photo AI](https://apps.apple.com/us/app/photo-ai-ai-photo-enhancer/id1585595160?mt=12) **[older review, 2023]**; [App Store: Local Photo Upscaler, 3.7 stars / 10 ratings](https://apps.apple.com/us/app/local-photo-upscaler-enhancer/id6758233962)
- Cloud credits: Gigapixel generative upscale costs **10 credits (≤25 MP) or 20 credits (25–56 MP)** in Adobe apps. Lightroom Super Resolution uses no credits. — [Adobe HelpX FAQ](https://helpx.adobe.com/vn_vi/lightroom-cc/kb/generative-upscale-topaz-gigapixel-faq.html)
- Adobe was already metering Topaz models (Gigapixel, Sharpen, Denoise, Bloom, Astra) as credit features before the deal. — [remio.ai](https://www.remio.ai/post/adobe-topaz-labs-acquisition-closes-but-independence-is-the-real-test)

### Inferences
- $59 one-time sits below every established denoise tool (PureRAW $129–139, ON1 NoNoise, Topaz $199/yr) and near Pixelmator ($49.99). That is attractive **if** quality is credible. The $39 launch price risks reading as "cheap App Store upscaler", a category with poor reviews.
- The $29/yr upgrade pass will be compared to DxO's and Skylum's upgrade schemes. To avoid that backlash: state "keep what you have forever", include new camera support in 1.x for free, and never fence bug or OS-compatibility fixes behind the pass.
- A watermarked full-feature trial is accepted practice. Crashes in the trial generate 1-star reviews, so stability before launch matters more than features.

### Gaps
- No direct survey of willingness to pay for this category. The vendor-blog survey figures couldn't be verified.

---

## 6. Spanish-speaking photographers' communities

### Takeaway
Little distinct signal was found. Spanish content is mostly reviews (Capture the Atlas ES, fotografiaflash) and a Fujistas forum thread. The advice is the same as in English: DxO PureRAW first, then Lightroom. Prices are quoted in euros (PureRAW €129.99; old Topaz DeNoise €79.99; Adobe photo plan about €12.09/month). Fuji X-Trans users (strong in the Spanish Fujistas community) care about DxO's late X-Trans support.

### Cited Findings
- A Spanish review: "DxO PureRaw funciona mejor para reducir el ruido que Topaz Denoise AI" ("DxO PureRaw reduces noise better than Topaz Denoise AI"). — [Capture the Atlas ES](https://capturetheatlas.com/es/dxo-pureraw-review/)
- Fujistas forum, "Experiencias y opiniones sobre DxO Pure RAW": users describe running PureRAW first, then editing in Lightroom. — [Fujistas](https://fujistas.com/foro/threads/experiencias-y-opiniones-sobre-dxo-pure-raw.69993/)
- PureRAW 6 at €129.99 from a Spanish retailer. Lightroom plan at €12.09/month. — [fotografiaflash](https://www.fotografiaflash.com/dxo-pureraw-elimina-el-ruido-sin-perder-detalles/); [Capture the Atlas ES](https://capturetheatlas.com/es/programas-para-reducir-el-ruido/)
- X-Trans support in PureRAW arrived in stages (v5 beta, v6 broader). — [Amateur Photographer](https://amateurphotographer.com/review/dxo-pureraw-6-review/)

### Inferences
- In LatAm, a one-time $59 is a bigger share of disposable income, and local-currency pricing or PPP coupons (Paddle supports coupons) may matter more than features. This is an inference; no source was found.
- Good Fuji X-Trans RAW decoding (via Apple's RAW engine) is worth verifying, given the size of the Fuji community in Spain.

### Gaps
- hispaniafoto, dzoom, r/fotografia and the Facebook groups didn't surface in search (Reddit and Facebook are blocked). No distinct Spanish/LatAm needs could be confirmed.

---

## 7. Common 1–2 star reasons in reviews of these apps

### Takeaway
Across sources, the recurring low-rating reasons are:
1. Subscription or forced upgrade pricing (Topaz, Skylum, DxO upgrades).
2. Artifacts and an over-processed or "AI" look.
3. Crashes and slowness, especially on older Macs or big upscales.
4. Account and licensing friction (Skylum).
5. Credits charged without a result (Adobe/Gigapixel).
6. Poor support response (Topaz).
7. Watermark-gated trials that crash (small Mac App Store apps).

### Cited Findings
- Media.io roundup: reviewers complain about "crashes, slow generative models, subscription pricing, or results that do not justify the cost". — [Media.io](https://www.media.io/comparison/topaz-labs-image-upscaler-review.html)
- Topaz: "always, always buggy" (forum reply to a 1-star-style complaint). Support "too often... a poor or no response". — [DPReview](https://www.dpreview.com/forums/threads/topaz-photo-ai-4-review.4804409/); [DPReview support post](https://www.dpreview.com/forums/post/67587118)
- Skylum: account and pass transfer refusals, freezing, features not working. — [Trustpilot](https://www.trustpilot.com/review/skylum.com?page=2)
- Mac App Store small apps: crashes on the free version; slow, crashing, poor results with a refund request; Photo Noise Reduction at 1.7 stars (16 ratings). — [App Store Upscale AI](https://apps.apple.com/us/app/upscale-ai-photo-enhancer-4k/id6753763810?mt=12); [App Store Photo AI](https://apps.apple.com/us/app/photo-ai-ai-photo-enhancer/id1585595160?mt=12); [App Store Photo Noise Reduction](https://apps.apple.com/us/app/photo-noise-reduction/id1209845752)
- Adobe credits deducted with no upscale. — [Adobe bug report](https://community.adobe.com/bug-reports-403/p-firefly-won-t-upscale-images-but-it-still-takes-credits-1626948/index3.html)

### Inferences
- For a new Mac App Store listing, the most avoidable 1-star causes are crashes on large files (tiling and memory, already in the plan), slow first run (model compile/warm-up should show progress), and a mismatch between marketing samples and real results. Use real, unretouched before/after examples.

### Gaps
- No systematic star-distribution data for Topaz/DxO/Luminar on the Mac App Store (they mostly sell direct). G2, Capterra and Trustpilot aggregates weren't retrievable in detail.
