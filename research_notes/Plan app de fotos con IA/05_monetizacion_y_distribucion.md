# Monetization, pricing and distribution for a $59 one-time Mac AI photo-enhancement app (direct via Paddle first, Mac App Store second), as of 2026-10-24

Scope: this checks the "Precio y canales de venta" and "Costos" sections of `00_plan_original.txt`. The plan proposes:
- a free trial that exports with a watermark;
- a $59 license ($39 in the first month) for 2 Macs, including 1.x updates;
- an optional $29/yr "pase de actualizaciones" (upgrade pass); if not renewed, the buyer keeps what they have;
- channels: Paddle (5% + $0.50) first, the Mac App Store (MAS, 15%) second, Setapp later;
- scenarios of 100/500/1,000 sales a year, giving $5.6k/$27.8k/$55.6k net;
- an optional $300–$500 launch ad budget.

Access note: direct fetches of developer.paddle.com, topazlabs.com, on1.com and docs.setapp.com failed with DNS errors from this environment. Figures from those sites therefore come from search-result summaries of the official pages or from third parties, and are flagged as such. Some MAS, Paddle, Lemon Squeezy, Setapp and Apple Ads facts are reused from the sibling PDF-app note (`../Plan editor PDF para Mac/04_monetizacion_app_store.md`), with their original sources.

---

## 1. Pricing benchmarks in the category (Oct 2026), and whether $59 is the right price

### Takeaway
Since Topaz went subscription-only (Sept/Oct 2025, roughly $199/yr for Photo) and Adobe agreed to buy it (June 2026), the one-time alternatives cluster in tiers:
- **$49.99:** Pixelmator Pro, which has ML denoise and super-resolution and is now also part of Apple's subscription;
- **$79–$99:** Aiarty "lifetime", on promotion;
- **$119–$130:** DxO PureRAW 5 and Luminar Neo, with paid major upgrades at about $80–$90;
- **about $300+:** Capture One.

Affinity is now free, but its AI super-resolution needs Canva Premium. A focused denoise + upscale + batch tool at **$59 sits just above Pixelmator Pro and about half the price of PureRAW**. That is defensible. $49 would compete head-on with Pixelmator Pro ($49.99), which is bundled with far more features. $79 is plausible if quality is close to Topaz/DxO, but leaves less room against Aiarty promotions. I would keep $59 list, test $69–$79 later, and not go to $99 at launch.

### Cited Findings
- **Topaz:**
  - Ended new perpetual licenses with the Topaz Studio launch in September 2025, with a final purchase window closing in early October. Existing owners keep their versions. — [Fstoppers](https://fstoppers.com/originals/adobe-buying-one-last-good-things-photo-editing-903215); [CGPress](https://cgpress.org/archives/topaz-labs-ends-perpetual-licenses-with-launch-of-topaz-studio-subscription.html)
  - Third-party pages quoting Topaz's pricing FAQ list Photo AI at $39/mo, $199/yr (Personal) or $599/yr (Pro), and Gigapixel at $149/yr. Krea lists Topaz Studio (all apps) at $399/yr Personal and $799/yr Pro. Topaz's own page could not be fetched. — [Renderahouse](https://www.renderahouse.com/blog/topaz-ai-pricing); [Krea](https://www.krea.ai/blog/is-topaz-ai-free-pricing-system-requirements-and-alternatives-in-2026)
  - The Personal tier reportedly limits commercial use to organizations under $1M in annual revenue. — [Krea](https://www.krea.ai/blog/is-topaz-ai-free-pricing-system-requirements-and-alternatives-in-2026)
  - A Topaz staff reply says "At this time, we do not offer a trial for the Topaz Studio Desktop Collection". Instead there is a 48-hour refund window. — [Topaz community](https://community.topazlabs.com/t/topaz-studio-transition-questions/95039?page=26) (via search summary)
  - Adobe agreed to buy Topaz on June 24/25, 2026, for about $340M according to its 10-Q, with closing expected in Adobe's fiscal Q4 2026. Topaz's standalone products and current licensing are said to continue "for now". — [Adobe 10-Q](https://www.sec.gov/Archives/edgar/data/0000796343/000079634326000156/adbe-20260828.htm); [TechCrunch](https://techcrunch.com/2026/06/25/adobe-acquires-image-and-video-enhancement-tool-maker-topaz-labs/); [PetaPixel](https://petapixel.com/2026/06/25/adobe-acquires-ai-upscaling-specialists-topaz-labs/)
- **DxO PureRAW 5:**
  - At launch (Apr 2025): $119.99 new, $79.99 upgrade from v3/v4. — [Amateur Photographer](https://amateurphotographer.com/latest/photo-news/dxo-pureraw-5-arrives-with-all-new-denoising/)
  - Later (5.5) figures: $129.99 new, $89.99 upgrade. 5.5 was free for v5 owners. The date is unclear and conflicts with the launch figures. — [Yahoo Tech](https://tech.yahoo.com/cameras/articles/raw-power-move-dxo-challenges-140000872.html)
  - Black Friday 2025: $99 new and $75 upgrade. A user claims DxO discounts only once a year. — [Slickdeals](https://slickdeals.net/f/18840493-dxo-photo-editing-software-download-once-a-year-bf-sale-up-to-50-off-includes-upgrades-photolab9-pureraw5-viewpoint5-nikcollection8-filmpack8)
- **Luminar Neo:** $119 one-time Desktop license for 2 computers, with generative tools for one year; Cross-device $159; Max $179 (dated July 30, 2026). This conflicts with another source citing a $249 "lifetime" license. — [Photutorial](https://photutorial.com/luminar-ai-review/); [Imagen](https://imagen-ai.com/post/lightroom-vs-luminar-neo.md)
- **Pixelmator Pro:**
  - One-time price on Mac is still $49.99 (€59.99 in Germany). It is also in Apple Creator Studio at $12.99/mo or $129/yr, launched Jan 28, 2026.
  - Some new features, such as Warp, are subscription-only, so one-time buyers do not get every new feature. Apple itself now runs a "pay once, plus subscription for new features" model.
  - — [Macworld](https://www.macworld.com/article/3031215); [heise](https://heise.de/-11157563); [TidBITS](https://tidbits.com/?p=72934)
- **Aiarty Image Enhancer:**
  - Official store: lifetime license listed at $155, promoted to $99, for 3 PCs with free lifetime updates.
  - Sponsored articles: $79.
  - MacG (France, Sept 2026): €69 instead of €145, for up to 3 Macs.
  - — [Aiarty buy page](https://www.aiarty.com/ai-image-enhancer/buy.htm); [MacG](https://www.macg.co/services/2026/09/photos-anciennes-ou-basse-resolution-aiarty-image-enhancer-les-ameliore-naturellement-licence-vie-52-311161)
- **ON1:**
  - An "ON1 NoNoise AI 2027" pre-order page exists, but I could not get a current standalone perpetual price (the store could not be fetched). — [ON1 store](https://www.on1.com/store/on1pk-eg26/)
  - A DPReview thread says a perpetual Photo RAW 2026 license gets updates for about a year, then updates stop. — [DPReview](https://www.dpreview.com/forums/threads/is-on1-following-c1.4816213)
- **Capture One:** perpetual Pro widely cited at $299. All prices rose 6% from June 2026, so the new perpetual price is unverified (about $317 by my arithmetic). — [PetaPixel](https://petapixel.com/2026/05/27/capture-one-to-increase-all-product-prices-by-6/); [Imagen](https://imagen-ai.com/post/lightroom-classic-price/)
- **Affinity (Canva):**
  - Relaunched as one free app around Oct 29, 2025.
  - AI tools, including super resolution, colorization and depth estimation, need a Canva premium plan.
  - The app works offline after activation with a free Canva account.
  - — [heise](https://heise.de/-10964820); [Neowin](https://www.neowin.net/software/canva-relaunches-affinity-as-a-free-all-in-one-creative-app/); [TidBITS](https://tidbits.com/?p=72234)
- **Adobe:** 1TB Photography Plan $19.99/mo; the 20GB plan rose to $11.99/mo (Adobe, Dec 2024; current 2026 figures from third parties). Lightroom includes AI Denoise. — [Adobe blog](https://blog.adobe.com/en/publish/2024/12/15/all-new-photography-innovations-pricing-updates); [Imagen](https://imagen-ai.com/post/lightroom-classic-price/)
- **Price sensitivity:** Fred Miranda forum users complained that Topaz Photo "will now be about 200 per year" and pointed to buy-outright options such as DxO. A Topaz moderator justified subscriptions as delivering "continuous value — faster improvements, more frequent updates". — [Fred Miranda forum](https://www.fredmiranda.com/forum/topic/1916403/); [Fstoppers](https://fstoppers.com/originals/adobe-buying-one-last-good-things-photo-editing-903215)

### Inferences
- **$59 is well placed.** It costs less than four months of Topaz Photo ($39/mo), under a third of a year of Topaz ($199/yr), about half of PureRAW or Luminar, and only $9 above Pixelmator Pro.
- **$49** gives no clear advantage and invites a direct "why not Pixelmator Pro?" comparison.
- **$79** fits if blind tests show quality near DxO DeepPRIME or Topaz. At that price the pitch "a quarter of the price of PureRAW + Topaz" still holds.
- **$99** puts the app in the Aiarty-promo and PureRAW-on-sale zone without those brands. That is not advisable for v1.0.
- **Launch price:** $39 (-34%) is deep. DxO's norm is about 20–25% off at launch or Black Friday, and Luminar runs about 20% sales. A $45–$49 launch price, or $39 only for waitlist and beta testers, protects more margin. This is a judgment call; no elasticity data was found.
- **Price anchoring:** the competitors' recurring costs ($199/yr Topaz, $129/yr Creator Studio, $240/yr Lightroom 1TB) make a good anchor table for the website.
- **Market risk:** Pixelmator Pro ($49.99 or in Creator Studio) and free Affinity mean "denoise/upscale on Mac" is partly commoditized. The app needs a quality and speed differentiator specifically on high-ISO RAW and batch work.

### Gaps
- No primary 2026 pricing pages were retrieved for Topaz, ON1, DxO or Capture One because of fetch failures. Re-check before publishing.
- No quantitative price-elasticity study for photographers was found. The evidence is forum sentiment only.
- Whether PureRAW and Luminar have moved prices again after Oct 2026 is unverified.

---

## 2. The "upgrade pass" ($29/yr, keep what you have): precedents, perception, renewal rates, Paddle support, alternatives

### Takeaway
The model is well established in Mac and dev tools:
- Sketch: renewal $120/yr, keep the last version;
- Panic Nova: $99 plus $49/yr, keep the last version and get point releases of your major version;
- JetBrains: perpetual fallback license after 12 months of subscription;
- Topaz: used annual "upgrade" renewals ($49–$148) before switching to subscriptions in 2025.

It is generally seen as fairer than a pure subscription. Topaz's experience shows the risk: renewal prices crept up and the model was eventually dropped. No public renewal-rate figures were found. Paddle Billing supports annual subscriptions natively, but **Paddle Billing no longer generates license keys**, so the license and entitlement layer has to be built or bought (for example Keygen or Cryptlex).

### Cited Findings
- **Sketch:** renewal $120/seat/yr for a year of Mac updates. When it lapses you can "keep running the last Mac version you updated to", with no further updates. In 2020 this was $99/yr. — [Sketch license](https://sketch.com/license); [Sketch support](https://www.sketch.com/support/mac-only-licenses/expired-license/); [MacStories 2020](https://www.macstories.net/news/sketch-changes-direction-on-pricing/)
- **Panic Nova:** $99 including the first year of updates, then $49/yr. "Your purchased copy of Nova will never expire". Without renewal "you will still be able to update to Nova 12.1 or Nova 12.2… you won't be able to update to Nova 13". "You will always get to keep your last update forever." — [Panic Nova FAQ](https://help.panic.com/nova/purchase-faq)
- **JetBrains:** after 12 consecutive months of subscription you get a perpetual fallback license "for the last major version that was available when your subscription started", plus minor releases. — [JetBrains sales FAQ](https://sales.jetbrains.com/hc/articles/207240845)
- **Topaz (before 2025):**
  - Users recall upgrades starting at $49 for one product and $99 for several.
  - Later quotes: Photo AI $74; Denoise, Sharpen and Gigapixel $49 each; Video AI $129. One user reported a 50% jump to $148 for Photo plus Gigapixel.
  - A $99 "Photo Upgrade Plan" covering all photo apps was withdrawn.
  - Prices were shown only when signed in.
  - — [Topaz community: Renewal Licenses](https://community.topazlabs.com/t/renewal-licenses/59515); [Topaz community: Photo AI Pricing](https://community.topazlabs.com/t/photo-ai-pricing/78645); [Topaz community: Upgrade plan](https://community.topazlabs.com/t/dont-see-photo-upgrade-plan-options/57195) (forum posts, anecdotal)
- **Tower:** went subscription-only (Basic $69/yr, Pro $99/yr). Updates and support end when the subscription lapses. Owners of v1/v2 licenses kept those versions and got 50% off the first year. — [Tower pricing](https://www.git-tower.com/pricing); [Michael Tsai 2018](https://mjtsai.com/blog/2018/06/26/git-tower-3-switches-to-subscription)
- **Retcon:** the developer says it is a subscription because "these make more money", and that he deliberately did not choose a keep-the-current-version model. This comes from the developer's Mastodon thread via search summary, so it is not a precedent for the pass. — [Retcon launch thread](https://friends.grishka.me/posts/1498752)
- **Paddle:**
  - In Paddle's Classic-vs-Billing feature comparison, "License key generation and activation" is marked deprecated in Billing.
  - Paddle's migration plan says license key generation isn't handled by Paddle in Billing and recommends building it yourself.
  - The Classic-only "Paddle License (SDK)" option generated licenses for Mac apps.
  - — [Paddle feature comparison](https://developer.paddle.com/migrate/learn/feature-comparison.md); [Paddle fulfillment (Classic)](https://paddle.com/support/which-fulfillment-method-to-choose) (via search summaries)
- **Integrations:**
  - Keygen's public Paddle example targets Paddle Classic (vendor ID, vendors.paddle.com) and is "not 100% production-ready". — [Keygen example](https://github.com/keygen-sh/example-paddle-integration)
  - Cryptlex publishes a Paddle Billing webhook server that creates and renews licenses on purchases and renewals. — [Cryptlex docs](https://mintlify.com/cryptlex/third-party-integrations/integrations/paddle)

### Inferences
- **The pass is a sound model, if it stays cheap and predictable.** At $29/yr it is about 49% of the $59 license. Nova's ratio is the same (49%), Sketch's is higher, and Topaz's old renewals were 37–50% of new. Commit publicly to a capped price (for example "never more than $29 for existing customers"), because Topaz's renewal creep is what users remember.
- **Simplify the wording:** "Licencia de $59 con 12 meses de actualizaciones incluidos; después, $29/año opcional para seguir recibiendo novedades. Lo que ya tienes es tuyo para siempre." This is the Sketch/Nova model, and it is easier to explain than "1.x updates plus a separate pass". It also avoids the "v2 is coming, so wait" problem, because every buyer gets 12 months of everything.
- **Alternatives:**
  - (a) Paid major upgrades, DxO-style ($59 new, about $35 upgrade). This is simple, but revenue arrives in lumps and the app can't ship new models mid-cycle without giving them away free.
  - (b) "Pay once, 1 year of updates, keep the version" plus optional renewal, i.e. the pass with a year included (recommended above).
  - (c) No updates beyond 1.x, then a new app. This is MAS-friendly, but buyers dislike it.
- **Renewal-rate assumption:** with no published data, plan conservatively at 15–30% of the previous year's buyers. That is my assumption and must be validated. At 25% renewal on 500 buyers: 125 × ($29 − 5% − $0.50) ≈ $3.4k extra a year.
- **Paddle setup:** a one-time price ($59) plus an annual subscription price ($29). A webhook server (Cloudflare Worker or a small serverless function) listens to Paddle Billing `transaction.completed` and `subscription.*` events and issues or extends entitlements in Keygen, Cryptlex or a self-made signed-license service. The app checks "updates-until" against each build's release date. This is an inference, not a Paddle-documented recipe.

### Gaps
- No public renewal rates were found for Sketch, Nova, Topaz or JetBrains.
- I could not confirm whether Paddle offers any first-party license add-on in Billing as of Oct 2026, or whether Keygen now ships an official Paddle Billing integration.
- No survey of user perception of "upgrade pass" vs subscription in photo software was found; there are only forum anecdotes.

---

## 3. Mac App Store: can it support the pass, a watermark trial, 2 Macs and Family Sharing? Sandbox, batch, Lightroom. Is it worth it?

### Takeaway
Technically, yes:
- a free download with a **non-consumable "Full license" IAP**;
- an optional **$0 "14-day Trial" non-consumable**, or just the watermark;
- plus an **auto-renewable yearly subscription** for "new models and major features".

Apple's own Pixelmator Pro now uses this pattern: a one-time app plus subscription-only features. Constraints:
- a MAS build can't take Paddle license keys or use Sparkle;
- the purchase covers every Mac on the Apple ID, which is more generous than "2 Macs";
- Family Sharing is optional and irreversible;
- Apple Ads probably can't promote Mac apps.

For pro photographers who already buy direct from DxO, Skylum and Topaz, the MAS is a discovery and trust channel for hobbyists, not the main revenue source.

### Cited Findings
- **Licensing and updates:** Guideline 2.4.5:
  - "(i) They must be appropriately sandboxed"
  - "(vi) They may not present a license screen at launch, require license keys, or implement their own copy protection"
  - "(vii) They must use the Mac App Store to distribute updates; other update mechanisms are not allowed."
  - Under 3.1.1, unlocking a full version must use IAP, and apps may not use license keys.
  - — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- **Trial:** 3.1.1 says "Non-subscription apps may offer a free time-based trial period … Non-Consumable IAP item at Price Tier 0 … 'XX-day Trial.'" Before it starts, the app must state the duration, what stops working and the downstream charges. — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- **Subscriptions:** 3.1.2(a) says "you must provide ongoing value to the customer, and the subscription period must last at least seven days and be available across all of the user's devices". When moving to subscriptions, "you should not take away the primary functionality existing users have already paid for". 3.1.2(c) requires describing clearly "what the user will get for the price". The guidelines do not contain the phrase "paid upgrades". — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- **Cross-platform purchases:** 3.1.3(b) Multiplatform says features bought on your website may be accessed in the app only if the same items are also available as IAP. — [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- **Apple precedent:** the Pixelmator Pro one-time purchase stays at $49.99, while new features such as Warp are subscription-only through Creator Studio. — [TidBITS](https://tidbits.com/?p=72934); [Macworld](https://www.macworld.com/article/3031215)
- **Non-consumable vs subscription:** an Apple forum reply notes that a non-consumable keeps features "locked in forever", while subscription features are available only during the subscription. — [Apple Developer Forums](https://developer.apple.com/forums/thread/52890)
- **Family Sharing:** off by default for non-consumables, enabled per product, cannot be turned off, up to 5 family members. — [Apple, Supporting Family Sharing](https://developer.apple.com/documentation/storekit/supporting-family-sharing-in-your-app.md) (via sibling note)
- **Fees:** the Small Business Program gives 15% for developers under $1M in proceeds, including new developers, starting 15 days after the end of the fiscal month of approval. Enroll before launch. — [Apple SBP](https://developer.apple.com/app-store/small-business-program/)
- **Apple Ads:** a Nov 2025 developer forum post says Apple Ads won't create campaigns for macOS apps, and Apple's 2026 ad-slot expansion covers iPhone and iPad only. — [Apple Developer Forums 806737](https://developer.apple.com/forums/thread/806737); [MacRumors](https://www.macrumors.com/2026/01/23/more-app-store-ads-coming-soon/) (re-verified via sibling note; still applies here)
- **Sandbox and files:** sandboxed apps get file access through entitlements such as read/write to user-selected files and folders (Open/Save dialogs). — [Eclectic Light, Explainer: sandboxes (Apr 2026)](https://eclecticlight.co/2026/04/11/explainer-sandboxes/)
- **Sandbox and Lightroom:** MAS Lightroom differs from Creative Cloud mainly in sandbox file-access rules. MarsEdit needed a sandbox fix to reach Lightroom libraries. — [Thomas Fitzgerald](https://blog.thomasfitzgeraldphotography.com/blog/2019/6/lightroom-returns-to-the-mac-app-store); [Red Sweater](https://redsweater.com/blog/3294/marsedit-4-0-6-lightroom-fix)
- **Channel split:** among multi-channel Mac developers, direct sales are 52% of revenue and the MAS 48% (MacPaw survey, via search summary). — [The State of Mac Apps](https://macapps.report/market)

### Inferences
- **MAS product setup:**
  - free app with the watermark as the trial;
  - non-consumable "Licencia completa" at about $59.99 (tier);
  - auto-renewable "Pase de novedades" at $29.99/yr, which unlocks models and features released while it is active;
  - optional $0 "14-day Trial" non-consumable for watermark-free export during the trial.
- **"Keep what you have" in the MAS:** record each feature or model's release date in the app, and unlock it if the subscription was active at any point on or after that date (from StoreKit 2 transaction history), or, more simply, if it was active when the feature first shipped. This is my design; Apple documents no such pattern. Review risk is that 3.1.2(a) "ongoing value" must be visible. Shipping new models several times a year meets that.
- **"2 Macs" vs MAS:** the MAS gives the same Apple ID unlimited Macs. That is fine, but the direct license should then say "hasta 3 Macs", or "todas tus Macs personales", to avoid looking stingier than the MAS. Aiarty already offers 3 devices and Luminar 2.
- **Batch folders:** fine in the sandbox when the user picks the folder in NSOpenPanel or drags it in. Use security-scoped bookmarks for watch folders or to remember output folders. Writing output next to the originals only works within user-granted folders. These are inferences from the general sandbox model; there is no specific Apple citation.
- **Lightroom (v1.5+):**
  - Lightroom Classic "Edit In / Additional External Editor" hands the app a TIFF/PSD file path and waits for it to save back to the same file. A sandboxed app that is launched to open a document generally gets access to that file, so this should work. That is an inference to test.
  - Lightroom plug-ins (Lua) that call the app's CLI, or that write to arbitrary paths, are harder from the MAS build.
  - Plan Lightroom integration for the **direct build first**.
- **Is the MAS worth it?**
  - Benefits: lightweight trust, Apple-handled refunds, and search discovery for "denoise" or "upscale photo".
  - Costs: a second build (no Sparkle, StoreKit instead of Paddle), 15% vs about 6%, no Apple Ads, and no way to steer users to the web outside the US storefront.
  - Recommendation: launch direct first. Add the MAS build in the first 3–6 months, priced at parity ($59.99) so it doesn't undercut the web.

### Gaps
- No Apple document confirms that "non-consumable base + subscription for new features, keep after lapse" passes review on macOS, though Apple's own Pixelmator Pro is a strong precedent. Test with an early TestFlight or App Review submission.
- No source confirms how Lightroom "Edit In" behaves with a sandboxed external editor in 2026.
- No data on the MAS share of revenue for photo tools specifically. DxO, Topaz and Skylum mainly sell direct; their MAS presence was not verified.

---

## 4. Paddle vs Lemon Squeezy / Stripe Managed Payments / FastSpring; licensing and activation; piracy; light activation

### Takeaway
**Paddle remains the sensible default** for a Mac license plus an annual pass:
- merchant of record at 5% + $0.50;
- country price overrides;
- a mature Mac-developer user base.

The caveat is that you must supply your own license keys. The alternatives:
- **Lemon Squeezy:** same price, has built-in license keys, but is being folded into Stripe Managed Payments with slower support. Risky for a new product.
- **Stripe Managed Payments:** about 3.5% plus Stripe processing (2.9% + 30¢), so roughly 6.4% + 30¢. Lacks license keys and digital delivery.
- **FastSpring:** quote-based, estimated at roughly 5.9% + $0.95.

For licensing, Keygen (free dev tier, paid tiers $49–$399/mo per Capterra) or Cryptlex are off the shelf. A self-signed offline license (Ed25519-signed JSON, verified in the app) with a single online activation is cheapest. Expect a lot of piracy (one Mac utility developer counted about 23 pirated copies per sale), but pirates rarely convert. Keep activation light.

### Cited Findings
- **Paddle:**
  - 5% + $0.50 per transaction with no monthly fee; includes merchant-of-record and global tax handling (third-party sources; Paddle's page not fetched). — [Spendflo](https://spendflo.com/vendors/paddle); [Fungies](https://fungies.io/alternatives/paddle)
  - Price per customer is chosen in this order: country-specific override, then automatic currency conversion, then base price. Overrides are set with `unit_price_overrides` per country. Paddle supports 200+ countries and territories and 30 currencies. There is no built-in PPP calculator. — [Paddle, Offer localized pricing](https://developer.paddle.com/build/products/offer-localized-pricing/) (via search summary)
  - License keys are deprecated in Billing (see Q2). — [Paddle feature comparison](https://developer.paddle.com/migrate/learn/feature-comparison.md)
- **Lemon Squeezy:**
  - Stripe bought it in July 2024.
  - Its Jan 2026 update said it is "building toward Stripe Managed Payments", acknowledging slower support and fewer updates.
  - Managed Payments works only with Checkout and Payment Links, and lacks built-in affiliates, digital download delivery and storefronts.
  - No source says license keys carry over to Managed Payments.
  - — [Fungies](https://fungies.io/lemon-squeezy-stripe-acquisition-saas-founders-2026/); [Dodo Payments](https://dodopayments.com/blogs/lemonsqueezy-alternatives) (both competitors, so biased)
- **Stripe Managed Payments:** about 3.5% per successful transaction on top of standard Stripe processing (2.9% + 30¢ for US cards), as of Sept 2026, third-party. — [devtoollab](https://devtoollab.com/blog/best-merchant-of-record-platforms) (via sibling note)
- **FastSpring:** rates are not published. Estimates: about 5.9% + $0.95, plus FX markups of 1–3%; a competitor puts the base fee at "high-5% to high-8%" plus a fixed fee. — [Fungies FastSpring review](https://fungies.io/fastspring-review-2026); [Dodo Payments](https://dodopayments.com/blogs/fastspring-pricing-explained/) (competitor sources)
- **Keygen:** supports node-locked, floating, timed-trial and feature licenses. Capterra lists 6 plans, with a free "Dev 0" tier and paid tiers from $49 to $399/mo, updated in 2026 (not official). — [Capterra Keygen pricing](https://www.capterra.com/p/168916/Keygen/pricing/)
- **Piracy:**
  - Tunabelly (TG Pro, a direct-sale Mac app with a free trial): on May 6, 2015 there were 6 sales and at least 138 new pirated copies, a ratio that stayed "pretty consistent". — [Tunabelly blog](https://tunabellysoftware.com/blog/files/our-apps-are-being-pirated.html)
  - Gen Digital documents cracked Mac apps as a common malware vector. — [Gen Digital](https://www.gendigital.com/blog/insights/research/macos-cracked-software-malware-risks)

### Inferences
- **Recommended stack:**
  - Paddle Billing: one-time price plus yearly subscription price, with country overrides.
  - Webhooks to a tiny serverless license service, or Keygen's free/low tier until volume justifies it.
  - Licenses delivered by email.
  - The app stores a signed license file in the Keychain.
  - One online activation per Mac (limit 2–3), with deactivation from inside the app and from a customer web page.
  - Afterwards the app works fully offline. This matches the plan's "nada sale a internet" promise, apart from the activation ping and optional update checks.
- **Paddle's effective fee:** about 5.8% at $59 and 6.3% at $39, still far below the MAS 15%. Currency conversion on payouts may add a little (unquantified).
- **Piracy:** pirated copies of photo tools will appear quickly, especially as a "Topaz alternative". The watermark trial already serves honest evaluators. Don't build DRM. Do sign licenses to avoid trivial keygens, don't ship a "pro" binary to the public, and rely on update-pass entitlements (new models downloaded or unlocked for licensed users) as a soft incentive. Model downloads must not violate MAS 2.4.5(iv) in the MAS build, so bundle the models there.
- **Avoid Lemon Squeezy for a new launch** because of its migration uncertainty. Stripe Managed Payments is viable only if you build licensing and delivery yourself and accept about 6.4% + 30¢.

### Gaps
- No primary 2026 Paddle pricing page was retrieved, and I could not confirm whether Paddle's fee applies to the tax-inclusive total.
- FastSpring's actual rates and Keygen's official price list were not obtained from the vendors.
- No recent, reliable piracy-rate data for Mac photo apps; the only data point is from 2015.

---

## 5. Affiliate programs in photo software: standard rates and running one with Paddle

### Takeaway
The category's public baseline is **20% commission with a 30-day cookie**: Topaz officially, Skylum "20% or more", with third-party reports of tiers up to 40–50%. Bundle sites pay developers about 50% of each license. For an indie app, offer **25–30%** to photography YouTubers and bloggers. That beats the big brands' 20%, is affordable at 6% Paddle fees, and costs about $15–18 per $59 sale. Paddle Billing has no native affiliate program, so use a third-party tool (check Paddle Billing support specifically) or simple coupon codes per creator.

### Cited Findings
- **Topaz:** "earn 20% commission on all orders placed through your exclusive link"; 30-day credit window; free to join; monthly payouts; approval by the marketing team, with replies "within a month". — [Topaz affiliates](https://topazlabs.com/affiliates); [Topaz docs](https://docs.topazlabs.com/sales-account-licensing/join-topaz-labs-community)
- **Skylum (Luminar):**
  - Official: "Earn 20% or more from every sale of Luminar", 30-day attribution. — [Skylum affiliates](https://www.macphun.com/affiliates)
  - Third parties report tiers rising to 40%, up to 50% "based on performance", $0.75 per free-trial download, and a FlexOffers payout range of 16–68%. These are unverified and may be dated. — [FlexOffers](https://www.flexoffers.com/affiliate-programs/luminar-affiliate-program/); [UpPromote](https://uppromote.com/blog/affiliate-programs-photography/)
- **DxO:** no affiliate commission details were found.
- **Affiliate tooling with Paddle:** a FirstPromoter post (a competitor) says Rewardful supports only Paddle Classic, not Billing. Tolt is listed as supporting Paddle, but Billing support is unconfirmed. Lemon Squeezy's built-in affiliates are not carried into Stripe Managed Payments. — [FirstPromoter](https://firstpromoter.com/blog/best-tolt-alternatives); [Rewardful Paddle announcement](https://www.rewardful.com/product-updates/rewardful-launches-paddle-integration); [Fungies](https://fungies.io/lemon-squeezy-stripe-acquisition-saas-founders-2026/)
- **Bundles:** a 2021 BundleHunt pitch offered developers "50% of every license sold", paid 14 days after the deal. — [Fetch Softworks forum](https://fetchsoftworks.com/fetch/messageboard/%25e2%2580%259c-fetch%25e2%2580%259d-is-invited-to-the-%25e2%2580%259c2021-epic-mac-bundle)

### Inferences
- **Economics at 30%:** $59 − $3.45 Paddle − $17.70 = **$37.85 net per affiliate sale**. At the $39 launch price: $39 − $2.45 − $11.70 = $24.85. Still positive, but the deep launch discount plus affiliates compounds, which is another reason for a smaller launch discount.
- **Minimum viable program:** a unique Paddle discount code per creator (for example 10% off for viewers), tracked through Paddle's transaction data and paid out monthly by hand. That needs no extra software until there are about 20 or more affiliates. Then add a tool with confirmed Paddle Billing webhook support.
- **Who to target:** photography YouTubers who review Topaz alternatives and denoise comparisons, wedding and event photographer communities, and Spanish-language photo channels for Spain and LatAm. The $300–$500 ad budget is better spent on free licenses and review units for creators than on ads, since Apple Ads can't target Mac apps anyway.

### Gaps
- DxO's and ON1's affiliate terms were not found.
- No confirmation of which affiliate SaaS tools support Paddle Billing (not Classic) as of Oct 2026.
- No data on what share of Topaz or Skylum sales comes from affiliates.

---

## 6. Setapp fit and bundle effects

### Takeaway
Setapp pays 70% of membership fees, split by which apps each member used in the month. Higher list prices get a higher tier multiplier, and frequency of use doesn't count. For a $59 pro tool used in bursts by a minority of Setapp's general-utility audience, payouts are likely modest. Setapp is better as a later, incremental channel, once the list price has been in effect for 3+ months and if Setapp accepts the app. Bundles (BundleHunt, about 50% share of a heavily discounted price) bring volume and reviews, but anchor the price low. Use them only after the launch window, if at all.

### Cited Findings
- **Setapp membership revenue:** developers get 70% of membership revenue, distributed by usage (any launch in the month counts; frequency doesn't), weighted by the app's price tier. A partner fee adds +20% for members the developer refers (up to 90%). Single-app distribution pays 85% and requires the app to be in the Membership catalog first. — [Setapp docs, Distributing revenue](https://docs.setapp.com/docs/distributing-revenue); [Setapp Membership revenue](https://docs.setapp.com/docs/setapp-membership-revenue); [AppleInsider 2022](https://appleinsider.com/articles/22/06/17/how-setapps-app-service-is-building-value-for-developers-and-users)
- **Setapp price tiers:** tiers are based on the list price outside Setapp, which usually must have been in effect for at least 3 months. Minimum macOS 13. — [Setapp docs, Marketplace overview](https://docs.setapp.com/docs/setapp-marketplace-overview) (via search summary)
- **Setapp status:** MacPaw closed Setapp Mobile (EU iOS) on Feb 16, 2026. Setapp for Mac continues. — [AppleInsider](https://appleinsider.com/articles/26/01/15/setapp-mobile-eu-app-store-cleanmymac-business-both-close-down-for-good) (via sibling note)
- **Bundles:**
  - Luminar Neo has been sold through StackSocial for $79.99. — [BoingBoing](https://boingboing.net/2026/02/08/award-winning-photo-magic-minus-the-monthly-commitment.html)
  - BundleHunt's Black Friday 2025 bundle had 37 apps for about $16.70, against a nominal value of $1,439. — [Macwelt](https://www.macwelt.de/article/2966131/bundlehunt-black-friday-2025-37-mac-apps-fur-167-statt-1439-us-dollar.html)
  - BundleHunt's terms are "all sales are final". — [MacPowerUsers](https://talk.macpowerusers.com/t/bundlehunt-mac-bundle/28044)

### Inferences
- **Setapp vs the upgrade pass:** Setapp members expect all updates included. A Setapp build would include new models without the $29 pass, which partly undercuts the pass's value for direct buyers. Defer Setapp until after v2.0, or treat it as a separate audience.
- **Bundles:** at about $16.70 for 37 apps, per-app payout is cents to a few dollars. Bundles work for acquiring users, and possibly upgrade-pass renewals later, not for revenue. A 50%-share sale through StackSocial at about $29–$39 is less damaging than BundleHunt.

### Gaps
- Setapp's actual per-tier multipliers and typical monthly payouts per active user are not public.
- No developer postmortem on bundle effects for a photo app was found.
- The current Setapp membership price in 2026 was not confirmed.

---

## 7. How realistic the revenue scenarios are: conversion, traffic, watermark vs time-limited trials

### Takeaway
The only broad desktop dataset (a 2009 survey of 92 small vendors) gives a median band of **1.3–6.4% of downloads converting to sales (average 4.5%)**, with roughly **1% of website visitors buying**. More recent freemium benchmarks (subscription apps) are about 2%.
- **100 sales/yr** (about 2,000–5,000 trial downloads; about 10,000 site visitors) is achievable with modest forum and YouTube presence.
- **500/yr** (about 10k–25k downloads; about 50k visitors) needs sustained creator or affiliate coverage.
- **1,000/yr** needs press or a viral comparison video.

Net per sale is lower than the plan's flat $55.55 once launch pricing, VAT-inclusive EU pricing and affiliates are blended in. Plan for about **$45–$50**. No rigorous evidence compares watermark trials with time-limited trials.

### Cited Findings
- Successful Software survey (2009, 92 vendors): average sales-to-downloads 4.5%, with half the products between 1.3% and 6.4%; sales-to-visits about 1%. The sample is biased toward small vendors and unverified. — [Successful Software](https://successfulsoftware.net/2009/04/08/average-visitor-conversion-ratio/)
- Curio (Mac, 15-day trial): about 5.2% yearly average download-to-sale (2006; range 2.75–8.77% by month). — [Zengobi](https://blog.zengobi.com/2006/06/conversion-rates.html)
- RevenueCat 2026 (subscription apps): median freemium conversion about 2.1%; hard paywall 10.7%. — [RevenueCat](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026.md) (via sibling note)
- Patrick McKenzie found desktop apps converted worse than web apps. — [Kalzumeus](https://kalzumeus.com/2010/06/04/the-most-radical-ab-test-ive-ever-done)
- **Indie revenue examples:**
  - Sensei (Cindori, solo, direct via Paddle): about $300K in 2021. Screen Studio: about $30K/month. BoltAI: about $25K/month (2025). These are self-reported, via search summary. — [The State of Mac Apps](https://macapps.report/market)
  - Redacted, a $4.99 Mac photo app, ranked #8 in US Top Paid with only 87 sales ($302) on launch day (2015). — [MacRumors](https://macrumors.com/2015/05/07/redacted-mac-app-profits)
- **Watermark vs time-limited trials:** vendors use both, often combined; for example a 30-day full trial, then watermark, or a watermark throughout. — [Aspose](https://forum.aspose.com/t/trial-limitations-complete-list/65426); [Millumin](https://forum.millumin.com/discussion/1196/watermark-after-trial); [OriginLab](https://docs.originlab.com/quick-help/graph-watermark/)
  - No comparative conversion data was found.
- **Competitors' trials:** Topaz now offers no trial, only a 48-hour refund. — [Topaz community](https://community.topazlabs.com/t/topaz-studio-transition-questions/95039?page=26)

### Inferences
- **Traffic required** (assuming 3% download-to-sale, 30% visitor-to-download, so about 1% visitor-to-sale; my assumptions anchored on the survey):

  | Sales/yr | Trial downloads | Site visitors | Visitors/day |
  |---|---|---|---|
  | 100 | ≈3,300 | ≈10,000 | ≈27 |
  | 500 | ≈16,700 | ≈50,000 | ≈137 |
  | 1,000 | ≈33,000 | ≈100,000 | ≈274 |

- **Blended net per sale** (my model):
  - 25% of year-one sales at the $39 launch price ($36.55 net);
  - 40% EU/LatAm with VAT-inclusive pricing (≈$45 net; see Q8);
  - 15% via 30% affiliates (≈$38 net).
  - The result is roughly **$45–$48 net**, not $55.55.
  - Revised scenarios: 100 sales ≈ **$4.6k**, 500 ≈ **$23k**, 1,000 ≈ **$46k**, plus the upgrade pass from year two (about $3–7k on a 500–1,000 base at 25% renewal).
- **Realistic year one:** 150–400 sales for a solo developer with no audience. 1,000 needs one or two hit comparison videos ("Topaz alternative without subscription") or a front-page Reddit or Fstoppers mention. The timing tailwind is real but temporary (Topaz subscription plus Adobe acquisition). This is a judgment call.
- **Trial design:** the watermark-only trial is generous and good for "try it on your own photos", but it lets users judge quality and then leave. Suggestions:
  - a **subtle, cornered watermark** plus full-resolution 100% before/after in the app;
  - batch export of watermarked results limited to, say, 10 images;
  - optionally a 7-day watermark-free window started by email capture, which also builds a list.
  - Topaz's lack of a trial is an advantage to highlight.

### Gaps
- No post-2015 public download-to-sale data for Mac desktop apps with one-time licenses was found.
- No A/B evidence comparing watermark and time-limited trials.
- No public revenue for an indie Mac photo-enhancement tool comparable to this one.

---

## 8. Taxes/VAT effect on net per sale; regional pricing for Spain and LatAm

### Takeaway
The plan's $55.55 holds only when tax is added on top, as is typical in the US. In the EU, consumers expect tax-inclusive prices. At €59 tax-inclusive, Spain's 21% VAT leaves about **€45–46 net** after Paddle. On the MAS, a €59.99 storefront price nets about **€42**, not $50.15, because Apple prices outside the US and Canada include tax. Paddle supports per-country price overrides, so a LatAm price of about $39–$45 (Mexico 16% IVA, plus lower purchasing power) is easy to set up.

### Cited Findings
- **Apple:** "Prices in all countries except the U.S. and Canada include taxes." Developers choose a base storefront and can override per storefront. — [9to5Mac](https://9to5mac.com/2023/03/09/apple-app-store-price-points-purchases/); [Apple tech talk 110364](https://developer-mdn.apple.com/videos/play/tech-talks/110364/) (via sibling note)
- **Paddle:** country-specific overrides take precedence over automatic currency conversion; supports 30 currencies. — [Paddle localized pricing](https://developer.paddle.com/build/products/offer-localized-pricing/)
- **Paddle tax:** merchant of record, handling VAT and sales tax. — [Spendflo](https://spendflo.com/vendors/paddle)
- **Pixelmator Pro** sells for $49.99 in the US and €59.99 in Germany, an example of tax-inclusive EU pricing set higher than USD. — [Macworld](https://www.macworld.com/article/3031215); [heise](https://heise.de/-11157563)
- **Aiarty** prices in Europe at €69 against $79–$99 in USD promotions. — [MacG](https://www.macg.co/services/2026/09/photos-anciennes-ou-basse-resolution-aiarty-image-enhancer-les-ameliore-naturellement-licence-vie-52-311161)

### Inferences
- **Net per sale** (assuming Paddle's fee is on the gross, tax-inclusive amount; unverified):
  - US $59 + sales tax added: $59 − $3.45 = **$55.55** (plan correct).
  - Spain €59 incl. 21% VAT: €48.76 ex-VAT − €3.45 ≈ **€45.31**. Alternatively, price at €64–€69 incl. VAT to match the US net. Pixelmator charges €59.99 against $49.99.
  - Mexico, if $59 is IVA-inclusive (16%): $50.86 − $3.45 ≈ **$47.41**.
  - MAS Spain €59.99 tier: €59.99 / 1.21 × 0.85 ≈ **€42.14**. MAS US $59.99 × 0.85 = **$50.99**.
- **Suggested regional prices:**
  - US/Canada: $59 + tax.
  - Eurozone: €59–€65 incl. VAT. €59 is a psychologically clean number for Spain, and the margin loss is about 18%.
  - UK: £55 incl. VAT.
  - Mexico, Colombia, Argentina, Chile: about $39–$45 USD-equivalent via Paddle overrides, in local currency where Paddle supports it. Spanish-language marketing makes LatAm a natural secondary market, but price sensitivity is high. This is a judgment call; no elasticity data was found.
- Keep the launch price separate from regional pricing so LatAm buyers don't stack a $39 launch price with a regional discount, unless that is intended.
- **Spanish income tax** (IRPF or corporate tax, depending on the seller's setup) applies to Paddle payouts; that is outside this note's scope. Paddle as merchant of record removes the need to register for VAT OSS in the EU.

### Gaps
- I could not confirm whether Paddle calculates its 5% on the tax-inclusive total or on the net. This changes net per sale by about €0.50.
- Paddle's supported local currencies for LatAm (MXN, COP, ARS, CLP) were not verified.
- No data on price elasticity of LatAm photographers for software.
