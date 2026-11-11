# edu-medical-monai — Medical imaging labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-medical-monai` container. They cover the standard medical imaging deep learning workflow, from handling medical image formats (DICOM, NIfTI) to MONAI preprocessing and augmentation and UNet segmentation.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_medical_image_io.ipynb` | Read medical images with DICOM (pydicom) and NIfTI (nibabel), visualize 3D volumes as slices, and inspect metadata with SimpleITK. |
| `02_monai_transforms.ipynb` | Preprocess (intensity normalization, etc.) and augment (flip, rotation, noise) medical images with MONAI transforms, and build a pipeline with `Compose`. |
| `03_segmentation_unet.ipynb` | Train a segmentation model with MONAI UNet and DiceLoss, and evaluate it with the Dice score. Walk through the full segmentation workflow using synthetic data. |

## How to run

1. Deploy a workload with the `edu-medical-monai` template (GPU with 8 GB+ VRAM recommended; 3D segmentation needs more VRAM).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-medical-monai` folder and run the notebooks in order, starting with `01`.

## Data

- The DICOM example for 01 is bundled with pydicom.
- 02 and 03 generate synthetic images and volumes, so no download is needed.
- In real labs, use datasets such as MedNIST and MSD (Spleen, Liver, etc.), or your own DICOM/NIfTI files.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for medical image processing preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-medical-monai:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| MONAI | 1.6.0 | Medical imaging deep learning framework (preprocessing, augmentation, models such as UNet, losses, metrics) |
| nibabel | 5.4.2 | I/O for neuroimaging formats such as NIfTI |
| pydicom | 3.0.2 | Reading and writing DICOM files |
| SimpleITK | 2.5.5 | Medical image I/O and processing (resampling, registration, etc.) |
| scikit-image | 0.26.0 | General image processing |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic) |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |