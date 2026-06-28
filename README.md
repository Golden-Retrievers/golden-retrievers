# 🦮 Golden Retrievers

**An open effort to understand canine hemangiosarcoma — the deadliest cancer in golden retrievers.**

This is the **hub repository** for the [`golden-retrievers`](https://github.com/golden-retrievers) organization. It holds the dataset index, model index, roadmap, and shared documentation. Large data and trained models live on the linked Hugging Face org: **https://huggingface.co/golden-retrievers**.

> Status: 🚧 Bootstrapping. Currently private. See [ROADMAP.md](ROADMAP.md) for the build-out plan.

## Mission

**Understand hemangiosarcoma (HSA).** A two-pass, adversarially verified literature review showed that for goldens the highest-impact AI work is health/cancer/genomics (cancer causes ~75% of deaths), and that HSA is the breed's deadliest cancer. Standard care has not improved survival (~4-6 months) in decades and the disease is caught late, so the durable lever is **understanding its biology and genetics**, not generic computer vision. The whole effort is HSA-only: build the deepest HSA research corpus and the analyses it enables. (HSA is a vascular-endothelial tumor; the human vascular-endothelial cancer is angiosarcoma. We study the canine disease on its own terms and make no translational claims.)

### One flagship repo

All research lives in **[`gr-hemangiosarcoma`](https://github.com/golden-retrievers/gr-hemangiosarcoma)**: the literature/dataset/image corpus, germline GWAS/PRS + variant annotation, the multimodal HSA risk model, the histopathology MIL infrastructure, and the verified knowledge base.

This `golden-retrievers` repo is the **hub**: the dataset index, model index, and roadmap.

### Archived

The earlier satellite repos are **archived** (read-only). Their HSA-relevant work was folded into the flagship: multimodal fusion (was `gr-health-multimodal`) and the attention-MIL histopathology infra (was `gr-histopathology`). `gr-vision-tooling` was general computer vision, off the HSA focus, archived without salvage.

## Where things live

| Surface | Holds | Where |
|---|---|---|
| 🤗 **Hugging Face** | Data + models | datasets [`grls-genomics`](https://huggingface.co/datasets/golden-retrievers/grls-genomics) · [`hsa-literature`](https://huggingface.co/datasets/golden-retrievers/hsa-literature); model [`gr-hsa-prs`](https://huggingface.co/golden-retrievers/gr-hsa-prs) |
| 📊 **Weights & Biases** | Experiments | [wandb.ai/golden-retrievers](https://wandb.ai/golden-retrievers) (`gr-hsa-gwas`, `gr-hsa-prs`), embedded in the [experiments Space](https://huggingface.co/spaces/golden-retrievers/experiments) |
| 🐙 **GitHub** | Code + docs | this org, flagship [`gr-hemangiosarcoma`](https://github.com/golden-retrievers/gr-hemangiosarcoma) |

## Layout

- [`DATASETS.md`](DATASETS.md) — the HSA corpus: GRLS genomics + phenotypes, the literature dataset, with sizes, licenses, and HF links.
- [`MODELS.md`](MODELS.md) — the HSA models we train and the foundation models they build on, with HF links.
- [`ROADMAP.md`](ROADMAP.md) — the phased plan for understanding HSA.

## Links

- 🤗 Hugging Face org (data + models): https://huggingface.co/golden-retrievers
- 🐙 GitHub org (code + docs): https://github.com/golden-retrievers
- 📊 Experiment dashboard (live W&B): https://huggingface.co/spaces/golden-retrievers/experiments — embeds [wandb.ai/golden-retrievers](https://wandb.ai/golden-retrievers)

## Licensing

Code in this org is released under permissive licenses (per-repo `LICENSE`). **Data and model licenses vary by source** — every dataset entry in [`DATASETS.md`](DATASETS.md) records its upstream license, and redistribution follows those terms. Nothing here is veterinary or behavioral advice.
