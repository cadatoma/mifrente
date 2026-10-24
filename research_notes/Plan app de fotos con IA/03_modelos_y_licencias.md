# Image restoration models for a closed-source commercial Mac app: licensing, quality and risk (as of 2026-10-24)

Scope: choosing models for denoise, super-resolution and sharpen/deblur, and checking their licenses (code, weights, training data). Core ML conversion and performance belong to another researcher.
Method: I downloaded the LICENSE and README files straight from each repo with `raw.githubusercontent.com` on 2026-10-24, pulled all 671 OpenModelDB model records from its GitHub data repo, and ran web searches and fetches. Some hosts were unreachable from this environment: arxiv.org, the York SIDD site and the ETH DIV2K page. Where that happened, the finding rests on search-result summaries, and it is marked as such.

---

## Q1. Licenses of the plan's four models (code and weights)

### Takeaway
The plan reads the code licenses correctly: SCUNet is Apache-2.0, NAFNet MIT, Real-ESRGAN BSD-3-Clause and SwinIR Apache-2.0. None of these repos has a separate license for the weights. The weights are release assets of the same repos, and in practice they are treated as covered by the repo license. Every one of the four sets of weights was trained on datasets that are research-only or have unclear terms (DIV2K, Flickr2K, OST, SIDD, RENOIR). That training-data question, not the code license, is the real legal risk.

### Cited Findings
- **SCUNet**: the LICENSE is Apache License 2.0, with the boilerplate filled in as "Copyright 2022 Kai Zhang (cskaizhang@gmail.com …). All rights reserved." The repo has no NOTICE file at the root. — [SCUNet LICENSE](https://github.com/cszn/SCUNet/blob/main/LICENSE)
- The SCUNet README says its real-denoise results come from "purely synthetic training data! We did not use the paired noisy/clean data by DND and SIDD during training". Noisy/clean pairs are synthesized from high-quality images through a pipeline with shuffled degradations: Gaussian, Poisson, camera-sensor noise with reverse-forward tone mapping, and JPEG. The README excerpt I fetched does not name the source HQ image set. — [SCUNet README](https://github.com/cszn/SCUNet)
- **NAFNet**: MIT License, "Copyright (c) 2022 megvii-model". The released weights are NAFNet-SIDD-width32/64 (denoise, trained on SIDD), NAFNet-GoPro-width32/64 (deblur, GoPro), NAFNet-REDS-width64 (deblur plus JPEG, REDS) and NAFSSR (stereo SR, Flickr1024). They are hosted on Google Drive and Baidu, and nothing states a weight-specific license. — [NAFNet LICENSE](https://github.com/megvii-research/NAFNet/blob/main/LICENSE); [NAFNet README](https://github.com/megvii-research/NAFNet)
- **Real-ESRGAN**: BSD 3-Clause, "Copyright (c) 2021, Xintao Wang". Clause 2: "Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution." — [Real-ESRGAN LICENSE](https://github.com/xinntao/Real-ESRGAN/blob/master/LICENSE)
- The Real-ESRGAN model zoo lists these weights as GitHub release assets: RealESRGAN_x4plus (v0.1.0), RealESRGAN_x2plus, RealESRNet_x4plus ("MSE loss (over-smooth effects)"), the official ESRGAN_x4 (DF2KOST), and **realesr-general-x4v3** (v0.2.5.0), described as "A tiny small model … not too strong deblur and denoise capacity". A companion **realesr-general-wdn-x4v3** is also released. — [Real-ESRGAN model_zoo.md](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/model_zoo.md)
- Real-ESRGAN training: "We use DF2K (DIV2K and Flickr2K) + OST datasets for our training." Training ran on four GPUs. — [Real-ESRGAN Training.md](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/Training.md)
- OpenModelDB lists 4x-realesr-general-x4v3, 4x-realesr-general-wdn-x4v3, 4x-realesrgan-x4plus and 2x-realesrgan-x2plus as BSD-3-Clause (from the database's `data/models/*.json`). — [OpenModelDB data repo](https://github.com/OpenModelDB/open-model-database)
- **SwinIR**: Apache License 2.0, "Copyright [2021] [SwinIR Authors]", no NOTICE file. Training data per the README: real-world SR SwinIR-M uses DIV2K (800) + Flickr2K (2650) + OST (plus more for SwinIR-L). Real denoising uses SIDD-Medium-sRGB (320 images) + RENOIR (221 images). — [SwinIR LICENSE](https://github.com/JingyunLiang/SwinIR/blob/main/LICENSE); [SwinIR README](https://github.com/JingyunLiang/SwinIR)
- OpenModelDB lists all official SwinIR weights as Apache-2.0: classicalSR DIV2K/DF2K, lightweight, and realSR-BSRGAN-DFO / DFOWMFC GAN. — [OpenModelDB data repo](https://github.com/OpenModelDB/open-model-database)
- The KAIR toolbox (Kai Zhang; it holds many of the SCUNet/SwinIR/BSRGAN training scripts) is MIT, "Copyright (c) 2019 Kai Zhang". — [KAIR LICENSE](https://github.com/cszn/KAIR/blob/master/LICENSE)

### Inferences
- The plan's table is right about the code licenses. "Weights = repo license" is the community convention, and OpenModelDB records it that way, but none of the authors says so explicitly for the weights. A short email asking each author to confirm commercial use of the released weights would be cheap insurance.
- SCUNet has the cleanest training-data story among the denoisers, because it uses synthetic noise and no SIDD/DND pairs. Its HQ source images still need checking (see Gaps).
- NAFNet-SIDD and SwinIR real-denoise weights are trained directly on SIDD, a smartphone dataset whose license I could not verify. They are also tuned to smartphone noise rather than large-sensor camera noise.

### Gaps
- I could not read the SIDD license text: the York University site was unreachable. One third-party aggregator claims "MIT", which is unverified and probably unreliable.
- The README text I fetched does not name SCUNet's HQ training sources. From memory, the paper lists DIV2K, Flickr2K, WED and FFHQ, but I did not verify that here.
- The exact training data for realesr-general-x4v3 is not documented in model_zoo.md. Presumably it is DF2K+OST like the rest of Real-ESRGAN, but that is unconfirmed.

---

## Q2. Legal risk of weights trained on non-commercial datasets (DIV2K, Flickr2K, LSDIR, SIDD, ImageNet, FFHQ)

### Takeaway
No court ruling or authoritative opinion settles whether weights trained on research-only data inherit that restriction. The whole open SR/denoise ecosystem (including the plan's four models and nearly every 2023–2026 model) is trained on DIV2K, Flickr2K, LSDIR or ImageNet, which are research-only or of unclear terms. The risk is therefore systemic and cannot be avoided by picking a different public model. The only full mitigation is to train your own weights on commercially licensed data (Q5).

### Cited Findings
- The DIV2K page says the dataset is for academic research only, and that the images were collected from the internet with copyright held by the original owners. (Search-result summary; the page was unreachable from my environment.) — [DIV2K](https://data.vision.ee.ethz.ch/cvl/DIV2K/)
- A 2026 arXiv paper's license appendix says it found no explicit license for Flickr2K (collected through the Flickr API by the EDSR/NTIRE2017 authors), and describes LSDIR as "made available for academic research purposes only", with copyright kept by the image owners. This is secondhand. — [arXiv 2603.06738](https://arxiv.org/pdf/2603.06738)
- LSDIR's own project page says the HR images were collected from Flickr. — [LSDIR project page](https://data.vision.ee.ethz.ch/yawli/index.html); [LSDIR CVPRW 2023 paper](https://openaccess.thecvf.com/content/CVPR2023W/NTIRE/papers/Li_LSDIR_A_Large_Scale_Dataset_for_Image_Restoration_CVPRW_2023_paper.pdf)
- Re-uploads on Kaggle and Roboflow label DF2K/DIV2K as CC0, MIT or CC-BY-4.0. Those labels are not authoritative and do not override the original terms. — [Kaggle DF2K](https://www.kaggle.com/datasets/anvu1204/df2kdata); [Roboflow DIV2K](https://universe.roboflow.com/asia-pacific-university-rfuyq/div2k-tqfkj)
- An academic licensing study ("Can I use this publicly available dataset to build commercial AI software? Most likely not") concludes that using a non-commercial dataset for commercial purposes is considered a license violation. It classes ImageNet, COCO and VOC as not commercially usable. That is a conclusion about datasets, not a ruling on weights. — [arXiv 2111.02374](https://arxiv.org/pdf/2111.02374)
- Practitioners have not resolved it. A Keras issue asks whether MIT weights trained on ImageNet can be used commercially, given that the weights are "a derivative of the imagenet data", and gets no definitive answer. MXNet maintainers say users are "in the same situation as using pre-trained models from any other deep learning framework". DrivenData competition rules accept permissively licensed external weights. — [Keras #13362](https://github.com/keras-team/keras/issues/13362); [MXNet forum](https://discuss.mxnet.apache.org/t/commercial-use-license-for-pre-trained-models/3343); [DrivenData](https://community.drivendata.org/t/clarification-on-imagenet-pre-trained-weights-under-open-source-commercial-rules/11475)
- Some dataset licenses do bind models explicitly. The Unsplash Full Dataset terms say: "Any machine learning models or algorithms that have been trained with or otherwise processed Non-Commercial Licensed Data must not be used for commercial purposes." — [Unsplash Dataset TERMS.md](https://github.com/unsplash/datasets/blob/master/TERMS.md)
- OpenModelDB's own license guide notes that a model's license does not extend to the upscaled images, which take the license of the original image. — [OpenModelDB licenses](https://openmodeldb.info/docs/licenses)

### Inferences
- Risk ranking, from my own judgment and not legal advice:
  - Low: weights trained on synthetic or own or CC0 data.
  - Low-moderate: DIV2K/Flickr2K/LSDIR-trained weights under Apache/MIT/BSD. The terms are "research only" notices without an explicit model clause; the practice is universal; the realistic plaintiffs are individual Flickr photographers, and the weights do not reproduce their images.
  - Higher: data whose terms explicitly bind derived models (Unsplash Full; LAION-derived SD bases carry their own RAIL terms).
  - Unacceptable: explicitly non-commercial weight licenses (SUPIR, StableSR, InvSR, LED, CC-BY-NC OpenModelDB models).
- A pragmatic path is to ship v1.0 with permissively licensed public weights (accepting the industry-wide data risk), state the training-data provenance in the Acknowledgements, and plan to retrain on owned or commercial data for v1.5 (Q5). That removes the residual risk and also becomes a marketing point ("trained on licensed data").

### Gaps
- I found no court decision or published law-firm analysis specifically on SR/denoise weights trained on DIV2K/LSDIR. A real opinion requires a lawyer.
- The FFHQ license (used by OSEDiff and SeeSR) was not checked in this session. From memory it is CC BY-NC-SA 4.0 for the dataset compilation, with images under various Flickr licenses. Unverified.

---

## Q3. Newer permissively licensed models (2023–2026), including OpenModelDB, NTIRE and diffusion SR

### Takeaway
Several stronger architectures have permissive code licenses: HAT, DAT, SPAN, MambaIR and DiffBIR are Apache-2.0, DRCT and Restormer are MIT. OpenModelDB has about 120 CC-BY-4.0 and 44 CC0 models, including photo-specific modern ones (RealPLKSR, DAT2, ATD, DRCT, SPAN). Diffusion SR splits in two. **SeeSR, OSEDiff and DiffBIR are Apache-2.0** but inherit Stable Diffusion's CreativeML OpenRAIL++-M terms. **SUPIR, StableSR and InvSR are non-commercial and must be excluded.**

### Cited Findings
**Regression/GAN architectures (code license verified from LICENSE files):**
- **HAT** (XPixelGroup): Apache-2.0. Weights include HAT_SRx4_ImageNet-pretrain and Real_HAT_GAN_SRx4(_sharper). Training uses about 20 GB of GPU memory per GPU at batch size 4. — [HAT](https://github.com/XPixelGroup/HAT)
- **DAT** (Zheng Chen): Apache-2.0, trained on DF2K. — [DAT](https://github.com/zhengchen1999/DAT)
- **DRCT** (2024): MIT, "Copyright (c) 2024 Chia-Ming Lee". Real-DRCT-GAN weights trained on DF2K + OST300; ImageNet-pretrained DRCT-XL also released. — [DRCT](https://github.com/ming053l/DRCT)
- **SPAN** (lightweight, NTIRE 2024 efficient SR): Apache-2.0. Its LICENSE/README notes that inherited BasicSR components include code from DFDNet under CC-BY-NC-SA. That code is not needed for SPAN inference, but do not copy those files. — [SPAN](https://github.com/hongyuanyu/SPAN); [SPAN LICENSE/README](https://github.com/hongyuanyu/SPAN/blob/main/LICENSE/README.md)
- **Restormer**: MIT, "Copyright (c) 2022 Syed Waqas Zamir and contributors". — [Restormer](https://github.com/swz30/Restormer)
- **MambaIR / MambaIRv2**: Apache-2.0; weights also on Hugging Face. MambaIR_realDN is trained on SIDD and scores 39.89 dB / 0.960 on SIDD. SR weights are trained on DF2K. — [MambaIR](https://github.com/csguoh/MambaIR)
- **BasicSR** (the training framework behind most of these): Apache-2.0. — [BasicSR](https://github.com/XPixelGroup/BasicSR)
- **neosr** (trainer used by the OpenModelDB community; adds RealPLKSR, MoSR and others): Apache license. — [neosr](https://github.com/neosr-project/neosr)

**OpenModelDB (counted from the 671 model JSONs in the database repo):**
- License mix: CC-BY-NC-SA-4.0 227, CC-BY-4.0 123, WTFPL 73, CC-BY-NC-4.0 53, Apache-2.0 51, CC0-1.0 44, unlicensed/None 27, GPL-3.0 27, MIT 22, CC-BY-SA-4.0 14, BSD-3 9. — [OpenModelDB data repo](https://github.com/OpenModelDB/open-model-database)
- Permissive **photo** models that are strong candidates (license / arch / date / dataset):
  - CC-BY-4.0 by Philip Hofmann (Phhofm/"helaman"):
    - 4x-Nomos2-hq-dat2 (DAT2, 2024-08), 4x-Nomos2-hq-atd (ATD, 2024-09), 4x-Nomos2-hq-drct-l (DRCT-L, 2024-09), 4x-Nomos2-hq-mosr (MoSR, 2024-08)
    - 4x-NomosWebPhoto-RealPLKSR / -atd / -esrgan (2024-05/06)
    - 4x-Nomos2-realplksr-dysample (2024-06)
    - 4x-RealWebPhoto-v4-dat2 / -drct-l (2024-04/05)
    - 1x-DeNoise-realplksr-otf (photo denoise, 2024-08), 1x-DeJPG-realplksr-otf (2024-07)
    - LSDIR-trained 4x-LSDIRplus*/LSDIRDAT (2023)
    - Nomos8k span-otf weak/medium/strong (2023-12)
  - CC0-1.0: 4x-realplksr-gan-pretrain and 4x-realplksr-mssim-pretrain (musl, 2024-05; trained on Nomos-v2); 4x-Rybu (compact, Nomos8k); 4x-Valar (ESRGAN+, 2021, "Hand selected 1471 Raw images from the Adobe-MIT 5K"); 1x-Film-Degrainer.
  - WTFPL: 1x-ISO-denoise v1/v2, 1x-NoiseToner-Poisson(-Detailed), 4x-NMKD-Superscale (2020–21, older ESRGAN).
  — [OpenModelDB data repo](https://github.com/OpenModelDB/open-model-database)
- The 1xDeNoise_realplksr_otf model card reads "License: CC-BY-0.4" (a typo). The database records CC-BY-4.0 and it is aimed at photography. The same typo appears on 4xNomos2_hq_dat2 and 4xNomosWebPhoto_RealPLKSR. — [OpenModelDB 1x-DeNoise-realplksr-otf](https://openmodeldb.info/models/1x-DeNoise-realplksr-otf); [Phhofm release](https://github.com/Phhofm/models/releases/tag/1xDeNoise_realplksr_otf)
- The Nomos-v2 dataset (6000 images, "multipurpose") is distributed through Google Drive in the neosr README with no license or provenance statement. FaceUp is a curated FFHQ and SSDIR a curated LSDIR. — [neosr README](https://github.com/neosr-project/neosr)

**Diffusion-based SR:**
- **SUPIR**: a custom "SUPIR Software License Agreement" from SupPixel Pty Ltd. "the proprietary neural network weights, biases, and architecture may only be used for non-commercial purposes"; commercial use "requires a separate commercial license agreement" (contact jinjin.gu@suppixel.ai). It even defines integrating it "into a commercial product that is sold to end-users" as commercial use. **Excluded** unless licensed. — [SUPIR LICENSE](https://github.com/Fanghua-Yu/SUPIR/blob/master/LICENSE)
- **StableSR**: S-Lab License 1.0, "Redistribution and use for non-commercial purpose". **Excluded.** — [StableSR LICENSE](https://github.com/IceClear/StableSR/blob/main/LICENSE.txt)
- **InvSR** (2025): S-Lab License 1.0, non-commercial. **Excluded.** — [InvSR LICENSE](https://github.com/zsyOAOA/InvSR/blob/master/LICENSE)
- **SeeSR**: "This project and related weights are released under the Apache 2.0 license." It is trained on LSDIR + FFHQ10k, and its DAPE tagger is trained on COCO. It is built on Stable Diffusion 2 base. — [SeeSR](https://github.com/cswry/SeeSR)
- **OSEDiff** (one-step diffusion SR, NeurIPS 2024): the README says Apache 2.0 (I found no LICENSE file at the root). It is trained on LSDIR (84,991) + the first 10k FFHQ images. Inference is "0.1046 seconds" per iteration on an A100. Reported RealSR metrics include PSNR 25.15, LPIPS 0.292 and MUSIQ 69.09. — [OSEDiff](https://github.com/cswry/OSEDiff)
- **DiffBIR**: Apache-2.0. v2.1 is "IRControlNet trained on filtered unsplash" with LLaVA captions, v2 is trained on filtered laion2b-en, v1 on ImageNet-1k. — [DiffBIR](https://github.com/XPixelGroup/DiffBIR)
- The Stable Diffusion 2.1 weights (the base for SeeSR/OSEDiff-type models) are under the CreativeML Open RAIL++-M License. Stability warns against product use "without additional safety mechanisms and considerations". — [SD 2.x release notes mirror](https://gitee.com/lining_it/stablediffusion)

**NTIRE challenges:**
- NTIRE 2025 SR x4: the SamsungAICamera team won the restoration track with 33.46 dB by combining a pre-trained HAT with NAFNet; SNUCV led the perceptual track. Official training sets are DIV2K, Flickr2K and LSDIR. — [NTIRE 2025 SR report, arXiv 2504.14582](https://arxiv.org/abs/2504.14582)
- NTIRE 2026 denoising (Gaussian σ=50, sRGB): 20 finalist teams. BuptMM was 1st at 29.90 dB, with the top four within 0.03 dB. The test set is DIV2K + LSDIR. At least one team used a revisited Restormer with x8 self-ensemble. The winners' licenses are unknown. — [NTIRE 2026 denoise report, arXiv 2606.16031](https://arxiv.org/abs/2606.16031) (via search summary)
- Other related reports exist: NTIRE 2026 "Mobile Real-World Image SR" and NTIRE 2025 RAIM (Restore Any Image Model in the wild). — [arXiv 2604.17306](https://arxiv.org/abs/2604.17306); [arXiv 2506.01394](https://arxiv.org/abs/2506.01394)

### Inferences
- The best permissive SR upgrade over the plan's 2021–22 picks is probably:
  - **High quality**: DAT2/DRCT-L/ATD-class models. Either the official Apache/MIT weights (which are bicubic-trained, so poor on real photos) or, better, Phhofm's CC-BY-4.0 *real-degradation photo* fine-tunes (4xNomos2_hq_dat2, 4xNomosWebPhoto_RealPLKSR).
  - **Fast**: RealPLKSR or SPAN, which are much lighter than SwinIR and handle real degradations, instead of realesr-general-x4v3.
- CC-BY-4.0 permits commercial closed-source use but requires attribution and a note of modifications; Core ML conversion and fp16 quantization are arguably modifications. The training data behind those models (Nomos-v2) has undocumented provenance.
- NTIRE winners are mostly ensembles of HAT/Restormer/NAFNet trained on DIV2K/LSDIR, tuned for PSNR on synthetic degradations. They are not directly useful for real high-ISO camera files, and often too heavy.
- Diffusion SR on-device: OSEDiff/SeeSR are licensable in principle (Apache plus OpenRAIL++-M use restrictions, which bar harmful uses but allow commercial use). Still, an SD-2-sized UNet+VAE on 45 MP photos on M1-class Macs would be slow, and they hallucinate texture. That suits an optional "Creative/Generative" mode in v2, not the v1.0 core.

### Gaps
- I did not check the licenses of MambaIRv2 HF weights, ATD, RealPLKSR/MoSR arch code repos, HMA, or newer 2025–26 SR models such as one-step diffusion distillations beyond OSEDiff.
- I could not identify any NTIRE 2025/2026 winner with a released, permissively licensed photo model.
- I did not verify per-image runtimes for SeeSR, SUPIR and DiffBIR against OSEDiff from a primary source.

---

## Q4. RAW-domain denoising: advantage, licenses, and what DxO/Adobe do

### Takeaway
The market leaders denoise in the RAW/mosaic domain, jointly with demosaicing. DxO DeepPRIME is joint demosaic+denoise. Adobe Denoise is trained on raw data and outputs a linear DNG. Apple's own RAW 9 (Core Image, OS 27) now does the same with a Core ML model. The research literature agrees that denoisers perform better in raw space. An sRGB-only denoiser (the plan's approach) will be at a structural disadvantage on high-ISO RAW. Permissive RAW code exists (PMRID Apache-2.0, SID MIT, ELD MIT), but there are few good, permissively licensed raw weights for modern cameras, so this is where own training pays off most.

### Cited Findings
- DxO: DeepPRIME runs demosaicing and denoising in one pass. DxO says that historically "whichever process is performed first will potentially undermine the quality of the second". DxO claims "two stops" of ISO gain for DeepPRIME and up to three for XD2s (vendor claim). — [DxO DeepPRIME](https://www.dxo.com/technology/deepprime-photolab/); [DxO demosaicing](https://www.dxo.com/en/technology/demosaicing/)
- Adobe: Denoise is the third Enhance feature, after Raw Details and Super Resolution. Adobe "continued to train directly from the raw data, which enables us to optimize the end-to-end quality", used dark frames for shadow pattern noise, and targets NVIDIA TensorCores and the Apple Neural Engine. — [Adobe blog, "Denoise demystified" (2023)](https://blog.adobe.com/en/publish/2023/04/18/denoise-demystified)
- Adobe Denoise works only on Bayer and X-Trans mosaic raw, linear DNG and ProRAW, and outputs a new "-Enhanced.dng". — [Adobe Help: Enhance](https://helpx.adobe.com/uk/lightroom/desktop/edit-photos/enhance-details.html)
- NTIRE 2020: "image denoisers tend to perform better in the rawRGB color space than in the sRGB color space". — [NTIRE 2020 Real Image Denoising report](https://arxiv.org/pdf/2005.04117)
- SIDD: noisy-input PSNRs differ hugely between domains (raw 36.70 dB vs sRGB 19.71 dB baseline), so PSNRs across domains are not comparable. — [SIDD CVPR 2018 paper](https://openaccess.thecvf.com/content_cvpr_2018/papers/Abdelhamed_A_High-Quality_Denoising_CVPR_2018_paper.pdf)
- Apple RAW 9 (WWDC26 session 305): "a tiled CoreML model, that combines demosaic with denoise for best quality … run on device using the Apple Neural Engine". It ships in iOS/iPadOS/macOS/visionOS 27, is opt-in through `CIRAWFilter.decoderVersion = .version9`, and supports "hundreds" of camera models. — [WWDC26 "Enhance RAW image processing with Core Image"](https://developer.apple.com/videos/play/wwdc2026/305/)
- Permissive RAW-denoise code and data:
  - **PMRID** (Megvii, ECCV 2020, "Practical Deep Raw Image Denoising on Mobile Devices"): Apache-2.0, with a released raw benchmark dataset. — [PMRID](https://github.com/megvii-research/PMRID)
  - **Learning-to-See-in-the-Dark** (SID): code under MIT; the Sony/Fuji raw datasets are downloadable (the README does not state a dataset license separately). — [SID](https://github.com/cchen156/Learning-to-See-in-the-Dark)
  - **ELD** (physics-based noise model; synthetic-only training "can compete with or sometimes even outperform" real paired data in extreme low light): MIT; the ELD dataset is "for evaluation purposes only". It releases calibrated camera noise parameters and code. — [ELD](https://github.com/Vandermode/ELD)
  - **LED** (ICCV 2023 few-shot raw denoising): **CC BY-NC 4.0**, "any commercial use … requires formal permission". **Excluded.** — [LED](https://github.com/Srameo/LED)
- Independent and single-photographer tests: DxO DeepPRIME XD2 gives slightly more feather detail than DeepPRIME 3, and Lightroom Denoise was the tester's second-best. XD2 takes about 11 s on GPU and about 125 s on CPU per image. — [Todd Marsh, DxO vs Lightroom](https://toddmarsh.com/dxo-pureraw-vs-lightroom-ai-denoise-high-iso/)

### Inferences
- For a "serious" RAW workflow the plan has two options:
  - **(a)** Use Apple RAW 9 as the demosaic+denoise front-end. It is free, on the ANE and legally clean, but only on macOS 27+ and only for supported cameras. Then apply the app's own SR/sharpen on the linear or sRGB result.
  - **(b)** Train a small raw-domain joint demosaic+denoise network, for example a PMRID/NAFNet-style U-Net on packed 4-channel Bayer, using the ELD-style calibrated noise synthesis on clean low-ISO raws the developer owns (Q5).
  
  Option (b) is the only way to truly match DxO/Adobe and own the weights. X-Trans (Fujifilm) needs separate handling.
- sRGB denoise (SCUNet/NAFNet) is still competitive for JPEG/HEIC input and as a fallback. On RAW it denoises *after* demosaic and tone curve, where noise is spatially correlated and signal-dependent in complex ways. It will likely trail Lightroom/DxO at ISO 6400+ in fine-detail retention (inference; no head-to-head benchmark found).
- Product consequence: if the plan keeps "RAW input" in v1.0, the realistic quality target is "near Lightroom" through RAW 9 + sRGB polishing, not "beats DxO".

### Gaps
- I found no published head-to-head of SCUNet/NAFNet (sRGB) vs DxO/Lightroom/RAW 9 on the same high-ISO camera RAWs. The developer needs to run this in the week-2 test.
- Apple has not published quantitative quality or speed for RAW 9, nor the exact list of supported cameras.
- The SID dataset license was not found.

---

## Q5. Training or fine-tuning your own weights: feasibility, cost, commercial data

### Takeaway
Owning the weights is feasible and moderately cheap, because the leading denoisers (SCUNet, ELD) already show that **synthetic noise on clean images** works. Fine-tuning a Real-ESRGAN/SPAN/RealPLKSR-class model runs on 1–4 consumer or cloud GPUs. The binding constraint is a commercially licensed set of clean high-quality images (and clean low-ISO raws for a raw model). Unsplash Lite is the only large public "commercial" option found, and its terms are restrictive.

### Cited Findings
- SCUNet reaches its real-denoise results with "purely synthetic training data" and no SIDD/DND. — [SCUNet](https://github.com/cszn/SCUNet)
- ELD: training only on synthetic data from a physics-based noise model "can compete with or sometimes even outperform the network trained with paired real data". The release includes calibrated noise parameters and a modern EMoR radiometric calibration. — [ELD](https://github.com/Vandermode/ELD)
- Real-ESRGAN provides an official guide for fine-tuning on your own dataset. The authors trained on four GPUs; single-GPU training is supported. — [Real-ESRGAN Training.md](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/Training.md)
- HAT training uses about 20 GB per GPU at batch size 4. — [HAT](https://github.com/XPixelGroup/HAT)
- Community photo models document their recipes. 4xNomosWebPhoto_RealPLKSR: 6000-image dataset, CC0 RealPLKSR GAN pretrain, 404k + 445k iterations, batch 12 then 4, GT 128/256/512. — [OpenModelDB record](https://github.com/OpenModelDB/open-model-database); [Phhofm release](https://github.com/Phhofm/models/releases/tag/4xNomosWebPhoto_RealPLKSR)
- CC0 pretrains exist that can be fine-tuned on your own data with no attribution duty: 4x-realplksr-gan-pretrain and 4x-realplksr-mssim-pretrain (musl, CC0-1.0). Their training data is Nomos-v2, whose provenance is undocumented. — [OpenModelDB record](https://github.com/OpenModelDB/open-model-database)
- Unsplash Lite (~25k photos) is "available for commercial and noncommercial usage". The licence, though, is to "internally use the Commercial Licensed Data to train machine learning models or algorithms for your internal business purposes". It forbids redistributing the data and requires indemnifying Unsplash for claims arising from "use of any machine learning models … trained with" the data. The Full dataset is non-commercial, and models trained on it "must not be used for commercial purposes". — [Unsplash TERMS.md](https://github.com/unsplash/datasets/blob/master/TERMS.md); [Unsplash datasets README](https://github.com/unsplash/datasets)
- DiffBIR v2.1 was trained on "filtered unsplash"; it does not say whether Lite or Full. — [DiffBIR](https://github.com/XPixelGroup/DiffBIR)

### Inferences
- Rough compute (my estimates, not sourced): fine-tuning a compact SR model (SPAN/RealPLKSR/Compact, under 1–5M parameters) from a CC0 pretrain takes about 1–3 days on one 24 GB GPU, roughly 25–75 GPU-hours, or about $15–$150 on rented RTX 4090/A100 at about $0.5–2 per hour. Training a SCUNet- or NAFNet-sized sRGB denoiser from scratch with synthetic noise is similar, about 50–150 GPU-hours. A raw-domain U-Net à la PMRID is smaller and cheaper. Large transformers (DAT-L/HAT-L/DRCT-L) from scratch need several hundred GPU-hours. Diffusion SR fine-tuning (SeeSR/OSEDiff) needs multiple A100s for days, which is out of scope for an MVP.
- Best data sources for owned weights:
  1. The developer's own photos plus photos from beta photographers, under a written license/assignment. For raw, a few hundred clean base-ISO raws per sensor family is enough for synthetic-noise training. Shooting the same scene at base ISO and high ISO on a tripod gives real pairs for validation.
  2. Commercially licensed stock bought with an explicit ML-training clause.
  3. Wikimedia Commons / Openverse images filtered to CC0/public domain. CC-BY works too, but attribution at scale is impractical.
  4. Unsplash Lite only after a lawyer confirms that shipping a model inside a sold app counts as "internal business purposes". It reads ambiguous to restrictive.
- Generating degradations is code and needs no license: Real-ESRGAN/BSRGAN second-order pipelines, SCUNet's shuffle pipeline, ELD calibrated raw noise. Starting from a CC0 pretrain (realplksr) or from scratch avoids inheriting third-party weights.

### Gaps
- I found no published GPU-hour figures for SCUNet, NAFNet or RealPLKSR training. The estimates above are inferences.
- I did not check the Wikimedia/Openverse filtering tools or the license of specific raw datasets with commercial terms (RAISE and MIT-Adobe FiveK are, to my knowledge, research-only; not verified here).

---

## Q6. Quality evidence: benchmarks, comparisons with commercial tools, known artifacts

### Takeaway
Benchmark numbers exist for synthetic or smartphone data: SIDD sRGB is NAFNet 40.30 dB, MambaIR 39.89 dB, and per the paper Restormer about 40.02 dB. They say little about large-sensor high-ISO RAW. No rigorous public comparison of open models against Topaz, DxO or Lightroom was found. Known failure modes are oversmoothing (MSE/L1 models), "painted" GAN textures (Real-ESRGAN family), and hallucinated detail and faces (diffusion).

### Cited Findings
- NAFNet SIDD: width64 40.3045 dB, width32 39.9672 dB. GoPro deblur: width64 33.7103 dB. — [NAFNet README](https://github.com/megvii-research/NAFNet)
- MambaIR_realDN on SIDD: 39.89 dB / 0.960. — [MambaIR](https://github.com/csguoh/MambaIR)
- Real-ESRGAN's own model zoo flags RealESRNet_x4plus (MSE loss) for "over-smooth effects", and says realesr-general-x4v3 has "not too strong deblur and denoise capacity". — [Real-ESRGAN model zoo](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/model_zoo.md)
- OSEDiff on the RealSR and DRealSR benchmarks: PSNR 25.15 / LPIPS 0.292 / MUSIQ 69.09, and PSNR 27.92 / LPIPS 0.297 / MUSIQ 64.65. Perceptual quality is high but fidelity (PSNR) low, the usual sign of generated detail. — [OSEDiff README](https://github.com/cswry/OSEDiff)
- NTIRE 2025 SR top fidelity is 33.46 dB (x4, synthetic bicubic degradation), and the winning recipe was HAT + NAFNet. — [NTIRE 2025 SR report](https://arxiv.org/abs/2504.14582)
- Commercial-tool tests are mostly vendor material or single-photographer blogs. One found DxO XD2 slightly ahead and Lightroom second. Another found DeepPRIME handled DJI drone RAWs better than Lightroom's AI denoise. — [Todd Marsh](https://toddmarsh.com/dxo-pureraw-vs-lightroom-ai-denoise-high-iso/); [Neukamp](https://neukamp.de/en/deepprime-xd2s-in-dxo-photolab-8-2/)

### Inferences
- PSNR on SIDD sRGB has saturated (about 40 dB) and does not predict a model's behaviour on full-frame ISO 12,800 RAWs. The developer's own 20-photo A/B test is the real decision tool. Add blind ratings by 5–10 photographers and no-reference IQA (MUSIQ, CLIP-IQA, MANIQA through the IQA-PyTorch toolbox) as a secondary signal.
- Expected artifacts:
  - SCUNet/NAFNet: waxy skin and loss of fine texture at high strength. Mitigate with the plan's blend slider and by re-injecting a little grain.
  - GAN SR: over-sharpened edges, "painterly" foliage and text distortion.
  - Diffusion SR: invented detail, altered faces and text, unacceptable for event and wedding documentation without user control.
- Faces are a known weak point for all general models. CodeFormer is excluded (NC), and the plan already defers face retouching.

### Gaps
- I found no rigorous public benchmark comparing open models (SCUNet, NAFNet, Real-ESRGAN, HAT) with Topaz Photo AI, DxO or Lightroom on the same files.
- I found no published SCUNet SIDD/DND scores in what I fetched, and could not confirm the Restormer SIDD score (about 40.02 dB) from its README in this session.

---

## Q7. Apple-provided options (Core Image, CIRAWFilter, MetalFX, Vision)

### Takeaway
**CIRAWFilter with RAW 9 (OS 27)** is a high-value, free, legally clean neural demosaic+denoise for RAW files, and the best baseline or front-end available. The older CIRAWFilter NR is pyramid-based, not ML. **MetalFX** denoised upscaling is built for real-time ray-traced rendering with auxiliary buffers, not for photos. I found no public Vision/Core Image super-resolution API.

### Cited Findings
- RAW 9: "combines demosaic with denoise … Apple Neural Engine". It is not enabled by default; opt in through `supportedDecoderVersions` containing `.version9`, then set `decoderVersion`. `luminanceNoiseReductionAmount`, `sharpnessAmount`, `contrastAmount` and `exposure` remain. `colorNoiseReductionAmount` has no effect because the model handles color noise, and `detailAmount`/`moireReductionAmount` are not supported. It "runs the CoreML model hundreds of times per image" (it is tiled) and needs memory tuning (`memoryLimit` 512–1024 MB, `cacheIntermediates` false for export). The camera list grows through OS updates; native-DNG cameras are supported automatically. — [WWDC26 session 305](https://developer.apple.com/videos/play/wwdc2026/305/)
- Legacy CIRAWFilter noise reduction "uses a pyramid-based algorithm" (Apple forum reply). — [Apple Developer Forums, Core Image](https://developer.apple.com/forums/tags/core-image?page=2)
- `luminanceNoiseReductionAmount` is documented only as the amount of NR applied to luminance. — [Apple docs](https://developer.apple.com/documentation/coreimage/cirawfilteroption/luminancenoisereductionamount)
- MetalFX denoised upscaler (WWDC25): presented as a companion to Metal 4 ray tracing, to render fewer rays and clean up the noise. WWDC26 session 359 describes "MetalFX Denoising" as a combined neural upscaler/denoiser taking auxiliary inputs (diffuse albedo, depth) with a denoise-strength mask. — [WWDC25 session 211](https://developer.apple.com/videos/play/wwdc2025/211/); [WWDC26 session 359](https://developer.apple.com/videos/play/wwdc2026/359/); [Apple forum thread](https://developer.apple.com/forums/thread/790642)

### Inferences
- Recommended use: RAW 9 as the default RAW decode/denoise on macOS 27+ when the camera is supported, with the app's own models as the fallback or extra step. A hard question for product positioning: Apple's free RAW 9 shrinks the denoise advantage of a $59 app for RAW shooters, so the app should differentiate on SR, batch workflow and JPEG/HEIC denoise.
- The plan targets macOS 14+. RAW 9 needs macOS 27, so it can only be an opportunistic path. The app still needs its own model for macOS 14–26 and for unsupported cameras.
- MetalFX is not usable for still photos without G-buffers (inference from the API design). Core Image's `CINoiseReduction` and Lanczos scaling remain usable as "classic" fallbacks or quick previews.

### Gaps
- I did not confirm whether macOS 26 or 27 exposes any public ML super-resolution API (for example in Vision or Core Image). None was found in the searches.
- RAW 9 quality and speed numbers and the camera list are not published.

---

## Q8. Attribution obligations and how to present them in-app

### Takeaway
All permissive options fit a closed-source app, provided you ship a **"Acknowledgements / Open-source licenses"** screen (plus a text file in the bundle) that reproduces each license text and copyright line. CC-BY-4.0 models additionally need the creator credit, a link to the license, and a note that the model was modified (converted/quantized). Never imply endorsement (BSD-3 clause 3).

### Cited Findings
- BSD-3 (Real-ESRGAN): binary redistributions "must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution". Clause 3 bars using the authors' names to endorse the product without permission. — [Real-ESRGAN LICENSE](https://github.com/xinntao/Real-ESRGAN/blob/master/LICENSE)
- Apache-2.0 (SCUNet, SwinIR, HAT, DAT, SPAN, MambaIR, SeeSR, OSEDiff, DiffBIR, BasicSR, PMRID): Section 4 requires giving recipients a copy of the license, marking modified files, retaining notices, and including a NOTICE file's attributions if one exists. None of SCUNet, SwinIR, HAT, DAT, SPAN, MambaIR, SeeSR, OSEDiff, BasicSR or PMRID has a NOTICE file at the repo root (checked 2026-10-24). Copyright lines to reproduce: "Copyright 2022 Kai Zhang" (SCUNet) and "Copyright [2021] [SwinIR Authors]" (SwinIR). — [SCUNet LICENSE](https://github.com/cszn/SCUNet/blob/main/LICENSE); [SwinIR LICENSE](https://github.com/JingyunLiang/SwinIR/blob/main/LICENSE)
- MIT (NAFNet "Copyright (c) 2022 megvii-model"; Restormer; DRCT; KAIR; SID; ELD): the copyright and permission notice must be included in all copies or substantial portions. — [NAFNet LICENSE](https://github.com/megvii-research/NAFNet/blob/main/LICENSE); [Restormer LICENSE](https://github.com/swz30/Restormer/blob/main/LICENSE.md); [DRCT LICENSE](https://github.com/ming053l/DRCT/blob/main/LICENSE)
- CC0 is "public domain … no restrictions, conditions, or obligations". The model license does not extend to output images. — [OpenModelDB licenses](https://openmodeldb.info/docs/licenses)
- RAIL-family terms (SD 2.x OpenRAIL++-M behind SeeSR/OSEDiff) carry use-based restrictions that must be passed downstream. — [SD 2.x release notes mirror](https://gitee.com/lining_it/stablediffusion)

### Inferences
- Implementation:
  - Add `Acknowledgements.rtf` (or a SwiftUI list) under the app menu → "Acknowledgements…", also linked from Help and the website.
  - Each entry: model name, role (Denoise/Upscale), authors, copyright line, license name with full text, source URL, a "converted to Core ML and quantized to FP16" note for CC-BY and Apache "modified" marking, and optionally the paper citation.
  - Also include licenses for Python-side tools only if their code ships in the app; coremltools output itself carries no license obligation.
  - If any RAIL-based model ships, put its use restrictions in the EULA.
- Keep a `models/LICENSES/` folder in the repo with the original LICENSE file and a SHA-256 of each shipped weight file, as provenance evidence.

### Gaps
- I did not verify whether any weight file has its own embedded license metadata. I did not check the Mac App Store's specific guidance on open-source attributions; none is known to be required beyond the licenses themselves.

---

## Q9. Recommended shortlist per task and risk assessment

### Takeaway
For v1.0 keep the plan's legally clean core, adjusted on several points:
- **Denoise:** SCUNet (Apache) as the main sRGB denoiser, with NAFNet-SIDD (MIT) as an alternative. Add Apple RAW 9 as the RAW path on macOS 27+.
- **Super-resolution:** replace SwinIR with a modern real-degradation model. Phhofm's CC-BY-4.0 RealPLKSR/DAT2 photo models work as-is; to own the weights, fine-tune the CC0 RealPLKSR pretrain yourself. Keep realesr-general-x4v3 (BSD-3) only as a "fast" mode.
- **Sharpen/deblur:** NAFNet-GoPro (MIT) at low blend.

Exclude SUPIR, StableSR, InvSR, LED, CodeFormer and every CC-BY-NC(-SA) model. Plan a v1.5 retrain on owned data, and especially a raw-domain denoiser.

### Cited Findings
- Licenses as verified above: SCUNet Apache-2.0; NAFNet MIT; Real-ESRGAN BSD-3; SwinIR, HAT, DAT and SPAN Apache-2.0; DRCT and Restormer MIT; OpenModelDB Phhofm photo models CC-BY-4.0; realplksr pretrains CC0; SUPIR proprietary NC; StableSR and InvSR S-Lab NC; LED CC-BY-NC. — [SCUNet](https://github.com/cszn/SCUNet), [NAFNet](https://github.com/megvii-research/NAFNet), [Real-ESRGAN](https://github.com/xinntao/Real-ESRGAN), [SwinIR](https://github.com/JingyunLiang/SwinIR), [HAT](https://github.com/XPixelGroup/HAT), [DAT](https://github.com/zhengchen1999/DAT), [SPAN](https://github.com/hongyuanyu/SPAN), [DRCT](https://github.com/ming053l/DRCT), [Restormer](https://github.com/swz30/Restormer), [OpenModelDB data](https://github.com/OpenModelDB/open-model-database), [SUPIR](https://github.com/Fanghua-Yu/SUPIR/blob/master/LICENSE), [StableSR](https://github.com/IceClear/StableSR/blob/main/LICENSE.txt), [InvSR](https://github.com/zsyOAOA/InvSR/blob/master/LICENSE), [LED](https://github.com/Srameo/LED)
- Competitors operate on raw (DxO joint demosaic+denoise; Adobe trained on raw; Apple RAW 9 Core ML). — [DxO](https://www.dxo.com/en/technology/demosaicing/), [Adobe](https://blog.adobe.com/en/publish/2023/04/18/denoise-demystified), [WWDC26-305](https://developer.apple.com/videos/play/wwdc2026/305/)

### Inferences

**Shortlist (v1.0):**

| Task | Primary | Alternative / fast | License (code / weights) | Training-data caveat | Risk |
|---|---|---|---|---|---|
| Denoise, RAW input | Apple CIRAWFilter RAW 9 (macOS 27+, supported cameras) | SCUNet on the decoded image | Apple OS API | none for the developer | Low (OS-version gating) |
| Denoise, sRGB/JPEG/HEIC and fallback | SCUNet (real, blind) | NAFNet-SIDD-w32/64; Phhofm 1xDeNoise_realplksr_otf (CC-BY-4.0, light) | Apache-2.0 / MIT / CC-BY-4.0 | SCUNet synthetic noise on HQ images (source not verified); NAFNet SIDD (license unverified); Nomos-v2 unknown | Low–moderate |
| Upscale "High quality" 2x/4x | Phhofm 4xNomos2_hq_dat2 or 4xNomosWebPhoto_RealPLKSR | Official DAT/DRCT/HAT weights (bicubic-trained, weaker on real photos); SwinIR-realSR GAN | CC-BY-4.0 / Apache / MIT | Nomos-v2 provenance unknown; DF2K/ImageNet research-only | Moderate (attribution plus data provenance) |
| Upscale "Fast" | realesr-general-x4v3 (and -wdn) | SPAN-class (Apache arch) or Nomos8k-span-otf (CC-BY-4.0) | BSD-3 / Apache / CC-BY-4.0 | DF2K+OST | Low–moderate |
| Sharpen/deblur (light) | NAFNet-GoPro-w32 at low blend | Restormer (MIT) motion deblur | MIT | GoPro dataset (license not checked) | Low–moderate |
| Generative "creative" upscale (v2 only) | OSEDiff (one-step) | SeeSR / DiffBIR | Apache-2.0 + SD2 OpenRAIL++-M | LSDIR, FFHQ (likely NC), LAION/Unsplash | Moderate–high; heavy on-device |
| Never ship | SUPIR, StableSR, InvSR, LED, CodeFormer, 4x-UltraSharp/Remacri (CC-BY-NC-SA) | — | Non-commercial | — | Unacceptable |

**Risk assessment:**
1. *Training-data inheritance* (all public weights): moderate likelihood of being questioned and low likelihood of enforcement, but unavoidable without your own training. Mitigation: document provenance, then retrain on owned or CC0 data for v1.5 starting from the CC0 RealPLKSR pretrain or from scratch.
2. *Quality vs DxO/Adobe on high-ISO RAW*: high. sRGB models are structurally disadvantaged. Mitigation: RAW 9 on macOS 27, plus a raw-domain model trained with ELD-style synthetic noise, which is the biggest quality lever.
3. *Attribution/CC-BY compliance*: low if the Acknowledgements screen is done properly.
4. *Supply-chain mislabeling*: OpenModelDB cards have typos (e.g. "CC-BY-0.4"), and weights are hosted on Google Drive with no license. Mitigation: archive the license, release page and SHA-256 of each weight at the time of download.
5. *Apple competition*: RAW 9 gives every Mac app free ML raw denoise from macOS 27, which shrinks differentiation. Pivot the value proposition to SR, batch processing and JPEG/HEIC denoise.

### Gaps
- No side-by-side visual test of the proposed shortlist against Topaz, DxO or Lightroom exists in public sources. The developer's week-2 test must cover it.
- The licenses of the GoPro, REDS and FFHQ datasets were not verified in this session.
