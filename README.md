# 🦮 Golden Retrievers

**The world's largest open corpus and model suite for golden retriever computer vision.**

This is the **hub repository** for the [`golden-retrievers`](https://github.com/golden-retrievers) organization. It holds the dataset index, model index, task roadmap, and shared documentation. Large data and trained models live on the linked Hugging Face org: **https://huggingface.co/golden-retrievers**.

> Status: 🚧 Bootstrapping. Currently private. See [ROADMAP.md](ROADMAP.md) for the build-out plan.

## Mission

Assemble the largest, best-curated, openly-documented collection of golden-retriever imagery and video, and train/curate state-of-the-art models across the full vision stack:

| Task | Description | Repo |
|------|-------------|------|
| 🏷️ Classification | Fine-grained breed ID + individual dog re-identification | `gr-classification` |
| ✂️ Segmentation | Semantic + instance segmentation of dogs and parts | `gr-segmentation` |
| 🦴 Pose | Keypoint / pose estimation | `gr-pose` |
| 🏃 Activity recognition | Action / behavior classification in images & video | `gr-activity-recognition` |
| 🎬 Video generation | Generative video of golden retrievers | `gr-video-generation` |
| 🔮 Behavior prediction | Activity / motion forecasting | `gr-behavior-prediction` |

(Task repos are created as work begins — see [ROADMAP.md](ROADMAP.md).)

## Layout

- [`DATASETS.md`](DATASETS.md) — index of all source + derived datasets, with sizes, licenses, and HF links.
- [`MODELS.md`](MODELS.md) — index of foundation models we build on and models we train, with HF links.
- [`ROADMAP.md`](ROADMAP.md) — the plan for assembling the corpus and training the model suite.
- `docs/` — data schema, annotation guidelines, licensing notes, evaluation protocol.

## Links

- 🤗 Hugging Face org (data + models): https://huggingface.co/golden-retrievers
- 🐙 GitHub org (code + docs): https://github.com/golden-retrievers

## Licensing

Code in this org is released under permissive licenses (per-repo `LICENSE`). **Data and model licenses vary by source** — every dataset entry in [`DATASETS.md`](DATASETS.md) records its upstream license, and redistribution follows those terms. Nothing here is veterinary or behavioral advice.
