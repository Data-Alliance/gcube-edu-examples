# edu-nlp-hf — Natural language processing (Hugging Face) labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-nlp-hf` container. Using Hugging Face Transformers, they cover the standard NLP workflow, from using pretrained models to fine-tuning for text classification and semantic search with sentence embeddings.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_pipeline_inference.ipynb` | Use `pipeline` to perform sentiment analysis, named entity recognition, question answering, summarization, and zero-shot classification without training. An introduction to using pretrained models. |
| `02_text_classification_finetune.ipynb` | Fine-tune a pretrained DistilBERT on IMDb data. Covers the standard NLP transfer learning process: tokenization → model setup → training and evaluation with `Trainer`. |
| `03_embeddings_semantic_search.ipynb` | Extract sentence embeddings, compare meaning with cosine similarity, and implement semantic search. A foundation for RAG and recommendation. |

## How to run

1. Deploy a workload with the `edu-nlp-hf` template (GPU with 8 GB+ VRAM recommended; 16 GB+ for fine-tuning large models such as BERT-large).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-nlp-hf` folder and run the notebooks in order, starting with `01`.

## Models and data

- Pretrained models (DistilBERT, MiniLM, etc.) and the dataset (IMDb) are downloaded automatically from the Hugging Face Hub when a notebook runs and are stored in `/workspace/.cache/huggingface`.
- No separate preparation is needed.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the Hugging Face NLP ecosystem preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-nlp-hf:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| transformers | 5.12.1 | Pretrained models, tokenizers, pipeline, Trainer |
| datasets | 5.0.0 | Dataset loading and preprocessing |
| tokenizers | 0.22.2 | Fast tokenizer backend |
| sentencepiece | 0.2.1 | Subword tokenizer for some models |
| accelerate | 1.14.0 | Training acceleration and distributed processing backend |
| evaluate | 0.4.6 | Evaluation metrics (accuracy, etc.) |
| tensorboard | 2.20.0 | Training log visualization |
| scikit-learn | 1.9.0 | Auxiliary evaluation and preprocessing |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |