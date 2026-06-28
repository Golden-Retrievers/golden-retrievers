# Datasets Index

Index of the datasets the hemangiosarcoma (HSA) work builds on, plus derived datasets we publish. Derived datasets live on the [HF org](https://huggingface.co/golden-retrievers). **Always check the upstream license before redistributing.**

> Compiled from a verified SOTA review (2026). Every row's figures were adversarially fact-checked against primary sources.

## The cohort

| Resource | Content | Notes |
|---|---|---|
| **Morris Animal Foundation, Golden Retriever Lifetime Study (GRLS)** | Longitudinal health/behavior data on ~3,000 goldens | The richest GR-specific cohort; the anchor for all HSA genomics + multimodal work | [data commons](https://datacommons.morrisanimalfoundation.org/data-roadmap) |

## GRLS genomics + phenotypes (the HSA corpus)

The HSA genomics + multimodal work is anchored on the GRLS cohort: **genotypes** (public, no login) plus **phenotype/clinical tables** (DUA-gated). Genotypes live on Hugging Face; phenotype tables are staged locally under `gr-hemangiosarcoma/data/datacommons/` (git-ignored under the DUA, not redistributed).

### Genotypes (public)

| Dataset | Size | License | Source |
|---|---|---|---|
| **GRLS Axiom HD genotyping** | ~1.1M markers (913,984 after release QC), 3,224 dogs (3,024 GRLS + 200 Golden Oldies), CanFam3/PLINK | CC-BY-SA | AWS Open Data `s3://mafgrlsgenome` (`aws s3 ls --no-sign-request`); [registry](https://registry.opendata.aws/maf-genome) · mirror `hf.co/golden-retrievers/grls-genomics` |

### Phenotype / clinical tables (DUA-gated; 37 CSVs across 24 datasets)

All key on `subject_id` = the genotype `.fam` IID (the public `grls…` ID), a **direct join to genotypes**; the lone exception is `atopic_dermatitis_questionnaire` (keys on the MAF-internal `094-…` form + carries a `public_id` column). Core cohort tables cover all 3,044 GRLS dogs, **3,024 of them genotyped**. Only the HSA-relevant roles are listed below.

| Table(s) | Rows | Dogs w/geno | Role in the HSA models |
|---|---|---|---|
| **`study_endpoints`** | 1,247 | 1,034 | **Adjudicated cancer endpoints** (`tracked_condition`, `tier_of_confidence`, `is_cause_of_death`, `is_recurrence`). HSA GWAS/PRS labels: hemangiosarcoma ~312 cases |
| **`conditions_summary`** + per-system `conditions_*` | 54,792 ea. | 3,024 | Per dog×year diagnosis flags; `summary.neoplasia` 0/1 = broad cancer flag used to define clean (cancer-free) GWAS controls for HSA |
| **`clinical_labs`** | 1.44M | 3,024 | Long-format labs (`test_group`/`test_name`/`test_value`/`ref_range`) → multimodal `labs-GRU` modality |
| **`dog_profile`** | 3,044 | 3,024 | Signalment + survival: `sex_status`, `birth_date`, `death_date`, `is_euthanized`, `spay_neuter_date`, `study_status` → covariates + censoring for age-at-HSA-onset |
| `exam_physical` | 20,973 | 3,024 | Weight, BCS, vitals → clinical modality covariates |
| `medications`, `over_the_counter_medications`, `supplements`, `flea_tick_heartworm`, `vaccines` | 49k–52k | ~3,024 | Treatment/exposure covariates + confounders |
| `environment_*` (7), `poison_exposure`, `location_history`, `lifestyle` | varies | ~3,024 | Environmental / GxE HSA risk factors |
| `activity_*` (4) | 8k–26k | ~3,024 | Activity/lifestyle → behavior modality |

> Build an HSA GWAS phenotype with `gr-hemangiosarcoma/scripts/prepare_phenotypes.py` (joins `study_endpoints` HSA cases + `conditions_summary`-purged controls to the `.fam`).

## HSA literature corpus (published)

| Dataset | Content | License | Source |
|---|---|---|---|
| **`hsa-literature`** | 4,485 HSA papers + 1,444 CC-BY/CC0 full-text | per-paper (CC-BY/CC0 subset redistributable) | [🤗 golden-retrievers/hsa-literature](https://huggingface.co/datasets/golden-retrievers/hsa-literature) |

Built by `gr-hemangiosarcoma/scripts/fetch_literature.py` + `build_corpus.py`. HSA-relevant expression series (GEO), the NCI Integrated Canine Data Commons, and imaging sources are tracked in `gr-hemangiosarcoma/corpus/datasets_registry.md` and `corpus/images_catalog.md`.

## Coverage gaps (no good public dataset found, 2026)

- **Canine hemangiosarcoma whole-slide histopathology** — no public digitized HSA WSI dataset; the [`gr-hemangiosarcoma`](https://github.com/golden-retrievers/gr-hemangiosarcoma) MIL pipeline is infrastructure waiting on GRLS necropsy slides (DUA).
- **HSA-specific germline GWAS power** — at 306–312 cases, GRLS is underpowered for genome-wide significance; larger multi-cohort HSA case collections are the bottleneck.
