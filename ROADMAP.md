# Roadmap: Understanding Canine Hemangiosarcoma

Derived from a 2026 literature review ([DATASETS.md](DATASETS.md), [MODELS.md](MODELS.md), [`docs/GR-AI-LANDSCAPE.md`](docs/GR-AI-LANDSCAPE.md)) and a two-pass adversarially verified HSA review. The findings that shape everything:

> **Hemangiosarcoma is the deadliest cancer in golden retrievers, caught late, with no curative therapy in decades — and it is a faithful genomic model for human angiosarcoma. The durable AI lever is understanding its biology and genetics, not detection or generic CV.**

## 🧭 Current direction (HSA-focused)

The program is now centered on **understanding hemangiosarcoma**. The flagship repo **`gr-hemangiosarcoma`** holds the research corpus (papers, datasets, images), the germline GWAS/PRS/variant-annotation pipeline, and the verified knowledge base. `gr-histopathology` and `gr-health-multimodal` feed in (tumor histology + multimodal integration); `gr-vision-tooling` is supporting CV only. Earlier generic-CV and early-detection framings are deprioritized (lead-time bias + HSA lethality make screening low-value).

**Immediate track (lowest friction → start now):**
1. ✅ Mirror open **GRLS genomics** (CC-BY-SA, `s3://mafgrlsgenome`) → HF dataset `golden-retrievers/grls-genomics` (3,224 dogs, 913,984 SNPs, PLINK/CanFam3).
2. PLINK QC + PCA population-structure baseline (`gr-hemangiosarcoma`).
3. Apply for **GRLS Data Commons** DUA (CZ Biohub) to unlock phenotypes/labs/histopath → enables disease GWAS + the flagship multi-modal cancer model.
4. Join genotypes ↔ phenotypes via `map_id_sex.tab` → first golden hemangiosarcoma / lymphoma / hip-dysplasia GWAS.

---


So the winning strategy is **not** to compete with multi-species foundation models on breadth. It's to build the **deepest, densest, best-labeled golden-retriever corpus in the world** and use it to *specialize* the best general models into a GR-native suite that beats them on every GR task.

## Strategic pillars

1. **Corpus first, models second.** The moat is the data. Every general model (DINOv3, SAM 2, X-Pose, MiewID) is one fine-tune away from a competitor; a 1M+ image/video golden-retriever corpus with re-ID identities, pose, masks, and behavior labels is not.
2. **Multi-task from one corpus.** Collect once, label for many tasks. The same clip yields detection, segmentation (SAM 2 auto-labels), pose (X-Pose pseudo-labels), action labels, and re-ID identity.
3. **License-clean by design.** Track provenance per asset. Avoid CC-BY-NC contamination (e.g. MegaDescriptor) in anything we want to release permissively. Prefer self-collected + CC-BY/CC0 + consented user contributions.
4. **Specialize, then distill.** Fine-tune big general models on GR data, then distill to small fast checkpoints for edge/app use.

## Phase 0 — Foundation (now)
- [x] GitHub hub repo + org, HF org, cross-links.
- [ ] HF write token for the org (per-org keychain entry).
- [ ] Define the **GR data schema** (`docs/schema.md`): image/video, source, license, breed-confidence, individual-id, bbox, mask, keypoints, action labels, capture metadata.
- [ ] Stand up task repos (see below) + HF dataset/model placeholders.
- [ ] Evaluation protocol (`docs/eval.md`): held-out GR test splits per task, leaderboards.

## Phase 1 — Bootstrap corpus (GR slices of existing data)
Cheap wins by extracting goldens from public sets:
- [ ] Golden-retriever class from **Stanford Dogs** + **Tsinghua Dogs** → seed classification set.
- [ ] Canine re-ID from **PetFace** / **DogFaceNet** / **MPDD** (golden subset) → seed re-ID set.
- [ ] Dog keypoints from **AP-10K / APTv2 / Quadruped-80K** → seed pose set.
- [ ] Dog clips from **Animal Kingdom** + **DogCentric** → seed action set.
- [ ] Auto-segment all of the above with **SAM 2** → seed masks (human-verified sample).
- **Deliverable:** `gr-core-v0` HF dataset, fully provenance-tracked.

## Phase 2 — Scale original collection (the moat)
- [ ] **Web + creative-commons harvest** of golden retriever imagery/video (Flickr CC, Wikimedia, iNaturalist, YouTube CC) with automated breed verification (fine-tuned classifier gate).
- [ ] **Community contribution pipeline**: owners submit photos/videos of their goldens with consent + (optional) individual identity → uniquely valuable re-ID + longitudinal data. Hook into communities (golden retriever subreddits, breed clubs, rescue orgs).
- [ ] **Multi-view / longitudinal capture** of consented individual dogs (puppy→senior) — nobody has this.
- [ ] Auto-label pipeline: detect → SAM 2 mask → X-Pose keypoints → action proposals → human QA in the loop.
- [ ] Link **Morris Animal Foundation Golden Retriever Lifetime Study** metadata where consented (health/behavior context).
- **Target:** ≥1M images + ≥1,000 hrs video, ≥10k uniquely-identified individuals.

## Phase 3 — Model suite (specialize the SOTA)
| Task | Base | Plan |
|---|---|---|
| Breed/sub-type classification | DINOv3 | Fine-tune; also GR coat-color / age / working-vs-show line heads |
| **Individual re-ID** | MiewID (or clean-license base) | Fine-tune on GR identities → best dog face/body re-ID in the world |
| Segmentation | SAM 2 | GR-specialized auto-mask + part segmentation (head/ears/tail/legs) |
| Pose | X-Pose / SuperAnimal | GR-tuned keypoints, add GR-specific points |
| Action recognition | VideoMAE/InternVideo | Fine-tune on GR action taxonomy (zoomies, play-bow, retrieve, swim…) |
| **Video generation** | SVD / CogVideoX / Veo-class | Fine-tune/LoRA on GR video → first GR-native video generator |
| **Behavior prediction** | motion model (AniMo-style) + video pred | Forecast next action / trajectory from observed clip |

## Phase 4 — Flagship & flywheel
- [ ] **GR-DINO**: a golden-retriever foundation embedding model powering all downstream heads.
- [ ] Public **leaderboards** + held-out benchmarks per task (define the field's standard).
- [ ] HF Spaces demos (breed/individual ID, segment-my-dog, pose, action tagging, video gen).
- [ ] Distilled edge checkpoints for a phone app → the app drives more community data → flywheel.
- [ ] Paper + dataset release; flip select assets to public.

## Differentiators (why this becomes #1)
- **Density over breadth** — every general model is broad-but-shallow on goldens; we go deep.
- **Identity + longitudinal data** — the one thing scraping can't easily produce.
- **Full-stack, one corpus** — classification→segmentation→pose→action→generation→prediction, consistently labeled.
- **License hygiene** — releasable where competitors' NC-tainted pipelines can't.

## Key risks
- **Licensing**: MegaDescriptor is CC-BY-NC; ImageNet-derived terms on Stanford Dogs. Keep a clean-license track.
- **Breed-verification noise** at scale — needs a strong classifier gate + human QA.
- **Re-ID label quality** — individual identity is the hardest, highest-value annotation; prioritize consented contributions.
