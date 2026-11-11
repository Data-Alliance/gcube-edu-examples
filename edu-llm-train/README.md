# edu-llm-train — LLM fine-tuning and RAG labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-llm-train` container. Fine-tune LLMs efficiently with LoRA and QLoRA, and implement FAISS-based RAG (retrieval-augmented generation).

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_lora_finetuning.ipynb` | With LoRA, keep the original weights frozen and train only small additional matrices. Run supervised fine-tuning of a small LLM on instruction data with `peft` + `trl` SFTTrainer. |
| `02_qlora_4bit.ipynb` | Fine-tune an LLM with less memory using bitsandbytes 4-bit quantization + LoRA (QLoRA). A standard technique for working with LLMs on limited resources. |
| `03_rag_faiss.ipynb` | Implement RAG: convert documents to embeddings, index and search them with FAISS, and put the search results into the LLM prompt to generate answers. |

## How to run

1. Deploy a workload with the `edu-llm-train` template (GPU with 16 GB+ VRAM recommended; 24 GB+ for QLoRA on 7B+ models).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-llm-train` folder and run the notebooks in order, starting with `01`.

## Models and data

- Models (TinyLlama, etc.) and datasets (Alpaca, etc.) are downloaded automatically from the Hugging Face Hub when a notebook runs and are stored in `/workspace/.cache/huggingface`.
- 4-bit quantization (bitsandbytes) and QLoRA require a CUDA GPU.
- The notebooks' default model (TinyLlama 1.1B) also works with 8 GB of VRAM. The 16 GB recommendation applies to training large 7B+ models with QLoRA.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for LLM fine-tuning and RAG preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-llm-train:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| transformers | 5.12.1 | LLMs, tokenizers, pipeline |
| datasets | 5.0.0 | Dataset loading and preprocessing |
| peft | 0.19.1 | Parameter-efficient fine-tuning such as LoRA (PEFT) |
| trl | 1.6.0 | Supervised LLM fine-tuning such as SFTTrainer |
| bitsandbytes | 0.49.2 | 4-bit/8-bit quantization (QLoRA) |
| accelerate | 1.14.0 | Training acceleration and distributed processing |
| faiss-cpu | 1.14.3 | Vector indexing and similarity search (RAG) |
| sentencepiece | 0.2.1 | Subword tokenizer |
| einops | 0.8.2 | Tensor operation notation |
| evaluate, scikit-learn | 0.4.6, 1.9.0 | Evaluation metrics |
| tensorboard | 2.20.0 | Training log visualization |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |