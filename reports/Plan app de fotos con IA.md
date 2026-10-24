# Estrechar el plan para ganar sin suscripción

La mejor app posible no es el "Topaz de pago único" que describe el plan, una herramienta que limpia RAW, amplía y enfoca, todo a la vez. Es una versión más estrecha: **la herramienta de Mac más rápida y honesta para limpiar y ampliar en lote fotos ya reveladas (JPEG, HEIC, TIFF) y recortes, con el RAW resuelto mediante el decodificador de Apple y un aspecto natural por defecto**. El "por qué ahora" es cierto, pero está desactualizado. Topaz dejó de vender licencias perpetuas entre septiembre y octubre de 2025, y Adobe no se quedó en "acordar" la compra en junio de 2026: **la cerró el 23 de septiembre de 2026**. Además, los modelos de Topaz ya estaban dentro de Photoshop desde octubre de 2025. Mientras tanto, el hueco de "$59, pago único, en el equipo" se ha ido llenando:

| Rival | Precio | Qué aporta |
|---|---|---|
| **Pixelmator Pro** (de Apple) | $49.99 | Un editor completo con reducción de ruido y ampliación por IA |
| **ON1 NoNoise AI 2027** | $69.99 ($49.99 de lanzamiento) | Salió el 1 de octubre de 2026 con el mismo mensaje "sin suscripción" |
| **DxO PureRAW 6** | $139.99 | Lidera en calidad sobre RAW |
| **Upscayl** | Gratis | Amplía imágenes |

A eso se suma que, desde macOS 27, Apple regala a cualquier app una red neuronal que hace demosaico y reducción de ruido del RAW en el Neural Engine (RAW 9). Los modelos del plan trabajan sobre RGB ya revelado, así que en RAW de ISO alto quedarán estructuralmente por detrás de DxO y Lightroom.

En lo técnico, el plan tiene que cambiar cuatro cosas:

- probar NAFNet antes que SCUNet, invirtiendo el orden;
- descartar SwinIR;
- asumir que Real-ESRGAN corre en la GPU y no en el Neural Engine;
- diseñar la salida 4x en streaming para no agotar los 8 GB de un M1.

Aun con esos cambios, 10–12 semanas a medio tiempo solo alcanzan para una v1 recortada, que de forma realista pide 12–15 semanas. El plan completo se va a 18–22. En dinero, $59 se sostiene, pero el neto medio ronda **$45–48 por venta** y Paddle Billing ya no genera claves de licencia. Mucha de esta evidencia viene de fragmentos de búsqueda y de proyectos de un solo desarrollador. Por eso lo que decide es la prueba de las semanas 1–2, con criterios numéricos de sí/no.

## El "por qué ahora" es cierto, pero llega con un año de retraso

Las dos fechas del plan se sostienen en lo esencial.

**Topaz.** Anunció el fin de las licencias perpetuas en septiembre de 2025 y lo hizo efectivo el **3 de octubre de 2025**, al lanzar la suscripción Topaz Studio ([Digital Production](https://digitalproduction.com/2025/10/02/topaz-drops-perpetual-licences-bets-on-subscriptions-with-studio-launch/); [CG Channel](https://www.cgchannel.com/2025/09/topaz-labs-to-end-perpetual-licenses-of-its-software/)). Las fuentes no coinciden en la fecha exacta del cierre de ventas: el foro de Topaz lo sitúa el 16 de septiembre ([Topaz community](https://community.topazlabs.com/t/topaz-studio-transition-questions/95039?page=50)) y una fuente secundaria habla de un "último aviso" el 26 de septiembre ([Crisp](https://crispvideo.app/learn/why-topaz-ended-perpetual-licences/)). Aun así, "octubre de 2025" es correcto como fecha efectiva. Las licencias ya compradas siguen funcionando, pero los modelos nuevos solo llegan con suscripción ([CG Channel](https://www.cgchannel.com/2025/09/topaz-labs-to-end-perpetual-licenses-of-its-software/); [Krea](https://www.krea.ai/blog/is-topaz-ai-free-pricing-system-requirements-and-alternatives-in-2026)). Los precios actuales también están en conflicto entre fuentes: aparecen Gigapixel desde $149/año, Topaz Photo cerca de $199/año, Studio a $399/año y Studio Pro a $799/año, con promociones activas. Hay que confirmarlos en la página oficial antes de usarlos en marketing ([Topaz pricing](https://www.topazlabs.com/pricing); [Topaz Studio Pro](https://www.topazlabs.com/studio-pro)).

**Adobe.** Anunció la compra el 25 de junio de 2026 ([Adobe newsroom](https://news.adobe.com/news/2026/06/adobe-to-acquire-topaz-labs); [TechCrunch](https://techcrunch.com/2026/06/25/adobe-acquires-image-and-video-enhancement-tool-maker-topaz-labs/)) y **la completó el 23 de septiembre de 2026** ([Adobe blog](https://blog.adobe.com/en/publish/2026/09/23/adobe-completes-acquisition-of-topaz-labs); [DPReview](https://www.dpreview.com/news/adobe-finalizes-its-topaz-labs-acquisition-heres-what-that-means-for-users/)). Forbes cifra la operación en unos **$340M** ([Forbes](https://www.forbes.com/sites/dbloom/2026/09/23/adobe-closes-topaz-labs-deal-adds-ai-video--image-enhancement-tools/)), y otra nota atribuye esa cifra al 10-Q de Adobe ([Adobe 10-Q](https://www.sec.gov/Archives/edgar/data/0000796343/000079634326000156/adbe-20260828.htm)). Tras el cierre:

- Topaz sigue como marca independiente.
- El anuncio no dijo nada sobre precios ni licencias.
- Adobe planea extender los modelos de Topaz a Firefly y Creative Cloud ([Fstoppers](https://fstoppers.com/news/adobe-closed-its-purchase-topaz-labs-topaz-stays-separate-brand-904758); [Camera Jabber](https://camerajabber.com/photography-news/adobe-completes-topaz-labs-acquisition-topaz-stays-a-standalone-brand/)).

Un plan fechado el 19 de octubre que todavía dice "acordó comprarlo" da sensación de poca investigación. La corrección es de una línea, y de paso conviene sustituir la fuente secundaria (PhotoWorkout) por las primarias.

**La parte débil es el relato** de que "muchos fotógrafos usaban Topaz para no depender de Adobe y hoy buscan una alternativa de pago único". Desde Adobe MAX (28 de octubre de 2025), Topaz Gigapixel y Bloom ya funcionaban dentro de Generative Upscale de Photoshop, pagando con créditos: 10 a 20 por imagen en Gigapixel y 35 en Bloom ([Adobe, nota de prensa MAX](https://news.adobe.com/news/downloads/pdfs/2025/10/102825-creative-cloud.pdf); [Adobe Help](https://helpx.adobe.com/ca/photoshop/using/enhance-image-quality-with-generative-upscale.html)). El enfado es real: hubo un hilo de transición de al menos 51 páginas y usuarios que hablan de "alergia a la suscripción" ([DPReview forum](https://www.dpreview.com/forums/threads/topaz-labs-apps-are-now-subscription-only.4824377/)). Pero lo que hacen después es otra cosa: **se quedan con su versión perpetua congelada "mientras funcione" o se pasan a nombres conocidos**, como DxO PureRAW, el Denoise de Lightroom u ON1. Las apps nuevas y desconocidas casi nunca aparecen en esas conversaciones ([BirdForum](https://www.birdforum.net/threads/what-is-your-post-processing-image-software.470510/); [Finding the Universe](https://www.findingtheuniverse.com/best-noise-reduction-software/)). El miedo concreto ante la compra por Adobe es que se acabe el procesamiento local y empiecen a cobrar créditos ([Topaz community](https://community.topazlabs.com/t/adobe-to-acquire-topaz-labs/103761); [remio.ai](https://www.remio.ai/post/adobe-topaz-labs-acquisition-closes-but-independence-is-the-real-test)). Eso respalda un mensaje central de "100% en tu Mac, sin créditos".

La ventana se abrió en octubre de 2025 y se ha ido llenando:

- PureRAW 6 salió en marzo de 2026.
- Capture One añadió reducción de ruido con IA en mayo de 2026.
- ON1 lanzó NoNoise 2027 en octubre de 2026.

El próximo pico llegará si Adobe sube precios o mete Topaz en Creative Cloud, y ninguna de las dos cosas ha pasado. Lo sensato es tener listo un kit de respuesta (entrada de blog, página comparativa y cupón) para publicar en 24–48 horas, sin apostar el plan a que ocurra. No hay datos sobre cuántos usuarios de Topaz han cancelado, ni datos de Google Trends sobre "topaz alternative" o "alternativa a topaz". El tamaño de la ventana sigue sin medirse.

## Cinco rivales de pago único ya ocupan el hueco de $59

El plan solo compara contra Topaz y Lightroom, pero la categoría tiene al menos cinco jugadores que importan. Ninguna nota tiene datos de ventas, así que el "top 5" de abajo combina dos criterios: el consenso de las reseñas de 2026 y la relevancia directa para un fotógrafo con Mac.

| # | App | Precio y modelo | En qué es fuerte | Debilidad o hueco aprovechable |
|---|---|---|---|---|
| 1 | **Topaz Photo / Gigapixel / Studio** | Solo suscripción, ~$149–$799/año ([Topaz pricing](https://www.topazlabs.com/pricing)) | Referencia en ampliación y enfoque (Super Focus, Wonder 3.5 en la v1.7.0 del 27 de agosto de 2026) ([release notes](https://docs.topazlabs.com/topaz-photo/release-summary)) | Artefactos, Autopilot agresivo, no hay pago único, ahora es de Adobe |
| 2 | **DxO PureRAW 6** | **$139.99 pago único**, actualización $89.99 ([PetaPixel](https://petapixel.com/2026/03/03/dxo-wants-pureraw-6-to-be-the-first-step-in-your-photo-editing-workflow/)) | El mejor denoise RAW (DeepPRIME XD3), DNG lineal, lote paralelo, integración con Lightroom | Caro, solo acepta RAW, actualizaciones de pago resentidas, ~26–42 s por foto en XD3 |
| 3 | **Adobe Lightroom / ACR** (Denoise + Super Resolution) | Desde $11.99/mes ([Toolradar](https://toolradar.com/tools/adobe-lightroom/pricing)) | Comodidad, "suficiente" para eventos, 5–7 s por foto en M4 Pro | **Denoise solo funciona con RAW** ([lightroom-tools.com](https://lightroom-tools.com/blog/lightroom-classic-ai-denoise)), Super Resolution solo 2x ([Krea](https://www.krea.ai/blog/best-ai-photo-enhancers-in-2026)) |
| 4 | **ON1 NoNoise AI 2027** | **$69.99, $49.99 de lanzamiento**, app propia y plugin ([ON1](https://www.on1.com/products/nonoise-ai/buy/)) | El más barato de los establecidos, se vende como "sin suscripción" ([DPReview](https://www.dpreview.com/news/on1-nonoise-ai-2027-announcement/)) | Calidad un escalón por debajo de DxO según las reseñas |
| 5 | **Pixelmator Pro (Apple)** | **$49.99 pago único** en la Mac App Store, o dentro de Creator Studio a $12.99/mes ([Apple](https://www.apple.com/pixelmator-pro/); [MacRumors](https://www.macrumors.com/2026/01/28/apple-creator-studio-hands-on/)) | ML Denoise, ML Super Resolution, más de 750 formatos RAW, marca Apple | No es un reductor de ruido dedicado. Una prueba antigua vio su denoise RAW "a veces menos eficaz" ([DPReview 2023](https://www.dpreview.com/reviews/3667956131/pixelmator-pro-3-4-camelot-review-2023/)) |

**Luminar Neo** se vende con pago único y trae Noiseless AI y Upscale AI. Los precios publicados se contradicen: unas fuentes dan entre ~$79 y $119 y otras entre $249 y $369 de lista, y las herramientas generativas quizá solo vengan 12 meses ([Comparedge](https://comparedge.com/tools/luminar-ai/cost-guide); [Photutorial](https://photutorial.com/luminar-ai-review/)). Arrastra además mala fama por sus "Upgrade Pass" ([Fstoppers](https://fstoppers.com/artificial-intelligence/review-luminar-neo-fall-update-winner-some-powerful-new-tools-715721)).

**Aiarty Image Enhancer** vende una licencia vitalicia de $155 de lista que en la práctica cuesta $69–$109 por los descuentos constantes, para 3 Macs ([Aiarty](https://www.aiarty.com/store.htm)). Casi todo lo que se encuentra sobre él es contenido del propio fabricante.

**Capture One** añadió denoise con IA en la versión 16.8.0, el 28 de mayo de 2026 ([Wikipedia](https://en.wikipedia.org/wiki/Capture_One)), y subió precios un 6% en junio ([PetaPixel](https://petapixel.com/2026/05/27/capture-one-to-increase-all-product-prices-by-6/)).

**Upscayl** es gratis, de código abierto y está en la Mac App Store ([App Store](https://apps.apple.com/us/app/upscayl/id6468265473?mt=12)). Ronda las 44.500 estrellas en GitHub ([Star History](https://www.star-history.com/upscayl/upscayl/)), una señal de que hay demanda latente de ampliación local sencilla.

**Affinity** es gratis desde el 29 de octubre de 2025, pero su IA requiere Canva Premium ([ProVideo Coalition](https://www.provideocoalition.com/affinity-new-version-is-free-forever-for-everyone/)).

**Las apps pequeñas de la Mac App Store** tienen reseñas pobres; Photo Noise Reduction, por ejemplo, está en 1,7 estrellas ([App Store](https://apps.apple.com/us/app/photo-noise-reduction/id1209845752)). La lección es que un precio bajo en esta categoría suena a "app barata de la tienda".

**Apple RAW 9** es el rival de plataforma, el que todos los demás reciben gratis; se analiza más abajo.

Si se mira tarea por tarea, el reparto es claro:

- **Ruido en RAW con ISO alto:** las reseñas de 2026 ponen a DxO primero, sobre todo por encima de ISO 12.800. Topaz y Lightroom van cerca y ON1 un paso detrás ([Capture the Atlas](https://capturetheatlas.com/noise-reduction-software/); [Finding the Universe](https://www.findingtheuniverse.com/best-noise-reduction-software/)).
- **Ampliación:** Topaz es la referencia, hasta el punto de que Adobe presenta Gigapixel como la opción de Photoshop que "conserva el detalle existente" ([Adobe Help](https://helpx.adobe.com/ca/photoshop/using/enhance-image-quality-with-generative-upscale.html)).

Esto marca dónde está la apertura. En ruido RAW, la respuesta por defecto de la comunidad ya es "usa PureRAW o Lightroom". En **ampliación**, en cambio, las alternativas de pago único son las más débiles. Y en **reducción de ruido de JPEG, HEIC y TIFF**, Lightroom ni siquiera compite, porque no acepta esos formatos. El plan, por cierto, presenta el denoise como "la razón principal por la que se compra Topaz", y la evidencia apunta a lo contrario: la ampliación es el hueco más ganable. A $59, la app no tiene ventaja de precio frente a Pixelmator Pro ni frente al lanzamiento de ON1. Tiene que ganar por velocidad en lote, por el aspecto natural de los resultados y por aceptar archivos ya editados.

## Los fotógrafos castigan el "look IA", no la falta de limpieza

Sin contar el enfado con las suscripciones, la queja de calidad más repetida en todas las herramientas es **el exceso de procesado**, mucho más que la falta de reducción de ruido:

- cuadrículas o damero en fondos oscuros ([Nikonites](https://nikonites.com/forum/threads/anyone-having-trouble-with-checkerboard-artifacts-in-the-backgrounds-with-topaz-ai.48274/));
- bloques pixelados en cerca del 20% de las imágenes de un usuario ([Topaz community](https://community.topazlabs.com/t/one-or-more-pixelated-square-artifacts-in-output-tif-from-photo-ai/76597));
- detalle borrado por un Autopilot demasiado agresivo ([CaptureLandscapes](https://www.capturelandscapes.com/topaz-photo-ai/));
- caras recuperadas que "pueden verse inquietantes" ([TechRadar](https://www.techradar.com/computing/creative-software/topaz-photo-ai-review-image-correction-with-artificial-intelligence));
- piel "encerada" en bodas cuando el denoise se empuja demasiado ([findme.photo](https://findme.photo/blog/ai-photo-editing-stack-wedding-photographers-2026)).

Varias de esas quejas sobre Topaz son de 2023–2024, pero el patrón se repite en 2026. El deslizador de intensidad y la mezcla con el original que ya prevé el plan atacan justo este problema. Por eso un valor por defecto moderado y la promesa de "sin look IA" son argumentos de venta, no detalles.

El segundo bloque de quejas viene de **los profesionales que trabajan en Lightroom o Capture One**. Su flujo de referencia es meter el RAW, recibir un **DNG lineal** limpio y seguir ajustando el balance de blancos y el perfil. Lo que les falla:

- los "DNG falsos" de Topaz, que en realidad son "TIFF dentro de un envoltorio DNG" ([Lightroom Queen](https://www.lightroomqueen.com/community/threads/lrc-and-topaz-denoise-raw-files.44527/));
- el perfil de cámara que desaparece al volver a Lightroom ([Topaz community](https://community.topazlabs.com/t/missing-camera-profile-in-lightroom-after-photo-ai-plug-in-edit-of-raw-file/52977));
- espacios de color mal asignados en PureRAW 4 ([DxO forum](https://forum.dxo.com/t/pureraw-4-useless-due-to-wrong-color-spaces-for-dng-and-jpg/42175?page=3)).

El TIFF funciona, pero deja "horneados" el balance de blancos y el perfil.

El tercer bloque es **la velocidad del lote y la interfaz bloqueada**:

- La versión 14.4 de Lightroom Classic aplica Denoise en un diálogo modal que bloquea la app ([Thomas Fitzgerald](https://blog.thomasfitzgeraldphotography.com/blog/2025/8/how-to-background-process-denoise-in-lightroom-classic-144-and-other-ai-settings)). La idea "devolver Enhance al segundo plano" acumula más de 11 páginas de votos ([Adobe community](https://community.adobe.com/t5/lightroom-classic-ideas/p-bring-back-the-ability-of-enhance-to-run-in-the-background-lrc/idi-p/15374596/page/11)).
- En febrero de 2026, con la 15.2 en un M4 Pro, una foto suelta tardaba 5–7 s, pero en lote la segunda tardaba 38–40 s ([Adobe community](https://community.adobe.com/questions-675/denoise-takes-five-times-longer-in-batch-mode-than-single-image-1551176)).
- Una sola guía afirma que la 15.3 (abril de 2026) devolvió el lote al segundo plano ([lightroom-tools.com](https://lightroom-tools.com/blog/lightroom-classic-ai-denoise)).

Competir solo con "más rápido que Lightroom" es frágil, porque Adobe está cerrando esa brecha.

La disposición a pagar está bien dibujada. Los fotógrafos **pagan $80–$140 de una vez** por DxO, y durante años toleraron renovaciones de $99 al año en Topaz. El punto de ruptura fue la renovación de unos $199, que alguien llamó "robo a mano armada" ([Topaz community](https://community.topazlabs.com/t/renewal-licenses/59515); [TalkPhotography](https://www.talkphotography.co.uk/threads/topaz-subscription-renewal-what.771872/)). También molestan las actualizaciones de pago sorpresa: alguien que compró PureRAW 2 tres semanas antes protestó por pagar $29 para pasar a la 3, y otro usuario calificó de "justo" un precio de actualización de unos $45 ([DxO forum](https://forum.dxo.com/t/customer-unfriendly-upgrade-policy/49285)).

Las peticiones explícitas de funciones son escasas, pero apuntan a cuatro cosas:

- lote en segundo plano;
- entrada que no sea RAW;
- poder reutilizar los ajustes entre tomas, algo así como presets por ISO ([Adobe community](https://community.adobe.com/t5/lightroom-classic-bugs/p-paste-settings-from-previous-denoises-again/idc-p/15397145));
- quitar desenfoque de movimiento, que Topaz y ON1 ya venden.

La ampliación generativa despierta sospecha, no demanda: un usuario contó que Gigapixel le "estropeó los coches de la escena" y otros se quejan de créditos cobrados sin resultado ([Adobe bug report](https://community.adobe.com/bug-reports-403/p-firefly-won-t-upscale-images-but-it-still-takes-credits-1626948/index3.html)).

**Objetivo de velocidad.** PureRAW 6 tarda unos 26–30 s por archivo de 45 MP en XD3 sobre un M1 Max, y unos 17 s en un M2 Pro ([Photography Life](https://photographylife.com/dxo-pureraw-6-review-amazing-compression); [Shotkit](https://shotkit.com/dxo-pureraw-6/)). Lightroom marca 5–7 s en un M4 Pro. Para ser competitiva en modo "estándar", la app debería quedar en **5–15 s por imagen de 24–45 MP en un Mac reciente**. Con eso, una boda de 2.000 fotos se procesa en una noche.

En español no apareció ninguna necesidad distinta. El consejo es el mismo de siempre, "PureRAW primero, luego Lightroom" ([Capture the Atlas ES](https://capturetheatlas.com/es/dxo-pureraw-review/); [Fujistas](https://fujistas.com/foro/threads/experiencias-y-opiniones-sobre-dxo-pure-raw.69993/)). Lo que sí se ve es que el contenido nativo en español es escaso: dominan las traducciones y Aiarty ya ataca el SEO en español ([Aiarty ES](https://www.aiarty.com/es/blog/topaz-denoise.htm)). Ojo con un límite importante: **no se leyó ningún hilo de Reddit**, porque el entorno lo bloqueaba, y las citas de foros vienen de extractos de búsqueda.

## El plan, afirmación por afirmación

| Afirmación del plan | Veredicto | Por qué |
|---|---|---|
| "Topaz pasó a suscripción en octubre de 2025" | **Cierto** | Efectivo desde el 3 de octubre de 2025; anunciado en septiembre ([Digital Production](https://digitalproduction.com/2025/10/02/topaz-drops-perpetual-licences-bets-on-subscriptions-with-studio-launch/)) |
| "Adobe acordó comprarlo en junio de 2026" | **Cierto pero desactualizado** | Anunciado el 25 de junio y **cerrado el 23 de septiembre de 2026** ([Adobe blog](https://blog.adobe.com/en/publish/2026/09/23/adobe-completes-acquisition-of-topaz-labs)) |
| "Muchos lo usaban para no depender de Adobe y hoy buscan pago único" | **Dudoso** | La emoción es real, pero la conducta observada es quedarse en la versión congelada o irse a DxO, Lightroom u ON1. Topaz ya estaba en Photoshop desde octubre de 2025 ([Adobe MAX](https://news.adobe.com/news/downloads/pdfs/2025/10/102825-creative-cloud.pdf)). La única fuente del "para evitar Adobe" es un blog de opinión |
| "Reducir ruido es la razón principal por la que se compra Topaz" | **Dudoso** | La comunidad recomienda DxO para el ruido; donde Topaz sigue sin rival de pago único es la ampliación ([Finding the Universe](https://www.findingtheuniverse.com/best-noise-reduction-software/)) |
| Licencias: SCUNet Apache 2.0, NAFNet MIT, Real-ESRGAN BSD-3, SwinIR Apache 2.0 | **Cierto** | Verificado en los LICENSE de cada repositorio ([SCUNet](https://github.com/cszn/SCUNet/blob/main/LICENSE); [NAFNet](https://github.com/megvii-research/NAFNet); [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN/blob/master/LICENSE); [SwinIR](https://github.com/JingyunLiang/SwinIR)) |
| "Con esos cuatro se cubre la v1.0 sin entrenar nada" | **Dudoso** | El código es libre, pero los pesos se entrenaron con datos de uso académico o con términos poco claros. SwinIR no tiene ninguna conversión pública a Core ML. Y en RAW los cuatro van por detrás de DxO |
| "SCUNet como modelo principal de ruido" | **Dudoso** | Un proyecto lo abandonó por lento y por agotar la memoria (más de 2 s por bloque) ([Lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)); ver la sección de conflictos |
| "La mayoría de modelos de OpenModelDB son CC-BY-NC-SA" | **Exagerado** | De 671 modelos, 227 son CC-BY-NC-SA (34%) y, sumando los CC-BY-NC, el 42% son no comerciales. Hay unos 120 CC-BY-4.0 y 44 CC0 utilizables ([OpenModelDB](https://github.com/OpenModelDB/open-model-database)). Que hay que evitar 4x-UltraSharp y Remacri sí es correcto |
| "CodeFormer y los pesos de RIFE son no comerciales" | **Sin verificar** | Las notas tratan CodeFormer como no comercial y lo excluyen, pero no citan su LICENSE. RIFE no se revisó |
| "Corren en el Neural Engine; si no, Core ML pasa a la GPU automáticamente" | **Dudoso** | El paso a la GPU es automático, pero Real-ESRGAN (incluido el x4v3) **nunca** corre en el ANE con `.all` según un port público ([gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)). En FP16, LayerNorm puede dar NaN en el ANE ([ax Inc.](https://medium.com/axinc-ai/using-mixed-precision-in-core-ml-77c2428ba728)) |
| "Dividir en bloques evita que una foto de 45 MP agote la memoria" | **Parcialmente cierto** | Resuelve la entrada, pero 4x de 24 MP son 384 MP de salida (unos 2,3 GB en RGB de 16 bits) y 4x de 61 MP unos 5,9 GB. Hace falta escribir la salida en streaming |
| "Enfocar suave se logra casi gratis al combinar modelos" | **Parcialmente cierto** | La mezcla con el original es barata, es una mezcla posterior al modelo ([benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)). Igualar el Super Focus de Topaz exige otro modelo |
| "Sin RAW no lo toman en serio" | **Cierto pero insuficiente** | Para los profesionales, el RAW sin DNG lineal ni ida y vuelta con Lightroom se queda en "terminador de JPEG y TIFF" |
| "Conservar EXIF, GPS y perfil evita quejas" | **Cierto** | Es una queja recurrente. Hay que implementarlo con `CGImageDestinationAddImageAndMetadata`, no con `CopyImageSource`, que no reescribe los píxeles ([Apple QA1895](https://developer.apple.com/library/archive/qa/qa1895/_index.html)) |
| "10 a 12 semanas a medio tiempo" | **Falso para el plan tal como está** | El cálculo por componentes da 12–15 semanas para una v1 recortada y 18–22 para el plan completo |
| "Semana 9: licencias y pagos" | **Subestimado** | Paddle Billing marcó como obsoleta la generación de claves de licencia ([Paddle](https://developer.paddle.com/migrate/learn/feature-comparison.md)); hay que montar o contratar la activación |
| "Paddle cobra cerca de 5% + $0.50 y maneja impuestos" | **Cierto** (fuentes de terceros) | ([Spendflo](https://spendflo.com/vendors/paddle)) |
| "MAS: 15% con el Small Business Program, obliga sandbox, no maneja bien las actualizaciones pagadas" | **Cierto con matiz** | El 15% aplica por debajo de $1M ([Apple SBP](https://developer.apple.com/app-store/small-business-program/)). Las actualizaciones de pago se pueden imitar con una compra no consumible más una suscripción, como hace la propia Pixelmator Pro ([TidBITS](https://tidbits.com/?p=72934)) |
| "MAS útil como escaparate" | **Dudoso** | Apple Ads aparentemente no crea campañas para apps de Mac ([Apple Developer Forums](https://developer.apple.com/forums/thread/806737)) |
| "Netos de $55.55, $36.55 y $50.15 (MAS)" | **Cierto solo en EE.UU.** | En la UE el IVA va incluido. €59 en España dejan unos €45; el MAS en España, unos €42 ([9to5Mac](https://9to5mac.com/2023/03/09/apple-app-store-price-points-purchases/)). El neto medio realista está en $45–48 |
| "Con unas 16 ventas se cubren los costos" | **Cierto** | $600–$850 entre $45–55 por venta dan 11–19 ventas |
| "Escenarios de 100, 500 y 1.000 ventas" | **Dudoso en lo alto** | 1.000 ventas al año exigen unos 100.000 visitantes a la web ([Successful Software](https://successfulsoftware.net/2009/04/08/average-visitor-conversion-ratio/)); lo realista para un desarrollador sin audiencia son 150–400 |
| "Licencia para 2 Macs" | **Mejorable** | Aiarty da 3, y el MAS no pone límite de Macs con el mismo Apple ID ([Aiarty](https://www.aiarty.com/store.htm)) |
| "$39 de lanzamiento el primer mes" | **Dudoso** | Un 34% de descuento es mucho para la categoría y suena a app barata; además se suma a las comisiones de afiliados |
| "Piratería: riesgo bajo" | **Cierto en impacto, falso en volumen** | Un desarrollador de Mac contó unas 23 copias piratas por venta (dato de 2015) ([Tunabelly](https://tunabellysoftware.com/blog/files/our-apps-are-being-pirated.html)), pero quien piratea rara vez compra. La estrategia de no invertir en DRM es correcta |
| "El riesgo principal es la calidad frente a Topaz" | **Incompleto** | Los riesgos reales son otros: un precio igual o mayor que Pixelmator y ON1 con calidad por debajo de DxO, la velocidad en un M1 base y el RAW 9 gratuito de Apple |

## Diez desacuerdos entre las notas, resueltos

Las notas de investigación no siempre coinciden. Estos son los choques que cambian decisiones, con la resolución que se adopta en el plan corregido.

| # | Tema | Una nota dice | Otra nota dice | Resolución |
|---|---|---|---|---|
| 1 | **Reductor de ruido principal** | Modelos: SCUNet sigue siendo el principal. Tiene la procedencia de datos más limpia (ruido sintético, sin pares SIDD) y un proyecto lo prefirió por calidad en ruido de cámara ([SCUNet](https://github.com/cszn/SCUNet); [Lumen PR #55](https://github.com/AngeloP46/lumen/pull/55)) | Técnica: SCUNet tarda más de 2 s por bloque y se queda sin memoria en un iPhone 17 Pro Max. NAFNet-SIDD-w32, todo convoluciones y apto para el ANE, cuesta aproximadamente un cuarto ([Lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)) | **Probar NAFNet primero como motor de lote, y SCUNet como modo "Alta calidad" con tiempo acotado.** Las dos evidencias salen del mismo proyecto de un solo desarrollador y en iPhone, no en Mac, así que deciden los números de la semana 1. Regla: SCUNet entra solo si en un M3/M4 queda a ≤2x el tiempo de NAFNet y gana en la prueba a ciegas. Como NAFNet-SIDD está entrenado con ruido de smartphone y SIDD tiene licencia sin verificar, en la v1.1 conviene reentrenar NAFNet con el pipeline sintético de SCUNet: eso suma la velocidad de uno y la procedencia limpia del otro |
| 2 | **Ampliación de alta calidad** | Plan: SwinIR | Modelos: sustituirlo por los modelos fotográficos CC-BY-4.0 de Phhofm (RealPLKSR o DAT2). Técnica: SwinIR no tiene ninguna conversión pública a Core ML y es el más arriesgado | **Descartar SwinIR.** El candidato es **RealPLKSR** (convolucional) y no DAT2, porque DAT2 es un transformer con el mismo riesgo de conversión que SwinIR. Para la v1.5, ajuste fino propio sobre el preentrenado CC0 de RealPLKSR |
| 3 | **DNG lineal en la v1.0** | Competencia y fotógrafos: probablemente debe ir en la v1.0, porque es el mayor hueco de flujo para profesionales | Técnica: cuesta unas 2 semanas con el DNG SDK y no cabe en 10–12. Además, un DNG lineal que sale de un denoise en RGB ya pasó por el demosaico de Apple | **Pasa a la v1.5**, junto con el plugin de Lightroom, como un paquete "flujo pro". La v1.0 se posiciona hacia quien no lo necesita (JPEG/HEIC, recortes, eventos con exportación final). Si la beta pide DNG de forma masiva, se adelanta |
| 4 | **Precio** | Competencia: $59 no tiene ventaja de precio; quizá $29–39 o un posicionamiento más estrecho | Monetización: $59 está bien situado; probar $69–79 más adelante. Fotógrafos: $39 suena barato | **Mantener $59 / €59.** El problema es la diferenciación, no el precio. Bajar a $29–39 confunde la app con las de la Mac App Store de 1,7 estrellas |
| 5 | **Lanzamiento con descuento** | Plan: $39 el primer mes | Monetización: entre $45 y $49, o $39 solo para la lista de espera | **$45–49 en el lanzamiento público y $39 solo para la lista de espera y los beta testers** |
| 6 | **¿Tiene prueba Topaz?** | Monetización: "no ofrecemos prueba de Topaz Studio Desktop Collection", con 48 h de reembolso ([Topaz community](https://community.topazlabs.com/t/topaz-studio-transition-questions/95039?page=26)) | UX: según la documentación de Topaz, "las pruebas no tienen límite de tiempo", con marca de agua y 30 días de reembolso ([Topaz docs](https://docs.topazlabs.com/sales-account-licensing/before-you-buy/trial)) | **Sin resolver.** Probablemente difiere entre la colección Studio y las apps sueltas. No usar "Topaz no tiene prueba" en marketing hasta comprobarlo |
| 7 | **Objetivo de velocidad** | Fotógrafos: 5–15 s por imagen de 24–45 MP para competir | Técnica: "sí" con ≤30–45 s por imagen de 24 MP en un M1 de 8 GB | **Dos umbrales**: un mínimo viable en el M1 base y un umbral competitivo en un M3/M4 (ver la prueba de las semanas 1–2) |
| 8 | **Diseño de la prueba gratis** | Plan: todas las funciones, exporta con marca de agua. Monetización: marca de agua discreta, lote de prueba de 10 imágenes y 7 días opcionales | UX: vista previa ilimitada sin marca, N exportaciones limpias y luego marca en una esquina | **Híbrido de la nota de UX**: vista previa sin marca siempre, 20 exportaciones a resolución completa sin marca, luego marca pequeña en la esquina, y 30 días de reembolso |
| 9 | **Calendario de lanzamiento** | UX: lanzar en Black Friday 2026 (27 de noviembre) a $39 | Técnica: la v1 no estará antes de enero o febrero de 2027 | **Black Friday 2026 sirve para la lista de espera y una preventa "fundador"**, no para el lanzamiento |
| 10 | **Comisión de afiliados** | Monetización: 25–30% | UX: 30–40% | **30% de base**, frente al 20% de Topaz y Skylum ([Topaz affiliates](https://topazlabs.com/affiliates)) |

Hay otros desacuerdos menores. Las notas difieren en si Adobe publicó el precio de la compra: la nota de prensa no lo dio, pero el 10-Q lo recogería. También en si Upscayl está en la Mac App Store, y lo está ([App Store](https://apps.apple.com/us/app/upscayl/id6468265473?mt=12)). Y los precios de Luminar y Aiarty varían entre fuentes. Nada de eso cambia el plan.

## Los pesos son legales en código y grises en datos

El plan acierta en lo que lee: los cuatro modelos tienen licencias permisivas de código.

- **SCUNet** es Apache-2.0, con la nota "Copyright 2022 Kai Zhang" ([LICENSE](https://github.com/cszn/SCUNet/blob/main/LICENSE)).
- **NAFNet** es MIT ([repo](https://github.com/megvii-research/NAFNet)).
- **Real-ESRGAN** es BSD-3-Clause. Su cláusula 2 obliga a reproducir el aviso en la documentación de cualquier binario, y su cláusula 3 prohíbe usar los nombres de los autores para promocionar el producto ([LICENSE](https://github.com/xinntao/Real-ESRGAN/blob/master/LICENSE)).
- **SwinIR** es Apache-2.0 ([repo](https://github.com/JingyunLiang/SwinIR)).

Ninguno de estos repositorios tiene una licencia aparte para los pesos. La convención, que OpenModelDB recoge, es que los pesos heredan la licencia del repositorio, pero ningún autor lo dice expresamente. **Un correo corto a cada autor pidiendo confirmación del uso comercial es un seguro barato.**

El riesgo real está en **los datos de entrenamiento**. Real-ESRGAN se entrenó con DIV2K, Flickr2K y OST ([Training.md](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/Training.md)). SwinIR usa DIV2K, Flickr2K y OST para ampliación, y SIDD y RENOIR para ruido ([README](https://github.com/JingyunLiang/SwinIR)). NAFNet-SIDD se entrenó con SIDD. La página de DIV2K dice que es solo para investigación académica y que el copyright es de los dueños originales; ojo, este dato viene de un resumen de búsqueda ([DIV2K](https://data.vision.ee.ethz.ch/cvl/DIV2K/)). Para Flickr2K no se encontró licencia explícita, y LSDIR es "solo para investigación académica" ([arXiv 2603.06738](https://arxiv.org/pdf/2603.06738)). La licencia de SIDD no se pudo leer. Un estudio académico concluye que usar un dataset no comercial con fines comerciales es una violación ([arXiv 2111.02374](https://arxiv.org/pdf/2111.02374)), pero no hay ningún fallo judicial sobre si los pesos heredan esa restricción ([Keras #13362](https://github.com/keras-team/keras/issues/13362)). Algunos datasets sí atan a los modelos de forma explícita. Los términos del dataset completo de Unsplash dicen que los modelos entrenados con él "no deben usarse con fines comerciales" ([Unsplash TERMS](https://github.com/unsplash/datasets/blob/master/TERMS.md)).

Como **casi todo el ecosistema abierto** de ampliación y denoise se entrenó con estos datos, el riesgo es sistémico: elegir otro modelo público no lo resuelve. Esta es una lectura razonada, no un consejo legal:

| Nivel de riesgo | Qué cae aquí |
|---|---|
| **Bajo** | Pesos entrenados con datos sintéticos, propios o CC0 |
| **Bajo-moderado** | Pesos Apache, MIT o BSD entrenados con DIV2K o LSDIR. Esos datasets tienen avisos de "solo investigación" sin cláusula sobre modelos, la práctica es universal y los pesos no reproducen las imágenes |
| **Alto** | Datos cuyos términos atan explícitamente a los modelos derivados |
| **Inaceptable** | Pesos con licencia no comercial |

La única mitigación completa es entrenar pesos propios. SCUNet ya demuestra que el ruido sintético sobre imágenes limpias funciona ([SCUNet](https://github.com/cszn/SCUNet)). Y ELD muestra que, en RAW, el entrenamiento sintético con un modelo físico de ruido "puede competir o incluso superar" a los pares reales ([ELD](https://github.com/Vandermode/ELD)). La restricción real es conseguir imágenes limpias con licencia comercial: fotos propias y de los beta testers con cesión por escrito, stock con cláusula de entrenamiento, o Wikimedia/Openverse filtrado a CC0. Unsplash Lite es ambiguo, porque solo permite entrenar "para fines internos de negocio" y exige indemnizar a Unsplash ([Unsplash TERMS](https://github.com/unsplash/datasets/blob/master/TERMS.md)). La nota de modelos estima entre 25 y 150 horas de GPU (entre $15 y $150 alquiladas) por un modelo compacto. **Esa cifra no tiene fuente y hay que comprobarla.**

**Lista corta para la v1.0, ya con los conflictos resueltos:**

| Tarea | Modelo | Licencia | Advertencia de datos | Estado |
|---|---|---|---|---|
| Ruido en RAW (macOS 27+) | Apple CIRAWFilter RAW 9 | API del sistema | Ninguna para el desarrollador | Opcional, según la versión del sistema |
| Ruido en sRGB, JPEG o HEIC (lote) | **NAFNet-SIDD-w32** | MIT | SIDD sin verificar; afinado para ruido de smartphone | Se prueba primero |
| Ruido "Alta calidad" | **SCUNet** | Apache-2.0 | Sintético; las imágenes de origen no se verificaron | Entra si pasa la prueba |
| Ruido ligero alternativo | 1xDeNoise_realplksr_otf (Phhofm) | CC-BY-4.0 | Dataset Nomos sin procedencia documentada | Candidato de reserva ([OpenModelDB](https://openmodeldb.info/models/1x-DeNoise-realplksr-otf)) |
| Ampliación rápida | **realesr-general-x4v3** | BSD-3 | DF2K + OST | Principal; 6 MB ([model zoo](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/model_zoo.md)) |
| Ampliación "Alta calidad" | **4xNomosWebPhoto_RealPLKSR** | CC-BY-4.0 | Nomos sin procedencia | Entra si convierte bien ([Phhofm](https://github.com/Phhofm/models/releases/tag/4xNomosWebPhoto_RealPLKSR)) |
| Enfoque suave | Mezcla posterior; NAFNet-GoPro con mezcla baja si sobra tiempo | MIT | Licencia de GoPro sin verificar | Mezcla en v1.0; modelo en v1.1 |
| Generativo (solo v2) | OSEDiff | Apache-2.0 + OpenRAIL++-M de SD2 | LSDIR y FFHQ (probablemente NC) | Fuera de la v1 ([OSEDiff](https://github.com/cswry/OSEDiff)) |
| Nunca | SUPIR, StableSR, InvSR, LED, CodeFormer, UltraSharp/Remacri | No comercial | — | Excluidos ([SUPIR](https://github.com/Fanghua-Yu/SUPIR/blob/master/LICENSE); [StableSR](https://github.com/IceClear/StableSR/blob/main/LICENSE.txt); [InvSR](https://github.com/zsyOAOA/InvSR/blob/master/LICENSE); [LED](https://github.com/Srameo/LED)) |

Los modelos CC-BY-4.0 piden tres cosas: crédito al autor, enlace a la licencia y una nota de que el modelo se modificó (convertido a Core ML y cuantizado a FP16). Las fichas de OpenModelDB tienen erratas, como "CC-BY-0.4" en lugar de CC-BY-4.0, y algunos pesos están alojados en Google Drive sin licencia. Por eso conviene guardar en `models/LICENSES/`, para cada peso que se incluya, el LICENSE original, una copia de la página de publicación y el SHA-256 del archivo. La pantalla de "Reconocimientos" que propone el plan cumple lo que exigen todas estas licencias si reproduce cada texto de licencia y cada línea de copyright ([OpenModelDB licenses](https://openmodeldb.info/docs/licenses)).

## RAW 9 de Apple regala la mitad del producto desde macOS 27

En la WWDC26, Apple presentó **RAW 9** en Core Image: "un modelo Core ML por bloques que combina demosaico con reducción de ruido para la mejor calidad… en el equipo usando el Apple Neural Engine". Llega con iOS, iPadOS, macOS y visionOS 27, y se activa a voluntad con `CIRAWFilter.decoderVersion = .version9` ([WWDC26, sesión 305](https://developer.apple.com/videos/play/wwdc2026/305/)). Detalles que importan:

- Admite "cientos" de cámaras de un total de 784, la lista crece con actualizaciones del sistema y las cámaras con DNG nativo funcionan automáticamente.
- `luminanceNoiseReductionAmount` sigue controlando la intensidad.
- `colorNoiseReductionAmount` no tiene efecto, porque el modelo ya se encarga del ruido de color, y `detailAmount` y `moireReductionAmount` no están soportados.
- Ejecuta el modelo "cientos de veces por imagen" y pide ajustar la memoria: `memoryLimit` entre 512 y 1024 MB y `cacheIntermediates` desactivado al exportar ([WWDC26-305](https://developer.apple.com/videos/play/wwdc2026/305/)).
- Apple no ha publicado cifras de calidad ni de velocidad, ni la lista exacta de cámaras.

Para la app, esto tiene tres efectos a la vez.

**Primero, sube el suelo de la competencia.** Cualquier app que llame a `CIRAWFilter` con `.version9` obtiene reducción de ruido RAW con IA gratis, así que "limpio tu RAW" deja de diferenciar para quien tenga macOS 27.

**Segundo, es el mejor componente disponible.** Es gratis, corre en el Neural Engine, **no arrastra el riesgo de los datos de entrenamiento**, y hace justo lo que los modelos RGB del plan no pueden: limpiar antes o durante el demosaico. Así trabajan también DxO, con DeepPRIME en una sola pasada ([DxO](https://www.dxo.com/technology/deepprime-photolab/)), y Adobe, que entrena directamente sobre datos RAW ([Adobe](https://blog.adobe.com/en/publish/2023/04/18/denoise-demystified)). En NTIRE 2020 los denoisers rindieron mejor en espacio RAW que en sRGB ([NTIRE 2020](https://arxiv.org/pdf/2005.04117)).

**Tercero, no llega al plan tal como está**, porque el plan apunta a macOS 14 o superior. La app necesita su propia ruta para macOS 14 a 26 y para las cámaras que RAW 9 no soporte.

La consecuencia de producto es un cambio de papel. En RAW, la app deja de prometer "limpio tu RAW mejor que nadie" y pasa a ofrecer "**RAW 9 de Apple (o nuestro modelo) + nuestra ampliación + nuestro lote + exportación con metadatos**". La meta de calidad realista en RAW pasa a ser **"cerca de Lightroom"**, no "mejor que DxO". La prueba de la semana 2 tiene que comparar contra la salida de RAW 9, no solo contra Lightroom y Topaz. Si RAW 9 limpia los RAW tan bien como el modelo propio, el valor de la app queda en tres sitios: la ampliación, el ruido en JPEG/HEIC y el flujo de lote.

En paralelo, Apple presentó **Core AI** en macOS 27 como sucesor de Core ML. Core ML no queda obsoleto, según una cita de un laboratorio de la WWDC ([InfoQ](https://www.infoq.com/news/2026/06/apple-core-ai-wwdc/); [mlcommons #1188](https://github.com/mlcommons/mobile_app_open/issues/1188)). Un port de Real-ESRGAN sobre Core AI sí corre en el ANE, gasta entre 4,5 y 4,9 veces menos energía que la GPU y "no se frena por temperatura" ([xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)). Encaja como vía rápida opcional detrás de un protocolo de inferencia, no como el único backend. Esto abre una decisión pendiente: **subir el mínimo a macOS 15 o seguir en 14**. Ninguna nota tiene datos de adopción por versión de macOS entre fotógrafos.

## El cuello de botella real es el lote en un M1 de 8 GB

Convertir los modelos es factible, pero la suposición de que "correrán en el Neural Engine" es débil:

- **Real-ESRGAN.** Un port público de Core ML afirma que con `compute_units=ALL` nunca envía RRDBNet ni SRVGGNetCompact (la arquitectura del x4v3) al ANE, y que todo corre en la GPU ([gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)).
- **Formato y formas de entrada.** El formato ML Program cargó más de 10 veces más lento que el antiguo, y el mantenedor confirmó este orden de rendimiento: forma fija, luego formas enumeradas y por último formas flexibles ([coremltools #2545](https://github.com/apple/coremltools/issues/2545)).
- **Precisión.** En FP16, LayerNorm puede desbordarse a NaN en el ANE. El arreglo habitual es dejarla en FP32 con precisión mixta ([ax Inc.](https://medium.com/axinc-ai/using-mixed-precision-in-core-ml-77c2428ba728); [coremltools typed execution](https://apple.github.io/coremltools/docs-guides/source/typed-execution-example.html)).
- **SwinIR.** No existe ninguna evidencia pública de su conversión a Core ML.

Las cifras de rendimiento son pocas y casi todas de un solo desarrollador:

- En un M3 Ultra, el x4v3 tarda **0,03 s por bloque de 512 px**, y el x4plus 0,47 s ([gil](https://github.com/gil/real-esrgan-coreml)).
- Los bloques grandes reducen el error en las costuras: la diferencia máxima baja de 0,596 con bloques de 64 px a 0,075 con bloques de 512 px ([gil](https://github.com/gil/real-esrgan-coreml)).
- SCUNet en un iPhone 17 Pro Max pasa de 2 s por bloque, necesita 126 bloques para 24 MP (más de 4 minutos por foto) y el sistema mató la app por memoria ([Lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)).
- Una decodificación con CIRAWFilter añade unos 200 ms fijos ([esperyong/lightcraft PR #19](https://github.com/esperyong/lightcraft/pull/19)).

A partir de esos datos, la nota técnica estima lo siguiente. Son estimaciones aritméticas, no mediciones:

| Cálculo | 24 MP | 45 MP | 61 MP |
|---|---|---|---|
| Bloques de 512 px con 32 px de solape | 117 | 216 | 280 |
| x4v3 en un M3 Ultra | ~3,5 s | ~6,5 s | ~8,4 s |
| x4v3 en un M1 base (extrapolado, sin verificar) | 30–80 s según el tamaño | | |

Un lote de 1.000 fotos de boda a 30 s por foto son unas 8,3 horas. A 4 minutos por foto, que es el orden de SCUNet en hardware débil, son unas 67 horas. **La velocidad del lote en un M1 o M2 base es el riesgo central del producto.**

La memoria es el segundo problema. Los pesos ocupan pocos megas; lo que pesa son los búferes a resolución completa. 4x de 24 MP producen 384 MP, que son unos 2,3 GB en RGB de 16 bits. 4x de 61 MP producen unos 976 MP, cerca de 5,9 GB, inviable en 8 GB y por encima del límite de 4 GB del TIFF clásico. La salida tiene que escribirse en streaming, por franjas, o hay que limitar la escala a 2x por encima de 40 MP en equipos de 8 GB.

En RAW, `CIRAWFilter` entrega RGB lineal ya demosaicado, y la app "nunca ve el mosaico" ([benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)). Antes de RAW 9, hay que poner la reducción de ruido del propio filtro a cero para no limpiar dos veces. Y hay que convertir al espacio con gamma antes de entrar al modelo, porque los modelos se entrenaron con sRGB. ImageIO no escribe DNG, así que un DNG lineal exige el DNG SDK de Adobe. Su licencia es gratuita y permite el uso comercial, con dos condiciones: mantener los avisos e incluir "This product includes DNG technology under license by Adobe" ([Adobe DNG SDK](https://www.adobe.com/support/downloads/dng/dng_sdk_eula_win.html)).

En metadatos, `CGImageDestinationCopyImageSource` copia los píxeles de origen sin cambiarlos ([Apple QA1895](https://developer.apple.com/library/archive/qa/qa1895/_index.html)), además de un bug publicado que trunca valores EXIF decimales, por ejemplo f/2.8 que pasa a 2 ([Apple Forums](https://developer.apple.com/forums/thread/705980)). Hay que usar `AddImageAndMetadata` y escribir una prueba de ida y vuelta.

Los modelos caben de sobra en la app: entre 100 y 150 MB en FP16 en total. El x4v3 pesa 6 MB ([gil](https://github.com/gil/real-esrgan-coreml)). Más adelante, Background Assets permite actualizar modelos desde Apple, aunque solo en la App Store y TestFlight ([WWDC25-325](https://developer.apple.com/videos/play/wwdc2025/325/)).

| Componente | Viabilidad | Enfoque | Riesgo principal | Semanas a medio tiempo |
|---|---|---|---|---|
| Conversión de modelos | Alta (x4v3, NAFNet); media (SCUNet); baja-media (SwinIR) | mlprogram, bloque fijo de 512 + relleno, FP16 con LayerNorm y softmax en FP32 | Que no corra en el ANE, NaN, SCUNet lento | 2–3 |
| Motor de inferencia + bloques | Alta | GPU por defecto, ANE donde el compute plan lo confirme, mezcla con pesos en float32 | Memoria en 4x | 2–3 |
| Entrada RAW (ruta RGB) | Alta | CIRAWFilter → RGB de 16 bits con su NR apagada; RAW 9 opcional | Retraso en cámaras nuevas; calidad frente a RAW 9 | 1 |
| Salida DNG lineal | Media | DNG SDK (C++) LinearRaw | Que la metadata de color sea correcta | 2 (se aplaza) |
| Exportación + metadatos + ICC | Alta | AddImageAndMetadata; salida en streaming | Bug de EXIF; TIFF de más de 4 GB | 1 |
| Interfaz SwiftUI + antes/después | Alta | Vista previa por bloques bajo demanda | Latencia de la vista previa | 2 |
| Cola de lote | Alta | Decodificar, inferir y codificar en paralelo; registro de trabajos reanudable | Rendimiento, temperatura | 1 |
| "Edit In" de Lightroom | Alta | Documentar + guardar en el mismo archivo | Acceso a archivos con sandbox | 0,5 |
| Plugin del SDK de Lightroom | Media | Plugin Lua + CLI | Documentación pobre del SDK | 1–2 (se aplaza) |
| Licencias (Paddle) | Media | Archivos de licencia firmados + activación mínima | Paddle no genera claves | 1 |
| Versión para el MAS | Media | Sandbox + bookmarks | Flujos con Lightroom; actualizaciones de pago | 1 (se aplaza) |
| Beta, notarización, web | Alta | Developer ID + Sparkle | — | 2–3 |

La suma de la v1 recortada da **12–15 semanas a medio tiempo**. El plan completo, con DNG, plugin de Lightroom, versión para el MAS y SCUNet/SwinIR, da **18–22**. Ningún dato dice cuántas horas reales hay detrás de "medio tiempo", y eso mueve todo el cálculo. Contando desde finales de octubre de 2026, la v1.0 pública cae de forma realista entre **finales de enero y febrero de 2027**.

## $59 aguanta, pero el neto real ronda $45–48

El precio de lista se sostiene. Equivale a menos de cuatro meses de Topaz Photo a $39/mes, a menos de un tercio de un año de Topaz a $199, a la mitad de PureRAW o Luminar, y está $9 por encima de Pixelmator Pro ([Renderahouse](https://www.renderahouse.com/blog/topaz-ai-pricing); [Macworld](https://www.macworld.com/article/3031215)). Por encima o por debajo hay problemas. Bajar a $49 invita a la pregunta "¿por qué no Pixelmator Pro?". Subir a $99 mete la app en la zona de PureRAW en oferta sin tener su marca. $69–79 se puede probar más adelante si las pruebas a ciegas acercan la calidad a DxO. No hay datos de elasticidad de precio: todo esto sale del sentimiento en foros.

**El neto medio.** El neto de $55.55 que calcula el plan solo vale en EE.UU., donde el impuesto se suma aparte. En la UE el IVA va incluido: €59 en España dejan unos **€45** después de Paddle, y la Mac App Store en España, a €59.99, unos **€42**, porque Apple incluye impuestos en todos los países excepto EE.UU. y Canadá ([9to5Mac](https://9to5mac.com/2023/03/09/apple-app-store-price-points-purchases/)). Si se mezclan lanzamientos con descuento, ventas en la UE y Latinoamérica y un 15% de ventas por afiliados al 30%, el neto ronda **$45–48**. Con eso, los escenarios del plan quedan así:

| Ventas | Neto anual |
|---|---|
| 100 | ~$4.6k |
| 500 | ~$23k |
| 1.000 | ~$46k |

Ese modelo es del investigador, no un dato publicado.

Paddle permite fijar precios por país, y cada país puede tener su propio precio por encima de la conversión automática ([Paddle](https://developer.paddle.com/build/products/offer-localized-pricing/)). Así se pueden poner €59–65 con IVA en la zona euro y unos $39–45 en México, Colombia, Argentina y Chile. No se verificó qué monedas latinoamericanas soporta Paddle, ni si su comisión se calcula sobre el total con impuestos.

**El pase de actualizaciones** es un modelo con precedentes:

- **Panic Nova** cuesta $99 con el primer año incluido y después $49 al año; si no se renueva, el usuario conserva su última versión "para siempre" ([Panic](https://help.panic.com/nova/purchase-faq)).
- **Sketch** renueva a $120 al año con un esquema parecido ([Sketch](https://sketch.com/license)).

El riesgo es el recuerdo de Topaz, cuyas renovaciones fueron subiendo hasta que abandonó el modelo. Conviene reformularlo de forma simple: **"Licencia de $59 con 12 meses de novedades incluidos; después, $29/año opcional. Lo que ya tienes es tuyo para siempre."** Y comprometerse en público a dos cosas: un precio máximo para clientes existentes, y no cobrar nunca por arreglos de errores, compatibilidad con macOS ni cámaras nuevas dentro de la 1.x. No hay tasas públicas de renovación de ningún producto. El 15–30% que usa la nota de monetización es una suposición.

**Paddle.** Sigue siendo la opción por defecto: actúa como merchant of record, cobra 5% + $0.50 y gestiona los impuestos. Pero **Paddle Billing ya no genera claves de licencia** ([Paddle](https://developer.paddle.com/migrate/learn/feature-comparison.md)). Hay que añadir un servicio de licencias, con dos opciones:

- **Contratarlo.** Cryptlex publica un servidor de webhooks para Paddle Billing ([Cryptlex](https://mintlify.com/cryptlex/third-party-integrations/integrations/paddle)). Keygen tiene un nivel gratuito para desarrollo y planes de $49 a $399 al mes según Capterra ([Capterra](https://www.capterra.com/p/168916/Keygen/pricing/)).
- **Hacerlo propio.** Un archivo de licencia firmado con Ed25519 y una única activación por Mac.

Las alternativas a Paddle tienen problemas. Lemon Squeezy está migrando hacia Stripe Managed Payments y conviene evitarlo para un lanzamiento. Stripe Managed Payments cuesta unos 6,4% + 30¢ y no trae claves ni entrega de descargas.

**La Mac App Store** puede vender lo mismo: una app gratis con marca de agua, una compra no consumible para la licencia completa y una suscripción anual para las novedades. Es justo el patrón de Pixelmator Pro ([TidBITS](https://tidbits.com/?p=72934)). Pero las reglas imponen cuatro condiciones ([App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)):

- prohíben pedir claves de licencia o mostrar una pantalla de licencia al arrancar (2.4.5);
- exigen distribuir las actualizaciones por la tienda;
- si una función se vende en la web, debe ofrecerse también como compra dentro de la app (3.1.3(b));
- cualquier suscripción debe aportar "valor continuo" (3.1.2(a)).

Hay que recordar también que Apple Ads no promociona apps de Mac ([Apple Developer Forums](https://developer.apple.com/forums/thread/806737)). La recomendación es lanzar primero en venta directa y añadir la versión para el MAS entre 3 y 6 meses después, al mismo precio ($59.99). El Small Business Program hay que solicitarlo antes de ese lanzamiento ([Apple SBP](https://developer.apple.com/app-store/small-business-program/)).

**Setapp** paga el 70% de las cuotas de sus miembros, repartido según las apps que cada uno usa ([Setapp](https://docs.setapp.com/docs/distributing-revenue)). Un miembro de Setapp espera recibir todas las novedades incluidas, lo que vacía el sentido del pase. Mejor después de la v2. **Los bundles** salen por céntimos por app: el de BundleHunt de Black Friday 2025 vendía 37 apps por unos $16.70 ([Macwelt](https://www.macwelt.de/article/2966131/bundlehunt-black-friday-2025-37-mac-apps-fur-167-statt-1439-us-dollar.html)). No conviene usarlos en el primer año.

**Lo que hace falta para llegar a esas ventas.** La única serie amplia de datos de escritorio, de 2009 y con 92 vendedores, da una media del 4,5% de descargas que acaban en venta y un 1% de visitas que compran ([Successful Software](https://successfulsoftware.net/2009/04/08/average-visitor-conversion-ratio/)). Con esos ratios:

| Ventas al año | Visitas a la web | Visitas al día |
|---|---|---|
| 100 | ~10.000 | ~27 |
| 500 | ~50.000 | ~137 |
| 1.000 | ~100.000 | ~274 |

El rango realista para el primer año, sin audiencia previa, es de **150–400 ventas**.

## La confianza se gana con una lupa al 100% en menos de dos segundos

La queja de UX mejor documentada contra Topaz es doble. El Autopilot procesa de más y malinterpreta la intención del usuario: sugiere ampliar cuando solo se quería quitar ruido ([CaptureLandscapes](https://www.capturelandscapes.com/topaz-photo-ai/)). Y la vista previa se reconstruye tras cada ajuste, con 5 a 10 segundos de espera cada vez. Este último dato viene de un resumen de búsqueda. En el otro lado, los revisores valoran poder comparar intensidades antes de aplicar y critican que Lightroom no lo permita ([PhotoWorkout](https://www.photoworkout.com/best-noise-reduction-software/)).

De ahí sale la lista de UX, ordenada por cuánta confianza genera:

1. **Una "lupa" al 100%** que procesa solo los bloques visibles y se actualiza en **menos de 1–2 s** al soltar el deslizador, con la estimación "Imagen completa: ~X s" al lado. Encaja directamente con la arquitectura por bloques.
2. **Vista dividida arrastrable**, lado a lado con zoom sincronizado, y una tecla para ver el original. Además, zoom al 200% y al 400%, y comparar la ampliación contra un bicúbico al mismo tamaño.
3. **No sobrescribir nunca el original**. Sufijos `-clean`, `-2x` y `-4x`, una plantilla de nombres configurable y un botón "Mostrar en Finder".
4. **Un deslizador por operación**, con valores por defecto con nombre ("Recomendado", "Suave", "Fuerte") y **sin Autopilot**. El mensaje sería "sin IA que adivine, tú decides".
5. **Tiempos estimados honestos**, notificación al terminar y la opción de mantener la Mac despierta.
6. **Cola de lote** con ajustes propios por foto, reanudable tras cerrar la app o un cuelgue.
7. **Presets** ("Recepción ISO 6400", "Recorte deportes 2x").
8. **Una línea visible "EXIF, GPS y perfil de color conservados"** en la exportación.
9. **Límites dichos por adelantado** antes de un lote de 40 minutos en un M1.

Todo esto es una recomendación del investigador, no algo medido con usuarios.

Las integraciones, ordenadas por valor frente a esfuerzo:

1. **Arrastrar y soltar** desde Finder y Fotos.
2. **"Additional External Editor" de Lightroom Classic.** No requiere SDK: Lightroom genera un TIFF, la app lo abre y guarda encima ([Lightroom Queen](https://www.lightroomqueen.com/add-external-editor/)).
3. **Acción rápida de Finder y App Intents.**
4. **Carpeta vigilada.**
5. **Plugin Lua de Lightroom** para enviar el RAW y recibir un DNG apilado con el original, como hace DxO ([Digital Camera World](https://digitalcameraworld.com/news/dxo-launches-pureraw-2-with-lightroom-classic-integration-and-x-trans-support)).
6. **Extensión de Fotos y plugin de Photoshop**, para la v2.

El "Edit In" es la integración profesional más barata, aunque no limpia en la fase RAW, y cuesta días, no semanas.

**La prueba gratis.** La categoría está dividida: ON1 da 30 días completos sin marca de agua ([ON1](https://www.on1.com/free-photo-editor-trial/)), DxO da 14 días con lote limitado ([DxO](https://support.dxo.com/hc/en-us/articles/4437215152401-I-tried-a-DxO-PureRAW-demo-and-it-has-expired-Can-I-extend-the-trial-period)) y en Topaz hay un hilo titulado "la marca de agua es tan grande que no veo la diferencia de calidad" ([Topaz community](https://community.topazlabs.com/t/the-watermark-is-so-huge-i-cant-see-the-quality-difference/42203)). La opción elegida en la tabla de conflictos (sección "Diez desacuerdos") es la que más sentido tiene: **vista previa sin marca siempre, 20 exportaciones a resolución completa sin marca, después una marca pequeña en una esquina y 30 días de reembolso**. Veinte exportaciones alcanzan para validar un trabajo real.

**El lanzamiento** se construye alrededor de creadores, no de anuncios. Lo primero es dar licencias gratuitas a 10–20 educadores de YouTube y blogueros que ya hayan hecho vídeos de "alternativas a Topaz", con un 30% de afiliación, un paquete de RAW "de tortura" y material de la vista dividida. Lo segundo, publicar una **página y un vídeo de comparación honestos**: la app frente a Topaz, Lightroom, DxO y RAW 9 sobre los mismos 10 RAW, con los archivos descargables y admitiendo dónde pierde. Las búsquedas de "topaz alternative" están dominadas por listados de los propios fabricantes, con datos contradictorios entre sí, así que una comparación precisa y mantenida destaca ([Aiarty](https://www.aiarty.com/ai-image-enhancer/topaz-labs-alternative.htm)).

Después vienen la prensa y las comunidades:

- **Prensa fotográfica**, con el gancho "alternativa indie de pago único tras el cierre de la compra de Topaz". DPReview, Fstoppers, PetaPixel y Creative Bloq ya tienen abierto ese hilo editorial ([Creative Bloq](https://www.creativebloq.com/design/design-software/what-does-adobes-topaz-labs-acquisition-mean-for-creatives)).
- **Prensa Mac**, con el gancho "nativa, Neural Engine, Shortcuts".
- **Reddit y foros**, participando como un usuario más y declarando ser el desarrollador.

Un cupón **"vienes de Topaz"** tiene precedente directo: en 2006, cuando Adobe compró RawShooter, Bibble ofreció a sus clientes una actualización competitiva ([Imaging Resource](https://Imaging-Resource.Com/NEWS/1151435749.html)). Las páginas SEO tendrían versión en inglés y en español, por ejemplo `/es/alternativa-a-topaz`. **Localizar la app y la web al español desde la v1.0** es barato y aprovecha que hay muy poco contenido nativo. La beta debe ser directa, con DMG y Sparkle, porque es la versión que se va a vender. Hay que reclutar unas 3 veces los 30–50 testers activos que se buscan, y en el formulario de la lista de espera pedir cámara, chip y RAM, editor que usan y un enlace a sus "peores RAW".

## Plan MVP corregido: menos frentes y mejor lote

**Promesa revisada:** "Limpia y amplía tus fotos —RAW, JPEG o HEIC— en lote, en tu Mac, con aspecto natural y sin suscripción." **Público principal de la v1.0:** fotógrafos de eventos y aficionados avanzados que necesitan limpiar exportaciones finales, JPEG de cámara y fotos de móvil, y ampliar recortes. Los profesionales de bodas con flujo RAW → DNG en Lightroom son el público de la v1.5.

| Elemento | Decisión | Motivo |
|---|---|---|
| Ruido sRGB/JPEG/HEIC con NAFNet-w32 y deslizador | **v1.0** | Lightroom no acepta esos formatos; es lo más rápido y apto para el ANE |
| SCUNet como "Alta calidad" | **v1.0 solo si pasa la prueba**; si no, v1.1 | Calidad frente a velocidad (conflicto 1) |
| Ampliar 2x/4x con x4v3 (rápido) | **v1.0** | 6 MB, rápido en la GPU, ya existe un port |
| Ampliación "Alta calidad" con RealPLKSR (CC-BY-4.0) | **v1.0 si convierte en ≤2 días**; si no, v1.1 | Sustituye a SwinIR |
| Enfoque suave como mezcla con el original | **v1.0** | Coste casi nulo |
| Modelo de enfoque y desenfoque (NAFNet-GoPro) | v1.1 | Demanda baja-media; riesgo de prometer de más |
| RAW con CIRAWFilter (NR del filtro a 0) → modelo → TIFF16 | **v1.0** | "Sin RAW no lo toman en serio" |
| Ruta RAW 9 en macOS 27 (opcional) | **v1.0** | Gratis, sin riesgo de datos, mejor calidad RAW |
| Salida JPEG, TIFF16 y PNG con EXIF, GPS, IPTC e ICC (AddImageAndMetadata) | **v1.0** | Queja recurrente; bug de CopyImageSource |
| Salida en streaming y tope de 2x por encima de 40 MP en 8 GB | **v1.0** | Memoria |
| Lote en paralelo, reanudable, con ETA y presets | **v1.0** | Es el diferenciador central |
| Lupa al 100% en <2 s, vista dividida, no sobrescribir | **v1.0** | Confianza |
| Arrastrar y soltar + "Edit In" de Lightroom documentado | **v1.0** | Días de trabajo y alto valor para profesionales |
| Español e inglés | **v1.0** | Barato; poca competencia nativa |
| Pantalla de Reconocimientos + `models/LICENSES` con SHA-256 | **v1.0** | Lo exigen las licencias |
| Developer ID, notarización, Sparkle, Paddle + licencia firmada para 3 Macs | **v1.0** | Paddle no genera claves; 3 Macs como la competencia |
| Prueba: 20 exportaciones limpias, luego marca en esquina, 30 días de reembolso | **v1.0** | Conflicto 8 |
| Acción rápida de Finder / App Intents | v1.1 | Gancho para la prensa Mac; poco esfuerzo |
| Carpeta vigilada | v1.1 | Útil para eventos |
| Presets por cámara/ISO con "aplicar a similares" | v1.1–1.5 | Petición implícita ("pegar ajustes") |
| DNG lineal (DNG SDK) + plugin Lua de Lightroom | **v1.5** (antes si la beta lo exige) | Paquete "flujo pro"; conflicto 3 |
| Versión para el MAS (compra no consumible + suscripción) | 3–6 meses después del lanzamiento | Segunda versión con sandbox; sin Apple Ads |
| Backend Core AI (macOS 27) | v1.5 | Ahorro de energía y sin frenado térmico |
| Pesos propios entrenados con datos con licencia | v1.5 | Elimina el riesgo de datos y sirve de argumento de marketing |
| Denoiser propio en el dominio RAW (estilo PMRID/ELD) | v2 | El único camino para igualar a DxO ([PMRID](https://github.com/megvii-research/PMRID)) |
| Ampliación generativa (OSEDiff), extensión de Fotos, Photoshop, iPad, vídeo | v2 o más | Pesado, inventa detalle |
| Setapp | Después de la v2 | Choca con el pase |
| SwinIR | **Descartado** | Riesgo de conversión; superado |
| RRDBNet x4plus | **Descartado** | ~0,47 s por bloque incluso en un M3 Ultra |
| SUPIR, StableSR, InvSR, LED, CodeFormer, modelos CC-BY-NC | **Descartados** | No comerciales |
| Autopilot, DRM fuerte, Apple Ads, BundleHunt en el primer año | **Descartados** | Ver las secciones anteriores |
| Afirmación "mejor que Topaz" y "Topaz no tiene prueba" | **Descartadas** | Sin evidencia, o contradictorias |

**Decisiones abiertas.** Estas son las que el desarrollador tiene que tomar, con la recomendación y el momento para decidir.

| Decisión | Opciones | Recomendación | Cuándo |
|---|---|---|---|
| Público y mensaje de la v1.0 | Profesionales RAW contra eventos/JPEG/ampliación | Eventos, JPEG y ampliación primero; RAW "cerca de Lightroom" | Fin de la semana 2, con los datos de calidad |
| macOS mínimo | 14, 15 o 27 | 14 o 15 con ruta propia, más RAW 9 y Core AI como extras | Semana 2 |
| Denoiser por defecto | NAFNet o SCUNet | Según la regla del conflicto 1 | Semana 1 |
| Ampliador de alta calidad | RealPLKSR CC-BY o ajuste fino propio | CC-BY en la v1.0 y propio en la v1.5 | Semana 2 |
| Precio y lanzamiento | $59 / $69 y $39 / $45–49 | $59; $45–49 en público; $39 para la lista de espera | Antes de la beta |
| Estructura del pase | "1.x + pase" o "12 meses incluidos + $29/año" | 12 meses incluidos, con precio tope publicado | Antes de configurar Paddle |
| Licencias | Keygen, Cryptlex o Ed25519 propio | Ed25519 propio si sobra una semana; si no, Cryptlex | Semana 8–9 |
| Entrenar pesos propios | Sí / no; con qué datos | Sí para la v1.5, con fotos propias y de testers bajo cesión | Después del lanzamiento |
| Consulta legal sobre los datos de entrenamiento | Ninguna, correo a los autores o abogado | Correo a los autores ya; abogado antes de pasar de unas 500 ventas | Semana 1 (correos) |
| Horas reales por semana | — | Fijarlas; cambian todo el calendario | Ya |

## Prueba de las semanas 1–2: números antes que pantallas

El objetivo es responder tres preguntas antes de escribir interfaz: si la app es lo bastante rápida en un M1 de 8 GB, si el resultado es lo bastante bueno frente a lo que el usuario ya tiene, y si cabe en memoria. El orden de trabajo sale de la nota técnica.

**Días 1–2.** Convertir NAFNet-SIDD-w32 y realesr-general-x4v3 con mlprogram, bloque fijo de 512 + relleno y FP16 con LayerNorm en FP32. Registrar en qué unidad corre cada operación usando `MLComputePlan` y el informe de rendimiento de Xcode.

**Día 3.** Hacer lo mismo con SCUNet, limitado a un día. RealPLKSR solo si sobra tiempo.

**Días 4–5.** Construir una CLI en Swift con esta cadena: decodificar → bloques 512/32 → Core ML → mezcla en float32 → TIFF16 con metadatos. Medir con `.cpuAndNeuralEngine`, `.cpuAndGPU` y `.all`.

**Semana 2.** Prueba de calidad a ciegas con 5–10 fotógrafos sobre 20 fotos de ISO alto (RAW de al menos 4 marcas, Fuji X-Trans incluida) y 10 recortes. Se compara contra:

- Lightroom Denoise;
- la prueba de DxO PureRAW 6 (son 14 días, así que conviene activarla justo al empezar la semana 2);
- ON1 NoNoise 2027;
- Pixelmator Pro;
- Upscayl;
- RAW 9 en macOS 27;
- Topaz, si su prueba existe.

| Criterio | "Sí" (seguir) | "No" o acción |
|---|---|---|
| Paridad numérica Core ML vs PyTorch FP32 | ≥50 dB PSNR por bloque, sin NaN ni Inf ([benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)) | Si falla: precisión mixta o FP32 en la GPU; si sigue fallando, se descarta el modelo |
| Costuras y color | Nada visible al 100% en cielos y fondos lisos; desvío de color entre bloques imperceptible | Más solape (64 px) o cambiar de modelo |
| Velocidad del denoise en un M1 de 8 GB (mínimo viable) | ≤30–45 s por foto de 24 MP | Si pasa de 60 s: solo NAFNet y mensaje "para Macs M2 o superiores", o se para el proyecto |
| Velocidad del denoise en un M3/M4 (competitivo) | ≤10–15 s por foto de 24 MP | Si no: la promesa "en segundos" cae |
| Ampliación 4x con x4v3 | ≤90 s en un M1 y ≤15 s en un M3/M4 para 24 MP (umbral propuesto) | Si no: limitar a 2x por defecto |
| Memoria | Pico <3 GB en el denoise de 24 MP; 4x de 45 MP termina en 8 GB sin cuelgue gracias al streaming | Si no: tope de escala por RAM |
| Frenado térmico | 50 imágenes seguidas sin bajar más de un 25% de velocidad (umbral propuesto) | Si no: priorizar el ANE o el pipeline mixto |
| Calidad JPEG/HEIC | Igual o mejor que Pixelmator Pro en ≥50% de los votos a ciegas, y claramente mejor que no hacer nada | **Si pierde contra Pixelmator en JPEG y en ampliación, se para el proyecto o se replantea** |
| Calidad de ampliación | Preferida frente a Pixelmator Super Resolution y Upscayl en ≥60% de los votos | Si no: no hay producto diferenciado |
| Calidad RAW | "Cerca de Lightroom" en ≥50% de los RAW, y no peor que RAW 9 | Si RAW 9 gana: usar RAW 9 como ruta RAW y vender ampliación + lote |

Los umbrales marcados como "propuestos" son del investigador. Los demás salen de las notas técnicas y de los tiempos de la competencia. El resultado más probable es **intermedio**: velocidad aceptable y RAW por debajo de DxO. Eso no es un "no". Es la señal para fijar el posicionamiento corregido.

## Próximos pasos para empezar con Claude Code

| Paso | Cuándo | Resultado |
|---|---|---|
| Fijar las horas reales por semana y corregir el texto del "por qué ahora" (cierre del 23 de septiembre) | Hoy | Plan honesto |
| Conseguir una MacBook Air M1 de 8 GB (prestada o usada) y tener a mano una M3/M4; instalar macOS 27 en una de las dos | Semana 1 | Banco de pruebas real |
| Reunir 20 RAW de ISO alto de al menos 4 marcas, 10 recortes, 10 JPEG/HEIC de móvil y cielos lisos | Semana 1 | Conjunto de prueba |
| Escribir a los autores de NAFNet, Real-ESRGAN, SCUNet y Phhofm para confirmar el uso comercial de los pesos | Semana 1 | Riesgo de licencia mitigado |
| Crear el repositorio y pegar el texto de abajo en Claude Code, **en la Mac** (Core ML y Xcode no corren en Linux) | Semana 1 | Spike de conversión y medición |
| Activar las pruebas de PureRAW 6 y ON1 y comprar Pixelmator Pro o usar su mes de prueba en Creator Studio | Inicio de la semana 2 | Comparación justa |
| Prueba a ciegas con 5–10 fotógrafos y decisión de sí/no | Fin de la semana 2 | Decisión |
| Si es "sí": web con lista de espera (cámara, chip, editor, "peores RAW"), dominio, cuenta de Paddle, comprobar Google Trends para "topaz alternative" y "alternativa a topaz" | Semanas 2–3 | Medir el interés antes de construir la interfaz |
| Preventa "fundador" a $39 para la lista de espera en Black Friday (27 de noviembre de 2026) | Semana 5 | Validación con dinero real |

Texto listo para pegar en una sesión nueva de Claude Code, abierta en la Mac y en una carpeta vacía:

```text
Vamos a hacer la prueba técnica de 2 semanas de una app nativa de Mac (Swift) que reduce ruido y amplía fotos con IA en el equipo. Todavía NO quiero interfaz: solo conversión de modelos, pruebas de paridad y una CLI de medición. Estoy en una Mac con Apple Silicon y Xcode instalado; tengo además acceso a [M1 8 GB / M3-M4 / macOS 27: completar].

Estructura del repositorio:
- models/   Python (venv, Python 3.11, torch, coremltools estable actual). Scripts de descarga, conversión y paridad.
- models/LICENSES/<modelo>/  LICENSE original, URL de publicación, fecha de descarga y SHA-256 de cada peso.
- bench/    Paquete Swift (CLI `bench`) que usa los .mlpackage convertidos.
- results/  CSV y un resumen en Markdown.

Tareas, en este orden:
1. Descargar desde los repositorios OFICIALES y registrar licencia y SHA-256:
   NAFNet-SIDD-width32 (MIT, megvii-research/NAFNet) y realesr-general-x4v3 (BSD-3, xinntao/Real-ESRGAN).
   No usar ningún modelo con licencia no comercial (nada de CC-BY-NC, SUPIR, StableSR, InvSR, LED, CodeFormer, 4x-UltraSharp, Remacri).
2. Convertir ambos a Core ML (formato mlprogram) con entrada FIJA de 512x512 más el relleno que necesite cada modelo, en FP16, dejando LayerNorm, softmax y reducciones en FP32 con op_selector. En NAFNet, reescribir LayerNorm2d con operaciones simples para que se pueda trazar.
3. Prueba de paridad: comparar 20 bloques reales contra PyTorch FP32. Criterio: PSNR >= 50 dB y cero NaN/Inf, por separado para .cpuAndNeuralEngine, .cpuAndGPU y .all.
4. Volcar con MLComputePlan (o el informe de rendimiento de Xcode) en qué unidad (ANE/GPU/CPU) corre cada operación y guardarlo en results/.
5. CLI Swift `bench`: decodificar con ImageIO (JPEG/HEIC/TIFF) o CIRAWFilter (RAW, con luminanceNoiseReductionAmount y colorNoiseReductionAmount a 0, convertido a gamma sRGB antes del modelo) -> bloques de 512 con 32 px de solape y relleno por reflejo en los bordes -> Core ML -> mezcla con pesos (rampa lineal o Hann) acumulada en float32 -> salida TIFF de 16 bits escrita en streaming por franjas, sin tener nunca la imagen completa en float en memoria -> metadatos con CGImageDestinationAddImageAndMetadata (NO CopyImageSource), conservando EXIF, GPS, IPTC e ICC.
   Opciones: --model, --compute {ane,gpu,all}, --scale {1,2,4}, --tile, --overlap, --raw9 (solo si macOS 27 lo soporta: decoderVersion = .version9).
   Registrar en CSV: modelo, unidad de cómputo, megapíxeles, s/imagen, s/bloque, tiempo de carga del modelo (primera vez y siguientes) y memoria pico (RSS).
6. Pruebas automáticas: escaneo de NaN, detector de costuras (energía del gradiente en los bordes de bloque) sobre un cielo liso, y prueba de ida y vuelta de metadatos (FNumber 2.8, ExposureTime, GPS, palabras clave IPTC, copyright).
7. Solo con lo anterior en verde: repetir los pasos 1-4 con SCUNet (Apache-2.0, cszn/SCUNet), con un tope de 1 día, y anotar s/bloque contra NAFNet. Después, si sobra tiempo, 4xNomosWebPhoto_RealPLKSR (CC-BY-4.0, Phhofm), anotando su atribución.
8. Script de lote: 50 imágenes seguidas para medir la caída de velocidad por temperatura.

Entregables: results/resumen.md con una tabla por máquina y modelo; marcar en verde o rojo estos criterios: denoise de 24 MP en M1 8 GB <= 30-45 s; en M3/M4 <= 10-15 s; 4x de 24 MP <= 90 s en M1; memoria pico < 3 GB en el denoise de 24 MP; 4x de 45 MP termina en 8 GB; caída por temperatura <= 25%.
Trabaja por fases cerradas, cada una con sus pruebas, y espera mi revisión antes de pasar a la siguiente. No inventes tiempos: si algo no se puede medir en esta máquina, dilo.
```

## Qué hay que verificar antes de confiar en estas cifras

Las notas avisan de sus propios límites, y conviene tenerlos presentes antes de publicar nada o de comprometer dinero.

**Fragmentos de búsqueda en lugar de páginas leídas.** El entorno bloqueó la lectura directa de casi todas las webs de noticias, foros y fabricantes: Adobe, Topaz, DPReview, Fstoppers, Paddle, ON1 y Setapp. Las cifras de la competencia, los precios, las citas de foros y las condiciones de Paddle y Setapp vienen de esos resúmenes. **Reddit no se leyó en absoluto.**

**Precios contradictorios.** Las fuentes no coinciden en lo que cuestan Topaz (Gigapixel a $99 o a $149 al año), Luminar Neo (entre $79 y $369), Aiarty ni el nuevo perpetuo de Capture One. ON1 aparece a $69.99 en una fuente y sin precio confirmado en otra. Todo eso hay que comprobarlo en las tiendas oficiales.

**Evidencia técnica de un solo desarrollador.** Toda la evidencia técnica sobre rendimiento sale de repositorios de una sola persona:

- que Real-ESRGAN no corre en el ANE ([gil](https://github.com/gil/real-esrgan-coreml));
- los tiempos de Core AI ([xocialize](https://github.com/xocialize/coreai-realesrgan-swift));
- que SCUNet es lento y NAFNet ligero (forks de Lumen, medidos en iPhone);
- los 200 ms de CIRAWFilter ([esperyong](https://github.com/esperyong/lightcraft/pull/19)).

Los tiempos en un M1 base son extrapolaciones.

**Datos de Apple sin publicar.** RAW 9 no tiene cifras públicas de calidad ni velocidad, ni lista de cámaras.

**Licencias y datos sin verificar:**

- la licencia de SIDD, de la que solo hay una afirmación de "MIT" que no merece confianza;
- las imágenes de origen con que se entrenó SCUNet;
- las licencias de FFHQ, GoPro y REDS;
- la procedencia del dataset Nomos;
- el coste en horas de GPU de entrenar pesos propios, que es una estimación sin fuente.

**Supuestos de negocio:**

- las tasas de renovación del pase (15–30%) son una suposición;
- las tasas de conversión vienen de una encuesta de 2009 a 92 vendedores;
- el ratio de piratería es de un único desarrollador en 2015;
- el neto medio de $45–48 sale de un modelo propio del investigador.

**Datos de un solo blog o una sola fuente:**

- el lote en segundo plano de Lightroom 15.3;
- el ANE reactivado en Lightroom, que viene de un blog;
- el "seriamente bueno" sobre el denoise de Capture One, que es una anécdota de beta testers;
- que Apple Ads no acepta apps de Mac, basado en un post del foro de noviembre de 2025;
- si existe o no la prueba de Topaz, donde las fuentes se contradicen.

**Comportamientos técnicos sin probar:**

- cómo se comporta "Edit In" de Lightroom con una app en sandbox;
- si ImageIO escribe BigTIFF.

**Sin medir en absoluto.** Ni Google Trends ni el volumen de búsquedas en inglés o español. El tamaño real de la ventana de mercado sigue sin cuantificarse.

## Conclusión

La investigación cambia la pregunta. Al principio era "¿podemos igualar a Topaz con modelos abiertos?". Ahora es "¿qué queda por hacer cuando Apple regala la limpieza del RAW y Pixelmator, ON1 y DxO ya venden con pago único?". La respuesta es concreta: velocidad en lote sobre hardware modesto, ampliación sin el look IA y un flujo que respete los archivos y los metadatos del fotógrafo. Ninguna de esas tres cosas depende de tener el mejor modelo del mundo. Las tres dependen de la ingeniería que el plan ya sabe hacer: bloques, colas, exportación y Core ML. Eso juega a favor de un desarrollador solo con Claude Code. El foso a largo plazo tampoco está en los modelos de terceros, que comparten el mismo riesgo de datos que todo el sector. Está en dos cosas que se pueden empezar a construir desde la beta: unos pesos propios entrenados con fotos cedidas por los propios testers, y una reputación de comparativas honestas en una categoría llena de listados de fabricantes.

La implicación práctica es que las semanas 1–2 no tienen que probar que la app es "mejor que Topaz", sino que es **lo bastante rápida en un M1 y claramente mejor que Pixelmator Pro en JPEG y en ampliación**. Si eso se cumple, el resto del plan corregido es ejecución. Si no, el proyecto se detiene con dos semanas invertidas, en lugar de doce.
