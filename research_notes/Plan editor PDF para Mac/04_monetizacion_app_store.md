# Monetization, pricing and Mac App Store rules for a $29.99 one-time-purchase Mac PDF app (as of 2026-10-24)

Scope: checks the pricing and channel section of `00_plan_original.txt`: Free tier with watermark, Personal $29.99 ($19.99 launch), Office $99 for 5 people via Paddle, Mac App Store (MAS) as the main channel at 15%, Paddle second, Setapp and universities later, revenue scenarios of 500/2,000/5,000 sales, and $300–$500 of Apple Search Ads.

Note on access: several sites could not be fetched directly (ads.apple.com, paddle.com, macapps.report, blog.eternalstorms.at, fatbobman.com all returned DNS errors). For those, the notes rely on search-result summaries, and each such case is flagged.

---

## 1. App Store Review Guidelines that apply (3.1.1, trials, 3.1.3, 2.4.5, 4.2) and the 2025–2026 changes (Epic v. Apple, DMA)

### Takeaway
A MAS build **cannot** unlock features with a license key bought on Paddle. Guideline 3.1.1 bans license keys as an unlock mechanism, and 2.4.5(vi) says Mac apps "may not … require license keys". The Office license therefore needs its own direct-download build, or has to go through IAP or Apple's volume purchasing. The free-tier-plus-watermark design and a $0 "XX-day Trial" non-consumable are both allowed. In the **US storefront only**, apps may now include buttons and links to outside purchases. That rule is still being litigated: the Ninth Circuit ruled in December 2025, and the Supreme Court granted review in June 2026. EU DMA alternative terms cover iOS/iPadOS, not macOS.

### Cited Findings
- 3.1.1: "If you want to unlock features or functionality within your app, (by way of example: … unlocking a full version), you must use in-app purchase. Apps may not use their own mechanisms to unlock content or functionality, such as license keys…" — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- Trial pattern, verbatim: "Non-subscription apps may offer a free time-based trial period before presenting a full unlock option by setting up a Non-Consumable IAP item at Price Tier 0 that follows the naming convention: 'XX-day Trial.' Prior to the start of the trial, your app must clearly identify its duration, the content or services that will no longer be accessible when the trial ends, and any downstream charges the user would need to pay for full functionality." — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- 2.4.5 (Mac App Store), the relevant items: (i) must be sandboxed; (iv) may not download additional code to add functionality; **(vi) "may not present a license screen at launch, require license keys, or implement their own copy protection"**; (vii) "must use the Mac App Store to distribute updates; other update mechanisms are not allowed" (so no Sparkle in the MAS build); (ix) every localization in one bundle. — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- 3.1.3(b) Multiplatform Services: apps "may allow users to access content, subscriptions, or features they have acquired in your app on other platforms or your web site … provided those items are also available as in-app purchases within the app." — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- 3.1.3(c) Enterprise Services: "If your app is only sold directly by you to organizations or groups for their employees or students … you may allow enterprise users to access previously-purchased content… Consumer, single user, or family sales must use in-app purchase." — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- 3.1.3(f), "Free Stand-alone Apps", is limited to companions for VoIP, cloud storage, email or web hosting, so it does not fit a PDF editor. — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- US storefront exception: 3.1.1(a) says link-out entitlements "are not required for developers to include buttons, external links, or other calls to action in their United States storefront apps". The 3.1.3 intro exempts "apps on the United States storefront" from the ban on encouraging other purchase methods. In every other storefront, apps "may not include buttons, external links, or other calls to action that direct customers to purchasing mechanisms other than in-app purchase". The entitlements "are limited to use only in specific storefronts … and only on certain platforms in each of those storefronts." — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- 4.2 Minimum Functionality: an app needs "adequate utility" and must be more than a repackaged website. 4.2.3(i): it should work without installing another app. — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- The guidelines page I fetched showed no "last updated" date and no change log. It calls itself "a living document". — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- Epic v. Apple: on Dec 11, 2025 the Ninth Circuit affirmed the civil-contempt finding, agreeing that Apple's 27% link-out commission was prohibitive. It held that a total ban on commissions was overbroad: Apple may charge a commission tied to costs "genuinely and reasonably necessary" for coordinating external links. It also narrowed the limits on link design and placement. — [Justia, 9th Cir. No. 25-2935](https://law.justia.com/cases/federal/appellate-courts/ca9/25-2935/25-2935-2025-12-11.html); [Fenwick](https://www.fenwick.com/insights/publications/ninth-circuit-largely-upholds-ruling-in-epic-v-apple)
- The Supreme Court granted cert in Apple Inc. v. Epic Games (No. 25-1311) on June 30, 2026. Apple filed its merits opening brief on Sept 14, 2026. — [Oyez](https://www.oyez.org/cases/2026/25-1311); [Supreme Court docket PDF](https://www.supremecourt.gov/DocketPDF/25/25-1311/424150/20260914154510009_2026-09-14%20No.%2025-1311%20Apple-Epic%20Merits%20Opening%20Brief.pdf)
- One secondary source says that in April 2026 the Ninth Circuit lifted a stay so the remand (setting a cost-based rate) could go ahead, and that links stay at zero commission until the district court approves a rate. Only that one source reports this, and it was not verified. — [tech-insider.org](https://tech-insider.org/apple-epic-supreme-court-2026/)
- EU DMA: Apple's alternative business terms, alternative marketplaces and web distribution apply to iOS and iPadOS. Macwelt reports that macOS is not affected because the EU does not treat it as a gatekeeper platform for this purpose, and Mac software could always be distributed outside the store. — [Apple, DMA and apps in the EU](https://developer.apple.com/fr/support/dma-and-apps-in-the-eu/); [Macwelt](https://www.macwelt.de/article/2822958/alternative-app-stores-europa.html)

### Inferences
- **Suspicion (1) is confirmed.** The MAS build cannot have an "enter license key" field. The workable setups are:
  - (a) a separate direct-download build, Developer ID signed and notarized, with Paddle licensing and Sparkle updates, which takes Office and Personal web sales;
  - (b) in the MAS, Personal sold as an IAP and businesses buying through Apple Business Manager (see Q2);
  - (c) only if the app is willing to add accounts: a 3.1.3(b) multiplatform setup, where a web-bought license unlocks the MAS app through an account login, provided the same unlock is also sold as IAP. This conflicts with the plan's "sin cuenta" (no account) promise, and the 2.4.5(vi) wording on license keys makes it risky for review. Not recommended for v1.0.
- The free tier with watermarked signing, OCR and compression is a normal freemium IAP unlock and fits 3.1.1. The watermark should not cover basic viewing. The free tier already gives "adequate utility" (view, annotate, organize), which helps with 4.2. That is an inference: no guideline mentions watermarks.
- US storefront: the guideline text sets the US exemption by storefront and does not exclude macOS, so a US-storefront MAS app can probably link to a Paddle checkout for the Office license. This is an inference that needs App Review confirmation. Two caveats: (a) the commission on linked-out purchases may become non-zero after the remand or the Supreme Court decision, expected in the 2026–27 term; (b) after a linked-out purchase, the unlock inside the MAS app runs into the same license-key and account problem described above. Treat it as optional, not something to build on.
- Spain, Mexico and LatAm: no steering is allowed. In those storefronts, the MAS app and its metadata may not point to the web store.

### Gaps
- No official changelog for the guidelines was found, so I could not confirm the exact 2025–2026 revision dates. Check the "What's new" news posts on developer.apple.com.
- No source states whether the US link-out freedom has been tested on Mac App Store apps in particular.
- The current status of the remand (whether any rate has been set as of Oct 2026) was not verified from a primary source.

---

## 2. Selling multi-seat/office licenses; volume purchase, education, Family Sharing; dual distribution (MAS + direct)

### Takeaway
Every public App Store app is automatically available in Apple Business Manager and Apple School Manager at its App Store price. There is an optional 50% education price for purchases of 20 or more, and it can **only be turned on before the app is approved**. Volume purchase applies to the app itself; nothing I found says IAP unlocks can be bought in volume. That makes a free app with an IAP unlock a poor fit for business volume buyers. The usual pattern is one codebase with two targets: a MAS build using StoreKit, and a direct build with Paddle licensing and Sparkle.

### Cited Findings
- "All apps on the App Store are automatically available for volume purchase for the same price in Apple Business and Apple School Manager." — [Apple, Volume purchase and custom apps](https://developer.apple.com/support/volume-purchase-and-custom-apps/)
- "You can choose to provide your app for 50% of its listed price for educational institutions purchasing quantities of 20 or more. Please note that this option is only available before your app has been approved." The setting is in App Store Connect › Pricing and Availability › App Distribution Methods › "Offer a reduced price on Apple School Manager for volume purchases." — [Apple, Volume purchase and custom apps](https://developer.apple.com/support/volume-purchase-and-custom-apps/)
- Custom apps can be distributed privately to specific organizations through their Organization ID. Delivery is by MDM or redemption codes, and this option is also only available before approval. — [Apple, Volume purchase and custom apps](https://developer.apple.com/support/volume-purchase-and-custom-apps/); [Apple, Distribute](https://developer.apple.com/business/distribute/)
- Family Sharing for non-consumable IAP is off by default. It is enabled per product in App Store Connect, cannot be turned off afterwards, and covers up to 5 family members. Family members may need to tap Restore Purchases. — [Apple, Supporting Family Sharing](https://developer.apple.com/documentation/storekit/supporting-family-sharing-in-your-app.md); [RevenueCat docs](https://www.revenuecat.com/docs/platform-resources/apple-platform-resources/apple-family-sharing.md); [Apple tech talk 110345](https://developer.apple.com/videos/play/tech-talks/110345/)
- One developer reported that shared non-consumables did not show up in `Transaction.currentEntitlements`, so test this. — [Apple Developer Forums](https://developer.apple.com/forums/thread/730570)
- Dual-distribution example: Eternal Storms Software (Matthias Gansrigler) sells both on the MAS and directly, with Paddle as merchant of record. Paddle's approval process included a review of the site's legal pages and checkout. Other options he lists are FastSpring, PayPal, Stripe and Gumroad. This comes from search summaries because the page could not be fetched. — [Eternal Storms blog](https://blog.eternalstorms.at/2024/12/06/selling-outside-of-the-mac-app-store-part-i-its-been-a-while/); [Michael Tsai](https://mjtsai.com/blog/2024/12/09/selling-outside-of-the-mac-app-store/)
- A MacPaw developer survey of about 400 developers, cited by The State of Mac Apps, found that among developers selling through several channels, direct sales were 52% of revenue and the MAS 48% (direct was 44% in 2023). About 20% of Mac developers rely on the MAS alone. This is from a search summary; the page could not be fetched. — [The State of Mac Apps](https://macapps.report/market)
- A Chinese indie developer (Zipic, by fatbobman) wrote about leaving the MAS and building his own distribution and sales system. Direct sellers have to build their own update and payment systems. From a search summary. — [fatbobman](https://fatbobman.com/en/posts/zipic-2-selling-and-distribution)
- PDF Squeezer, a close comparable, is sold directly at €19.99 with a free trial and is also in Setapp. App Store prices in older articles (€9.99, €3.59) are out of date. — [ifun.de](https://www.ifun.de/pdf-squeezer-4-7-schneller-und-fuer-apple-prozessoren-optimiert-276570/); [appgefahren](https://www.appgefahren.de/tag/pdf-squeezer)

### Inferences
- **The Office license is best handled in three parts:**
  1. Web/Paddle "Office 5-seat" license that works only in the **direct build**. That build has the same features under a different bundle ID, Developer ID signing, notarization, Sparkle updates and Paddle license activation. The checkout should name the macOS version requirements and say "download from our site".
  2. Organizations that buy through Apple Business Manager or School Manager get the MAS app. Because of the IAP limitation, one option is a **separate paid-upfront MAS listing** (for example "AppName Pro", $29.99, no IAP) so organizations can volume-buy seats. Its education price must be set **before first approval**.
  3. The MAS Personal IAP should have Family Sharing enabled. This is cheap goodwill and a marketing line ("hasta 5 familiares"), but it is permanent, so decide before launch.
- One Swift codebase with two Xcode targets or schemes, and a compile flag such as `#if MAS` that swaps StoreKit for the Paddle SDK and removes Sparkle, is the standard approach. It is consistent with 2.4.5(vii), which requires MAS updates to come only from the MAS. This is an inference; I found no Apple doc that prescribes it.
- Customers who buy the direct build can open the same PDFs, but their purchase does not move to the MAS version, and the reverse is also true. The FAQ should say so.

### Gaps
- No Apple documentation was found confirming whether IAP can be bought through volume purchase. My understanding (unverified) is that it cannot, so an organization cannot buy the IAP unlock for its staff in bulk. Confirm in the Apple Business Manager user guide.
- I could not fetch first-hand details of how Rogue Amoeba, Panic, CleanShot X or PDF Squeezer split their MAS and direct builds, so their practices are not cited. Some of them have left the MAS altogether, which is not verified here.
- Whether the MAS supports paid upgrades for v2 (it historically has not, so developers publish a new app or add a new IAP) was not verified for 2026.

---

## 3. Fees and tools: Small Business Program, Paddle vs Lemon Squeezy/Stripe vs FastSpring vs Gumroad, tax/VAT, StoreKit 2

### Takeaway
The Small Business Program rate is 15% for developers under $1M in proceeds in the prior and current calendar year, and new developers qualify. The rate applies 15 days after the end of the fiscal month in which enrollment is approved, so **enroll before launch**. Paddle's list price is 5% + $0.50, and it acts as merchant of record that handles VAT and sales tax. Lemon Squeezy has the same headline rate, but its future inside Stripe is uncertain. Stripe Managed Payments is about 3.5% on top of Stripe's processing fees. Apple prices outside the US and Canada **include VAT**, which lowers the plan's net-per-sale figure in Spain and Mexico.

### Cited Findings
- Small Business Program: 15% on paid apps and IAP. Eligible: "Existing developers who made up to 1 million USD in proceeds in the prior calendar year … as well as developers new to the App Store." Proceeds across Associated Developer Accounts count together. Exceeding $1M in the current year moves future sales to the standard rate. "Your proceeds will be adjusted fifteen (15) days after the end of the fiscal calendar month in which your enrollment is approved." — [Apple, Small Business Program](https://developer.apple.com/app-store/small-business-program/)
- The same page mentions a further reduction to 10% for developers on the EU alternative terms. That applies to iOS/iPadOS terms, not the MAS. It also mentions free Apple Foundation Models on Private Cloud Compute for enrolled developers with fewer than 2 million first-time downloads. — [Apple, Small Business Program](https://developer.apple.com/app-store/small-business-program/)
- Paddle: 5% + $0.50 per transaction, no monthly fee. The fee covers processing, merchant-of-record services and global tax. Paddle's own page could not be fetched, so this comes from third parties. One competitor says products under $10 are outside standard pricing ("contact them"). Another, Dodo Payments, warns that currency conversion before payout is an extra hidden cost; it is a competitor, so treat that as biased. — [Spendflo](https://spendflo.com/vendors/paddle); [Fungies](https://fungies.io/alternatives/paddle); [Dodo Payments](https://dodopayments.com/blogs/paddle-fees-explained)
- Lemon Squeezy: Stripe bought it in July 2024. It is a merchant of record at 5% + $0.50. Sources disagree on whether international cards add 1.5%. One 2026 source says it is being absorbed into Stripe Managed Payments (public preview Feb 2026), with slower development and support complaints. Another says it still runs as its own product. — [learnwithhasan](https://learnwithhasan.com/payment-gateways/lemonsqueezy/); [Rework](https://resources.rework.com/tools/billing-revenue/paddle-vs-lemon-squeezy); [ChargePanda](https://www.chargepanda.com/blog/post/lemonsqueezy-alternative); [devtoollab](https://devtoollab.com/blog/best-merchant-of-record-platforms)
- Stripe Managed Payments, Stripe's own merchant-of-record product: about 3.5% per successful transaction on top of standard Stripe processing (2.9% + 30¢ for US cards), checked Sept 2026 by a third party. It covers indirect tax in 80+ countries and works with Checkout and Payment Links. — [devtoollab](https://devtoollab.com/blog/best-merchant-of-record-platforms); [Dodo Payments](https://dodopayments.com/blogs/paddle-vs-lemon-squeezy/)
- Apple pricing: there are 900 price points, a base storefront is chosen, and Apple generates equalized prices for other storefronts, adjusting them for exchange rates and taxes. "Prices in all countries except the U.S. and Canada include taxes." — [9to5Mac](https://9to5mac.com/2023/03/09/apple-app-store-price-points-purchases/); [Apple tech talk 110364](https://developer-mdn.apple.com/videos/play/tech-talks/110364/)

### Inferences
- **Net per sale, corrected:**
  - US MAS: $29.99 × 0.85 = **$25.49**, matching the plan, because US sales tax is added on top of the price.
  - Spain MAS: an equalized price around €29.99 includes 21% VAT. €29.99 / 1.21 × 0.85 ≈ **€21.07**, about 17% less than the plan assumes.
  - Mexico (16% IVA): roughly price / 1.16 × 0.85.
  - The plan's single "$25.49 per sale" figure is therefore only right for the US and Canada.
- Paddle on the $99 Office license: $99 − (5% + $0.50) = $93.55 gross, matching the plan. Paddle as merchant of record also handles VAT, so EU and Mexican buyers' VAT is added to or included in the checkout price depending on configuration. Currency conversion and payout costs may cut a little more.
- On $19.99 or $29.99 personal web sales, Paddle's take is about 6.7–7.5% effective. That is still much cheaper than Apple's 15%. In non-US storefronts, though, the MAS app may not mention the web store (Q1).
- StoreKit 2 setup for the MAS build:
  - one non-consumable "Full unlock";
  - optionally one $0 non-consumable named "14-day Trial", with the duration and what gets locked shown before it starts, per 3.1.1;
  - entitlement check through `Transaction.currentEntitlements`.
  - The freemium watermark design makes the trial IAP optional. Having both (free tier plus a 14-day full trial) is allowed and probably raises conversion. This is an inference with no Mac-specific data.

### Gaps
- FastSpring and Gumroad fees were not retrieved from primary or secondary sources in this pass. Gumroad's widely reported rate of about 10% + $0.50 is unverified here.
- Paddle's official 2026 pricing page could not be fetched, so the "under $10 needs custom pricing" claim comes from a competitor.
- Mexico's digital-services tax treatment (IVA plus income-tax withholding on platforms) for App Store proceeds was not researched.

---

## 4. Pricing strategy: is $29.99 right? One-time vs subscription vs paid upgrades, launch discounts, regional and education pricing

### Takeaway
I found little hard evidence comparing pricing models for indie Mac utilities. The closest comparable, PDF Squeezer, sells for €19.99 direct, and the rivals in the plan list at $79.99–$149.99, so $29.99 sits in a defensible "impulse" band. The main pricing levers backed by sources are Apple's automatic equalization, which can be overridden per storefront, and the 50% education price, which has to be set before approval.

### Cited Findings
- Comparable price: PDF Squeezer is €19.99 direct with a free trial, and is also in Setapp ($9.99/month for Setapp). — [ifun.de](https://www.ifun.de/pdf-squeezer-4-7-schneller-und-fuer-apple-prozessoren-optimiert-276570/); [Setapp DE](https://setapp.com/de/so-gehts/pdf-verkleinern)
- Apple equalizes prices from a base storefront and lets developers set prices per storefront manually. Prices on the base storefront are not adjusted for tax or exchange-rate changes. — [9to5Mac](https://9to5mac.com/2023/03/09/apple-app-store-price-points-purchases/); [Apple tech talk 110364](https://developer-mdn.apple.com/videos/play/tech-talks/110364/)
- Education: optional 50% price for institutions buying 20 or more, chosen before approval. — [Apple](https://developer.apple.com/support/volume-purchase-and-custom-apps/)
- Hard paywalls vs freemium (subscription apps, RevenueCat 2026): median trial-to-paid at day 35 is 10.7% for hard paywalls vs 2.1% for freemium. Revenue per install at day 60 is $3.09 vs $0.38. — [RevenueCat 2026 benchmarks](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026.md)
- Direct (non-MAS) revenue keeps growing for Mac developers (52% vs 48% MAS among multi-channel developers). — [The State of Mac Apps](https://macapps.report/market)

### Inferences
- $29.99 is reasonable as the US anchor. A $19.99 launch price cuts net per sale by a third ($16.99 vs $25.49). It only pays off if it drives reviews and ranking. Better: limit it to 1–2 weeks around launch, and possibly offer it only to beta testers and mailing-list subscribers.
- **Regional pricing (LatAm):** Apple's automatic equalization will put Mexico at roughly the USD price converted plus IVA. For Mexico and LatAm, consider manually setting lower prices in those storefronts (for example a MXN tier near $19.99 USD equivalent). That is a judgment call with no conversion data behind it. Spain can stay at the €29.99 tier, which still nets about €21.
- **Paid upgrades:** with a one-time purchase, a later "v2 Pro" (text editing) can be a separate IAP, such as a "Pro editing pack". The plan's v2 idea needs no paid-upgrade mechanism.
- "Too cheap = low quality" risk: at $29.99 the app is still priced as a real tool, not a $4.99 utility. The free tier plus watermark lets users judge quality before buying. I found no empirical source on this perception.
- Freemium converts much worse than a hard paywall (subscription data). The plan's generous free tier (view, annotate, organize free) makes the app more discoverable but will likely mean low download-to-paid conversion.

### Gaps
- No source compared one-time, subscription and paid-upgrade revenue for indie Mac utilities specifically.
- No data on how launch discounts affect MAS ranking or long-run revenue.
- No affordability or price-elasticity data for Spain, Mexico or LatAm on the MAS.
- No direct evidence on how price signals quality for productivity apps.

---

## 5. How realistic the revenue scenarios are: indie Mac revenue, conversion rates, case studies, Setapp payouts

### Takeaway
The scenarios imply large download volumes. At an assumed 2% freemium conversion, 500 / 2,000 / 5,000 sales need about 25k / 100k / 250k downloads a year. Disclosed indie Mac revenues show $50k–$300k+ a year is possible but belongs to well-marketed hits, so 500–2,000 sales in year one is a more realistic planning range than 5,000. Setapp pays 70% of membership revenue, split by usage. Setapp Mobile (EU iOS) closed in Feb 2026, but Setapp for Mac continues.

### Cited Findings
- Freemium (subscription apps) median trial or download to paid is about 2.1%, vs 10.7% for hard paywalls. Hard-paywall download-to-paid was 12.11% in 2025. — [RevenueCat 2026 benchmarks](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026.md)
- A widely quoted freemium conversion range of "1 to 10%" is described as too broad to be useful. — [Parsa substack](https://parsa.substack.com/p/consumer-subscription-kpi-benchmarks-retention-engagement-and-conversion-rates-9ac13b57c3d3)
- Self-reported indie Mac revenues (search summary, not fetched):
  - Sensei (Cindori, solo developer): about $300K in 2021, sold directly through Paddle.
  - Screen Studio: about $30K/month with a team of three.
  - BoltAI: about $15K–$30K/month in 2025, averaging around $25K.
  - — [The State of Mac Apps](https://macapps.report/market); [stealwhatworks](https://stealwhatworks.com/blogs/news/mac-apps-making-real-money-now)
- Setapp: developers receive 70% of Membership revenue, split by which apps each member used in the billing period, weighted by app price tier. How often an app was opened does not count. A +20% partner fee is paid for members a developer refers (up to 90%). Single-app sales through Setapp pay 85%. Payouts are monthly. — [Setapp docs, Distributing revenue](https://docs.setapp.com/docs/distributing-revenue); [Setapp Membership revenue](https://docs.setapp.com/docs/setapp-membership-revenue)
- MacPaw closed **Setapp Mobile** (EU iOS store) on Feb 16, 2026 and CleanMyMac Business on July 14, 2026. It said Setapp desktop apps are unaffected. Wikipedia's wording, "closing the app", is ambiguous; the press confirms it refers to the mobile store only. — [AppleInsider](https://appleinsider.com/articles/26/01/15/setapp-mobile-eu-app-store-cleanmymac-business-both-close-down-for-good); [dig.watch](https://dig.watch/updates/eu-alternative-app-store-setapp-mobile-closes); [Wikipedia](https://en.wikipedia.org/wiki/Setapp)
- A July 2026 headline mentions Setapp offering early access to an "unstore" alternative to the Mac App Store. I did not read the details. — [AppleWorld.Today](https://appleworld.today/setapp-offers-early-access-to-its-unstore-alternative-to-the-mac-app-store)

### Inferences
- **Downloads needed** (assuming 2% conversion and the US net of $25.49; the EU net is lower, see Q3):

  | Sales/yr | Downloads/yr | Downloads/day | Net (US) |
  |---|---|---|---|
  | 500 | ≈25,000 | ≈70 | ≈$12.7k |
  | 2,000 | ≈100,000 | ≈275 | ≈$51k |
  | 5,000 | ≈250,000 | ≈685 | ≈$127k |

  For a new, unknown MAS app in the crowded "PDF" category, sustaining 275–685 downloads a day without ranking top 10 for "pdf" or getting Apple features is optimistic. **Suspicion (3) is plausible.** A realistic plan: base case 300–800 sales in year one, with an upside case of 2,000 if the app ranks well for "pdf editor" or "ocr" or gets press. This is a judgment call; no MAS PDF-category download data was found.
- The plan should model a blended price, not the flat $29.99:
  - launch-month sales at $19.99;
  - Spain/EU VAT-included storefronts;
  - possibly lower LatAm prices.
  - A blended net of about $20–22 per sale may be more realistic than $25.49, which cuts the scenarios by 15–20%.
- Setapp would add a small, usage-based income stream. For a utility opened occasionally (to sign or compress a PDF), payouts depend on how many Setapp members open it in a month. It is worth adding later as incremental income, not as a core channel.

### Gaps
- No MAS-specific download-to-paid conversion data was found for free apps with a one-time IAP unlock. RevenueCat's figures cover subscriptions.
- No disclosed revenue for a MAS PDF utility at about $30 was found.
- Setapp's actual per-app payout amounts are not public in the sources found.

---

## 6. Apple Search Ads ("Apple Ads") on the Mac App Store: availability, CPT/CPI, is $300–$500 meaningful?

### Takeaway
Available evidence says **Apple Ads does not serve Mac App Store apps**. A November 2025 developer forum thread reports that the Apple Ads site would not create a campaign for a macOS app. Apple's help text, quoted second-hand, requires an iPhone or iPad app, and Apple's 2026 expansion of ad slots covers iOS/iPadOS only. The planned $300–$500 Search Ads budget for "PDF editor" therefore probably cannot be spent on the MAS at all. Even on iOS, CPT benchmarks of about $1.6–$2.3 would buy only about 150–300 taps.

### Cited Findings
- Developer forum, Nov 2025: "Are Apple Search ads supported for apps in the macOS App Store? … the Apple ads website does not seem to allow this. The Apple ads website seems to assume that my app is in the iOS App Store." It has no replies and about 586 views. — [Apple Developer Forums 806737](https://developer.apple.com/forums/thread/806737)
- An older forum thread quotes Apple's help saying an Apple Search Ads account requires an iPhone or iPad app currently on the App Store. This is second-hand. — [Apple Developer Forums 693552](https://developer.apple.com/forums/thread/693552)
- Apple added more ad positions to App Store search results starting March 3, 2026 (UK and Japan first, all Apple Ads markets by the end of March), on iPhone with iOS 26.2+ and iPad with iPadOS 26.2+. Mac is not mentioned. Billing stays cost-per-tap, and advertisers cannot choose positions. — [MacRumors](https://www.macrumors.com/2026/01/23/more-app-store-ads-coming-soon/); [AppleInsider](https://appleinsider.com/articles/26/01/22/the-app-store-will-have-even-more-ads-in-march-2026-starting-with-the-uk); [9to5Mac](https://9to5mac.com/2026/01/22/app-store-search-ads-more-ads-march/)
- Conflicting signal: a Mainspring blog post (updated Aug 2026) says Mac users see sponsored App Store results and explains the Apple Advertising privacy settings on macOS. It is a secondary, non-Apple source and does not show that developers can buy Mac placements. — [Mainspring](https://trymainspring.com/blog/stop-apple-targeting-ads-mac)
- CPT benchmarks (iOS):
  - AppTweak median search-results CPT: about $0.92 globally, $1.91 in the US.
  - SplitMetrics average CPT in 2025: $2.25; average CPA: $3.76.
  - MobileAction: Productivity CPT rose from $0.94 to $1.64 in 2025.
  - — [AppTweak 2026 benchmarks](https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks?lang=en-US); [SplitMetrics](https://splitmetrics.com/blog/apple-search-ads-cost); [MobileAction](https://www.mobileaction.co/?p=16483)

### Inferences
- **Suspicion (2) is confirmed, and it is worse than "too small".** The channel probably does not exist for Mac apps, so this line should come out of the budget or be repointed. Confirm in the Apple Ads console before launch.
- Even if Mac ads existed, $400 at $1.64–$2.25 CPT is about 180–245 taps. At about 50% tap-to-install and about 2% install-to-paid, that is roughly 2–5 sales. It is meaningless as a growth lever and only useful as a keyword test.
- Better uses of $300–$500:
  - a small Reddit or Google Ads test on "compress pdf mac" / "ocr pdf mac" pointing to the website or the MAS link;
  - review copies and outreach to Mac blogs and newsletters, including Spanish-language Mac media;
  - a Product Hunt launch;
  - bundle or deal sites, as PDF Squeezer has used Bundlehunt.

### Gaps
- Apple's own Apple Ads help page could not be fetched (DNS error), so there is no first-party, 2026-dated statement on Mac support.
- No CPT data for the "pdf", "pdf editor" or "pdf reader" keywords specifically; only category and global benchmarks.

---

## 7. ASO: name, subtitle and keyword rules; trademark risks; competitor naming

### Takeaway
Use the 30-character name, the 30-character subtitle and the 100-character keyword field. Keywords are separated by commas without spaces and should not repeat words already in the name. Apple names trademarked terms and competitor app names in keywords as a common reason for rejection. "Acrobat", "Adobe", "PDF Expert" and "UPDF" must stay out of the name, subtitle and keywords. "PDF" itself is a generic term (an ISO standard), so a name that includes "PDF" is fine and helps search.

### Cited Findings
- Keywords: 100 characters total, separated by commas without spaces. Don't repeat plurals or words already used, "app", or category names. Apple warns against "unauthorized use of trademarked terms, celebrity names, and other protected words and phrases" and competitor app names in keywords. — [Apple, Product page](https://developer.apple.com/app-store/product-page)
- App name limit is 30 characters, and only about the first 26 may show in iPhone search results. Subtitle is 30 characters and can be changed with each version (older third-party source). — [MobileAction](https://www.mobileaction.co/blog/how-to-name-an-app/); [AppsFlyer](https://appsflyer.com/blog/mobile-marketing/app-title/)
- Do a trademark search before choosing a name. — [MobileAction](https://www.mobileaction.co/blog/how-to-name-an-app/)

### Inferences
- Name pattern: "[Brand] – PDF Editor & OCR" (30 characters max). Subtitle example: "Firma, comprime, OCR, formularios" in the Spanish localization and "Sign, fill, compress & OCR PDFs" in English.
- Keyword field per locale: use different terms in each localization, such as escanear, firmar, comprimir, unir, formulario, ocr, sign, merge, compress, fill, scan, annotate. Mexico and Spain may index additional locales; verify in App Store Connect.
- Avoid "Acrobat-like", "alternative to Adobe" and similar wording in the metadata. Comparisons can go on the website.

### Gaps
- No 2026 Apple-authored page confirming the 30-character name and subtitle limits was retrieved (these limits are widely known).
- Which locales the Spain and Mexico Mac App Store storefronts index was not researched.
- Competitor MAS names and keyword difficulty for "pdf" were not retrieved; no ASO tool data was accessible.
