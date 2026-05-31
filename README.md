# 🦮 Golden Retrievers

**The world's largest open corpus and model suite for golden retriever computer vision.**

This is the **hub repository** for the [`golden-retrievers`](https://github.com/golden-retrievers) organization. It holds the dataset index, model index, task roadmap, and shared documentation. Large data and trained models live on the linked Hugging Face org: **https://huggingface.co/golden-retrievers**.

> Status: 🚧 Bootstrapping. Currently private. See [ROADMAP.md](ROADMAP.md) for the build-out plan.

## Mission

Build the highest-**impact** golden-retriever AI collection, not just the broadest. A verified literature survey ([`docs/GR-AI-LANDSCAPE.md`](docs/GR-AI-LANDSCAPE.md)) shows the golden-retriever × AI field is dominated by **health, cancer, and genomics** — anchored on the **Golden Retriever Lifetime Study (GRLS)**, where cancer causes ~75% of deaths — while generic computer vision is low-uniqueness for the breed. So we center on health/genomics and treat CV as **enabling tooling**.

### 🩺 Health & genomics track (primary)

| Task | Description | Repo |
|------|-------------|------|
| 🧬 Cancer genomics / GWAS | Disease-risk modeling on GRLS genotypes (3,224 dogs, ~914K SNPs) | `gr-cancer-genomics` |
| 🔬 Histopathology AI | Mast cell tumor / hemangiosarcoma / lymphoma detection & grading | `gr-histopathology` |
| 🧩 Multi-modal cancer risk | Fuse genomics + labs + histopath + behavior (the open opportunity) | `gr-health-multimodal` |

### 👁️ Enabling-CV track (supports the above)

All consolidated into a single repo — **`gr-vision-tooling`** — since CV is now supporting infrastructure, not a set of flagship tasks:

| CV capability | Serves health task |
|------|-----------------|
| 🦴 Pose / keypoints | gait / lameness / orthopedic analysis |
| ✂️ Segmentation | body-condition scoring |
| 🏷️ Classification / re-ID | lost-dog recovery, cohort QC |
| 🏃 Activity / behavior | welfare & working-dog (guide-dog) selection |

(Video generation was dropped as novelty. See [ROADMAP.md](ROADMAP.md) for the phased plan.)

### Repos
`golden-retrievers` (hub) · `gr-cancer-genomics` · `gr-histopathology` · `gr-health-multimodal` · `gr-vision-tooling`

## Layout

- [`DATASETS.md`](DATASETS.md) — index of all source + derived datasets, with sizes, licenses, and HF links.
- [`MODELS.md`](MODELS.md) — index of foundation models we build on and models we train, with HF links.
- [`ROADMAP.md`](ROADMAP.md) — the plan for assembling the corpus and training the model suite.
- `docs/` — data schema, annotation guidelines, licensing notes, evaluation protocol.

## Links

- 🤗 Hugging Face org (data + models): https://huggingface.co/golden-retrievers
- 🐙 GitHub org (code + docs): https://github.com/golden-retrievers
- 📊 Experiment dashboard (live W&B): https://huggingface.co/spaces/golden-retrievers/experiments — embeds [wandb.ai/golden-retrievers](https://wandb.ai/golden-retrievers)

## Licensing

Code in this org is released under permissive licenses (per-repo `LICENSE`). **Data and model licenses vary by source** — every dataset entry in [`DATASETS.md`](DATASETS.md) records its upstream license, and redistribution follows those terms. Nothing here is veterinary or behavioral advice.
