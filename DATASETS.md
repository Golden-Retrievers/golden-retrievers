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

## Coverage gaps (no good public dataset found, 2026)

- **Dog/golden-retriever-specific video-generation** training corpora — none.
- **Behavior *forecasting*** (predicting future actions, not recognizing observed ones) — none dog-specific.
- **Golden-retriever-specific segmentation / part-segmentation** — none; relies on class-agnostic SAM 2.
