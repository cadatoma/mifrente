# Fast-to-build, proven-revenue app ideas for a solo Swift/SwiftUI dev using Claude Code (as of 2026-10-24)

Scope note: this file covers the overlap of "proven revenue" and "small build scope". The client's apps are only used to avoid direct duplicates. His full published catalog (App Store Connect sales report, Sept 2026) is: Orejita (Entertainment, his most-downloaded app), Aprueba (Dominican Republic driver's license exam, plus CDL Pro), Texas Electrician License Exam, Licensed: Cosmetology Exam, ScrubCert (Medical Assistant), Tidebook (NOAA tide charts), Tipstack (tips & hours tracker), CadaToma (pill reminder), and Daywitness and AxleSet (no sales activity). There are also planned Mac PDF and AI-photo apps. **Key fact from his sales data: his paid apps convert reasonably once found, and the main problem is low traffic.** So this shortlist favors ideas that people actively search for on the App Store, and each idea notes how users would find it.

Method caveat: appfigures.com, trustmrr.com, getgrumpi.com, thebotpost.com and michalkosecki.com could not be fetched from this environment (DNS failure). Figures from those domains come from search-result excerpts of the pages, not from full-page reads. Third-party revenue estimates (Appfigures, AppGoblin, ScreensDesign, Latka, Adapty) are rough, and one 2026 source says an exact estimate for an indie app is "false precision" ([Appaloma](https://www.appaloma.com/research/app-intelligence-commodity-2026)).

---

## 1. Which small-scope app types made indie-scale revenue in 2024–2026, and what is the shortlist?

### Takeaway
Revenue evidence is strongest, and the build is small, for five types: (a) storage/photo cleaners, (b) single-purpose identifiers (plants, then coins and rocks), (c) AI photo calorie trackers, (d) screen-time/app blockers, and (e) quit/sobriety counters. Second-tier types with smaller proven revenue but cheap builds and little competition are teleprompters, invoice/estimate makers and Spanish-language faith apps. Each core feature can be built in 1–4 weeks with Claude Code. Distribution, not the build, is what limits success.

### Cited Findings

**Base rates (set expectations first)**
- RevenueCat data, via Appfigures and others: the median app earns about $72/month one year after launch, the top quarter $429 and the top 10% $2,574. — [Appfigures/RevenueCat summary via search](https://getgrumpi.com/blog/how-much-do-indie-apps-make) (excerpt only)
- 17.3% of new subscription apps reach $1K MRR within two years, and 4.6% reach $10K MRR (RevenueCat 2026 data, as cited). — [thebotpost](https://thebotpost.com/startups/indie-ai-apps-making-real-money) (excerpt only)
- 58% of new apps earn under $1K in their first year (Adapty, as cited). Adapty data also says the top 10% of apps take 94.5% of revenue. — [Grumpi](https://getgrumpi.com/blog/how-much-do-indie-apps-make) (excerpt only)
- Appfigures estimates non-game app spending grew 33.9% to $82.6B in 2025. — [Appfigures via search](https://appfigures.com/resources/insights/most-downloaded-highest-earning-apps-january-2026) (excerpt only)

**Storage / photo cleaners**
- Appfigures (June 2025): consumers spent nearly $40M on storage cleaner apps in the past month. 161 cleaner apps grossed at least $1,000 that month, 42 grossed more than $100K and 7 grossed more than $1M. The top earners grossed an estimated $197M in 2024. — [Appfigures, "Storage Cleaner Apps is a Multi Million Dollar Industry No One's Talking About"](https://appfigures.com/resources/insights/20250606?f=1) (excerpt only)
- Swipewipe: Photo Cleaner is listed at about $1M revenue with a 4.7 rating (third-party, unverified). — [ScreensDesign](https://screensdesign.com/apps/photo-cleaner-swipewipe/?vs=304106)
- Small indie swipe cleaners: a marketplace listing shows $323/month revenue and $1,245 ARR, sold at a $50K asking price. A Nov 2025 solo case reports 465 users and about $200 MRR after 30 days. — [Microns listing](https://www.microns.io/startup-listings/photo-management-app-that-allows-swipe-right-to-save-or-left-to-delete); [Swipes case summary](https://gist.ly/youtube-summarizer/how-swipes-app-reached-465-users-200-revenue-in-30-days) (AI summary of a video, low reliability)

**Identifiers**
- Appfigures (May 2025) looked at all 1,328 identifier apps: $27M in consumer spending in one month. Plant identifiers were 23% of the apps but 78% of revenue (about $21M). Coin identifiers were about 9% of the apps and 13% of revenue ($3.5M/month). Rock/gem identifiers were the only other group above $1M/month (4%). Multi-purpose identifiers were 26% of the apps but only 1.4% of revenue. Birds, bugs and mushrooms were each under $1M. — [Appfigures, "Monthly Consumer Spending in This Niche Just Hit $27M"](https://appfigures.com/resources/insights/20250509?f=1) (excerpt only)

**AI photo calorie tracking (Cal AI)**
- Cal AI launched in May 2024 and costs $2.49/month or $29.99/year. — [Latka/YPulse via search](https://getlatka.com/companies/calai.app)
- In early 2025 the founder claimed more than $2M in revenue in a single month. TechCrunch could not verify it. — [TechCrunch](https://techcrunch.com/2025/04/03/teen-with-4-0-gpa-who-built-the-viral-cal-ai-app-was-rejected-by-15-top-universities)
- CNBC reviewed documents showing about $1.4M per month in gross profit after store fees and about $274K per month in net operating income (as reported by The Nightly). — [The Nightly](https://thenightly.com.au/business/cal-ai-18yo-ceo-zach-yadegari-learned-to-code-at-age-7-now-he-has-a-21-million-a-month-ai-app-c-20025032)
- MyFitnessPal acquired Cal AI, announced 2 March 2026. Terms were not disclosed. TechCrunch reported more than 15M downloads and more than $30M in annual revenue, while other outlets said more than $40M in the trailing 12 months. Cal AI had 7 employees plus contractors and continues as a standalone app. — [TechCrunch](https://techcrunch.com/2026/03/02/myfitnesspal-has-acquired-cal-ai-the-viral-calorie-app-built-by-teens); [Techleap](https://finder.techleap.nl/news/note/myfitnesspal-acquires-teen-built-cal-ai-after-40m-in-annual-sales)

**Screen-time / app blockers**
- Opal: RevenueCat reports it reached $5M ARR with a hard paywall, then moved to freemium and passed 1M DAU and $10M ARR. — [RevenueCat Sub Club](https://www.revenuecat.com/blog/growth/kenneth-schlenker-sub-club-podcast-2026)
- One sec costs $19.99/year. Brick sells $39–69 hardware plus an optional subscription. No revenue figures were found for either. — [Screen Time Index comparison](https://screentimeindex.com/posts/screen-time-app-comparison); [Slate on Brick](https://slate.com/technology/2025/09/brick-app-review-digital-detox-instagram-tiktok.html)
- Warning: a Latka page titled "opal.so $17.1M ARR" is about a different company (a marketing platform). Do not use it. — [Latka](https://getlatka.com/companies/opal.so)

**Quit / sobriety counters**
- I Am Sober: AppGoblin estimates about 735K MAU and "$10K+" monthly revenue, all from in-app purchases. A directory lists it at "$200k revenue". The two do not agree. — [AppGoblin](https://appgoblin.info/apps/672904239); [ScreensDesign](https://screensdesign.com/apps/i-am-sober/)
- QUITTR (porn-addiction quitting app): the founder publicly claimed about $35K revenue in one day (unverified). — [vc.ru](https://vc.ru/growth/1762617-kak-quittr-dorosli-do-35k-den)

**Teleprompter**
- Sufler Teleprompter: TrustMRR lists 404 active subscriptions and $3.4K in the last 30 days, verified through RevenueCat. Tracked since May 2026 and listed for sale at $45K. — [TrustMRR](https://trustmrr.com/startup/sufler-teleprompter) (excerpt only)
- Teleprompter – VILO: about 21K MAU and under $10K/month (AppGoblin estimate). Teleprompter (Teleprompter Apps Ltd): about 139K MAU, under $10K/month, all in-app purchases. — [AppGoblin VILO](https://www.appgoblin.info/apps/1590820344); [AppGoblin](https://appgoblin.info/apps/941620509)
- Apple promoted "Detail: AI Video Editor", which uses Foundation Models to turn a draft into a teleprompter script and generate titles and hashtags. — [Neowin](https://www.neowin.net/news/apple-highlights-third-party-apps-using-its-on-device-apple-intelligence-models/)

**Invoice / estimate makers**
- A Flippa seller listing for "Invoice Maker: Estimate App" claims about 31K downloads per month and $2,173/month profit from subscriptions (self-reported). — [Flippa](https://flippa.com/11245961-invoice-maker-estimate-app)
- Adapty's paywall library estimates an "Invoice Maker" app at about 6K downloads and $100K revenue in the past month. It is unclear which app this is or what period it covers. — [Adapty](https://adapty.io/paywall-library/invoice-maker-billing-app/%7B%7Bs%7D%7D)
- One invoice/estimate app targeting contractors charges about $9.99/month or $49.99/year. — [Sensor Tower listing](https://app.sensortower.com/api/ios/apps/6758699359?country=US)

**Faith / devotional (Spanish)**
- Glorify: Dealroom puts revenue at $1–10M (latest year; details paywalled). — [Dealroom](https://dealroom.co/companies/glorify-1/)
- Hallow runs a Spanish edition (Hallow Español) for Hispanic Catholics in all Spanish-speaking countries and the US, with a 14-day trial. Amen App merged into Hallow in 2024. — [ACI Prensa](https://www.aciprensa.com/noticias/91497/conoce-a-hallow-la-app-con-oraciones-y-meditaciones-catolicas-guiadas-en-espanol); [Subger](https://subger.com/es/spiritual/faith-apps)
- YouVersion passed 1 billion installs (The Objective, Dec 2025, which reports Spain as 21st among countries). — [The Objective](https://theobjective.com/sociedad/2025-12-02/app-biblica-1000-millones-mundo-21-espana/)
- Many Spanish devotional apps are free and ad-supported ("Devocionales Cristianos Biblia"). — [Marlvel](https://marlvel.ai/apps/devocionales-cristianos-biblia)

**Habit trackers (weak evidence)**
- Habit Pixel, a solo habit tracker, was at $28 MRR in June and took 8 months to reach $1K MRR. — [Indie Hackers](https://www.indiehackers.com/post/from-0-to-1k-mrr-in-8-months-bootstrapping-habit-pixel-as-a-solo-dev-53d8687d15)
- Portfolio approach: one developer built 28 apps in 8 months and went from $100 to $10K MRR across the portfolio. — [BuildMVPFast](https://www.buildmvpfast.com/blog/portfolio-app-strategy-multiple-apps-revenue-solo-founder-2026)

**Other**
- Hypic (ByteDance photo editor): about $6.7M before fees in 2025, per Appfigures. This is a big-studio app and not a solo-dev target. — [Appfigures This Week in Apps, Dec 2025](https://appfigures.com/resources/this-week-in-apps/20251219) (excerpt only)
- Baby trackers: Statista has a US revenue chart (paywalled). Sensor Tower's Q1 2025 parenting snapshot gives downloads only. TrustMRR lists several small indie baby trackers (Buggy, Babygrid, Nanny Me) with RevenueCat-verified MRR, but the per-app figures could not be read. — [Statista](https://statista.com/statistics/1622626/baby-parenting-apps-revenue-us/); [TrustMRR Buggy](https://trustmrr.com/startup/buggy-baby-tracker-log)

### Inferences — the shortlist (~10 concepts)

Build times assume an experienced SwiftUI developer using Claude Code who already has a working StoreKit 2 / paywall / localization setup from his 10+ shipped apps. They cover a v1 that passes review, not a finished product. "FM" means Apple Foundation Models. "PCC" means the Apple Foundation Model on Private Cloud Compute, which has no cloud API cost for developers under 2M first-time downloads (see Q4).

| # | Concept | Revenue evidence for incumbents | What the winners do | Weakness to exploit | Build (solo + Claude Code) | Backend / variable cost | Main technical risk | App Review risk |
|---|---|---|---|---|---|---|---|---|
| 1 | **Storage/photo cleaner** (swipe to keep/delete, duplicates, similar photos, large videos, screenshots) | Category about $40M/month; 7 apps above $1M/month (Appfigures, Jun 2025) | Aggressive weekly subscriptions, scary "storage full" onboarding, heavy paid ads/ASA | Users dislike dark-pattern paywalls. Room for a one-time price, privacy, Spanish/LatAm-first, iPhone+Mac version | **1–2 weeks** (PhotoKit + Vision feature prints for similarity, on device) | None ($0). Fully on device | Performance on 50K+ photo libraries, limited-library permission UX | **High 4.3 risk** (crowded clone category). Avoid misleading "virus/space" claims. Needs a clear 5.1 Photos usage string |
| 2 | **Single-niche identifier: coins (Spanish/LatAm/Euro coins & banknotes), or rocks/minerals** | Coins about $3.5M/month, rocks above $1M/month (Appfigures, May 2025). Plants about $21M/month but saturated | Camera → ID → "value"/"rarity" card, collection, hard paywall | No Spanish-first coin app focused on peseta/euro/peso/LatAm series found (unverified gap). Value database is the moat | **2–4 weeks** (camera + model call + collection UI is about 1 week. The coin catalog/value data is the real work) | Vision API about $0.001–0.003/scan (see Q3), or FM on-device vision / PCC at $0 | Accuracy, and wrong "value" claims cause 1-star reviews | Medium: 4.3 for generic identifiers. Accuracy disclaimers needed |
| 3 | **AI photo calorie/macro tracker, Spanish/LatAm cuisine-first** | Cal AI $30–40M/yr, acquired by MyFitnessPal Mar 2026 | Photo → macros, streaks, onboarding quiz, $29.99/yr, organic TikTok at scale | Incumbents are US-food-centric (inference). Spanish dishes (tortilla, arepas, tacos, menú del día) and LatAm price points | **2–3 weeks** for v1 | Vision API about $0.002/photo, or FM vision (iOS 27) / PCC at $0 but with per-user daily quotas | Estimate accuracy is the product. FM on-device vision quality for food portions unproven | Medium: 1.4.1 health claims. 5.1.2(i) consent if photos go to a third-party AI. 4.3 (many clones) |
| 4 | **App blocker / focus app with a physical "brick" trigger** (NFC sticker or QR to unlock, Spanish-first) | Opal above $10M ARR. Brick sells $39–69 hardware + subscription | Shield screens, schedules, streaks, friction | Brick needs proprietary hardware. A $1 generic NFC sticker plus software does the same job. Spanish market under-served (inference) | **2–4 weeks** (FamilyControls + DeviceActivity + ManagedSettings + Core NFC) | None ($0) | Requires the Family Controls *distribution* entitlement from Apple (possible approval delay). DeviceActivity extensions are fragile and memory-limited | Medium: entitlement review. Must not appear to manage other people's devices without consent |
| 5 | **Quit/sobriety counter** (alcohol, smoking/vaping, porn, sugar), widget-first, with an on-device FM "craving coach" | I Am Sober about 735K MAU, $10K+/month est. QUITTR claimed $35K in one day | Day counter, money saved, milestones, community, widgets | Spanish "dejar de fumar/beber" apps are thin (inference). Privacy: on-device AI coach, no account | **1–2 weeks** | $0 with FM on device. Optional PCC | Low technical risk | Low–medium: avoid medical-treatment claims (1.4.1). Sensitive-data privacy label |
| 6 | **Teleprompter for iPhone + Mac** with FM script rewrite, auto-scroll by voice (on-device speech) | Sufler $3.4K/30 days verified, 404 subs. VILO / Teleprompter Apps under $10K/month est. | Mirror mode, remote control, camera recording overlay | Many are dated. Mac + iPhone + Continuity, voice-tracking scroll, bilingual scripts | **1–3 weeks** (voice-follow scrolling is the hard part) | $0 (on-device Speech + FM) | Speech-tracked scrolling accuracy. Camera+text overlay recording | Low |
| 7 | **Bilingual invoice/estimate maker for US Hispanic contractors** (factura/estimado EN↔ES, photo of job, e-sign) | Flippa listing $2,173/month profit at 31K downloads/month. Adapty est. one "Invoice Maker" at about $100K/month | Templates, PDF export, $9.99/month or $49.99/year | No found competitor positioned bilingual-first for Hispanic tradespeople (inference, unverified). Fits his EN/ES-switch pattern from ScrubCert | **2–3 weeks** (PDF generation, client list, tax lines, ShareSheet. FM to draft line items from voice) | $0 core. Optional iCloud/CloudKit sync | Getting PDF layout and tax/locale formatting right | Low (avoid 4.3 by not cloning a template). Payment links must not route digital goods around IAP (physical services are fine) |
| 8 | **Spanish Catholic/Christian daily devotional** with on-device FM reflection prompts and widgets | Glorify $1–10M/yr (Dealroom). Hallow has a Spanish edition. Many Spanish apps are ad-funded | Daily verse/prayer, audio, streaks, subscription | Spanish market served mostly by ad-supported apps or US apps translated into Spanish (inference). Good fit for a native Spanish speaker | **2–3 weeks** for text-only. Audio content takes much longer | $0 with FM. Content licensing is the cost | **Bible translation licensing** (needs verification. Some Spanish translations are public domain, others copyrighted). FM guardrails on religious text unknown | Medium: 4.3 (Bible apps are a classic template category) |
| 9 | **Private AI journal** (on-device FM prompts, summaries, mood, no account) | Apple promoted Stoic (journaling prompts via FM). **No revenue figure found** | Prompts, streaks, insights | Privacy plus zero API cost lets a one-time price work | **1–2 weeks** | $0 (FM on device) | FM 4K–8K context limits long-history summaries. PCC gives 32K | Low |
| 10 | **Habit/streak tracker** | Habit Pixel: $1K MRR after 8 months | Widgets, streaks | Saturated. Only works as part of a portfolio | 1 week | $0 | Low | 4.3 risk high |

Ranking for this developer (inference): best mix of proof, small scope and differentiation = #1 cleaner (biggest category, but marketing-heavy), #4 blocker + NFC, #5 quit counter, #7 bilingual invoices, #2 coin identifier in Spanish, #6 teleprompter. #3 calorie AI has the strongest proof of revenue, but in 2026 it is an ad-spend race against an incumbent owned by MyFitnessPal.

- Collision check: none of the shortlist overlaps CadaToma (medications), Daywitness, AxleSet, ScrubCert, the Mac PDF editor or the Mac photo enhancer. #3 and #5 are health-adjacent like CadaToma, but they are different products.

### Gaps
- No verified revenue found for One sec, Brick, Zero (fasting), Huckleberry or other baby trackers, homework helpers (Gauth/Photomath-type), receipt scanners, voice-memo-to-text apps, AI headshot apps, widget-customization apps, step/walking apps or language/flashcard apps. Their potential could not be quantified here. Other researchers covering market revenue may have figures.
- The Appfigures cleaner and identifier figures are from mid-2025, and no 2026 update was found.
- No data found on revenue from Spanish-speaking/LatAm users for any category.

---

## 2. Which types are saturated and which are still winnable in 2026, and what differentiation works?

### Takeaway
Plant identifiers, generic calorie AI, generic habit trackers and generic cleaners are crowded clone categories. In them a newcomer competes on ad spend and faces 4.3 rejection risk. Openings in 2026 are narrower niches inside proven categories (coins/rocks, Spanish-cuisine calories, Spanish quit/faith apps, bilingual trade tools), plus "privacy + no subscription + on-device AI" positioning. That positioning is now cheap to build because Apple's on-device and PCC models have no per-call API cost.

### Cited Findings
- Multi-purpose identifiers are 26% of identifier apps but earn only 1.4% of revenue, while single-purpose plant apps earn 78%. Specialization wins. — [Appfigures](https://appfigures.com/resources/insights/20250509?f=1) (excerpt only)
- The cleaner category has a long tail: 161 apps above $1K/month but only 42 above $100K. Many small players earn something and a few dominate. — [Appfigures](https://appfigures.com/resources/insights/20250606?f=1) (excerpt only)
- Calorie AI is consolidating. MyFitnessPal bought Cal AI and keeps it standalone "continuing to invest in its development and marketing". — [TechCrunch](https://techcrunch.com/2026/03/02/myfitnesspal-has-acquired-cal-ai-the-viral-calorie-app-built-by-teens)
- Opal grew faster after moving from a hard paywall to freemium (from $5M ARR to more than $10M ARR and 1M DAU). — [RevenueCat](https://www.revenuecat.com/blog/growth/kenneth-schlenker-sub-club-podcast-2026)
- Guideline 4.3 targets duplicates, clones and unimproved apps in oversaturated categories. Apple reportedly rejected more than 248K submissions for spam, copycatting or misleading users in 2023 (vendor-cited). — [vp0](https://vp0.com/blogs/does-apple-reject-ai-generated-apps)
- A niche-plus-integration example: a time-tracker for freelance designers reached $10K MRR, credited to the narrow niche and invoicing integration (podcast claim). — [Podimo / Indie Hacker Podcast](https://podimo.com/en/shows/the-indie-hacker-podcast-with-fexingo-solo/episode/8259b94c-b310-5423-b992-22f2ea55c11a)
- Apple Intelligence language support is limited, and some features may not be available in every region or language. — [9to5Mac](https://9to5mac.com/2025/09/29/apple-intelligence-ios-26-models-developers/)

### Inferences
- **Saturated (avoid unless you have a distribution edge):** plant ID, generic calorie AI, generic habit trackers, generic photo cleaners, generic Bible readers, generic "AI chat" wrappers.
- **Winnable with a twist:** coin/rock ID in Spanish with local coin series; calorie AI for Spanish/LatAm food; quit counters in Spanish; app blocker sold as "Brick without the $59 hardware" (NFC sticker); bilingual contractor invoicing; teleprompter that runs on both Mac and iPhone.
- **Differentiators that fit this developer's existing style** (no account, offline, Spanish+English, one-time purchase, cited sources): they show trust, but on their own they have not produced sales. His four public apps already use this positioning and have "almost zero sales". That suggests the problem is acquisition and search visibility rather than positioning. A one-time price also gives up the subscription revenue model that every revenue leader cited here uses. A hybrid (free tier, then a yearly subscription with a lifetime option) is a common compromise.
- Spanish/LatAm localization is a cheap edge for discovery (less competition for Spanish keywords), but LatAm price points are lower. No revenue data was found to size it (see Gaps).

### Gaps
- No quantitative data on how saturated Spanish-language App Store keywords are (e.g. "identificador de monedas", "dejar de fumar", "factura") versus English. Checking would need an ASO tool such as Appfigures or AppTweak with keyword difficulty.
- No evidence found on whether "no subscription" positioning converts better or worse in 2026.

---

## 3. How much does the identifier/AI-wrapper model depend on paid UGC/TikTok marketing versus organic search, and what are the unit economics with API costs?

### Takeaway
The big winners (Cal AI, QUITTR, Flamingo-type apps) were built on high-volume TikTok content: many brand-owned accounts, carousels and creator programs. Search alone produces long-tail income such as the $200–$3K/month cleaner and teleprompter examples. API cost per scan is a fraction of a cent, so cost of acquisition (CPI, creator fees) decides profitability, not inference. With Apple FM/PCC the API cost can drop to $0.

### Cited Findings
- Cal AI ran 12+ brand-owned TikTok accounts from January 2025, mostly carousels and repurposed faceless videos. A secondary source credits organic social for $1.5M MRR and 15M downloads. Another blog says $400K MRR. The figures conflict and are unverified. — [8x.social](https://www.8x.social/en/blog/cal-ai-multi-account); [Shortimize](https://www.shortimize.com/blog/from-zero-to-80k-mrr-in-75-days-how-rayz-ai-mastered-tiktok-marketing)
- Creator tactics cited for calorie apps: varied creators, challenges, skits, "day in the life", under-1-minute TikToks (newsletter claims 40M+ views). — [PlayKit newsletter](https://playkit.beehiiv.com/p/calorie-tracker-app)
- A tool vendor claims Flamingo reached $80K MRR from 6,535 slideshows and 671M views in one year (self-reported). — [Shortimize](https://www.shortimize.com/blog/from-zero-to-80k-mrr-in-75-days-how-rayz-ai-mastered-tiktok-marketing)
- QUITTR's team said it planned to grow MRR and test regular paid ads after its viral growth. — [vc.ru](https://vc.ru/growth/1762617-kak-quittr-dorosli-do-35k-den)
- An indie developer reached $6,772 MRR on $20/day Meta ads (headline claim). — [MRRStory](https://www.mrrstory.com/stories/this-indie-hacker-reached-6772-mrr-with-just-20day-meta-ads)
- Cost benchmarks (vendors, not consistent with each other): average iOS CPI cited at $4.90 in 2026 (Android $2.10). Another vendor claims $0.30–0.50 CPI in the US. Human UGC creators cost $150–500 per video, or $15–20 per video for small creators. AI-generated UGC costs $5–20 per video. Bonus structure about $400 per 1M views. — [UGC Copilot](https://ugccopilot.ai/blog/ai-ugc-mobile-app-marketing/); [Superappp](https://www.superappp.com/blog/how-to-scale-your-mobile-app-to-10k-with-ugc-everything-you-need-to-know-in-a-single-playbook); [Stormy](https://stormy.ai/blog/scaling-ugc-mobile-app-cpi-strategy)
- Vision/LLM API prices: Gemini 2.5 Flash $0.30 per 1M input and $2.50 per 1M output tokens. Gemini 3.6 Flash introductory $0.75/$3.75 per 1M through 31 Dec 2026, then $1.50/$7.50. Gemini 3.1 Flash Image preview listed at $0.25/$1.50 (aggregator). — [Google Vertex AI pricing via search](https://cloud.google.com/vertex-ai/generative-ai/pricing?hl=nl); [anotherwrapper](https://anotherwrapper.com/llm-pricing/gemini-2.5-flash); [pricepertoken](https://pricepertoken.com/pricing-page/model/google-gemini-2.5-flash-image-preview)
- AI-wrapper margins: typical AI product gross margins are 50–60% (Bessemer, Feb 2026, as cited). The heaviest 10% of users can cost 5–10× the average, so caps or credits are recommended. — [beancount.io](https://beancount.io/blog/2026/07/13/llm-api-cost-cogs-ai-wrapper-gross-margin-guide); [Dodo Payments](https://dodopayments.com/blogs/ai-wrapper-business-model-monetization/)
- Cal AI price: $29.99/year. — [Latka](https://getlatka.com/companies/calai.app)

### Inferences
- **Per-scan cost (rough, assumption-based):** a food or coin photo plus prompt is likely about 1–3K input tokens and 200–500 output tokens. At Gemini 3.6 Flash introductory rates that is about $0.002–0.004 per scan. A heavy user doing 5 scans/day × 30 days ≈ 150 scans ≈ $0.30–0.60/month, against about $2.50/month of revenue from a $29.99/year plan before Apple's 15–30% cut. API cost is manageable with a daily cap. The token counts per image are an assumption to check against provider documentation.
- **CAC dominates:** at a $4.90 iOS CPI and typical paid conversion rates of a few percent (assumed, not sourced here), cost per paying user can reach $100+, far above first-year revenue of about $21–25 per subscriber. That is why the winners rely on organic or semi-organic short-video volume rather than paid installs. For a solo developer with "almost zero sales", the realistic choice is (a) commit to daily short-form content in Spanish and English (faceless carousels, which tools now automate), or (b) pick categories where App Store search alone produces revenue (utilities like cleaners, teleprompters, invoices) and accept long-tail $100–$3K/month per app, then build a portfolio.
- **Identifier/calorie apps in particular** are "visual demo" products well suited to TikTok (scan → surprising result). They depend more on TikTok than utilities such as invoices and teleprompters, which people find through searches like "invoice maker".
- **Zero-API-cost option:** with PCC ($0 under 2M downloads) or on-device FM vision (OS 27), variable cost goes to zero, which makes a lifetime purchase or cheap LatAm pricing viable. The trade-off is quotas and quality (see Q4).

### Gaps
- No verified CPI or conversion data for any specific identifier or calorie app. No Cal AI or QUITTR ad-spend disclosures found.
- No data on organic-search-only revenue for identifier apps.

---

## 4. Which proven app types can Apple Foundation Models and other new frameworks now support cheaply, with zero API cost?

### Takeaway
As of OS 27 (WWDC26), Apple offers (1) an on-device model with **vision input**, an 8K context on newer devices, and system OCR and barcode tools, and (2) a **Private Cloud Compute model with 32K context, reasoning, and no cloud API cost for developers under 2M first-time downloads**. Both require Apple Intelligence-capable devices and are subject to per-user quotas. This makes text-AI features (journaling prompts, script rewriting, coaching, summaries, invoice line-item drafting) essentially free. It may also cover basic image identification (coin/rock/food), though there is no public accuracy evidence for that yet.

### Cited Findings
- Foundation Models shipped with iOS/iPadOS/macOS 26. Inference is free and works offline, with guided generation (@Generable) and tool calling. It needs an Apple Intelligence-compatible device with Apple Intelligence turned on, and language and region support is limited. — [9to5Mac](https://9to5mac.com/2025/09/29/apple-intelligence-ios-26-models-developers/)
- Apple-highlighted adopters: Detail (teleprompter scripts, titles, hashtags), SmartGym (workout summaries), Stoic (journaling prompts), CellWalk, Streaks, Stuff, OmniFocus, Agenda. — [Neowin](https://www.neowin.net/news/apple-highlights-third-party-apps-using-its-on-device-apple-intelligence-models/); [Cult of Mac](https://www.cultofmac.com/news/apple-foundation-models-framework)
- WWDC26 (OS 27): the on-device model "is also gaining Vision capabilities". It accepts images in any size or aspect ratio (UIImage, NSImage, CGImage, CVPixelBuffer, file URLs), and larger images use more tokens and add latency. New system tools are `OCRTool` (structured text from images), `BarcodeReaderTool` and a Spotlight-based local RAG tool. On-device context is 4,096 tokens on OS 26.0 and 8,192 on OS 27 for newer devices. iOS 26.4 reduced guardrail false positives, with more improvements in iOS 27. — [Apple WWDC26 "What's new in the Foundation Models framework"](https://developer.apple.com/videos/play/wwdc2026/241/)
- PCC model: no token cost for developers under 2M first-time downloads. No account, API key or auth (requires an entitlement or application). Each user has a daily limit counted against their iCloud account, and iCloud+ raises it. 32K context. Reasoning levels .light/.moderate/.deep. Same @Generable/tool APIs. Needs internet and an Apple Intelligence device. The app must handle quota states (Apple recommends in-context UI). Xcode can simulate availability. — [Apple WWDC26 session 319](https://developer.apple.com/videos/play/wwdc2026/319/); [Apple Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2026/102/); [WWDC26 ML guide](https://developer.apple.com/wwdc26/guides/machine-learning/)
- New `LanguageModel` protocol: Anthropic and Google publish Swift packages for their server models, so an app can fall back to a paid model behind the same API. Tokens should be fetched via OAuth and kept in Keychain, never in the app binary. Also new: an Evaluations framework, an `fm` CLI on macOS 27 and a Python SDK. — [Apple WWDC26 session 241](https://developer.apple.com/videos/play/wwdc2026/241/)
- One third-party article ties PCC eligibility to the App Store Small Business Program. Apple's own pages only state the 2M-download threshold. — [aitechconnect](https://aitechconnect.in/news/apple-wwdc-2026-foundation-models-ios-builders) (unverified)

### Inferences
- **Now $0-API and well matched to proven types:** quit-counter coach (#5), private journaling (#9), teleprompter script rewrite (#6), invoice line-item drafting from dictation (#7), devotional reflection prompts (#8), habit insights (#10).
- **Possibly $0 but unproven quality:** food calorie estimation (#3) and coin/rock identification (#2) with on-device vision or PCC. Accuracy for fine-grained ID (coin year/mint, mineral species) is unknown. A hybrid is the safer design: Vision `VNClassifyImageRequest`/OCRTool on device for the coin legend and year text, FM for structuring, and a paid server model (Gemini/Claude package) only as an opt-in fallback.
- **Reach limit:** FM/PCC only run on Apple Intelligence devices (iPhone 15 Pro and later, plus M-series Macs/iPads, from general knowledge, not verified here) with Apple Intelligence enabled and a supported language. An app that depends entirely on FM loses older iPhones, which matters for LatAm, where older devices are common (inference). Plan a non-AI fallback.
- **Free PCC under 2M downloads covers essentially every indie app.** The real limits are per-user daily quotas the developer cannot control and the need for internet.
- iOS 27 was presumably released in September 2026, following Apple's usual cycle (not verified in this research). Check adoption share before setting the minimum target to 27.

### Gaps
- Actual PCC daily quota numbers per user were not published in the material read.
- Spanish support for FM on-device vision and PCC was not confirmed in the material read. Earlier coverage says language support is limited.
- No independent benchmarks found for FM vision accuracy on food, coins or rocks.
- The PCC entitlement application process and approval criteria are not described.

---

## 5. What are the App Review guideline risks for these app types?

### Takeaway
The main risks are: **4.3 spam/copycat** for clone categories (cleaners, identifiers, calorie AI, Bible, habit apps); **4.2 minimum functionality** for thin AI wrappers; **5.1.2(i)** (since 13 Nov 2025), which requires disclosure and permission before sharing personal data with third-party AI; **1.4.1 health/medical** accuracy claims for calorie and quit apps; and the **Family Controls entitlement** for blockers. On-device FM processing avoids most of the 5.1.2(i) issues.

### Cited Findings
- 4.3 covers duplicates, clones and unimproved apps in oversaturated categories. Thin wrappers more often fail 4.2 (too little functionality, repackaged website). Developers report vague 4.3 feedback, e.g. "It's spam, refer to 4.3, fix your app, and resubmit". — [vp0](https://vp0.com/blogs/does-apple-reject-ai-generated-apps); [vp0 spam/design](https://vp0.com/blogs/app-store-rejection-spam-design-ai-fix)
- A 2019 app with about 200K users was rejected under 4.3(a) after adding DeepSeek AI features, and was still rejected after removing them (Apple Developer Forums thread, unresolved). — [Apple Developer Forums](https://developer.apple.com/forums/thread/780440)
- A 4.3 rejection notice cited "similar binary, metadata, and/or concept" to apps already submitted. — [Apple Developer Forums search](https://developer.apple.com/forums/search?q=4.3)
- Apple's 13 Nov 2025 guideline update requires apps to disclose and get permission before sharing personal data with third-party AI under 5.1.2(i). This is the first time Apple's privacy rules name AI companies. It is unclear whether on-device models are covered or how strictly the rule will be enforced. — [TechCrunch](https://techcrunch.com/2025/11/13/apples-new-app-review-guidelines-clamp-down-on-apps-sharing-personal-data-with-third-party-ai); [Storyboard18](https://www.storyboard18.com/amp/how-it-works/apple-tightens-app-review-rules-on-ai-data-sharing-84183.htm); [Product Hunt discussion](https://www.producthunt.com/p/murror/your-we-use-ai-line-is-now-a-consent-screen-apple-s-rule-5-1-2-i-has-been-live-since-november)
- The same update added crypto exchanges to the highly regulated category in 5.1.1(ix) and tightened age controls. — [PPC Land](https://ppc.land/apple-tightens-app-store-age-controls-and-data-sharing-disclosure/)
- AI-generated code itself is not grounds for rejection. Apple reviews the app, not the tool used to build it (vendor claim). — [vp0](https://vp0.com/blogs/does-apple-reject-ai-generated-apps)

### Inferences
- **Per concept:** cleaner (#1) and habit (#10) carry high 4.3 risk. Ship something with a distinct concept (e.g. Mac+iPhone, Spanish-first, a unique "trip/event cleanup" angle) and avoid fake "storage full" warnings, which also fall under 2.3 accuracy. Identifier (#2) and calorie (#3): medium 4.3 risk; add an in-app consent screen if using Gemini/Claude (5.1.2(i)); avoid diagnostic or medical-nutrition claims (1.4.1); show estimates with disclaimers. Blocker (#4): request the Family Controls (Distribution) entitlement early, before building (general knowledge of Apple's process; not re-verified here). Quit counter (#5): don't claim to treat addiction; mark it as a self-help tool. Invoice (#7): low risk; payments for physical services can use external processors. Faith (#8): 4.3 risk from template Bible apps. Original content and FM features help.
- Using Claude Code to ship several near-identical apps from the same codebase under one developer account is exactly the pattern the "similar binary, metadata, and/or concept" rejection targets. A portfolio strategy should vary concept and UI substantially between apps.
- On-device FM keeps photos and text on the device, which supports a privacy-label story and probably avoids 5.1.2(i) consent screens. Whether on-device processing is exempt has not been confirmed by Apple.

### Gaps
- The primary text of the current App Review Guidelines (sections 4.3, 1.4.1, 5.1.2) was not fetched directly. The wording above comes from news and vendor summaries.
- No data on 2026 rejection rates for specific categories (cleaners, identifiers, calorie AI).
