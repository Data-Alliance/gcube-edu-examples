# Image tags and package versions

**English** | [한국어](VERSIONS.ko.md)

The notebooks in this repository are written and tested against the **pinned package versions** of the EDU template images. This document covers which image tag to use, why versions are pinned, and what to watch out for regarding versions.

## Which tag should I use?

Template images are provided with a tag per CUDA version. Choose the tag that matches the **NVIDIA driver version** of the node you deploy to. You can check the driver version with `nvidia-smi` in the container terminal or a notebook cell.

| Template | CUDA 13.0 (driver 580 or later) | CUDA 12.8 (driver 570 or later) |
|---|---|---|
| edu-dl-tensorflow | — | `tf2.17-cuda12.8` |
| edu-ml-data | `ubuntu24.04-cuda13.0` | `ubuntu24.04-cuda12.8` |
| 9 PyTorch templates | `torch2.11-cuda13.0` | `torch2.11-cuda12.8` |

- The image address format is `ghcr.io/data-alliance/<template>:<tag>`. Example: `ghcr.io/data-alliance/edu-cv-pytorch:torch2.11-cuda12.8`
- The same images are also on Docker Hub [`gcubeai`](https://hub.docker.com/u/gcubeai) with the same names and tags. Example: `gcubeai/edu-cv-pytorch:torch2.11-cuda12.8`
- 9 PyTorch templates: edu-cv-pytorch, edu-nlp-hf, edu-rl-pytorch, edu-genai-sd, edu-llm-train, edu-audio-pytorch, edu-medical-monai, edu-geo-gdal, edu-gnn-pyg
- For the same template, **package versions are identical** regardless of CUDA version, so the same notebooks run as-is with either tag.
- The `latest` tag points to the newest combination and may move when a new combination is released. To keep the lab environment consistent, use the tags above instead of `latest`.

## Why pin versions?

- The notebooks are written against the APIs and behavior of specific package versions. When a package changes, function names, arguments, or output formats can change, so a notebook may stop working or give different results.
- Without pinning, each image rebuild installs the latest versions at that time, so the same tag could end up with different contents.
- For this reason, each template's package versions are pinned in the template repository's `requirements.txt`, and version upgrades are applied only after the notebooks are re-checked.

## Key versions by template

For the full version list, see `requirements.txt` and the "Installed packages" section of the README in each template folder of the [gcube-edu-templates](https://github.com/Data-Alliance/gcube-edu-templates) repository.

| Template | Key versions |
|---|---|
| edu-dl-tensorflow | TensorFlow 2.17, NumPy 1.26.4, scikit-learn 1.5.2 |
| edu-ml-data | NumPy 2.5.0, pandas 3.0.3, scikit-learn 1.9.0 |
| edu-cv-pytorch | PyTorch 2.11.0, albumentations 2.0.8, OpenCV 4.13 |
| edu-nlp-hf | PyTorch 2.11.0, transformers 5.12.1, datasets 5.0.0 |
| edu-rl-pytorch | PyTorch 2.11.0, gymnasium 1.3.0, stable-baselines3 2.9.0 |
| edu-genai-sd | PyTorch 2.11.0, diffusers 0.38.0, transformers 5.12.1 |
| edu-llm-train | PyTorch 2.11.0, transformers 5.12.1, peft 0.19.1, trl 1.6.0, bitsandbytes 0.49.2 |
| edu-audio-pytorch | PyTorch 2.11.0, librosa 0.11.0, openai-whisper 20250625 |
| edu-medical-monai | PyTorch 2.11.0, MONAI 1.6.0 |
| edu-geo-gdal | PyTorch 2.11.0, rasterio 1.5.0, geopandas 1.1.3 |
| edu-gnn-pyg | PyTorch 2.11.0, PyTorch Geometric 2.8.0 |

## Cautions

- **Do not upgrade existing packages with `pip install -U` inside the container.** The notebooks may stop working. Installing new packages that the notebooks do not use is fine.
- **The torch version is locked in PyTorch templates.** Switching torch to a different CUDA build makes the GPU unusable, so torch, torchvision, torchaudio, and triton are blocked from changing from the versions installed in the image. Installing a package that requires a different torch version fails with a `ResolutionImpossible` error and nothing is installed.

## When you need a different Python version

The images are based on Ubuntu 24.04 and Python 3.12. If you need a different Python version, you can create a separate environment with [uv](https://docs.astral.sh/uv/) inside the container.

```bash
pip install uv
uv venv -p 3.10 /workspace/py310        # Create a Python 3.10 environment (Python is downloaded automatically)
source /workspace/py310/bin/activate
uv pip install ipykernel numpy pandas    # Install the packages you need into the new environment
python -m ipykernel install --user --name py310 --display-name "Python 3.10"
```

The new environment has no packages installed, so you need to reinstall torch and any other packages you need. In the new environment, use `uv pip` as in the example above. Plain `pip` applies the torch version lock set in the image (`PIP_CONSTRAINT`), so it cannot install a different torch into the new environment. The registered kernel is available in JupyterLab's kernel selector.
