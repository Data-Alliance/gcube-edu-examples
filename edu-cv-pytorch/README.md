# edu-cv-pytorch — Computer vision labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-cv-pytorch` container. Using PyTorch, they cover the standard computer vision workflow, from image classification to transfer learning and data augmentation. All notebooks use the **CIFAR-10** dataset, which is downloaded automatically from the Hugging Face Hub at run time and stored in `/workspace/.cache/huggingface`.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_image_classification_cnn.ipynb` | Design your own CNN to classify CIFAR-10 images. Learn the basic deep learning computer vision workflow: data loading and visualization, CNN architecture design, training, and evaluation. |
| `02_transfer_learning.ipynb` | Fine-tune an ImageNet-pretrained ResNet18 on CIFAR-10. Covers **transfer learning**, which reaches higher accuracy with less training. |
| `03_data_augmentation.ipynb` | Apply data augmentation with albumentations and compare accuracy with and without augmentation to see how it improves generalization. |

## How to run

1. Deploy a workload with the `edu-cv-pytorch` template (GPU with 8 GB+ VRAM recommended).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically as soon as the workload starts.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-cv-pytorch` folder and run the notebooks in order, starting with `01`.

## Dataset

- **CIFAR-10** — 60,000 32×32 color images in 10 classes (airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck).
- When a notebook runs, the dataset is downloaded automatically from the Hugging Face Hub (`uoft-cs/cifar10`) and stored in `/workspace/.cache/huggingface`.
- The `datasets` package is needed to get CIFAR-10 from the Hugging Face Hub. It is not part of the computer vision image's default setup, so **each notebook installs it with `%pip install datasets` in its first cell** (once installed, it does not need to be reinstalled in the same session).

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for computer vision labs preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-cv-pytorch:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| torch, torchvision | 2.11.0, 0.26.0 (+cu130 / +cu128) | Deep learning framework, plus vision models, datasets, and image transforms |
| opencv-python-headless | 4.13.0.92 | Image reading and processing (server build without GUI) |
| albumentations | 2.0.8 | Data augmentation (rotation, flipping, brightness changes, etc.) |
| Pillow | 12.1.1 | Basic image I/O |
| scikit-learn | 1.9.0 | Auxiliary machine learning tools such as evaluation metrics and preprocessing |
| SciPy | 1.18.0 | Scientific computing |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic, so Korean can be used in plot titles and labels) |
| tqdm | 4.68.3 | Training progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |