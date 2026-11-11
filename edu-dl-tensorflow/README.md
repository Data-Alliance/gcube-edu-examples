# edu-dl-tensorflow — TensorFlow/Keras deep learning labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-dl-tensorflow` container. Using Keras, TensorFlow's high-level API, they cover the standard deep learning workflow, from image classification to transfer learning and handling overfitting. Datasets are downloaded automatically at run time.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_image_classification_keras.ipynb` | Classify Fashion-MNIST with Keras. Learn the basic TensorFlow/Keras workflow: data loading and visualization, model definition (Sequential), `model.fit`/`evaluate`, and visualizing learning curves and predictions. |
| `02_transfer_learning.ipynb` | Apply transfer learning from an ImageNet-pretrained MobileNetV2 to Fashion-MNIST. Grayscale images are converted to 3 channels at 96×96, then the model goes through feature extraction (freeze) followed by fine-tuning, with data augmentation via Keras preprocessing layers. |
| `03_overfitting_callbacks.ipynb` | Diagnose overfitting from training/validation curves, and compare how data augmentation, Dropout, and the EarlyStopping callback mitigate it. |

## How to run

1. Deploy a workload with the `edu-dl-tensorflow` template (GPU with 8 GB+ VRAM recommended).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-dl-tensorflow` folder and run the notebooks in order, starting with `01`.

> `gcube_quiet.py` in this folder is a helper file that filters out harmless warning messages TensorFlow prints during GPU initialization. Each notebook loads it automatically in its first cell; you do not need to run it yourself.

## Dataset

- **Fashion-MNIST** — 70,000 28×28 grayscale images of 10 clothing types (T-shirts, trousers, shoes, etc.). A standard introductory deep learning dataset.
- All data is downloaded automatically via `tf.keras.datasets` when a notebook runs. No separate preparation is needed.

## Installed packages

Based on TensorFlow 2.17 (CUDA 12.8), with the packages needed for deep learning labs preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-dl-tensorflow:tf2.17-cuda12.8` image. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| TensorFlow (includes Keras) | 2.17.0 | Deep learning framework and high-level API. Model definition, training, evaluation, pretrained models (applications), preprocessing layers |
| scikit-learn | 1.5.2 | Auxiliary machine learning tools such as evaluation metrics and preprocessing |
| SciPy | 1.12.0 | Scientific computing |
| Pillow | 12.2.0 | Basic image I/O |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic, so Korean can be used in plot titles and labels) |
| tqdm | 4.67.1 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |