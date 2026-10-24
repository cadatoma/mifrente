# Dónde está el dinero en el App Store (iOS y Mac) para desarrolladores indie/solo — octubre 2026

> Nota de método (leer primero): el acceso directo a páginas web (WebFetch/curl) estuvo bloqueado por la política de red de esta sesión. **No pude abrir los PDF ni las páginas originales** de RevenueCat, Adapty, Sensor Tower ni Appfigures, y todos los datos vienen de resúmenes de búsqueda que citan esas páginas o coberturas secundarias. Donde la cifra viene de un blog secundario lo marco. Varios resúmenes secundarios **mezclan cifras de RevenueCat y de Adapty** (por ejemplo "top 10% = 94,5–95% de los ingresos" o "planes semanales = 55,5%", que son de Adapty y se atribuyen a veces a RevenueCat). Los dos informes "State of…" 2026 (RevenueCat y Adapty) salieron en marzo de 2026 y cubren sobre todo datos de 2025. No encontré ningún informe nuevo de este tipo entre abril y octubre de 2026.
>
> Actualización del cliente: las 4 apps de `00_mis_apps_actuales.txt` NO son sus apps principales, así que estas notas no las analizan y se centran en el mercado en general.

## 1. ¿Qué categorías generan más ingresos (no-juegos) y cuáles son accesibles para un indie?

### Takeaway
En dinero absoluto, los no-juegos ya superan a los juegos (IAP +21% en 2025). Las categorías más grandes (redes sociales, streaming, citas) las dominan las grandes marcas. El crecimiento y la parte accesible para un indie están en IA, edición de foto/vídeo, utilidades y salud y fitness. Según RevenueCat, Photo & Video es la categoría donde más apps nuevas llegan a $1K/mes, aunque también es la que peor retiene.

### Cited Findings
- En 2025 el gasto in-app global fue de $167.000M (+10% interanual). El IAP de no-juegos creció un 21% y por primera vez superó a los juegos, que crecieron un 1,3% — [Sensor Tower, State of Mobile 2026](https://sensortower.com/press/press-release-boosted-by-gen-ai-services-consumers-spent-more-money-in-apps-than-games-for-first-time); [Sensor Tower blog](https://sensortower.com/blog/state-of-mobile-2026)
- Las categorías no-juego que más ingresan siguen siendo redes sociales, streaming de películas/TV y citas — [Sensor Tower blog](https://sensortower.com/blog/state-of-mobile-2026)
- Crecimiento de ingresos en 2025 por categoría: apps de IA +254% interanual, "short dramas" +115%, edición de medios +71% — [Sensor Tower](https://sensortower.com/blog/state-of-mobile-2026)
- Las apps de IA generativa duplicaron descargas (3.800M) y casi triplicaron su IAP hasta superar los $5.000M en 2025 — [Sensor Tower press](https://sensortower.com/press/press-release-boosted-by-gen-ai-services-consumers-spent-more-money-in-apps-than-games-for-first-time)
- Las cifras de Sensor Tower son estimaciones de App Store + Google Play. No incluyen las tiendas Android de China ni las ventas D2C/web — [Sensor Tower](https://sensortower.com/blog/state-of-mobile-2026)
- Apple (estudio de ecosistema publicado en junio de 2026): el ecosistema facilitó más de $1,4 billones (trillion) en facturación y ventas en 2025. Los bienes y servicios digitales fueron unos $149.000M. El resto son sobre todo bienes físicos y publicidad, no "ingresos de apps" — [Apple Newsroom, jun 2026](https://www.apple.com/newsroom/2026/06/app-store-ecosystem-reaches-1-point-4-trillion-usd-as-developers-thrive-globally/); [9to5Mac](https://9to5mac.com/2026/06/04/app-store-ecosystem-generated-1-4-trillion-in-2025-90-commission-free/)
- LTV de instalación a 1 año (mediana, Adapty 2026) por categoría: Health & Fitness $1,21, Productivity $1,10, Utilities $1,09, Education $1,06, Entertainment $0,59 — [Adapty, State of In-App Subscriptions 2026](https://adapty.io/state-of-in-app-subscriptions-report/). Otro post de Adapty da $1,20 para Health & Fitness.
- Photo & Video es la categoría con más apps nuevas que llegan a $1K/mes en dos años: 21,4%, frente al 17,3% global. Pero está entre las dos peores en renovación: anual 23%, mensual 48%, semanal 45% (secundario, cita RevenueCat 2026) — [tasu.ai / mirava.io, resumen de RevenueCat](https://tasu.ai/library/app-category-revenue-per-install-benchmark); [RevenueCat, renovaciones por categoría](https://www.revenuecat.com/blog/growth/average-subscription-renewal-rates-by-app-category)
- Revenue per install a D14 (RevenueCat 2026, secundario): mediana global $0,23. El cuartil superior de Health & Fitness supera $0,48. Education está en $0,30 — [tasu.ai](https://tasu.ai/library/app-category-revenue-per-install-benchmark); [sahha.ai](https://sahha.ai/blog/health-app-monetization-first-month/)
- Health & Fitness (RevenueCat 2026, secundario): trial-to-paid mediano 37,7%; download-to-paid a 35 días 2,9% (cuartil superior >6,2%); valor del primer mes por pagador $24,23 de mediana — [sahha.ai](https://sahha.ai/blog/health-app-monetization-first-month/)
- Hay páginas de categoría oficiales de RevenueCat 2026 (Utilities, Education, Productivity, Business, Shopping, Gaming), pero no pude leerlas — [RevenueCat Utilities](https://www.revenuecat.com/state-of-subscription-apps-2026-utilities); [Education](https://www.revenuecat.com/state-of-subscription-apps-2026-education); [Productivity](https://www.revenuecat.com/state-of-subscription-apps-2026-productivity)

### Inferences
- Las categorías "grandes" (social, streaming, citas) no son realistas para un solo dev. Donde convergen dinero y accesibilidad es en Health & Fitness, Utilities, Productivity, Photo & Video y Education, en ese orden de LTV por instalación según Adapty. Sobre esa base corre la ola de IA: la edición de medios y las utilidades con IA crecen mucho más rápido que el mercado.
- Photo & Video es la que más rápido da los primeros ingresos, pero retiene mal. Encaja con apps de "uso puntual" (foto con IA, filtros, avatares) que viven del pago inicial o de planes semanales y necesitan adquisición continua.

### Gaps
- No pude obtener la tabla oficial de RevenueCat por categoría (precio mediano, conversión, reembolsos para Photo & Video y Productivity) porque las páginas originales estaban bloqueadas.
- No encontré datos de Appfigures sobre la cuota indie frente a grandes marcas por categoría.

## 2. Modelo de negocio: suscripción vs pago único vs consumibles (créditos) vs anuncios

### Takeaway
En los datos de RevenueCat y Adapty manda la suscripción con paywall duro y prueba gratuita. El paywall duro convierte unas 5 veces más que el freemium, y el plan semanal con prueba es la configuración con más LTV a 12 meses. El pago único funciona en nichos y sobre todo en Mac, pero casi no hay benchmarks rigurosos. Los créditos/consumibles se están imponiendo en las apps de IA con coste por uso.

### Cited Findings
- Paywall duro frente a freemium: conversión descarga→pago a día 35 de 10,7% frente a 2,1% (unas 5 veces más) — [9to5Mac / RevenueCat 2026](https://9to5mac.com/?p=1042212); [buildmvpfast (secundario)](https://www.buildmvpfast.com/blog/hard-paywall-vs-free-trial-revenuecat-indie-app-2026)
- Revenue per install a día 60: paywall duro $3,09 de mediana (cuartil superior >$5,50) frente a $0,38 en freemium — [RevenueCat blog "in 10 minutes" 2026](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026)
- Duración de la prueba: las pruebas de 17–32 días convierten al 42,5% de mediana, frente al 25,5% de las de menos de 4 días — [RevenueCat blog 2026](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026)
- En Utilities la prueba añade más LTV que en ninguna otra categoría: +85,1% frente a la compra directa. Le siguen Health & Fitness (+63,6%) y Education (+50,4%). En Productivity, el 71,9% de las conversiones ocurre el día 1 (secundario, cita RevenueCat 2026) — [arpubrothers](https://arpubrothers.com/blog/revenuecat-subscription-app-report-2026/); [Medium, resumen RC+Adapty](https://chuvak-pavel.medium.com/state-of-app-monetization-2026-key-trends-from-revenuecat-and-adapty-8bdc23a4bb6f)
- Apps de IA: generan un 41% más de ingresos por pagador en el primer año ($30,16 frente a $21,37), pero retienen peor en todas las duraciones. La cifra de "+30% de churn" sale de un resumen secundario que no pude verificar — [PPC Land, RevenueCat](https://ppc.land/ai-apps-earn-41-more-per-user-but-churn-30-faster-revenuecat-finds/); [Medium](https://chuvak-pavel.medium.com/state-of-app-monetization-2026-key-trends-from-revenuecat-and-adapty-8bdc23a4bb6f)
- Adapty 2026: el plan semanal con prueba da el mayor LTV a 12 meses, unos $54,50, frente a $7,40 del semanal sin prueba. Los planes semanales pasaron del 43,3% de los ingresos (dos años antes) al 55,5% en 2025 — [Adapty report](https://adapty.io/state-of-in-app-subscriptions-report/); [PPC Land](https://ppc.land/95-of-app-subscription-revenue-goes-to-top-10-adaptys-2026-benchmark-report/)
- Tramos de precio habituales en 2026 (secundario, sin fuente primaria clara): semanal $4,99–6,99, mensual $7,99–9,99, anual $29,99–39,99 — [consumoteca (secundario)](https://consumoteca.com.co/articles/en/revenuecat-recurring-subscriptions-explained-platform-pricing-and-2026-benchmarks)
- Precio mensual mediano por región (RevenueCat 2026): desde $9,99 en Norteamérica hasta $3,75 en India/Sudeste Asiático. Según un resumen secundario, las apps europeas cobran un 29–39% más que las norteamericanas — [RevenueCat SOSA 2026](https://www.revenuecat.com/state-of-subscription-apps); [Medium (secundario)](https://chuvak-pavel.medium.com/state-of-app-monetization-2026-key-trends-from-revenuecat-and-adapty-8bdc23a4bb6f)
- Reembolsos (Adapty): suelen estar entre el 2% y el 5% de las transacciones de pago, más altos en Education y Health & Fitness. Photo & Video lidera en reembolsos de prueba con un 6,4% global, que sube al 14,1% en APAC — [Adapty, refund rate](https://adapty.io/blog/refund-rate-metrics-and-benchmarking/); [Adapty report](https://adapty.io/state-of-in-app-subscriptions-report/)
- Errores de facturación: Google Play subió al 31% (desde 28,2%) y el App Store bajó al 14% (RevenueCat 2026, vía resumen) — [RevenueCat blog 2026](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026)
- Pago único: no encontré un benchmark 2026 riguroso. Algunos blogs citan que RevenueCat 2025 da "4,5 veces más ingresos de por vida por usuario con suscripción que con pago único", pero no pude verificarlo. Otra afirmación secundaria: ofrecer un lifetime junto a la suscripción subiría la conversión total un 15–25% — [theswiftk.it (secundario)](https://theswiftk.it.com/blog/how-to-monetize-ios-app-indie-developer); [appopportunity (secundario)](https://appopportunity.com/blog/indie-app-revenue-models-2026)
- Créditos/consumibles: varios blogs los presentan como el modelo en auge de 2026 para apps de IA con coste por uso (API), con el precio del crédito por encima del coste de API. Es opinión, no un benchmark — [funnelfox](https://blog.funnelfox.com/app-pricing-models-guide/); [catdoes](https://catdoes.com/blog/mobile-app-monetization-strategies)

### Inferences
- Para un indie que quiere ingresos rápidos, la palanca más probada es un paywall duro (o casi duro) tras el onboarding, con prueba. Prueba larga (17–32 días) si el valor tarda en notarse. Prueba corta o semanal si el valor es inmediato (IA foto/escáner). Un freemium generoso con "todo gratis para siempre" es la estrategia que peor convierte en estos datos.
- Pago único y freemium generoso tienen la peor economía de estos datos. Si un desarrollador ya usa esa combinación con ventas casi nulas, el modelo es parte del problema (Inference).
- En apps de IA conviene un plan semanal/anual más créditos, porque cada uso cuesta y el churn es mayor.

### Gaps
- No hay datos públicos fiables 2025–2026 de ingresos por anuncios para apps indie de utilidades en iOS.
- No hay comparación directa y rigurosa entre pago único y suscripción en 2026.

## 3. iOS vs Mac App Store vs iPad: ¿es el Mac buen sitio para un indie en 2026?

### Takeaway
Hay muy pocos datos duros sobre Mac. Apple no desglosa por plataforma, y RevenueCat y Adapty son casi todo móvil. Lo que existe indica que el Mac es un mercado mucho más pequeño pero menos saturado, donde el pago único y la venta directa (Paddle/Stripe/Setapp) pesan tanto o más que el Mac App Store. Sirve para utilidades "pro" de pago único. No es un atajo hacia ingresos rápidos.

### Cited Findings
- Encuesta de MacPaw/Setapp a unos 400 desarrolladores Mac: entre quienes venden por varios canales, la venta directa/web supone el 52% de los ingresos (44% en 2023), y solo ~20% depende únicamente del Mac App Store. Una encuesta de Setapp de 2023 decía lo contrario (Mac App Store 57%). La muestra tiene sesgo indie — [macapps.report "State of Mac Apps 2026" (vía resumen de búsqueda)](https://macapps.report/market); [Setapp](https://en.wikipedia.org/wiki/Setapp)
- Ejemplos declarados por sus fundadores (no verificados): BoltAI (cliente de IA para Mac) ingresaba unos $15.000–30.000/mes en 2025, con media cercana a $25.000. Sensei (Cindori, dev solo) facturó unos $300K en 2021 vendiendo directamente vía Paddle (dato antiguo) — [stealwhatworks / getgrumpi (secundarios)](https://stealwhatworks.com/blogs/news/mac-apps-making-real-money-now); [getgrumpi](https://getgrumpi.com/blog/how-much-do-indie-apps-make)
- Setapp, el marketplace de suscripción para Mac, ofrece más de 260 apps (mediados de 2025). Su marketplace alternativo de iOS en la UE cerró en febrero de 2026 — [Wikipedia: Setapp](https://en.wikipedia.org/wiki/Setapp)
- macOS tenía un 14,58% del mercado mundial de escritorio en junio de 2026 (StatCounter, vía resumen) — [commandlinux](https://commandlinux.com/statistics/macos-market-share-yearly-trends/)
- Comisión: 30% estándar, 15% con el Small Business Program (menos de $1M de ingresos el año anterior), igual en Mac — [theswiftk.it](https://theswiftk.it.com/blog/how-to-monetize-ios-app-indie-developer)

### Inferences
- Cuando los datos de Sensor Tower muestran que el crecimiento de los no-juegos está en móvil (IA, edición de medios), lo más rápido para facturar es iPhone. El Mac compensa como segundo canal para herramientas "pro" (productividad, desarrollador, PDF, IA local) con pago único de $20–60 o licencia directa, y para un dev que ya construye en Swift/SwiftUI, porque el coste de portar es bajo.
- En Mac, la búsqueda y el boca a boca (Product Hunt, Reddit, X, newsletters de apps Mac, Setapp) pesan más que la ASO del Mac App Store.

### Gaps
- No encontré cifras públicas de los ingresos totales del Mac App Store frente a iOS en 2025–2026.
- No encontré datos específicos de iPad.

## 4. Geografía: cuota de EE. UU. frente a España/LatAm; ¿tiene sentido "Spanish-first"?

### Takeaway
EE. UU. vale aproximadamente 70 veces España en gasto digital en iOS. Los usuarios norteamericanos pagan más (LTV del primer año $32 frente a $25 en Europa Occidental) y convierten mejor. LatAm convierte poco (1,5%) y paga precios bajos, aunque crece rápido y la adquisición es barata. Comercialmente compensa apuntar primero a EE. UU. en inglés y localizar al español (incluido el público hispano de EE. UU.), no empezar en español.

### Cited Findings
- Según el estudio de Apple, los bienes y servicios digitales en iOS sumaron en 2025 unos $62.000M en EE. UU. y unos $24.000M en Europa (Reino Unido $6.700M, Alemania $4.400M, Francia $2.500M, Italia $1.300M, España $0.900M). Brasil sumó $1.400M en iOS, y el IAP total (iOS+Android) fue de $2.500M en Brasil y $1.900M en México (resumen secundario de cifras de Apple y PPC Land) — [getpanto.ai (secundario)](https://www.getpanto.ai/blog/apple-app-store-statistics); [Apple Newsroom](https://www.apple.com/newsroom/2026/06/app-store-ecosystem-reaches-1-point-4-trillion-usd-as-developers-thrive-globally/). Otra fuente da $55.500M de gasto de consumo en EE. UU. (+18%) con otra metodología.
- LTV realizado mediano del primer año por pagador (RevenueCat 2026): Norteamérica $32, Europa Occidental $25, India/SEA $14. La conversión de Latinoamérica (1,5%) está cerca de India/SEA. RevenueCat define LatAm como Brasil, México, Argentina, Chile, Colombia y Perú. Las diferencias geográficas de conversión son menores que las de ingresos — [RevenueCat SOSA 2026](https://www.revenuecat.com/state-of-subscription-apps)
- Revenue per install a día 60: Norteamérica $0,55 de mediana (cuartil superior >$1,39), unas 5 veces la de India/SEA ($0,11) — [RevenueCat SOSA 2026](https://www.revenuecat.com/state-of-subscription-apps)
- Tasa instalación→prueba: Norteamérica 14,5% frente a 7,6–10,2% en otras regiones. Con $1.000 de adquisición pagada se consiguen 65 suscriptores en Brasil frente a 15 en EE. UU. — [Adapty 2026](https://adapty.io/state-of-in-app-subscriptions-report/)
- LatAm tuvo el mayor crecimiento mediano de MRR (17,2%) (secundario). Los tests de localización (traducción y moneda) dieron el mayor aumento de LTV de todos los tipos de experimento, +62,3% (secundario, no verificado) — [Medium](https://chuvak-pavel.medium.com/state-of-app-monetization-2026-key-trends-from-revenuecat-and-adapty-8bdc23a4bb6f); [PricePush, lectura de las 336 páginas](https://newsletter.pricepush.app/p/i-read-all-336-pages-of-revenuecats)
- CPI mediano en Apple Ads: EE. UU. ~$4,06, España ~$1,43, México ~$1,10 — [AppTweak, Apple Ads benchmarks 2026](https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks)

### Inferences
- España (~$0,9 mil millones en iOS digital) más todo LatAm en iOS es una fracción pequeña de EE. UU. Una app "Spanish-first" limita su techo de forma estructural.
- La estrategia con mejor relación coste/beneficio es inglés y EE. UU. primero, con precios en USD de nivel norteamericano, más la localización al español con precios regionales (LatAm a $3–5/mes). El español sigue siendo una ventaja diferencial en nichos de EE. UU. con muchos hispanohablantes (sanidad, transporte, construcción, inmigración).
- Para probar barato si un concepto convierte, LatAm/España sirve como mercado de prueba con CPI bajo, pero los ingresos de verdad estarán en EE. UU./Reino Unido/DACH/Australia.

### Gaps
- No encontré un porcentaje oficial de la cuota de EE. UU. sobre los ingresos globales del App Store. Las cifras mezclan iOS solo, iOS+Android e IAP total, y las fuentes de EE. UU. no coinciden ($20.000M frente a $55.000–62.000M).
- No encontré datos sobre el tamaño de la demanda de apps en español por parte de hispanos en EE. UU.

## 5. Arquetipos con menor tiempo hasta el primer ingreso y ejemplos reales (orgánico vs pago)

### Takeaway
Los grandes éxitos indie recientes (Cal AI, Umax, RizzGPT) son apps de consumo con IA, paywall duro y crecimiento por influencers/UGC en TikTok e Instagram, que luego se escalaron con publicidad pagada. No son orgánicos. Las cifras son autodeclaradas y no cuadran entre fuentes. Por categoría, Photo & Video y las utilidades de IA son las que más rápido llegan a $1K/mes.

### Cited Findings
- **Cal AI** (contador de calorías por foto): MyFitnessPal dijo que superó los $30M de ingresos anuales en menos de dos años y lo adquirió en 2026 (condiciones no reveladas, equipo de 7). Otras fuentes hablan de $40M (Latka) o $50M ARR. TechCrunch señaló que no pudo verificar los ingresos, mientras que Fortune dijo haber revisado registros con "varios millones al mes" — [valueaddvc](https://valueaddvc.com/pulse/cal-ai-30m-revenue-myfitnesspal-acquisition-2026); [Latka](https://getlatka.com/companies/calai.app); [TechCrunch](https://techcrunch.com/2025/04/03/teen-with-4-0-gpa-who-built-the-viral-cal-ai-app-was-rejected-by-15-top-universities); [Fortune](https://www.fortune.com/2025/10/12/zach-yadegari-entrepreneur-gen-z-coder-rejected-by-the-ivy-league-despite-founding-a-30-million-app-you-dont-need-college-to-find-success-millionaire-co-founder)
- Cronología de Cal AI según Latka: $1M MRR en noviembre de 2024 y más de $2M MRR en enero de 2025. Según Yadegari, la publicidad pagada lo llevó de $2M a $4M/mes — [Latka](https://getlatka.com/companies/calai.app)
- Marketing de Cal AI: el primer post de influencer costó unos $2.000 y dio unas 1.000 descargas en dos días. En mayo de 2025 tenían 250 influencers en nómina y un gasto mensual en marketing de varios cientos de miles de dólares. Usar el contenido de influencers como anuncio pagado en Facebook topaba en unos $5.000/día de gasto rentable — [NetInfluencer](https://www.netinfluencer.com/cal-ai-founder-zach-yadegari-breaks-down-the-influencer-playbook-behind-his-apps-growth/); [Latka](https://getlatka.com/companies/calai.app)
- **Umax** (rating de apariencia con IA, Blake Anderson): según su fundador, más de 10M de descargas, pico cercano a $700K/mes, luego unos $400K. Un análisis chino estima ingresos de por vida de ~$2M frente a los >$3M declarados. **RizzGPT/Plug AI**: unos 3M de descargas y ~$200K/mes (declarado) — [transcripción de podcast](https://sozai.app/transcript/80-millions-dollars-20-years-apps-mobile/); [huxiu](https://www.huxiu.com/article/4050088.html); [Startup Ideas Podcast](https://audioscrape.com/podcast/the-startup-ideas-podcast/episode/how-to-build-1m-viral-ai-apps)
- Photo AI (Pieter Levels, web, no App Store) se cita por encima de $130K/mes. Los casos de $20K–60K MRR "son reales pero raros, y casi todos tenían distribución antes que producto" (secundario) — [getgrumpi](https://getgrumpi.com/blog/how-much-do-indie-apps-make); [youcouldshipthis](https://youcouldshipthis.com/blog/indie-app-revenue-realistic-expectations)
- Estrategia de portafolio: un caso (blog de marketing, una sola persona) pasó de $100 a $10K MRR en 8 meses lanzando 28 apps y llegó a más de $25K MRR — [buildmvpfast (secundario)](https://www.buildmvpfast.com/blog/portfolio-app-strategy-multiple-apps-revenue-solo-founder-2026)
- Mediana de tiempo hasta $1.000 MRR: "58 días" (secundario, sin cohorte definida) — [termsandconditionstemplate (secundario)](https://termsandconditionstemplate.com/app-revenue-statistics-2026)
- Photo & Video: 21,4% de las apps llegan a $1K/mes en dos años, la tasa más alta por categoría — [tasu.ai/mirava (secundario de RevenueCat)](https://www.mirava.io/blog/subscription-revenue-by-app-category-2026-data)
- Oleada de "lightweight AI consumer utility apps" (escáneres, contadores por foto, rating/analizadores) — [Consumer Startups substack](https://consumerstartups.substack.com/p/lightweight-ai-consumer-utility-apps)

### Inferences
- Los arquetipos más rápidos hasta el primer ingreso comparten cinco rasgos: (a) un "momento wow" en menos de 30 segundos (foto → resultado con IA), (b) un resultado visual que se comparte en TikTok/Reels, (c) un paywall duro, a menudo con plan semanal, (d) una categoría con alto revenue per install (Health & Fitness, Photo & Video, Utilities) y (e) audiencia en EE. UU. Los ejemplos de contador de calorías, escáner/analizador, mejora de foto y rating con IA encajan.
- Los casos famosos no son orgánicos puros. Arrancan con influencers/UGC, que cuestan dinero aunque sea poco al principio (~$2.000 por post en Cal AI), y escalan con publicidad pagada. Un solo dev sin presupuesto ni distribución no debería esperar resultados similares.
- Las calculadoras "pro" de nicho y las apps de examen tienen techo bajo pero más demanda por búsqueda (ASO/Apple Ads). Encajan mejor con Apple Search Ads que con TikTok.

### Gaps
- No pude obtener estimaciones de Appfigures de apps indie concretas (el acceso a appfigures.com estaba bloqueado y las búsquedas solo devolvían páginas de perfil vacías).
- No encontré datos de Rise ni de Quittr.
- No hay desglose verificable del porcentaje orgánico frente a pagado en ninguno de los casos.

## 6. Distribución de resultados: % de apps con $0, $1K+/mes, $10K+/mes; qué distingue a los ganadores

### Takeaway
La distribución es brutalmente desigual y empeora. En Adapty, el 10% superior de las apps se lleva ~95% de los ingresos de suscripción. Según RevenueCat, solo el 17,3% de las apps nuevas llega a $1K/mes en dos años y el 4,6% a $10K/mes. El top 10% creció su MRR un 306% mientras el cuartil inferior cayó un 33%. La oferta de apps nuevas se ha multiplicado (de ~2.000 a casi 15.000 lanzamientos de apps de suscripción al mes), en parte por el desarrollo con IA.

### Cited Findings
- Muestra de RevenueCat 2026: más de 115.000 apps y más de $16.000M de ingresos — [RevenueCat SOSA 2026](https://www.revenuecat.com/state-of-subscription-apps); [SaaStr](https://www.saastr.com/the-top-10-learnings-from-revenuecats-state-of-subscription-apps-how-115000-mobile-apps-deliver-16b-in-revenue-whats-working-whats-quietly-killing-growth/)
- Los lanzamientos mensuales de nuevas apps de suscripción pasaron de ~2.000 hace tres años a casi 15.000 (carta de Jacob Eiting, CEO de RevenueCat) — [9to5Mac](https://9to5mac.com/?p=1042212); [PPC Land](https://ppc.land/the-app-middle-class-is-dying-and-revenuecats-data-shows-exactly-how-fast/)
- Crecimiento interanual de MRR: mediana +5,3%. El cuartil superior creció un 80% y el top 10% un 306%; el cuartil inferior cayó un 33% ("la clase media de las apps se está muriendo") — [RevenueCat blog 2026](https://www.revenuecat.com/blog/growth/subscription-app-trends-benchmarks-2026); [9to5Mac](https://9to5mac.com/?p=1042212); [Subscription Insider](https://www.subscriptioninsider.com/blog/revenuecat-data-shows-subscription-app-growth-concentrating-at-the-top-news)
- Apps nuevas que alcanzan $1K/mes en dos años: 17,3%; $10K/mes: 4,6% (cifras de RevenueCat 2026 vía secundarios) — [getgrumpi](https://getgrumpi.com/blog/how-much-do-indie-apps-make); [termsandconditionstemplate](https://termsandconditionstemplate.com/app-revenue-statistics-2026)
- Ingreso mensual mediano un año después del lanzamiento: ~$72; el top 10% supera los $2.574 (secundario que cita RevenueCat). Otro resumen dice que la mediana de ingreso mensual por app bajó de $627 a $492 (probablemente otra base o muestra; no cuadra con lo anterior) — [termsandconditionstemplate](https://termsandconditionstemplate.com/app-revenue-statistics-2026); [Medium](https://chuvak-pavel.medium.com/state-of-app-monetization-2026-key-trends-from-revenuecat-and-adapty-8bdc23a4bb6f)
- Adapty 2026 (16.000+ apps, más de $3.000M): el 95% de los ingresos de suscripción va al top 10% de apps (92,7% en 2023). Otras versiones dan 94,5%. Las apps nuevas ganan ~25% menos de mediana que las lanzadas pocos años antes — [Adapty](https://adapty.io/state-of-in-app-subscriptions-report/); [PPC Land](https://ppc.land/95-of-app-subscription-revenue-goes-to-top-10-adaptys-2026-benchmark-report/); [Data Analysis Journal](https://dataanalysis.substack.com/p/2026-benchmarks-more-apps-less-quality)
- Afirmación sin metodología de que "la app solo-dev mediana verificada gana $3.000–8.000 MRR": contradice a RevenueCat y conviene descartarla — [thebotpost (secundario)](https://thebotpost.com/startups/indie-ai-apps-making-real-money)

### Inferences
- Para un dev con 10+ apps y ventas casi nulas, estar en la mediana (~$72/mes por app, o $0) es lo esperable estadísticamente, no una anomalía. El 83% de las apps nuevas no llega a $1K/mes.
- Lo que distingue a los ganadores en estos datos: paywall duro con prueba (unas 5 veces más conversión), precios de nivel EE. UU., una categoría con alto revenue per install, experimentación de precio y paywall, localización (+62% de LTV en tests, secundario) y, sobre todo, distribución (influencers, UGC, publicidad) en vez de esperar al tráfico orgánico de la tienda.
- La avalancha de apps hechas con IA (unas 7 veces más lanzamientos) hace que "construir rápido" ya no sea una ventaja por sí sola. La ventaja está en distribución y nicho.

### Gaps
- No encontré un porcentaje fiable de apps con exactamente $0 de ingresos. El dataset de RevenueCat solo incluye apps que usan su SDK, lo que sesga hacia apps con monetización activa.
- No pude verificar en la fuente primaria las cifras de 17,3%, 4,6% y $72.

## 7. Economía de Apple Search Ads y TikTok/UGC para indies en 2026

### Takeaway
Apple Ads en EE. UU. cuesta ~$1,6–1,9 por tap y ~$4 por instalación (mediana), y convierte a pago bastante mejor que otros canales (1,92% frente a 0,91%). TikTok da instalaciones más baratas ($1,5–3 en EE. UU. para no-juegos), pero de menor intención. Con un LTV de primer año de ~$32 por pagador en NA y conversiones del 2–10%, la adquisición pagada solo se recupera si la app tiene paywall duro y buena conversión.

### Cited Findings
- AppTweak 2026: CPT mediano en EE. UU. $1,91. CPI mediano: EE. UU. ~$4,06, España ~$1,43, México ~$1,10 — [AppTweak](https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks)
- CPT en EE. UU. por categoría (AppTweak): Sports $14,56, Finance ~$4,17, Business ~$3,33, Games ~$2,03; Shopping, Books y Social por debajo de $1. CPI en resultados de búsqueda: de $1,33 (Shopping) a $26,70 (Sports) — [AppTweak](https://www.apptweak.com/en/aso-blog/apple-ads-benchmarks)
- Adapty 2026 (90 países): CPT mediano en EE. UU. $1,58 y CPA $2,51 en EE. UU. SplitMetrics 2025: CPT medio ~$2,25 en las 15 categorías principales. Business of Apps: $1,56 en EE. UU. — [Adapty, Apple Ads benchmarks 2026](https://adapty.io/blog/apple-ads-benchmarks-2026/); [Business of Apps](https://www.businessofapps.com/marketplace/apple-search-ads/research/apple-search-ads-costs/)
- Instalación→pago con Apple Ads: 1,92% frente a 0,91% en otros canales pagados. Los mejores países llegan al 9–17% y las mejores categorías en EE. UU. al 3–8% — [Adapty, install-to-paid](https://adapty.io/blog/apple-ads-install-to-paid-rate-benchmarks/); [Adapty, Apple Ads por nicho](https://adapty.io/apple-ads-for-subscription-apps/)
- TikTok (blogs de proveedores, no auditados): CPI para no-juegos en EE. UU. de $1,50–3,00 en el primer trimestre de 2026, frente a $2,50–5,00 en Instagram Reels. Fintech llega a $12–18. Presupuesto mínimo de $50/día por campaña y $20/día por grupo de anuncios — [RocketShip HQ](https://www.rocketshiphq.com/tiktok-vs-instagram-reels-app-advertising/); [Admetrics](https://www.admetrics.io/post/tiktok-ads-costs-complete-2026-pricing-guide); [theviralapp](https://theviralapp.com/blog/tiktok-cpi-benchmarks-app-category-2026/)
- En suscripción, Instagram Reels da usuarios de más intención y mejor retención a D7 pese a su CPI más alto que TikTok — [RocketShip HQ](https://www.rocketshiphq.com/tiktok-vs-instagram-reels-app-advertising/)
- UGC: $100–500 por vídeo de nano-influencer; UGC generado con IA $5–50 por vídeo. Hay que sumar un 15–25% de gestión. Los CPI "efectivos" de UGC de $0,30–2,50 son autodeclarados — [theviralapp](https://theviralapp.com/blog/ugc-vs-paid-ads-mobile-apps-2026/); [stormy.ai](https://stormy.ai/blog/scaling-ugc-mobile-app-cpi-strategy); [stackmatix](https://www.stackmatix.com/blog/tiktok-ugc-ads-strategy)

### Inferences
- Cuenta rápida de payback (Inference). Con un CPI de $4 en Apple Ads EE. UU. y un 2–3% de instalación→pago, cada pagador cuesta ~$130–200, frente a un LTV mediano del primer año de $32 en NA. **No se recupera** salvo con conversión de top-cuartil (~6–10% con paywall duro), precios más altos (anual de $40–60) o palabras clave de nicho baratas (CPT < $1). Por eso Apple Ads funciona mejor en nichos de alta intención y baja puja que en categorías genéricas.
- UGC/TikTok tiene otra economía: el coste es el vídeo, no la instalación. Un vídeo orgánico viral cuesta lo mismo que uno que no funciona, lo que lo convierte en una lotería barata y repetible para un solo dev: muchos vídeos, de una cuenta propia o de micro-creadores a $100–500.
- Empezar en LatAm/España con CPI de $1,1–1,4 sirve para validar la conversión del paywall barato, no para facturar.

### Gaps
- No hay datos públicos de ROAS/payback para apps indie pequeñas (todos los benchmarks son de proveedores o agregados).
- Los CPT de Apple Ads para España/México por categoría no aparecieron en los resultados.
