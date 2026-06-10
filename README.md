# 🦮 Golden Retrievers

**An open effort to understand canine hemangiosarcoma — the deadliest cancer in golden retrievers, and a translational model for human angiosarcoma.**

This is the **hub repository** for the [`golden-retrievers`](https://github.com/golden-retrievers) organization. It holds the dataset index, model index, roadmap, and shared documentation. Large data and trained models live on the linked Hugging Face org: **https://huggingface.co/golden-retrievers**.

> Status: 🚧 Bootstrapping. Currently private. See [ROADMAP.md](ROADMAP.md) for the build-out plan.

## Mission

**Understand hemangiosarcoma (HSA).** A two-pass, adversarially verified literature review showed that for goldens the highest-impact AI work is health/cancer/genomics (cancer causes ~75% of deaths), and that HSA is both the breed's deadliest cancer and a faithful genomic model for the rare human angiosarcoma. Standard care has not improved survival (~4-6 months) in decades and the disease is caught late, so the durable levers are **understanding its biology and genetics** and **translational target discovery** — not generic computer vision. We are therefore focused on building the deepest HSA research corpus and the analyses it enables.

### 🩸 Flagship: understanding HSA

| Focus | Description | Repo |
|------|-------------|------|
| 🩸 Hemangiosarcoma program | Literature/dataset/image corpus + germline GWAS/PRS + variant annotation + knowledge base | **`gr-hemangiosarcoma`** |
| 🔬 Histopathology AI | Tumor histology (HSA + breed-relevant tumors): detection, grading, mitotic figures | `gr-histopathology` |
| 🧩 Multi-modal integration | Fuse genomics + labs + histopath + behavior for HSA biology | `gr-health-multimodal` |

### 👁️ Enabling-CV track (support only)

Consolidated into **`gr-vision-tooling`** (pose→gait, segmentation→body-condition, re-ID→cohort QC) — supporting infrastructure, not a focus.

### Repos
`golden-retrievers` (hub) · **`gr-hemangiosarcoma`** (flagship) · `gr-histopathology` · `gr-health-multimodal` · `gr-vision-tooling`

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
