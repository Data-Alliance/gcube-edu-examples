# edu-genai-sd — Generative AI (Stable Diffusion) labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-genai-sd` container. Using Stable Diffusion with Hugging Face `diffusers`, they cover text-to-image generation, prompt and parameter experiments, and image-to-image transformation.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_text_to_image.ipynb` | Generate images from text prompts with StableDiffusionPipeline. Load the pipeline, generate images, and compare multiple prompts. |
| `02_prompt_and_parameters.ipynb` | Experiment with how `guidance_scale`, `num_inference_steps`, and negative prompts affect results, comparing outputs with the same seed. |
| `03_img2img.ipynb` | Cover img2img, which generates a new image from an input image and a prompt, and compare `strength` values (degree of change). |

## How to run

1. Deploy a workload with the `edu-genai-sd` template (GPU with 16 GB+ VRAM recommended; 24 GB+ for large models such as SDXL).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-genai-sd` folder and run the notebooks in order, starting with `01`.

## Models

- The Stable Diffusion v1.5 model is downloaded automatically from the Hugging Face Hub when a notebook runs and is stored in `/workspace/.cache/huggingface`. On GPU, the half-size fp16 variant (`variant='fp16'`) is downloaded to reduce download size. The model is still several GB, so the first run may take a while to download; after that, it loads quickly from the cache.
- Image generation uses a lot of GPU memory. If memory is tight, use `enable_attention_slicing()`.
- The notebooks' default model (Stable Diffusion v1.5) also works with 8 GB of VRAM. The 16 GB recommendation applies to large models such as SDXL or to LoRA training.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for generative AI labs preinstalled. Attention uses PyTorch's built-in SDPA (xformers is not needed).

These examples are based on the `ghcr.io/data-alliance/edu-genai-sd:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| diffusers | 0.38.0 | Diffusion model pipelines (text-to-image, img2img, etc.) |
| transformers | 5.12.1 | Model components such as the text encoder (CLIP) |
| accelerate | 1.14.0 | Faster model loading and execution |
| safetensors | 0.8.0 | Safe model weight format |
| datasets | 5.0.0 | Dataset loading (for fine-tuning) |
| opencv-python-headless | 4.13.0.92 | Image processing |
| Pillow | 12.1.1 | Image I/O |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |