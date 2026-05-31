# Models Index

Foundation models we build on, and models we train/publish. Trained checkpoints live on the [HF org](https://huggingface.co/golden-retrievers).

> Compiled from a verified SOTA review (2026). **Watch licenses** — several SOTA animal models are non-commercial.

## Models we are building

| Model | Repo · 🤗 | Input → Output | Status |
|---|---|---|---|
| **Disease GWAS** (mixed model) | [gr-cancer-genomics](https://github.com/golden-retrievers/gr-cancer-genomics) | genotypes + phenotype + GRM → per-SNP association | ✅ scaffold, λ=1.025 |
| **Polygenic Risk Score** | [gr-cancer-genomics](https://github.com/golden-retrievers/gr-cancer-genomics) · [🤗 gr-cancer-prs](https://huggingface.co/golden-retrievers/gr-cancer-prs) | genotypes → per-dog risk score | 🚧 next |
| **MIL slide classifier** | [gr-histopathology](https://github.com/golden-retrievers/gr-histopathology) · [🤗](https://huggingface.co/golden-retrievers/gr-histopathology) | tile embeddings → slide grade + heatmap | ✅ built, CCMCT-wired |
| **Mitotic-figure detector** | [gr-histopathology](https://github.com/golden-retrievers/gr-histopathology) | HPF tiles → mitosis boxes/count | 🚧 planned |
| **Multi-modal cancer risk** | [gr-health-multimodal](https://github.com/golden-retrievers/gr-health-multimodal) · [🤗](https://huggingface.co/golden-retrievers/gr-health-multimodal) | genomics+labs+path+behavior → risk + hazard | ✅ architecture built |
| **CV tooling** (pose/seg/re-ID) | [gr-vision-tooling](https://github.com/golden-retrievers/gr-vision-tooling) | image/video → keypoints/masks/embeddings | 🚧 planned |

The sections below catalog the **foundation models we build on** (the SOTA bases).

## Re-identification (individual ID)

| Model | Arch | SOTA notes | License | Source |
|---|---|---|---|---|
| **MiewID** (msv3) | — | Current best multispecies re-ID; 49 species / 37,138 individuals / 225k annotations; **+19.2% top-1 over MegaDescriptor** on 33 unseen species | check repo | [arXiv 2412.05602](https://arxiv.org/html/2412.05602v1) |
| **MegaDescriptor-L-384** | Swin-L (~229M) | First re-ID foundation model; beats CLIP & DINOv2 | **CC-BY-NC-4.0** (non-commercial) | [HF: BVRA](https://huggingface.co/BVRA/MegaDescriptor-L-384) · [WACV'24](https://arxiv.org/abs/2311.09118) |
| DINOv2 / DINOv3 | ViT | Strong general embeddings; re-ID baseline (beaten by above) | varies | — |

## Pose / keypoints

| Model | Notes | Source |
|---|---|---|
| **X-Pose** | Promptable (visual/text) multi-object keypoints; 73.2 AP on AP-10K (+27.7 over ED-Pose); trained on UniKPT | [arXiv 2310.08530](https://arxiv.org/html/2310.08530v2) |
| **SuperAnimal-Quadruped** | Zero-shot quadruped pose (incl. dogs), 39 kpts; DeepLabCut ecosystem | [Nat. Comms](https://pmc.ncbi.nlm.nih.gov/articles/PMC11192880/) |
| ViTPose | Strong ViT pose backbone | — |

## Segmentation

| Model | Notes | Source |
|---|---|---|
| **SAM 2** | Promptable image+video segmentation, streaming memory, real-time; class-agnostic → directly usable on dogs | [arXiv 2408.00714](https://arxiv.org/abs/2408.00714) |

## Action recognition & behavior

| Model / approach | Notes |
|---|---|
| Video transformers (VideoMAE / InternVideo class) fine-tuned on Animal Kingdom | Leading approach for animal multi-label action recognition |

## Video & motion generation

| Model | Notes | Source |
|---|---|---|
| **AniMo** | Species-aware *text-driven animal motion* generation (CVPR'25) — motion, not pixels | [CVPR'25 PDF](https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_AniMo_Species-Aware_Model_for_Text-Driven_Animal_Motion_Generation_CVPR_2025_paper.pdf) |
| Sora-2 / Veo-3 / Runway Gen-4 | General SOTA text/image→video; no animal-specific fine-tunes | [comparison](https://reezo.ai/blog/sora-2-vs-veo-3-vs-runway-gen-4-comparison-2025) |
| SVD / CogVideoX | Open video diffusion bases to fine-tune | — |

## Gaps (build opportunities)

- **No dog-specific or golden-retriever-specific foundation model exists.** Everything above is multi-species.
- No open **dog video-generation** model or **behavior-forecasting** model.
- → Our edge is *specialization*: fine-tune these general models on a dense, GR-specific corpus.
