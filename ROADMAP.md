# Roadmap: Understanding Canine Hemangiosarcoma

Derived from a 2026 literature review ([DATASETS.md](DATASETS.md), [MODELS.md](MODELS.md)) and a two-pass adversarially verified HSA review. The finding that shapes everything:

> **Hemangiosarcoma is the deadliest cancer in golden retrievers, caught late, with no curative therapy in decades, and it is a faithful genomic model for human angiosarcoma. The durable AI lever is understanding its biology and genetics, not detection or generic CV.**

## Current direction

The org is now centered on **understanding hemangiosarcoma**, in a single flagship repo, [`gr-hemangiosarcoma`](https://github.com/golden-retrievers/gr-hemangiosarcoma): the research corpus (papers, datasets, images), the germline GWAS/PRS/variant-annotation pipeline, the multimodal HSA risk model, the histopathology MIL infrastructure, and the verified knowledge base. The earlier satellite repos are archived and their HSA-relevant work was folded in. Generic-CV and early-detection framings are dropped (lead-time bias + HSA lethality make screening low-value).

## Phases

### Phase 0 — Corpus + open genomics (done / in progress)
- [x] Mirror open **GRLS genomics** (CC-BY-SA, `s3://mafgrlsgenome`) → HF dataset `golden-retrievers/grls-genomics` (3,224 dogs, 913,984 SNPs, PLINK/CanFam3).
- [x] PLINK QC + PCA population-structure baseline.
- [x] Build + publish the **HSA literature corpus** (`hsa-literature`, 4,485 papers) and the verified knowledge base (`docs/HSA-KNOWLEDGE.md`).

### Phase 1 — HSA germline genetics (done, open data)
- [x] **Disease GWAS** (GEMMA LMM) for hemangiosarcoma on GRLS (306 cases / 1,329 controls): λ=0.955, h²≈0.13, non-coding signal.
- [x] **Polygenic Risk Score** (clumping+thresholding) + held-out evaluation.
- [x] **Variant annotation**: consequence calls + ESM-2 scoring of missense hits.

### Phase 2 — Multimodal HSA risk (DUA-gated)
- [ ] Apply for / use the **GRLS Data Commons** DUA (CZ Biohub) to unlock phenotypes, labs, behavior.
- [ ] Train the **multimodal fusion model** (`scripts/multimodal_fusion.py`): genomics + labs + behavior + clinical → HSA risk + age-at-onset hazard. Beat the single-modality baselines on PPV/calibration, not AUROC.

### Phase 3 — HSA histopathology (data-gated)
- [ ] Source digitized **HSA whole-slide images** (GRLS necropsy slides, if available under the DUA).
- [ ] Run the attention-MIL pipeline (`scripts/mil_model.py` + `tile_and_embed.py`) on real HSA WSI; feed slide embeddings into the multimodal model.

### Phase 4 — Translational angiosarcoma
- [ ] Cross-map HSA germline/somatic findings to human **angiosarcoma** (shared TP53/PIK3CA, KDR, AXIN1).
- [ ] Publish the corpus, models, and findings; flip releasable assets to public.

## Key constraints
- **Power:** HSA is underpowered at 306–312 GRLS cases; larger multi-cohort HSA case collections are the real bottleneck for genome-wide significance.
- **Data access:** phenotypes/labs/histopath are DUA-gated and non-commercial; keep derived artifacts compliant.
- **Leakage & confounding:** split by dog, fit PCA on train only, control for age/sex/neuter.
