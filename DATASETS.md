# Datasets Index

Index of upstream datasets we build on and derived datasets we publish. Derived datasets live on the [HF org](https://huggingface.co/golden-retrievers). **Always check the upstream license before redistributing.**

> Compiled from a verified SOTA review (2026). Every row's figures were adversarially fact-checked against primary sources.

## Classification & breed ID

| Dataset | Size | Dog content | License | Source |
|---|---|---|---|---|
| **Stanford Dogs** | 20,580 imgs, 120 breeds (12k train / 8.58k test), bboxes | All dogs (incl. golden retriever class) | ImageNet terms (research) | [vision.stanford.edu](https://vision.stanford.edu/aditya86/ImageNetDogs/) · [TFDS](https://www.tensorflow.org/datasets/catalog/stanford_dogs) |
| **Tsinghua Dogs (ThuDogs)** | ~70k imgs, 130 breeds | All dogs; larger & more intra-class variation than Stanford | Research | [cg.cs.tsinghua.edu.cn/ThuDogs](https://cg.cs.tsinghua.edu.cn/ThuDogs/) |
| ImageNet dog synsets | — | Source of Stanford Dogs | ImageNet terms | — |

## Individual re-identification

| Dataset | Size | Notes | License | Source |
|---|---|---|---|---|
| **PetFace** | 257,484 individuals, ~1.01M imgs, 13 families, 319 breeds | Largest animal-face dataset (>110× prior); re-ID (seen) + verification (unseen) tasks | Research (ECCV'24) | [arXiv 2407.13555](https://arxiv.org/abs/2407.13555) · [project](https://dahlian00.github.io/PetFacePage/) |
| **WildlifeReID-10k** | 140,488 imgs, 10,772 individuals, ~33 species, 37 datasets | Unified re-ID benchmark; ArcFace baselines | Mixed (Kaggle) | [CVPRW'25 PDF](https://openaccess.thecvf.com/content/CVPR2025W/FGVC/papers/Adam_WildlifeReID-10k_Wildlife_re-identification_dataset_with_10k_individual_animals_CVPRW_2025_paper.pdf) |
| **wildlife-datasets** toolkit | 53 re-ID datasets + 3 metadatasets | Unified loader; includes canine sets below | Per-dataset | [GitHub](https://github.com/WildlifeDatasets/wildlife-datasets) · [WACV'24](https://arxiv.org/abs/2311.09118) |
| **DogFaceNet** | dog faces | Canine re-ID, in toolkit | Per-source | via toolkit |
| **MPDD** | 1,657 imgs, 192 dogs | Multi-pose dog re-ID | Per-source | via toolkit |

## Pose / keypoints

| Dataset | Size | Dog content | License | Source |
|---|---|---|---|---|
| **AP-10K** | 10,015 imgs, 23 families, 54 species, manual keypoints | Includes Canidae | Research | [arXiv 2108.12617](https://arxiv.org/abs/2108.12617) |
| **APTv2** | 2,749 clips, 41,235 frames, 84,611 instances, 30 species, 17 kpts | Video pose + tracking; incl. dogs | Research | [arXiv 2312.15612](https://arxiv.org/html/2312.15612v1) |
| **Quadruped-80K** | ~80k imgs, 45+ species, 39 kpts | Training set for SuperAnimal; incl. dogs | Research | [Nat. Comms](https://pmc.ncbi.nlm.nih.gov/articles/PMC11192880/) |
| **UniKPT** | 226,547 imgs, 418,487 instances, 338 kpts, 1,237 categories | Unifies 13 datasets; trains X-Pose | Research | [arXiv 2310.08530](https://arxiv.org/html/2310.08530v2) |

## Action recognition & behavior

| Dataset | Size | Notes | License | Source |
|---|---|---|---|---|
| **Animal Kingdom** | 50h video, 30k clips (action), 33k frames (pose), 850 species | Leading broad animal behavior benchmark; multi-label | Research | [site](https://sutdcv.github.io/Animal-Kingdom/) · [CVPR'22](https://arxiv.org/abs/2204.08129) |
| **DogCentric Activity** | first-person (dog-mounted camera) activity clips | Dog-specific egocentric activities | Research | [Kyushu Univ.](http://robotics.ait.kyushu-u.ac.jp/yumi/db/first_dog.html) |

## Golden-retriever-specific (non-CV, but valuable)

| Resource | Content | Notes |
|---|---|---|
| **Morris Animal Foundation — Golden Retriever Lifetime Study** | Longitudinal health/behavior data on ~3,000 goldens | Not imagery, but the richest GR-specific cohort; potential metadata/behavior linkage | [data commons](https://datacommons.morrisanimalfoundation.org/data-roadmap) |

## GRLS genomics + phenotypes (the health track's primary corpus)

The cancer-genomics + multimodal work is anchored on the GRLS cohort: **genotypes** (public, no login) plus **phenotype/clinical tables** (DUA-gated). Genotypes live on Hugging Face; phenotype tables are staged locally under `gr-hemangiosarcoma/data/datacommons/` (git-ignored under the DUA — not redistributed).

### Genotypes (public)

| Dataset | Size | License | Source |
|---|---|---|---|
| **GRLS Axiom HD genotyping** | ~1.1M markers (913,984 after release QC), 3,224 dogs (3,024 GRLS + 200 Golden Oldies), CanFam3/PLINK | CC-BY-SA | AWS Open Data `s3://mafgrlsgenome` (`aws s3 ls --no-sign-request`); [registry](https://registry.opendata.aws/maf-genome) · mirror `hf.co/golden-retrievers/grls-genomics` |

### Phenotype / clinical tables (DUA-gated; 37 CSVs across 24 datasets)

All key on `subject_id` = the genotype `.fam` IID (the public `grls…` ID) — **direct join to genotypes**; the lone exception is `atopic_dermatitis_questionnaire` (keys on the MAF-internal `094-…` form + carries a `public_id` column). Core cohort tables cover all 3,044 GRLS dogs, **3,024 of them genotyped**.

| Table(s) | Rows | Dogs w/geno | Role in our models |
|---|---|---|---|
| **`study_endpoints`** | 1,247 | 1,034 | **Adjudicated cancer endpoints** (`tracked_condition`, `tier_of_confidence`, `is_cause_of_death`, `is_recurrence`). GWAS/PRS labels. Cases: hemangiosarcoma ~312, mast cell tumor ~184, lymphoma ~145, osteosarcoma ~19 |
| **`conditions_summary`** + 11 `conditions_<system>` (`cardio`-via-summary, `dental`, `ear_nose_throat`, `endocrine`, `eye`, `gastrointestinal`, `hematologic`, `infectious`, `musculoskeletal`, `reproductive`, `skin`, `urinary`) | 54,792 ea. | 3,024 | Per dog×year diagnosis flags; `summary.neoplasia` 0/1 = broad cancer flag used to define clean (cancer-free) GWAS controls |
| **`clinical_labs`** | 1.44M | 3,024 | Long-format labs (`test_group`/`test_name`/`test_value`/`ref_range`) → multimodal `labs-GRU` modality; strongest unimodal cancer predictors |
| **`dog_profile`** | 3,044 | 3,024 | Signalment + survival: `sex_status`, `birth_date`, `death_date`, `is_euthanized`, `spay_neuter_date`, `study_status`, `coat_color` → covariates + censoring |
| `exam_physical` | 20,973 | 3,024 | Weight, BCS, vitals → clinical modality; body-condition label for CV tooling |
| `medications`, `over_the_counter_medications`, `supplements`, `flea_tick_heartworm`, `vaccines` | 49k–52k | ~3,024 | Treatment/exposure covariates + confounders |
| `environment_*` (7), `poison_exposure`, `location_history`, `lifestyle` | varies | ~3,024 | Environmental / GxE risk factors |
| `activity_*` (4) | 8k–26k | ~3,024 | Activity/lifestyle; gait/welfare links for CV tooling |
| `goldenage_load`, `goldenage_coast`, `goldenage_dishaa`, `atopic_dermatitis_questionnaire` | 1.2k–1.9k | 886–1,621 | Aging sub-study (osteoarthritis, cognition) + dermatitis; secondary endpoints |

> Build a GWAS phenotype with `gr-hemangiosarcoma/scripts/prepare_phenotypes.py` (joins `study_endpoints` cases + `conditions_summary`-purged controls to the `.fam`).

## Coverage gaps (no good public dataset found, 2026)

- **Dog/golden-retriever-specific video-generation** training corpora — none.
- **Behavior *forecasting*** (predicting future actions, not recognizing observed ones) — none dog-specific.
- **Golden-retriever-specific segmentation / part-segmentation** — none; relies on class-agnostic SAM 2.
