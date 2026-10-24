# Unmet demand on the App Store (as of 2026-10-24): requests, switching categories and fresh gaps

Scope note: the coordinator says the four apps in `00_mis_apps_actuales.txt` (CadaToma medication reminder, Daywitness residency-day counter, AxleSet truck axle calculator, ScrubCert phlebotomy/MA exam prep) are not the developer's main apps. They also list two planned apps (a Mac PDF editor and an AI photo enhancer). They were used only to avoid obvious collisions, not to shape the research.

Method note / limitations: reddit.com, Wikipedia and several blogs could not be fetched from this environment (DNS failures). Generic searches for "is there an app that" / "I'd pay for" did not return 2025–2026 Reddit threads. Most demand evidence below therefore comes from news coverage, app-store listings, review aggregators (Trustpilot, Capterra, JustUseApp) and competitor/vendor blogs. Competitor blogs are flagged where they are used, because they have a commercial stake.

## Objective: ranked list of 10–15 opportunities with demand evidence

### Takeaway
The strongest signals for a solo, fast-shipping developer are in three places:
- **Trust gaps** in large categories where the incumbents monetize aggressively: photo/storage cleaners, bill splitting, calorie tracking, budgeting and period tracking.
- **Orphaned users** of apps that shut down: TV Time and Pocket/Omnivore.
- **Simple B2B tools** priced far above their complexity: contractor estimates and invoices, and Mexican CFDI invoicing on iPhone.

New Apple platform features (Foundation Models in iOS 26/27, App Intents replacing SiriKit, scheduled Live Activities) are the main way to differentiate inside these categories, and apps that adopt them early are the ones Apple names.

### Cited Findings (ranked; demand evidence and why current apps fail)

**1. Honest photo/storage cleaner (iPhone + Mac): one-time price, on-device, no weekly trap**
- Demand and revenue: the category leader, Cleanup: Phone Storage Cleaner (Codeway), is a top download with large review volume — [App Store](https://apps.apple.com/us/app/cleanup-phone-storage-cleaner/id1510944943).
- Why users are unhappy: a Pixtide analysis found about 67 of the 209 low-star Cleanup reviews it read describe a charge during a trial, after cancelling, or a refused refund — [Pixtide](https://pixtide.com/guides/photo-cleaner-subscription-trap).
- Pricing: the app reportedly defaults to about $7.99/week after a short trial. Sources disagree on trial length (3 vs 7 days) — [Pixtide](https://pixtide.com/guides/is-cleanup-app-safe), [JustUseApp reviews](https://justuseapp.com/en/app/1510944943/cleanup-phone-storage-cleaner/reviews).
- Earlier analysis calls the category "predatory iOS cleanup applications" — [Connor Tumbleson, Jan 2025](https://connortumbleson.com/2025/01/13/predatory-ios-cleanup-applications/).
- Apple Community users complain that Apple still lists "scam" cleaner apps (anecdotal) — [Apple Community](https://discussions.apple.com/thread/255920043).
- Technical scope: third-party apps can only meaningfully clean the Photo Library, through PhotoKit with user permission, and deletions go to Recently Deleted for 30 days — [dblabsapps 2026 guide](https://dblabsapps.com/blog/iphone-storage-cleaning-apps-safe/). The scope is small, so this is fast to build.
- Collision check: it sits next to the planned AI photo enhancer but is a different job (deleting and deduplicating, not enhancing).

**2. "Are you OK?" daily check-in for people who live alone (and for older parents)**
- Viral demand: "Are You Dead?" (rebranded Demumu) briefly topped Apple's China paid chart in January 2026 — [BGR](https://www.bgr.com/2074610/are-you-dead-top-paid-iphone-app-china/), [The Standard HK](https://www.thestandard.com.hk/china/article/321520/Are-you-dead-app-to-rebrand-as-Demumu-after-topping-Chinas-paid-chart), [Sixth Tone](https://www.sixthtone.com/news/1018076).
- How it works: a daily check-in. If the user misses two consecutive check-ins, the app emails their contacts — [Euronews](https://euronews.com/next/2026/01/14/what-is-the-are-you-dead-app-and-why-is-it-so-popular-in-china-and-beyond).
- Cost and pricing: a three-person team built it for under 1,500 yuan. It launched at a one-off 8 yuan, then moved to a roughly 8-yuan subscription to cover SMS and server costs — [Malay Mail](https://malaymail.com/news/life/2026/01/13/are-you-dead-app-tops-chinas-charts-as-solo-living-fears-spark-viral-sensation/205234).
- Outside China: as Demumu it also climbed charts in the US, Singapore and Australia, probably driven by the Chinese diaspora — [Jiemian](https://en.jiemian.com/article/13883722.html), [Marketing-Interactive](https://www.marketing-interactive.com/chinese-app-are-you-dead-rebrands-as-demumu).
- Why existing apps fail: the original's name is off-putting, and critics suggested "Are You Still Alive" instead — [The Standard HK](https://www.thestandard.com.hk/china/article/321520/Are-you-dead-app-to-rebrand-as-Demumu-after-topping-Chinas-paid-chart). It is China-centric and depends on SMS.

**3. Calorie/macro tracking with photo logging, a free barcode scanner and Spanish/LatAm foods**
- Revenue proof: Cal AI reached more than 15M downloads and more than $30M in annual revenue in under two years (figures from MyFitnessPal, which acquired it; the acquisition date is reported as Dec 2025 or Mar 2026) — [TechCrunch](https://techcrunch.com/?p=3098039), [Latka ($35M in 2025)](https://getlatka.com/companies/calai.app).
- Smaller sellers: an AI meal-photo tracker listed on Acquire reports $54K/month revenue — [Acquire.com](https://app.acquire.com/startup/1653rgn95k-ai-meal-photo-calorie-tracker-with-54k-month-revenue-and-1-000-five-star-reviews). Appfigures counted $2M of consumer spend in Cal AI in Feb 2025 alone — [Appfigures](https://appfigures.com/resources/insights/20250228/4-this-is-where-ai-shines-(and-generates-millions)).
- Discontent with the incumbent: a 2026 MyFitnessPal redesign is described as harder to use, adding friction to the food diary and removing shortcuts. These sources are competitor blogs — [Fitia](https://fitia.app/learn/article/best-myfitnesspal-alternatives-2026/), [PlateLens](https://platelens.app/blog/best-myfitnesspal-alternatives-2026-smarter-calorie-tracking).
- Paywalls: barcode scanning is the main paywall pain point (Lose It! keeps it in Premium; FatSecret's is free). MacroFactor costs about $71.99/yr with no free tier — [AskVora](https://askvora.com/blog/best-myfitnesspal-alternatives-2026).
- Fit for the developer: Fitia (a LatAm-origin app) is visible here, which shows a Spanish-first angle is viable — [Fitia](https://fitia.app/learn/article/best-myfitnesspal-alternatives-2026/).

**4. Bill splitting with no daily cap (Splitwise refugees), Spanish-first, offline**
- The cap: Splitwise free users can add only about 3–5 expenses per day; its help centre is cited as saying four — [ITVoice](https://www.itvoice.in/splitwise-has-introduced-restrictions-on-the-number-of-free-expenses-users-can-add), [Finny (competitor)](https://getfinny.app/blog/splitwise-pricing-2026).
- Price: Pro is about $4.99/month or $39.99/year in the US — [Finny (competitor)](https://getfinny.app/blog/splitwise-pricing-2026).
- Complaints: ads, time delays and "constant upselling modals" after the paid tier arrived — [Trustpilot](https://au.trustpilot.com/review/splitwise.com).
- Where users go: reviewers most often name Tricount, plus Settle Up (ads on free tier) and Spliit (web only) — [Trustpilot](https://nl-be.trustpilot.com/review/splitwise.com), [Finny alternatives](https://getfinny.app/blog/best-splitwise-alternatives-2026).
- Competition: at least two new competitors (Finny, Splitly) are already chasing this gap, which validates it — [Splitly blog](https://mynextdeveloper.com/blogs/how-splitly-compares-to-other-expense-splitting-apps).

**5. Simple estimate + invoice app for tradespeople (US Hispanic contractors / Spanish-English)**
- Incumbent price: Joist's Standard plan is $79/month, or $59/month billed annually (vendor's own blog) — [Joist](https://www.joist.com/?p=27229).
- Market size: Joist claims more than 1.3M contractors and more than $85B invoiced (vendor claim) — [Joist](https://www.joist.com/?p=27229).
- Complaints from reviews:
  - "Works occasionally without a glitch" — [Capterra](https://www.capterra.com/p/230138/Joist/reviews/?page=2)
  - "They increase the price while they hold your information hostage" — [Software Advice AU](https://www.softwareadvice.com.au/software/233734/joist)
  - Outages, and payment fees that add up on many small transactions — [Capterra UK](https://www.capterra.co.uk/software/1004933/joist)
  - Features locked to higher tiers, limited search, and no automatic invoice-number sequencing — [Capterra UK](https://www.capterra.co.uk/software/1004933/joist), [Capterra](https://www.capterra.com/p/230138/Joist/reviews/?page=2)

**6. Mexico CFDI 4.0 invoicing on iPhone for freelancers and micro-businesses (LatAm-specific)**
- The official SAT app is limited: users report problems loading the .key/.cer files, CFDI lists that show only fiscal folios, and missing tax regimes. It only issues income CFDI, with no complements — [El Contribuyente](https://www.elcontribuyente.mx/2023/08/cuales-son-las-quejas-mas-recurrentes-de-la-app-factura-sat-movil/) (2023, based on Play Store reviews).
- Weak iPhone coverage:
  - Factura Gorila lacks some complements and needs internet — [App Store](https://apps.apple.com/us/app/-/id1322057745)
  - ClickBalance's listing still says CFDI 3.3, although 4.0 is the only valid version — [App Store](https://apps.apple.com/us/app/id1204564610), [Forbes MX](https://forbes.com.mx/?p=1127148)
  - Newer apps such as Emite CFDI (sends invoices via WhatsApp) have almost no ratings — [App Store MX](https://apps.apple.com/mx/app/emite-cfdi/id6757446474)
  - CFDI Snogari is iPhone-only and supports carta porte — [App Store MX](https://apps.apple.com/mx/app/cfdi-snogari/id6444322283)

**7. Manual/envelope budgeting at a one-time price (and for LatAm, where US bank sync does not apply)**
- Incumbent prices: YNAB is $14.99/month or $109/yr with no free tier, after a controversial increase from $84 — [FinanceFeeds](https://financefeeds.com/the-best-budgeting-apps-of-2026/), [Wallet Grower](https://walletgrower.com/compare/ynab-vs-monarch-vs-copilot). Monarch is $99.99 (Core) or $199 (Plus) — [BudgetLabs](https://www.budgetlabs.io/blog/ynab-vs-monarch). Copilot is about $95/yr — [era.app](https://era.app/articles/era-vs-monarch-vs-copilot-vs-ynab/).
- Mint refugees mostly went to paid apps (Monarch added a Mint CSV importer) — [Online Tool Guides](https://onlinetoolguides.com/best-budgeting-apps/).
- EveryDollar's monthly price rose to $17.99 — [getitplanned](https://www.getitplanned.com/blog/monarch-money-alternatives).

**8. Local-only period/cycle tracker (privacy after the Flo/Meta verdict)**
- Verdict: a federal jury found Meta violated California privacy law by collecting menstrual data from the Flo app (August 2025) — [Bloomberg Law](https://news.bloomberglaw.com/ip-law/meta-illegally-recorded-womens-menstrual-data-jury-finds), [Data Privacy & Security Insider](https://www.dataprivacyandsecurityinsider.com/2025/08/federal-jury-finds-against-meta-for-collecting-data-from-flo-health/).
- Settlement: Flo, Google and Flurry agreed to $59.5M. Claims were due Oct 15, 2026, and the final fairness hearing is set for Oct 29, 2026, which will bring fresh news coverage — [Paubox](https://www.paubox.com/blog/google-flo-health-and-flurry-to-pay-59.5-million).
- Conflict: Wikipedia reportedly says Flo did not settle — [Flo (Wikipedia)](https://en.wikipedia.org/wiki/Flo_(app)).

**9. Read-later / "save the web forever" for Pocket and Omnivore refugees (local-first, Markdown, AI summaries)**
- Shutdowns: Omnivore closed in Nov 2024 on about two weeks' notice. A vendor blog says about half a million libraries were deleted — [Yaps](https://www.yaps.ai/sv/blogg/omnivore-lades-ner-basta-alternativet-2026-ag-dina-data.md).
- Pocket: Mozilla announced the shutdown in May 2025, the export deadline was Oct 8, 2025, and data was deleted by Nov 2025 — [Fabric](https://fabric.so/comparison/best-pocket-alternative), [TechCrunch](https://techcrunch.com/2026/08/14/read-it-later-app-pocket-is-shutting-down-here-are-the-best-alternatives/).
- Alternatives: Matter costs $79.99/yr for premium features. Instapaper's best features are paywalled and its "future remains unclear" (said by a competitor, Wallabag) — [TechCrunch](https://techcrunch.com/2026/08/14/read-it-later-app-pocket-is-shutting-down-here-are-the-best-alternatives/), [Wallabag blog](https://wallabag.it/en/blog/2026/06/15/which-read-it-later-app-to-choose-in-2026/).
- Users' lesson: data portability and the fear of another shutdown — [Yaps](https://www.yaps.ai/sv/blogg/omnivore-lades-ner-basta-alternativet-2026-ag-dina-data.md).

**10. TV/movie tracker for TV Time refugees**
- Shutdown: TV Time shut down after July 15, 2026, and account data was deleted — [Moviebase](https://moviebase.app/resources/tv-time-shutting-down), [TechCrunch](https://techcrunch.com/?p=3149675), [Neowin](https://www.neowin.net/news/tv-time-is-on-its-last-legs-its-founder-is-already-building-its-replacement/).
- Warning sign: Whip Media said it was "no longer sustainable to continue operating the service as a free app, and there was not enough demand for a paid app" — [Engadget](https://engadget.com/2213944/tv-time-is-relaunching-as-its-parent-company-pivots-to-ai).
- Competition: TV Time's founder launched Bingers, which imports TV Time exports. Trakt (about $5/month for advanced features) and Moviebase also absorb these users — [Neowin](https://www.neowin.net/news/tv-time-is-on-its-last-legs-its-founder-is-already-building-its-replacement/), [Korben](https://korben.info/en/what-to-replace-tv-time-with-before-shutdown.html).

**11. ADHD "time-blindness" visual timer built around Live Activities / Dynamic Island / CarPlay**
- Many small apps appeared in 2025–2026, which shows demand without a clear leader:
  - DuePal ($1.99, Dynamic Island/Lock Screen countdown) — [App Store](https://apps.apple.com/app/id6756181712)
  - TimeSee (shrinking ring with an overtime count-up) — [App Store](https://apps.apple.com/app/id6759831241)
  - See Time (interval alerts) — [App Store](https://apps.apple.com/my/app/see-time/id6479330586)
  - ADHD Timer Collection (iPad) — [App Store](https://apps.apple.com/ua/app/adhd-timer-collection/id6634579526)
- Analysts see "tools for ADHD" as a source of differentiation in productivity apps — [Iterative Improvements](https://iterativeimprovements.substack.com/p/differentiation-in-personal-productivity).
- New APIs: iOS 26 opened scheduled Live Activities to third parties, and Live Activities now appear on CarPlay and on the Mac through iPhone Mirroring — [9to5Mac](https://9to5mac.com/2025/12/04/ios-26-made-live-activities-even-better-on-iphone-heres-whats-new/), [Gear Patrol](https://www.gearpatrol.com/tech/iphone-live-activities-ios-26-upgrades/).

**12. Habit tracker that never loses your history, with fair pricing**
- Recurring 1–3 star complaints (competitor analysis): lost streak data after sync or reinstall, paywalls that appear mid-flow, gamification fatigue, and "losing years of habit history after major updates" — [Unstar](https://unstar.app/blog/habitica-streaks-productive-way-of-life-habit-bull-habit-tracker-apps-ranked-2026).
- Price complaints: Productive reviewers report prices doubling — [Habi](https://habi.app/insights/productive-alternatives/). A Habitty lifetime buyer was asked to pay again (a single review) — [AppFollow](https://apps.appfollow.io/ios/habitty-habit-tracker/1228128916?country=au).
- Pricing benchmarks: Streaks is about $5–6 one-time, and Habitify Premium is $39.99/yr — [Habi](https://habi.app/insights/productive-alternatives/).
- Apple named Streaks among the first Foundation Models adopters — [9to5Mac](https://9to5mac.com/2025/09/29/apple-intelligence-ios-26-models-developers/).

### Inferences
- **Suggested ranking**, scored on demand evidence × weakness of the incumbent × build speed × fit for a Spanish-speaking developer:
  - 1 photo cleaner
  - 5 contractor invoice (bilingual)
  - 4 bill splitting
  - 2 check-in app
  - 3 calorie tracker (huge but crowded)
  - 6 CFDI (high fit, regulatory work)
  - 7 manual budget
  - 8 period tracker
  - 9 read-later
  - 11 ADHD timer
  - 12 habit tracker
  - 10 TV tracker (lowest monetization)
- **Common winning pattern:** "the same thing, minus the abuse." No weekly subscriptions, no account, data stays on the device, export always works, plus a one-time or low annual price. In every category above, the 1–2 star complaints are about monetization and trust, not missing features.
- **Calorie tracking** probably has the largest money pool. Cal AI's acquisition by MyFitnessPal may push indie users toward independent apps, but the category is crowded with well-funded AI clones. Differentiation would need to be language/cuisine (LatAm foods) or on-device privacy.
- **Check-in app:** the Demumu case shows a dirt-cheap app can top a paid chart when it names a fear. A Spanish/English version aimed at seniors living alone and their adult children (with the family as contacts) fits the developer's caregiving experience. It does not duplicate the medication app, though it could later integrate with it.
- **CFDI invoicing:** stamping invoices requires a certified provider (PAC), which means a per-invoice cost and integration work. This is not verified here and should be checked before committing.
- **TV tracker:** TV Time's own owner says free tracking was unsustainable and paid demand insufficient. Treat this as an orphaned-user acquisition play, not a revenue engine.
- **Budgeting:** a "no bank link, Spanish, multi-currency, one-time price" budgeter avoids Plaid costs and fits LatAm, where US aggregators have weak coverage. This is an inference; I found no source quantifying LatAm bank-sync coverage.

### Gaps
- No direct access to Reddit, Product Hunt or X, so I can't quote first-hand "is there an app that…" requests from 2025–2026. Every opportunity above rests on news, reviews and aggregator evidence instead.
- No Google Trends data was retrieved.
- A Calendara blog claimed that Maple (family organizer) shuts down on Dec 31, 2026 after its team was acquired. I could not confirm this. The App Store listing was updated in June 2026, and CB Insights only says "Acq - Talent" — [App Store](https://apps.apple.com/us/app/maple-family-organizer/id1551070188), [CB Insights](https://www.cbinsights.com/investor/maple-2). Treat it as unverified.
- Petfinder's mobile app reportedly closed on Oct 15, 2026, but the only source is a competitor blog — [WeRescue](https://www.werescue.pet/petfinder-app-alternative/). Not verified, and the monetization potential looks low.
- No hard switching-rate data for any category.

## "Is there an app that…" / "I'd pay for an app that…" requests (2025–2026)

### Takeaway
I could not reach first-hand Reddit/HN request threads. The clearest stated-demand signals came instead from viral chart events (Demumu) and from refugee waves after shutdowns or paywalls (TV Time, Pocket/Omnivore, Splitwise cap). Each of these produced a burst of "what do I use now?" content.

### Cited Findings
- A generic search for "is there an app that" plus Reddit returned no relevant 2026 threads — search result only, no URL to cite.
- A 2026 Ask HN thread, "What developer tool do you wish existed in 2026?", exists, but it is about dev tools, not consumer iOS apps — [HN](https://news.ycombinator.com/item?id=46345827).
- Demumu / "Are You Dead?": a three-person team, under 1,500 yuan spent, #1 paid in China in Jan 2026 — [BGR](https://www.bgr.com/2074610/are-you-dead-top-paid-iphone-app-china/), [Malay Mail](https://malaymail.com/news/life/2026/01/13/are-you-dead-app-tops-chinas-charts-as-solo-living-fears-spark-viral-sensation/205234).
- Replacement-content waves after shutdowns: TV Time (July 2026) — [Moviebase](https://moviebase.app/resources/tv-time-shutting-down); Pocket — [TechCrunch Aug 2026](https://techcrunch.com/2026/08/14/read-it-later-app-pocket-is-shutting-down-here-are-the-best-alternatives/); Google Fit to be replaced by the Google Health app by end of 2026 (per Wikipedia, via search snippet) — [Wikipedia](https://en.wikipedia.org/wiki/Google_Fit).

### Inferences
- Waves of competitor "best X alternatives 2026" blogs (Splitwise, MyFitnessPal, Pocket, TV Time, Monarch) are themselves a demand signal: other indie developers are paying for SEO traffic from these refugees.

### Gaps
- No quantified "request" data (upvote counts, thread volumes) for r/AppIdeas, r/iphone, r/macapps, r/ADHD, r/Teachers or r/personalfinance. A follow-up with Reddit access is recommended.

## Switching categories with strong recent discontent (2025–2026)

### Takeaway
The categories with the most visible 2025–2026 discontent are:
- photo/storage cleaners (dark-pattern weekly subscriptions)
- bill splitting (Splitwise daily cap)
- calorie tracking (MyFitnessPal redesign and paywall, Cal AI acquired)
- budgeting (high prices after Mint)
- read-later (shutdowns)
- TV tracking (shutdown)
- period tracking (privacy verdict)
- habit trackers (data loss, price hikes)

### Cited Findings
- Splitwise: daily expense cap, ads and upselling modals; users move to Tricount — [Trustpilot](https://au.trustpilot.com/review/splitwise.com), [ITVoice](https://www.itvoice.in/splitwise-has-introduced-restrictions-on-the-number-of-free-expenses-users-can-add).
- Budgeting prices: YNAB $109/yr after rising from $84; Monarch $99.99/$199; Copilot about $95 and Apple-only — [FinanceFeeds](https://financefeeds.com/the-best-budgeting-apps-of-2026/), [BudgetLabs](https://www.budgetlabs.io/blog/ynab-vs-monarch), [era.app](https://era.app/articles/era-vs-monarch-vs-copilot-vs-ynab/).
- MyFitnessPal 2026 redesign backlash (competitor blogs) — [Fitia](https://fitia.app/learn/article/best-myfitnesspal-alternatives-2026/), [Welling](https://www.welling.ai/articles/best-myfitnesspal-alternatives-2026).
- MyFitnessPal acquired Cal AI (15M+ downloads, $30M+ ARR) — [TechCrunch](https://techcrunch.com/?p=3098039).
- Cleanup app trial-to-weekly complaints — [Pixtide](https://pixtide.com/guides/photo-cleaner-subscription-trap).
- Pocket/Omnivore shutdowns — [Fabric](https://fabric.so/comparison/best-pocket-alternative); TV Time shutdown — [Engadget](https://engadget.com/2213944/tv-time-is-relaunching-as-its-parent-company-pivots-to-ai).
- Flo/Meta privacy verdict and $59.5M settlement — [Bloomberg Law](https://news.bloomberglaw.com/ip-law/meta-illegally-recorded-womens-menstrual-data-jury-finds), [Paubox](https://www.paubox.com/blog/google-flo-health-and-flurry-to-pay-59.5-million).
- Habit trackers: data loss and price doubling — [Unstar](https://unstar.app/blog/habitica-streaks-productive-way-of-life-habit-bull-habit-tracker-apps-ranked-2026), [Habi](https://habi.app/insights/productive-alternatives/).
- Market context: RevenueCat's 2026 report says annual prices drifted up while weekly and monthly prices did not — [RevenueCat State of Subscription Apps 2026](https://www.revenuecat.com/state-of-subscription-apps).

### Inferences
- Users in these categories habitually re-buy. Discontent is about pricing model and trust, which a solo developer can beat on positioning ("one payment, no account, nothing leaves your phone"). The developer's existing apps already use this positioning, so it is a reusable brand template.

### Gaps
- Not researched for 2025–2026 discontent: journaling (Day One), sleep, fasting, note-taking, scanners, widgets, language learning, plant care, baby tracking, pet care and workout logging. They were out of budget, not ruled out.

## Recurring unmet needs in 1–2 star reviews of top apps

### Takeaway
Across cleaners, contractor invoicing and habit trackers, the low-star reviews repeat the same things: surprise charges and hard cancellation, outages or lost data, features locked behind higher tiers, and price increases on users who are "locked in."

### Cited Findings
- Cleanup: about 32% of the 209 low-star reviews sampled (67) concern charges or refunds; the cancel option is hard to find — [Pixtide](https://pixtide.com/guides/photo-cleaner-subscription-trap), [JustUseApp](https://justuseapp.com/en/app/1510944943/cleanup-phone-storage-cleaner/reviews).
- Joist: unreliable, price increases while data is "held hostage," payment fees, tier-locked features, no automatic invoice numbering — [Software Advice AU](https://www.softwareadvice.com.au/software/233734/joist), [Capterra UK](https://www.capterra.co.uk/software/1004933/joist), [Capterra](https://www.capterra.com/p/230138/Joist/reviews/?page=2).
- Habit trackers: streak or history loss after sync or update, and mid-flow paywalls — [Unstar](https://unstar.app/blog/habitica-streaks-productive-way-of-life-habit-bull-habit-tracker-apps-ranked-2026).
- SAT Factura app: .key/.cer loading failures, unreadable CFDI lists, income CFDI only — [El Contribuyente](https://www.elcontribuyente.mx/2023/08/cuales-son-las-quejas-mas-recurrentes-de-la-app-factura-sat-movil/).

### Inferences
- Features that answer these complaints directly: a one-tap in-app cancel link, a visible "you will be charged on <date>" notice, automatic local and iCloud backup with one-tap export, and invoice auto-numbering. Each can go straight into App Store copy.

### Gaps
- I did not pull raw App Store review feeds (AppFollow/Appfigures) for MyFitnessPal, YNAB, Splitwise or Flo. The review findings above come from secondary analyses.

## New iOS 26/27 and macOS 26/27 platform features that create gaps

### Takeaway
iOS 26 brought on-device Foundation Models (free inference, offline) and scheduled Live Activities for third parties. WWDC26 (June 8, 2026; iOS 27 ships fall 2026) reportedly added Private Cloud Compute access, third-party model support through a Language Model protocol, and possibly image input, and moved Siri to App Intents only. Category apps that adopt these early are the ones Apple names in its announcements.

### Cited Findings
- iOS 26 Foundation Models: on-device, offline, no inference cost, guided generation (`@Generable`) and tool calling. Apple named Stoic, Streaks, SmartGym, Stuff, Agenda and OmniFocus among early adopters — [9to5Mac](https://9to5mac.com/2025/09/29/apple-intelligence-ios-26-models-developers/), [Atelier Socle guide](https://www.atelier-socle.com/en/articles/foundation-models-api-guide).
- Supported languages include Spanish and Portuguese (Brazil) — [9to5Mac](https://9to5mac.com/2025/09/29/apple-intelligence-ios-26-models-developers/).
- Limits: the on-device model is small, so features mostly improve quality of life rather than change workflows — [Infinum](https://infinum.com/blog/apple-on-device-ai/).
- WWDC26 (secondary reports): Foundation Models rebuilt with Google/Gemini, spanning on-device and Private Cloud Compute, plus Dynamic Profiles and third-party models (Gemini, Claude) through a Language Model protocol — [mer.vin](https://mer.vin/2026/06/apple-wwdc26-siri-ai-and-gemini-backed-foundation-models-on-device-and-private-cloud-compute/), [TechCabal](https://techcabal.com/2026/06/08/wwdc-2026-announcements/), [FoneArena](https://www.fonearena.com/blog/tag/visionos-27).
- Image input for Foundation Models is reported by a single Spanish-language source and is unconfirmed — [Stork](https://www.stork.ai/blog/es/tag/foundation-models).
- SiriKit is reportedly deprecated, with App Intents the only route to Siri. A new LongRunningIntent shows progress as a Live Activity — [Apple WWDC26 session 345](https://developer.apple.com/videos/play/wwdc2026/345/), [Bitrise](https://bitrise.io/blog/post/wwdc26-under-the-radar) (single blog for the deprecation claim).
- Live Activities: third parties can schedule them (iOS 26), they appear on CarPlay and on the Mac through iPhone Mirroring, and an EU-only accessory forwarding framework arrived in iOS 26.5 — [9to5Mac](https://9to5mac.com/2025/12/04/ios-26-made-live-activities-even-better-on-iphone-heres-whats-new/), [9to5Mac iOS 26.5](https://9to5mac.com/2026/03/30/ios-26-5-adds-live-activities-support-for-third-party-accessories-in-the-eu/), [MacRumors](https://www.macrumors.com/2026/03/31/apple-sets-privacy-rules-live-activities-alerts/).

### Inferences
- **If image input is confirmed:** on-device food-photo logging becomes feasible without cloud costs. That is a direct cost advantage over Cal AI-style apps, which pay for cloud vision. Verify before building.
- **On-device features by opportunity:**
  - Read-later: summaries
  - Budgeting: receipt/bank-text categorization
  - Contractor invoicing: estimate drafting from voice notes
  - CFDI: concept and description suggestions
  - Habit tracker: coaching
- **Siri and Live Activities:** shipping App Intents early ("Hey Siri, log 300 pesos for dinner split with Ana"), plus scheduled Live Activities for timers and check-ins, is a cheap way to be feature-worthy in iOS 27.

### Gaps
- I could not fetch Apple's iOS 27 newsroom or release notes. iOS 27 widget, Liquid Glass and Apple Watch specifics for 2026 are unverified.

## Professional/B2B niches and Spanish-speaking/LatAm needs

### Takeaway
Tradespeople pay $59–79/month for estimate and invoice tools they find unreliable. Mexican freelancers and micro-businesses have no good native iPhone CFDI 4.0 app. Both are high-willingness-to-pay, low-complexity niches where a bilingual Spanish developer has an edge.

### Cited Findings
- Joist: $59–79/month, 1.3M contractors claimed, reliability and pricing complaints — [Joist](https://www.joist.com/?p=27229), [Capterra](https://www.capterra.com/p/230138/Joist/reviews/?page=2).
- CFDI apps on iPhone: the official SAT app is limited, at least one incumbent's listing still shows CFDI 3.3, and new apps have almost no reviews — [El Contribuyente](https://www.elcontribuyente.mx/2023/08/cuales-son-las-quejas-mas-recurrentes-de-la-app-factura-sat-movil/), [App Store](https://apps.apple.com/us/app/id1204564610), [App Store MX](https://apps.apple.com/mx/app/emite-cfdi/id6757446474).
- Spanish-first proof: Fitia (calorie tracking) and Tricount appear in Spanish-language switching contexts — [Fitia](https://fitia.app/learn/article/best-myfitnesspal-alternatives-2026/), [Trustpilot Splitwise](https://pt.trustpilot.com/review/splitwise.com).

### Inferences
- A bilingual (EN/ES) estimate and invoice app for US tradespeople is probably the best B2B fit: no regulatory integration, offline-capable, and a clear price anchor at $59–79/month to undercut with a $9.99/month or one-time option. I found no statistic on the share of Hispanic US contractors in this research, so that would need its own source.
- Other niches (nurses, real estate agents, teachers, drivers, small shops) were not covered by sourced evidence in this pass.

### Gaps
- No sourced data on Argentina (ARCA/AFIP factura electrónica), Colombia (DIAN) or Spain (Verifactu 2026). The same "official app is bad" pattern may hold there and is worth a follow-up search.
- Nothing found on teachers, real estate agents or nurses within budget.
