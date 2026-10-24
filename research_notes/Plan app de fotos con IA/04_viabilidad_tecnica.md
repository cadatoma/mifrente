# Technical feasibility: on-device AI denoise/upscale Mac app (Swift, Core ML, Apple Silicon), as of Oct 2026

Scope: engineering only (model licensing and quality selection are covered by another researcher). Plan reviewed: `00_plan_original.txt` (Swift/SwiftUI, macOS 14+, M1+, SCUNet / NAFNet / Real-ESRGAN x4v3 / SwinIR via coremltools, tiles → Core ML (ANE, GPU fallback) → stitch → JPEG/TIFF16/PNG with EXIF/GPS/ICC; 10–12 weeks part-time).

Research note: tool budget was limited (~21 calls). Several items rely on single-developer GitHub projects; these are flagged. Points that come from prior knowledge and were NOT re-verified in this session are explicitly labelled "(unverified prior knowledge)" and placed under Inferences or Gaps, never under Cited Findings.

**Two Oct-2026 platform changes the plan does not account for:**
1. **Core AI** (WWDC26, macOS 27): Apple's successor framework to Core ML. Core ML is not deprecated, but new ANE-first tooling is going to Core AI.
2. **Core Image RAW 9** (WWDC26, macOS 27): Apple's own RAW decoder now uses a tiled Core ML model for **joint demosaic + denoise on the Neural Engine**, available free to every app that calls `CIRAWFilter`. This is a competitor (any free RAW app gets "AI denoise") and also a component this app could use.

---

## 1. Core ML conversion: SCUNet, SwinIR, NAFNet, Real-ESRGAN; ANE fallback, FP16, shapes, existing ports, alternatives

### Takeaway
Conversion is feasible for all four models, but the plan's assumption that the models will "run on the Neural Engine" is weak. A public Core ML port of Real-ESRGAN reports that `computeUnits = .all` never puts RRDBNet or SRVGGNetCompact (x4v3) on the ANE; they run on the GPU. One developer dropped SCUNet as too slow on-device and switched to NAFNet, with LayerNorm rewritten to stay inside FP16. Expect GPU execution as the default path, FP16 LayerNorm/attention fixes, and fixed (or enumerated) tile shapes. SwinIR has no public Core ML conversion evidence and is the highest-risk model.

### Cited Findings
- **Real-ESRGAN on ANE:** the gil/real-esrgan-coreml project says CoreML's `compute_units=ALL` does not dispatch RRDBNet or SRVGGNetCompact (the x4v3 "general" architecture) to the ANE, attributed to "dense channel concatenation and residual connections that ANE does not efficiently support"; all inference runs on the GPU regardless of compute-unit setting — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- The same project ships pre-converted fp16 Core ML models: x4plus (RRDBNet-23, 64 MB), x2plus (64 MB), anime_6B (17 MB), animevideo (SRVGGNetCompact-16, 3 MB), **general / x4v3 (SRVGGNetCompact-32, 6 MB)**; zipped downloads 30 MB / 7.9 MB / 1.1 MB / 2.2 MB. It uses one fixed 522×522 model (512 tile + 10 px pre-pad) for any input size — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- **Contrasting ANE result via Core AI (not Core ML):** xocialize/coreai-realesrgan-swift runs Real-ESRGAN fp16 on the ANE via Apple's new CoreAI.framework, **macOS 27+ only**, with tile geometry (128×128, 8 px overlap) baked in at export, because "the ANE compiles one executable per static shape" — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)
- coremltools issue #2545 (Jun 2025, Real-ESRGAN): ML Program format was much slower than the old NeuralNetwork format, with load times over 10× longer; switching to fixed input shape made tracing/conversion extremely long. The maintainer said first-load ML Program work is cached, advised profiling in Instruments, and confirmed performance ordering **fixed shape > enumerated shapes > flexible (RangeDim) shapes**. Issue still open — [coremltools #2545](https://github.com/apple/coremltools/issues/2545)
- **SCUNet:** a Lumen-fork PR (iPhone 17 Pro Max) found SCUNet too slow: a 24 MP photo split into 126 tiles took over 2 s per tile and "never reached 25% of a 24 MP photo in 60–100 s"; iOS also killed the app for memory on the second run — [AngeloP46/lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)
- An earlier PR in the same project converted SCUNet to Core ML in CI at 512 px float16 tiles, and picked it over NAFNet-SIDD on quality for camera-like noise — [AngeloP46/lumen PR #55](https://github.com/AngeloP46/lumen/pull/55)
- **NAFNet:** the replacement was NAFNet-SIDD-width32 (MIT): "all convolutions", about a quarter of SCUNet's work (author's estimate, not measured), LayerNorm2d rewritten as plain ops so it traces, Neural Engine only. A commit is titled "NAFNet: LayerNorm scaled to stay inside float16". Target under 30 s per image; no measured timings published — [AngeloP46/lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)
- **FP16 risks:** ANE FP16 has a 5-bit exponent (max finite 65,504). Ops such as SquaredDifference/Pow, used inside LayerNorm, can overflow to NaN on the ANE; a common fix is to keep LayerNorm in FP32 with an op selector (mixed precision) — [ax Inc. / Medium: Mixed Precision in Core ML](https://medium.com/axinc-ai/using-mixed-precision-in-core-ml-77c2428ba728); a research paper proposes static scale factors for exact FP16 LayerNorm — [SLaNC, arXiv 2410.10553](https://arxiv.org/pdf/2410.10553)
- Apple's coremltools workflow: convert to an FP16-typed model (eligible for ANE+GPU+CPU), check accuracy against the source, and reconvert as FP32 (GPU/CPU only) if accuracy is not good enough — [coremltools: Typed Execution Workflow](https://apple.github.io/coremltools/docs-guides/source/typed-execution-example.html)
- Another Core ML raw-denoise implementation exported an mlprogram with Float16 I/O for macOS 15, kept a `reduce_mean` in fp32, and offered flexible H/W 16–2048 **or** fixed enumerated shapes for the ANE. It found an fp16-built noise-std map came out 5–8% too small at ISO ≤100 because of fp16 subnormals, so it uses fp32 there — [benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)
- ONNX Runtime's CoreML Execution Provider can silently convert a model to FP16 when using the ML Program format — [ym2132: ONNX Runtime & CoreML may silently convert to FP16](https://ym2132.github.io/ONNX_MLProgram_NN_exploration)
- **SwinIR:** no public source found on converting SwinIR (shifted windows, relative position bias, attention masks) with coremltools or on its ANE residency. Apple's ANE vision-transformer guidance covers MOAT with local 8×8 window attention, not Swin — search result for [Apple ML Research: Deploying Attention-Based Vision Transformers to ANE](https://machinelearning.apple.com/research/vision-transformers) (page fetch failed; summary from search snippet only)
- **Core AI status:** Apple announced Core AI at WWDC26 as the successor to Core ML, shipping with iOS/macOS 27 — [InfoQ, Jun 2026](https://www.infoq.com/news/2026/06/apple-core-ai-wwdc/). A GitHub issue quotes a WWDC26 lab remark that it is "not a call to migrate off… Core ML works" and that Core ML is not deprecated — [mlcommons/mobile_app_open #1188](https://github.com/mlcommons/mobile_app_open/issues/1188)
- **MLX:** for Real-ESRGAN on an M3 Ultra, Core ML (GPU) was 1.2–1.6× faster than MLX and used less energy (x4plus: 100 J vs 122 J per image) — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml). On M5 Max, CoreAI static executables ran 2.2–2.4× faster than MLX dynamic GPU — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)
- **Upscayl / ncnn-vulkan:** no benchmark of Upscayl's ncnn+Vulkan (MoltenVK) path on Apple Silicon was found. Upscayl is in the Mac App Store — [Upscayl on Mac App Store](https://apps.apple.com/us/app/upscayl/id6468265473?mt=12)

### Inferences
- **Recommended approach:** (a) Real-ESRGAN x4v3: start from the existing pre-converted models or convert it yourself; it is tiny (6 MB fp16) and fast on the GPU, so low risk. (b) Denoise: prototype **NAFNet first** (pure conv, ANE-friendly after the LayerNorm rewrite); treat SCUNet (Swin-style window attention plus conv blocks) as the "quality mode" that will likely run on the GPU and be several times slower. (c) Defer SwinIR to v1.x, with a hard time-box in the spike. Given the evidence, the plan's ordering (SCUNet first, then NAFNet/SwinIR if needed) should be reversed.
- Export with **fixed tile shapes** (e.g. 256 or 512 plus padding), or `EnumeratedShapes` with 2–3 sizes; avoid `RangeDim` if the ANE matters. Keep LayerNorm/softmax/reductions in FP32 via `op_selector` (mixed precision) where NaNs or color shifts appear.
- Use `MLComputePlan` (macOS 14.4+ / coremltools 8 era, unverified prior knowledge) and the Xcode Core ML performance report to see which ops fall back to GPU/CPU per device, rather than trusting `.all`.
- Because the app targets macOS 14+, Core AI (macOS 27+) cannot be the only backend. A reasonable design is a protocol-based inference backend: Core ML (macOS 14+) now, Core AI as an optional fast path on macOS 27, chosen at runtime.
- ONNX Runtime CoreML EP and ncnn/MoltenVK add binary size and another precision layer for little benefit over direct Core ML on GPU. MPSGraph is a fallback only if a specific op is unsupported. MLX is viable (Swift API) but measured slower than Core ML for these conv nets.

### Gaps
- No public SwinIR→Core ML conversion report or timing; no data on whether its shifted-window masking and `torch.roll` convert cleanly with coremltools 8/9.
- No published per-tile NAFNet/SCUNet timings on any Mac (only iPhone and estimates).
- No coremltools 9 release notes were checked in this session (version-specific bugs unknown).
- Why x4v3 (plain conv + PixelShuffle + PReLU) is refused by the ANE under Core ML is attributed by one developer only; may vary by OS version/chip. Must be confirmed with a compute plan in the spike.

---

## 2. Performance: M1–M5, ANE vs GPU, 24/45/61 MP, 1,000-photo batches, 8 GB M1, thermals

### Takeaway
No credible public benchmark covers these models at 24–61 MP on M1–M5. The data points that do exist (M3 Ultra, M4, M5 Max, iPhone 17 Pro Max) imply: x4v3 upscale is fast (seconds per image on high-end chips); heavy models (RRDBNet x4plus, SCUNet) take minutes per 24 MP image on a base M1, so a 1,000-photo wedding batch could take many hours to days. The ANE's main benefit is energy and thermals (about 4.5–4.9× less energy, no throttling), not raw speed.

### Cited Findings
- M3 Ultra, fp16, per 512×512 input tile, Core ML (GPU) vs MLX: x4plus 0.47 s vs 0.75 s; x2plus 0.12 s vs 0.20 s; anime_6B 0.15 s vs 0.23 s; **general (x4v3) 0.03 s vs 0.04 s**; animevideo 0.02 s — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- Same source, tile-size sweep on one image: tile 64 → 165 tiles, 3.46 s; 128 → 42 tiles, 1.80 s; 256 → 12 tiles, 1.55 s; 512 → 4 tiles, 1.71 s. Max pixel difference vs reference falls with tile size: 0.596 / 0.518 / 0.212 / 0.075 — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- Power on M3 Ultra (x4plus): Core ML 110 W (100 J/image) vs MLX 131 W (122 J/image) — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- M5 Max, 128-px tiles: ANE (via Core AI) wall-clock ties the best MLX-GPU configuration; ~17 W ANE vs ~83 W GPU; ~14.5 J vs ~67 J per frame (4.5–4.9× less energy); **"the ANE does not throttle, while the GPU drops from 1616 to 1366 MHz"**; first-run compile ~8 s per variant per machine, then cached by the OS — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)
- A TouchDesigner Core ML Real-ESRGAN tutorial reports about 1–1.3 s per frame on M4 for a 512→2048 upscale — [derivative.ca CoreML upscaler](https://derivative.ca/community-post/tutorial/coreml-upscaler/74428)
- SCUNet on iPhone 17 Pro Max: over 2 s per tile, 126 tiles for 24 MP (so over 4 min per image), plus an out-of-memory kill — [AngeloP46/lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)
- Apple's own RAW 9 ML demosaic+denoise model "runs hundreds of times per image" (tiled) on the ANE — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)
- A CIRAWFilter decode carries roughly 200 ms fixed overhead per image (developer measurement) — [esperyong/lightcraft PR #19](https://github.com/esperyong/lightcraft/pull/19)

### Inferences
(Arithmetic estimates, not measurements. Tile counts assume 512-px tiles with 32-px overlap, stride 480.)
- Tiles per image: 24 MP (6000×4000) ≈ 13×9 = **117**; 45 MP (8256×5504) ≈ 18×12 = **216**; 61 MP (9504×6336) ≈ 20×14 = **280**.
- x4v3 at 0.03 s/tile (M3 Ultra GPU, 80-core class) → about 3.5 s / 6.5 s / 8.4 s for 24/45/61 MP. A base M1 (8-core GPU, very roughly 8–10× less GPU throughput; unverified prior knowledge) might take about 30–80 s per 24–61 MP image for 4× upscaling, before I/O and encoding.
- x4plus at 0.47 s/tile → about 55 s for 24 MP on M3 Ultra; likely 5–10 min on M1. Not viable for batch use; x4v3 is the right default.
- Denoise (1×, same resolution): NAFNet-width32 is probably on the order of x4plus-to-x4v3 cost per tile; SCUNet is several times heavier. A 1,000-photo, 24 MP wedding batch at 30 s/photo ≈ 8.3 h; at 4 min/photo (SCUNet-class on weak hardware) ≈ 67 h. **Batch throughput on M1/M2 base is the central product risk** for the wedding/event persona, and must be measured in week 1.
- On fanless MacBook Air, sustained GPU load throttles (shown by the GPU clock drop even on an M5 Max). Running ANE-eligible models (NAFNet after the LayerNorm rewrite) has a real advantage for long batches. Mixing ANE and GPU (e.g. denoise on ANE while the GPU handles upscale or Core Image work) is a pipelining option.
- Memory on 8 GB M1: model weights are small (MBs). The pressure comes from full-resolution buffers. 4× upscaling of 24 MP gives 384 MP output (24000×16000): about 1.15 GB in 8-bit RGB, 2.3 GB in 16-bit RGB, 4.6 GB as RGBA half-float. A 61 MP image upscaled 4× gives about 976 MP, roughly 5.9 GB as 16-bit RGB, which is not viable on 8 GB in memory. The app needs **streaming/strip-based output** (or a cap such as 2× for >40 MP on 8 GB), memory-mapped intermediates, and should never hold a full-resolution float buffer.
- Batch pipelining (decode N+1 while inferring N, parallel encoding) gave 1.48× in the gil video pipeline; similar overlap of RAW decode (~200 ms+), inference and JPEG/TIFF encode should be designed in from the start.

### Gaps
- No measured numbers for M1/M2/M3/M4/M5 base or Pro chips with SCUNet/NAFNet/SwinIR at 24/45/61 MP. No published ANE-vs-GPU comparison for these models under Core ML (only Core AI on M5 Max).
- No MacBook Air sustained-throttling measurements for ML workloads were found.
- No public peak-memory measurement for tiled Core ML inference on 8 GB M1.

---

## 3. Tiling: overlap, blending, edges, color consistency

### Takeaway
This is a solved engineering problem. Use fixed tiles of 256–512 px, reflect-pad the image borders, overlap 8–32 px (more for attention models), and blend with normalized feathered weights accumulated in float32. Larger tiles reduce seam error. Global color/brightness drift between tiles is the main subtle risk for models with normalization layers.

### Cited Findings
- Larger tiles reduce boundary error: max pixel difference 0.596 (64 px) → 0.075 (512 px); the author recommends 512 — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- 128×128 tiles with an 8-px overlap, normalized feathered blend Σwᵢxᵢ/Σwᵢ in float32; full-pipeline parity vs a torch-fp32 oracle of 66.85 dB, max difference 1 LSB, 1.3% of pixels differing — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)
- Raw-denoise pipeline: reflect-pad to a multiple of 16; feathered weights normalized by the weight sum with a floor of 1e-6; short tiles get flat weights; image borders get full weight; denoise strength applied as a post-blend with the original (no recompute when the slider moves) — [benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)
- WWDC26 adds `CIImageProcessorKernel` explicit output tiles (`apply(withTiledExtent:inputs:arguments:)`) and Core Image-managed recycled temporary buffers (`temporaryPixelBuffer(identifier:format:width:height:pixelBufferAttributes:)`, e.g. `kCVPixelFormatType_64RGBAHalf`) — on OS 27 — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)

### Inferences
- Recommended: tile 512 (or the fastest size measured per model), overlap 32 px at input resolution for conv nets and 64 px for SCUNet/SwinIR (larger receptive field and window shifts), raised-cosine/Hann or linear-ramp weights, float32 accumulator, reflect padding at image borders, and tile sizes that are multiples of the model's window/downsampling factor (8 for SwinIR windows, 16/32 for UNet-style SCUNet/NAFNet).
- Color consistency: per-tile normalization layers (LayerNorm over the channel only is fine; any global-mean ops are not) can shift tone between tiles. Test with flat gradients (sky, studio backdrops). The plan's "Enfocar suave" blend-with-original feature is cheap to implement as a post-blend, as the Lumen PR does.
- Implementation: a vImage/Accelerate or Metal accumulation buffer is simpler than going through Core Image for v1; the OS-27 CIImageProcessor tiling features cannot be the only path with a macOS 14 minimum.

### Gaps
- No quantitative study found comparing Gaussian vs linear feathering for these specific models.

---

## 4. RAW pipeline: CIRAWFilter quality and coverage, linear data, denoise position, DNG output, how PureRAW/Lightroom do it

### Takeaway
`CIRAWFilter` (macOS 12+) is a good-enough RAW decoder that can supply linear, scene-referred, demosaiced RGB. It gives no access to the Bayer mosaic. The proposed models (SCUNet/NAFNet trained on sRGB/SIDD) are post-demosaic RGB denoisers. The competitive standard (DxO PureRAW, Lightroom Denoise) is **pre-demosaic, outputting a linear (demosaiced) DNG**, which this plan cannot match without Bayer-domain models and a DNG writer. On macOS 27, Apple's own RAW 9 decoder already runs an ML demosaic+denoise on the ANE, which changes the competitive landscape.

### Cited Findings
- **RAW 9 (WWDC26, OS 27):** a tiled Core ML model for combined demosaic + denoise, running on the ANE; opt-in via `supportedDecoderVersions.contains(.version9)` → `filter.decoderVersion = .version9`; `colorNoiseReductionAmount` has no effect in RAW 9 (the model handles color noise); `detailAmount` and `moireReductionAmount` are not supported; `luminanceNoiseReductionAmount` still controls it — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)
- **Camera coverage:** 784 camera models supported (up from 21 in 2006); hundreds support RAW 9; the list grows via over-the-air updates; native-DNG cameras are supported automatically; `supportedCameraModels` lists models per version — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)
- WWDC26 export guidance: a context with intermediate caching off, a higher `memoryLimit` (512–1024 MB vs the iOS default of 256 MB), and `CIContext` `heifRepresentation`/`jpegRepresentation` to save memory vs calling ImageIO directly; the Extended Virtual Addressing entitlement lets the cache use more memory — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)
- Through `CIRAWFilter` an app "never sees the mosaic"; there is no hook before demosaic, and `linearSpaceFilter` was unused in that project. To run a Bayer-domain model, that project reads the CFA from a DNG (via Adobe DNG Converter plus its own Swift DNG raw-IFD reader), runs Core ML on the 4-channel packed mosaic plus a noise-std map, and writes a denoised DNG back for `CIRAWFilter` — [benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)
- Apple's decoder can produce scene-linear Rec.2020 output, with about 200 ms fixed overhead per decode — [esperyong/lightcraft PR #19](https://github.com/esperyong/lightcraft/pull/19); a separate project requests linear, scene-referred output (no tone curve, no default look) from CIRAWFilter — [storytold/lightcraft #1347](https://github.com/storytold/lightcraft/issues/1347)
- `linearSpaceFilter` is the filter applied while RAW processing is in linear color space (secondhand, .NET binding docs) — [Microsoft Learn: CIRawFilterOptions](https://learn.microsoft.com/en-us/dotnet/api/coreimage.cirawfilteroptions?view=net-ios-26.5-10.0&viewFallbackFrom=xamarin-ios-sdk-12)
- **DxO PureRAW output:** a linear DNG, already demosaiced, with corrections baked in — [Have Camera Will Travel: PureRAW 6 review](https://havecamerawilltravel.com/workflow/dxo-pureraw-review/); PureRAW 5 DNGs were 3–4× the original size — [Life after Photoshop: PureRAW 5 review](https://lifeafterphotoshop.com/dxo-pureraw-5-review/); PureRAW 6 DNGs are significantly smaller than v5's — [Have Camera Will Travel: PureRAW 6 hands-on](https://havecamerawilltravel.com/dxo-pureraw-6-released/)
- **Lightroom Denoise:** runs on undemosaiced RAW data and outputs a linear DNG — [Todd Marsh: PureRAW vs Lightroom AI Denoise](https://toddmarsh.com/dxo-pureraw-vs-lightroom-ai-denoise-high-iso/); it only works on undemosaiced RAW (not JPEG/TIFF/PNG) — [Mastering Lightroom](https://mastering-lightroom.com/denoise-lightroom-classic/)
- DxO cannot take linear DNGs as input because they are "already demosaiced" and the raw information is no longer accessible — [DxO support](https://support.dxo.com/hc/en-us/articles/4433898493329-Which-DNG-files-are-supported-by-DxO-PureRAW-as-input)
- **DNG SDK license:** royalty-free, worldwide licence to use, reproduce, modify and distribute "for any purpose", main restriction being to keep copyright notices — [Adobe DNG SDK License Agreement](https://www.adobe.com/support/downloads/dng/dng_sdk_eula_win.html). The DNG spec licence requires the notice "This product includes DNG technology under license by Adobe" and is revocable if the licensee sues Adobe over DNG patents — [Adobe DNG SDK notices (PDF)](https://www.adobe.com/content/dam/cc/en/products/eula/third_party/photoshop_lightroom/Lightroom_DNG_SDK_3P_Notices_Clean_Final_100312.pdf)

### Inferences
- **v1 recommendation:** decode RAW with `CIRAWFilter` to 16-bit/half-float linear or lightly tone-mapped RGB (wide gamut), denoise/upscale in RGB, and export TIFF16. This is what models trained on sRGB data expect. Tone-map or encode **before** the model when the model was trained on gamma-encoded sRGB (SIDD-trained NAFNet, SCUNet); feeding scene-linear data to a gamma-domain model will mis-scale noise and shadows. Turn CIRAWFilter's own NR to zero (`luminanceNoiseReductionAmount = 0`, `colorNoiseReductionAmount = 0`) on pre-RAW-9 decoders to avoid double denoising.
- **Linear DNG output** (so users keep editing in Lightroom/Capture One) is feasible: the DNG SDK licence is permissive and C++ builds on macOS. ImageIO does not write DNG (unverified prior knowledge; Apple only exposes DNG reading). This means adding the DNG SDK (C++ bridging, ~1–2 weeks part-time to write a correct LinearRaw DNG with color matrices, white balance and baseline exposure). It is **not** a v1 item in a 10–12-week plan. Note that a linear DNG from an RGB-domain denoise is still "demosaiced by Apple's decoder", so Lightroom users lose Adobe's own demosaic, unlike Lightroom Denoise/PureRAW, which denoise before demosaic.
- **RAW 9 implication:** on macOS 27 any app calling `CIRAWFilter` with `.version9` gets ML demosaic+denoise on the ANE for free. The app could (a) use RAW 9 as its RAW denoise stage on macOS 27 and its own model on macOS 14–26, and (b) must benchmark its quality against RAW 9 output, not only against Lightroom/Topaz. The "denoise RAW" value proposition weakens for macOS 27 users; JPEG/HEIC denoise and upscaling remain differentiators.
- Camera lag: CIRAWFilter support for new bodies arrives via OS updates (OTA, per WWDC26), typically weeks to months after a camera launch (timing unverified prior knowledge). Plan a fallback ("convert to DNG with Adobe DNG Converter first") and show a clear error for unsupported cameras.
- Bayer-domain denoise (true parity with PureRAW/Lightroom) needs a different model class (RAW-trained), a CFA reader (DNG SDK or LibRaw) and a DNG writer, a multi-month project better suited to v2.

### Gaps
- No official Apple documentation fetched on exactly where `linearSpaceFilter` runs relative to demosaic, or on RAW 9 behaviour on M1 or its availability on macOS 14–26 (assumed OS 27 only).
- No independent quality comparison of CIRAWFilter (RAW 8/9) vs Adobe Camera Raw demosaic was found.
- No measured data on CIRAWFilter support lag for 2025–2026 camera releases.

---

## 5. Color management and metadata (P3/ProPhoto, TIFF16, ICC, EXIF/GPS/XMP/IPTC)

### Takeaway
ImageIO handles 16-bit TIFF/PNG with embedded ICC and full metadata, but **`CGImageDestinationCopyImageSource` is the wrong API for this app**: it copies the source's existing pixels unchanged and only edits metadata. For new pixels, use `CGImageDestinationAddImage` (or `…AddImageAndMetadata`) with the properties/metadata read from the source, keeping the color space on the `CGImage`.

### Cited Findings
- `CGImageDestinationCopyImageSource` copies the contents of the image source to the destination **without modifying the image data**; only metadata changes through the options dictionary; supported formats JPEG, PNG, PSD, TIFF (as of 2015) — [Apple QA1895](https://developer.apple.com/library/archive/qa/qa1895/_index.html)
- `CGImageDestinationAddImageAndMetadata` takes a `CGImage` + `CGImageMetadata` + options — a separate path that does not copy from a source — [ImageIO API diffs macOS 10.11](https://developer.apple.com/library/archive/releasenotes/General/APIDiffsMacOSX10_11/Objective-C/ImageIO.html)
- `kCGImageMetadataShouldExcludeGPS` excludes GPS from EXIF/XMP (useful as a privacy option) — [Apple CGImageDestination docs](https://developer.apple.com/documentation/imageio/cgimagedestination.md)
- Reported bug: with CopyImageSource, float-like EXIF entries were truncated (e.g. FNumber 2.8 → 2); GPS latitude/longitude unaffected; unresolved forum report — [Apple Developer Forums thread 705980](https://developer.apple.com/forums/thread/705980)
- Reading/writing metadata patterns with ImageIO (CGImageSourceCopyPropertiesAtIndex / CopyMetadataAtIndex) — [ikyle.me](https://ikyle.me/blog/2020/ios-metadata-from-file)

### Inferences
- Recommended export path: `CGImageSourceCopyMetadataAtIndex` (XMP tree incl. IPTC/EXIF/GPS) + `CGImageSourceCopyPropertiesAtIndex` → modify `PixelWidth/Height`, `Orientation` (normalize to 1 after baking rotation), remove the embedded thumbnail and stale MakerNote fields if size changed → `CGImageDestinationAddImageAndMetadata`. Write a regression test that checks round-trip of FNumber/ExposureTime/GPS/IPTC keywords/copyright, given the reported float truncation.
- RAW sources: EXIF lives in the RAW, but some MakerNote/lens data will not map to TIFF/JPEG; accept loss of MakerNotes, and keep EXIF/GPS/IPTC/XMP (rating, labels) which photographers actually care about.
- Color: run the model in the space it was trained in (sRGB-gamma for most), but for wide-gamut sources convert to an extended-range linear or gamma working space with `CGColorSpace(name: .extendedSRGB/.displayP3)` and clamp carefully; the FP16 model may clip out-of-gamut negatives. Embed the source ICC (Display P3, Adobe RGB, ProPhoto) in TIFF16/PNG; JPEG output should default to sRGB or P3 with an embedded profile. Upscaling 16-bit TIFF at 4× quickly exceeds the 4 GB classic-TIFF limit (61 MP ×16 = 976 MP × 6 B ≈ 5.9 GB); BigTIFF support in ImageIO is unverified, so cap or warn.
- JPEG maximum dimension is 65,535 px per side; 4× of a 61 MP (9504 px wide) image = 38,016 px, which is still within the limit.

### Gaps
- Not verified in this session: whether ImageIO writes BigTIFF; whether `CGImageDestinationAddImageAndMetadata` preserves all IPTC/XMP from RAW sources; color shift behaviour of FP16 models on Display P3/ProPhoto input.

---

## 6. Lightroom Classic / Capture One / Photos integration

### Takeaway
"Edit In" (Additional External Editor) needs no code: any Mac app that opens TIFF/PSD and saves back over the file works, so it should come first. A Lightroom Classic SDK (Lua) plugin is needed for RAW workflows (sending the original RAW and returning a DNG/TIFF next to it), which is how Topaz and DxO integrate; this takes one to two weeks and is reasonable for v1.5. The plan already defers plugins to v1.5, which matches this evidence.

### Cited Findings
- Many "plugins" are really external editors under Edit In rather than in the Export dialog — [Adobe Community](https://community.adobe.com/questions-675/installing-a-plugin-in-lightroom-classic-947442)
- Topaz separates the two paths: RAW files go through File > Plug-in Extras (needed for RAW denoise); non-RAW go through Edit In, which converts the file to TIFF; using Edit In on RAW is discouraged because it loses RAW denoise access (search-result summary of [Topaz docs: Lightroom Classic](https://docs.topazlabs.com/topaz-photo/plugins/lightroom-classic); direct fetch failed)
- SDK: the `processRenderedPhotos` export callback runs for each exported photo after Lightroom renders it and after all post-process actions — [LrC SDK reference mirror: Export service provider](https://lrc.mcor.dev/modules/SDK%20-%20Export%20service%20provider.html); a filter can return a string used as the new file path — [LrFilterContext](https://lrc.mcor.dev/modules/LrFilterContext.html)
- A DNG returned by DxO PureRAW's Lightroom integration is stacked with the RAW, but always at the bottom of the stack; users ask for better stacking — [Adobe Community](https://community.adobe.com/t5/lightroom-classic-discussions/stapelsortierung-nach-externer-bearbeitung-%C3%A4ndern/m-p/15122618); [DxO forum](https://forum.dxo.com/t/simplify-round-trip-to-lightroom-classic/34671)
- Developers find the SDK manual's post-processing examples vague — [Adobe Community](https://community.adobe.com/t5/lightroom-classic-discussions/lightroom-sdk-manual-and-sample-plugins-vague-documentation-for-post-processing-actions/td-p/13228047)
- The SDK did not initially expose new Denoise/Distraction Removal settings (fixed-issues list) — [Adobe: Fixed issues in Lightroom Classic](https://helpx.adobe.com/lightroom-classic/desktop/troubleshooting/fixed-issues.html)

### Inferences
- **v1:** document "Edit In" setup (Preferences → External Editing → choose app, TIFF 16-bit ProPhoto/AdobeRGB). The app must handle `open` of a file, process it, and overwrite the same file in place (or offer "Save & return"). This costs only days. In a sandboxed MAS build, files opened through Launch Services get access, so overwrite in place works (unverified prior knowledge; test it).
- **v1.5:** a Lua export plugin (`LrExportServiceProvider` with `processRenderedPhotos`, or a Library menu item via `LrTasks` + `LrShell.openFilesInApp`/command line), sending the original RAW or a rendered TIFF and reimporting with `catalog:addPhoto(path, {stackWithPhoto=…})` (API names are unverified prior knowledge). Requires the app to have a CLI or URL-scheme batch entry point and a way to signal completion. Estimate 1–2 weeks part-time including installer/testing. A plugin from a sandboxed MAS app is awkward because the plugin lives in Lightroom's folder and must launch the app with paths; the Developer ID build is easier.
- **Capture One:** "Edit With / Open With" to an external app (TIFF/PSD) gives the same Edit-In route; Capture One's plugin SDK access is restricted to partners (unverified prior knowledge).
- **Photos.app extension** (`PHContentEditingController`, macOS Photo Editing Extension): feasible for JPEG/HEIC, but extensions run with tighter memory/time limits and must return a rendered image plus adjustment data. Heavy 45 MP inference inside an extension is risky. Defer to v2.

### Gaps
- Could not fetch Topaz docs directly (DNS failure) to confirm the exact returned format (DNG vs TIFF) of their RAW plugin path.
- Current Lightroom Classic SDK version and the exact catalog/stacking APIs were not verified from Adobe's SDK guide in this session.
- No source found on Capture One plugin SDK terms or Photos-extension memory limits on macOS 14–27.

---

## 7. Distribution engineering: app size, bundled vs on-demand models, MAS sandbox vs Developer ID, licensing for Paddle

### Takeaway
Model size is not a problem: all four models fit in about 100–150 MB fp16 in total, so bundling them is fine for v1. Apple-hosted Background Assets (App Store/TestFlight, macOS included) cover later model updates. Developer ID + notarization is the simpler primary channel. The MAS build is feasible but needs security-scoped bookmarks for batch folders and has awkward Lightroom-plugin flows.

### Cited Findings
- Real-ESRGAN fp16 Core ML sizes: x4v3 6 MB (2.2 MB zipped), x4plus 64 MB (30 MB zipped) — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml); Core AI Real-ESRGAN assets 2.3–4.6 MB — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)
- **Apple-hosted Background Assets** (WWDC25): macOS supported; 200 GB of Apple hosting included with Developer Program membership; download policies `essential` / `prefetch` / `onDemand`; requires an app group (`BAAppGroupID`) shared with a downloader extension; read via `AssetPackManager`; works for App Store and TestFlight; direct distribution is not covered (self-hosting via `BAManifestURL` is the alternative); explicitly pitched for updating on-device ML models with accelerated review; **caution: promoting a new asset pack switches all App Store installs, including older app versions** — [WWDC25 session 325](https://developer.apple.com/videos/play/wwdc2025/325/)
- Main app bundle limit cited as 4 GB on most platforms — [WWDC25 session 325](https://developer.apple.com/videos/play/wwdc2025/325/)
- Core ML's `MLModelAsset` (macOS 13+) loads compiled models from `.mlmodelc` or in-memory representations — [Apple: MLModelAsset](https://developer.apple.com/documentation/coreml/mlmodelasset.md)
- Core AI / ANE: first-run device specialization ~8 s per model variant per machine, cached by the OS — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift); Core ML ML-Program first-load can be over 10× slower than later loads — [coremltools #2545](https://github.com/apple/coremltools/issues/2545)

### Inferences
- Size estimate (fp16): x4v3 ~6 MB; NAFNet-width32 roughly 30–60 MB; SCUNet roughly 30–40 MB; SwinIR-M ~25 MB (fp32 parameter counts from papers converted to fp16; unverified estimates). Total ~100–150 MB plus a ~20–40 MB Swift app. **Bundle everything in v1**; optional 8-bit weight palettization (coremltools `optimize`) can halve size if needed, at a quality cost to validate.
- Precompile `.mlpackage` → `.mlmodelc` at build time (Xcode does this) and warm up the models (dummy inference) at first launch with a progress UI, to hide the first-load/specialization cost.
- **Developer ID + notarization** (Paddle): Hardened Runtime; no sandbox requirement; easy CLI/Lightroom plugin integration; Sparkle for updates. **MAS:** App Sandbox; user-selected read/write entitlement; security-scoped bookmarks to persist batch input/output folders and "Edit In" round-trips; no paid-upgrade mechanism (the plan already notes this). Keep one codebase with two build configurations.
- **Licensing for the Paddle build:** Paddle Billing does not natively issue license keys for desktop apps (the old Paddle Mac SDK was tied to Paddle Classic; unverified prior knowledge). Plan for a small license server (or a service such as Keygen) with offline-validating signed license files (Ed25519) and a 2-Mac activation limit; ~1 week part-time. This is likely under-estimated in the plan's single "Semana 9".
- The trial watermark must be applied at export only (not in preview), and a cracked build is out of scope (the plan accepts low DRM).

### Gaps
- No verified current info on Paddle Billing license-key support for macOS apps (Oct 2026).
- Exact fp16 Core ML sizes for SCUNet/NAFNet/SwinIR not measured.
- Not verified whether Apple-hosted Background Assets work for macOS 14 (minimum OS for the feature not stated).

---

## 8. Testing / quality assurance

### Takeaway
Use a three-layer QA strategy: (1) numerical parity of each Core ML model against PyTorch fp32 (PSNR ≥ 50–65 dB per tile) per compute unit; (2) full-image regression with stored golden outputs plus perceptual metrics (LPIPS/DISTS/SSIM) and seam/flat-field checks; (3) memory/thermal soak tests on the lowest-end target (8 GB M1 MacBook Air) with 45–61 MP files and 1,000-image batches.

### Cited Findings
- Parity gate example: Core ML must reach ≥ 50 dB tone-space PSNR vs torch fp32 — [benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)
- fp16 ANE vs fp32 PyTorch on real 128² tiles: 68.56 dB min / 69.36 dB mean (general), 58.15 / 65.09 dB (generalWDN); full pipeline 66.85 dB, max 1 LSB — [xocialize/coreai-realesrgan-swift](https://github.com/xocialize/coreai-realesrgan-swift)
- Tile-size seam error can be measured as max pixel diff vs a no-tile reference (0.075 at 512 px) — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- Element-by-element CPU vs ANE parity testing at multiple input sizes is used in other Core ML ports — [ChinChangYang/KataGo #36](https://github.com/ChinChangYang/KataGo/issues/36)
- Device diagnostics that log model load time and the first three tile times give early speed data even from unfinished runs — [AngeloP46/lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)
- Apple's Typed Execution workflow: validate FP16 accuracy vs source; fall back to FP32 if insufficient — [coremltools docs](https://apple.github.io/coremltools/docs-guides/source/typed-execution-example.html)

### Inferences
- Regression set (~60 images): high-ISO RAW from at least 6 camera brands (Sony, Canon, Nikon, Fuji X-Trans, Panasonic, iPhone ProRAW), 24/45/61 MP sizes, JPEG/HEIC/PNG, P3 and ProPhoto TIFF16, images with flat skies/backdrops (seam/banding detection), saturated colors (FP16 clipping), and near-black shadows (NaN/denormal checks). Automate: NaN/Inf scan, mean color shift ΔE per tile vs input, seam detector (gradient energy at tile boundaries), LPIPS vs golden.
- Run per-model parity tests separately for `.cpuAndNeuralEngine`, `.cpuAndGPU` and `.all`, since op placement differs by chip/OS.
- Memory tests: XCTest with `XCTMemoryMetric`, plus Instruments Allocations, on an 8 GB M1 with the largest file × 4× upscale; batch soak test with 1,000 files to catch leaks (autoreleasepool per tile, `MLMultiArray`/`CVPixelBuffer` reuse).
- Metadata round-trip tests (Section 5) and colour-profile round-trip tests (embedded ICC equals source ICC).

### Gaps
- No published LPIPS/DISTS baselines for these models on real camera high-ISO data vs Topaz/Lightroom were found (quality is the other researcher's scope).

---

## 9. Is 10–12 weeks part-time realistic? Biggest risks and recommended week-1/2 spike

### Takeaway
10–12 weeks part-time is realistic only for a narrowed v1: JPEG/HEIC/TIFF + RAW via CIRAWFilter to RGB, NAFNet denoise + x4v3 upscale, GPU/ANE via Core ML, TIFF16/JPEG/PNG output with metadata, Edit-In support, Developer ID/Paddle only. Adding linear DNG output, a Lightroom SDK plugin, SCUNet/SwinIR quality modes, MAS sandbox hardening and a license server pushes it to roughly 16–22 weeks part-time. The biggest risks are batch throughput on base M1/M2 and quality versus Apple's free RAW 9 denoise on macOS 27, not conversion itself.

### Cited Findings
- SCUNet was too slow and memory-hungry on a current flagship Apple device (>2 s/tile, OOM) and was replaced — [AngeloP46/lumen PR #60](https://github.com/AngeloP46/lumen/pull/60)
- Real-ESRGAN models run on GPU, not ANE, under Core ML `.all` — [gil/real-esrgan-coreml](https://github.com/gil/real-esrgan-coreml)
- Apple ships ML demosaic+denoise in CIRAWFilter RAW 9 on OS 27 — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)
- Core AI (macOS 27) is the new ANE-first path; Core ML remains supported — [InfoQ](https://www.infoq.com/news/2026/06/apple-core-ai-wwdc/); [mlcommons #1188](https://github.com/mlcommons/mobile_app_open/issues/1188)
- Competitors output linear DNG from pre-demosaic denoise — [Todd Marsh](https://toddmarsh.com/dxo-pureraw-vs-lightroom-ai-denoise-high-iso/); [Have Camera Will Travel](https://havecamerawilltravel.com/workflow/dxo-pureraw-review/)
- Even a well-structured single-developer Core ML raw-denoise effort shows the end-to-end Mac parity check and real-camera timings still pending after the design/port PR — [benedek-art/lumen PR #16](https://github.com/benedek-art/lumen/pull/16)

### Inferences
**Component feasibility summary**

| Component | Feasibility | Recommended approach | Main risk | Est. effort (part-time weeks) |
|---|---|---|---|---|
| Model conversion | High (x4v3, NAFNet); Medium (SCUNet); Low–Medium (SwinIR) | coremltools mlprogram, fixed/enumerated tiles, FP16 with FP32 LayerNorm/softmax | ANE fallback, NaNs, slow SCUNet | 2–3 |
| Inference engine + tiling | High | Core ML GPU default, ANE where compute plan confirms; 512 tiles, 32–64 px overlap, float32 feather | 8 GB memory at 4× | 2–3 |
| RAW input | High (RGB path) | CIRAWFilter → 16-bit/half RGB, NR off; RAW 9 option on macOS 27 | Camera lag; quality vs RAW 9 | 1 |
| Linear DNG output | Medium | Adobe DNG SDK (C++) LinearRaw | Color metadata correctness | 2 (defer) |
| Export + metadata + ICC | High | AddImageAndMetadata, not CopyImageSource; streaming for huge outputs | EXIF float bug, >4 GB TIFF | 1 |
| SwiftUI UI + before/after | High | Metal/CI-backed zoomable preview, tile-on-demand preview | Preview latency | 2 |
| Batch queue | High | Pipelined decode/infer/encode, resumable job journal | Throughput, thermals | 1 |
| LR "Edit In" | High | Document + in-place save | Sandbox file access | 0.5 |
| LR SDK plugin | Medium | Lua export/menu plugin + CLI | Thin SDK docs | 1–2 (defer) |
| Licensing (Paddle) | Medium | Signed license files + small activation server | Paddle lacks native keys | 1 |
| MAS build | Medium | Sandbox + bookmarks + Background Assets later | Lightroom flows, paid upgrades | 1 |
| Beta, notarization, site | High | Developer ID + Sparkle | — | 2–3 |

- Sum of the narrowed v1 ≈ 12–15 part-time weeks; full plan as written incl. DNG + LR plugin + MAS + SCUNet/SwinIR ≈ 18–22 weeks. The plan itself flags phase 1 as the most likely to slip, which the evidence supports.
- **Biggest risks (ranked):** (1) throughput on base M1/M2 for 1,000-photo batches with a model good enough to compete, which may force NAFNet-class models and low "quality mode" usage; (2) Apple RAW 9 (free, ANE, macOS 27) narrowing the RAW-denoise differentiator; (3) no Bayer-domain/DNG workflow vs PureRAW/Lightroom, which pro wedding users expect; (4) FP16/ANE numerical issues causing colour shifts or NaNs on some chips; (5) memory on 8 GB for 4× of 45–61 MP; (6) licensing/activation work under-scoped.
- **Recommended week-1/2 spike (go/no-go):**
  1. Day 1–2: convert NAFNet-SIDD-w32 and Real-ESRGAN x4v3 with coremltools (mlprogram, fixed 512 + pad, FP16, LayerNorm in FP32). Run `MLComputePlan` and Xcode performance reports to record per-op device placement on M1 and newest available chip.
  2. Day 3: same for SCUNet (time-boxed to 1 day); SwinIR only if time remains.
  3. Day 4–5: a minimal Swift CLI: CIRAWFilter/ImageIO decode → tile (512/32) → Core ML → feather stitch → TIFF16 + metadata. Measure s/image for 24/45/61 MP on an 8 GB M1 Air (borrow or buy used) and one M3/M4, for `.cpuAndNeuralEngine` vs `.cpuAndGPU` vs `.all`; peak RSS; 50-image sustained run for throttling.
  4. Week 2: quality on the 20 high-ISO photos vs Lightroom Denoise, Topaz trial **and CIRAWFilter RAW 9 on macOS 27**; parity (≥50 dB vs PyTorch), NaN scan, seam check.
  5. Go/no-go criteria (suggested): denoise ≤ 30–45 s per 24 MP on M1 8 GB; no seams/colour shift visible at 100%; visible advantage over RAW 9 on at least JPEG/HEIC inputs; peak memory under ~3 GB.

### Gaps
- No verified data on M1/M2 base-chip timings for the target models; the spike is the only way to close this gap.
- Developer skill level and the actual hours per week behind "medio tiempo" are unknown, and they strongly affect the estimate.
