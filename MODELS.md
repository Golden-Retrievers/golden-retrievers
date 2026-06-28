# Models Index

Models we train/publish for the hemangiosarcoma (HSA) program, and the foundation models they build on. Trained checkpoints live on the [HF org](https://huggingface.co/golden-retrievers).

> Compiled from a verified SOTA review (2026). **Watch licenses** — several SOTA bases are non-commercial.

## Models we are building

All HSA models now live in the single flagship repo, [`gr-hemangiosarcoma`](https://github.com/golden-retrievers/gr-hemangiosarcoma).

| Model | Code · 🤗 | Input → Output | Status |
|---|---|---|---|
| **Disease GWAS** (mixed model) | `scripts/run_gwas.py` | genotypes + phenotype + GRM → per-SNP HSA association | ✅ real HSA run, λ=0.955, h²≈0.13 |
| **Polygenic Risk Score** | `scripts/prs.py` · [🤗 gr-hsa-prs](https://huggingface.co/golden-retrievers/gr-hsa-prs) | genotypes → per-dog HSA risk score | ✅ built, AUC 0.635 (sim) |
| **Variant annotation** (ESM-2) | `scripts/annotate_gwas_esm.py` | HSA missense hits → consequence + ESM-2 LLR | ✅ built |
| **Multi-modal HSA risk** | `scripts/multimodal_fusion.py` | genomics+labs+path+behavior → HSA risk + age-at-onset hazard | ✅ architecture built |
| **HSA histopathology MIL** | `scripts/mil_model.py` + `tile_and_embed.py` | tile embeddings → slide label + heatmap | ✅ infra built; awaiting HSA WSI |

## Foundation models we build on

Only the bases the HSA models actually use.

| Model | Used for | License | Source |
|---|---|---|---|
| **ESM-2** | Protein-level effect scores for HSA missense variants (variant annotation) | MIT | [HF: facebook/esm2](https://huggingface.co/facebook/esm2_t33_650M_UR50D) |
| **Pathology FMs** (UNI / UNI2, CONCH, Virchow2, Prov-GigaPath, H-optimus-0) | Frozen tile encoders for the HSA histopathology MIL pipeline | gated, mostly research / non-commercial — check each | [HF: MahmoodLab](https://huggingface.co/MahmoodLab) and others |

## Gaps (build opportunities)

- No **canine HSA histopathology foundation model**; the pipeline relies on human-H&E pathology FMs, and human→dog transfer is an assumption to validate.
- HSA germline signal is **non-coding/regulatory** and underpowered at current case counts; larger multi-cohort HSA collections would change what is learnable.
