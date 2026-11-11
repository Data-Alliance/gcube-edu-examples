# gcube-edu-examples

**English** | [한국어](README.ko.md)

Lab examples for the gcube EDU templates. Deploy a workload with an EDU template container, get this repository, and you can start the notebook labs right away.

The repository has 11 folders that map 1:1 to the 11 EDU templates. Each folder contains 3 notebooks and its own guide (README).

## How to use

1. Deploy a gcube workload with the EDU template you want to use.
   There are two ways to get the lab repository.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to this repository's URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the folder with the same name as the deployed template and run the notebooks in order, starting with `01`.

Each folder contains only the notebooks for its template. For example, if you deployed the `edu-cv-pytorch` template, use the `edu-cv-pytorch` folder.

## Templates

| Folder (= template) | Domain | Notebook topics |
|---|---|---|
| edu-cv-pytorch | Computer vision | Image classification (CNN) · Transfer learning · Data augmentation |
| edu-dl-tensorflow | Deep learning with TensorFlow | Image classification (Keras) · Transfer learning · Overfitting control |
| edu-ml-data | Basic ML · Data analysis | EDA · Regression · Classification and clustering |
| edu-nlp-hf | Natural language processing | pipeline inference · Text classification fine-tuning · Embedding search |
| edu-rl-pytorch | Reinforcement learning | gymnasium basics · PPO training · Algorithm comparison |
| edu-genai-sd | Generative AI | text-to-image · Prompts and parameters · img2img |
| edu-llm-train | LLM fine-tuning · RAG | LoRA · QLoRA · RAG (FAISS) |
| edu-audio-pytorch | Speech · Audio | Audio features (librosa) · Speech recognition (Whisper) · Audio classification |
| edu-medical-monai | Medical imaging | DICOM · NIfTI I/O · MONAI transforms · UNet segmentation |
| edu-geo-gdal | Remote sensing · Geospatial | Raster (rasterio) · Vector (geopandas) · NDVI |
| edu-gnn-pyg | Graph neural networks | Graph basics (PyG) · Node classification (GCN) · Graph classification |

## Folder structure

```
gcube-edu-examples/
├─ edu-cv-pytorch/
│  ├─ 01_image_classification_cnn.ipynb
│  ├─ 02_transfer_learning.ipynb
│  ├─ 03_data_augmentation.ipynb
│  └─ README.md
├─ edu-dl-tensorflow/        # 3 notebooks + README.md, same as above
├─ edu-ml-data/
├─ edu-nlp-hf/
├─ edu-rl-pytorch/
├─ edu-genai-sd/
├─ edu-llm-train/
├─ edu-audio-pytorch/
├─ edu-medical-monai/
├─ edu-geo-gdal/
├─ edu-gnn-pyg/
└─ README.md
```

Each folder's README describes the lab order, recommended GPU specs, and installed packages for its template.

## Notes

- All notebooks are designed to be run top to bottom in JupyterLab.
- Visualizations use a Korean font (NanumGothic).
- Template images are provided with a tag per CUDA version, and package versions are pinned. See [VERSIONS.md](VERSIONS.md) for how to choose a tag and how versions are pinned.
- Datasets and models are downloaded automatically when a notebook runs and are stored in `/workspace/.cache`. (Some notebooks use synthetic data and need no download.)
- Each notebook runs its own kernel, and the kernel keeps using GPU memory after the run finishes until you shut it down. If you keep several notebooks open, the kernel may die from running out of memory, depending on the GPU spec (VRAM). Especially for notebooks that use large models, such as `edu-genai-sd` and `edu-llm-train`, shut down the previous notebook's kernel with **Kernel → Shut Down Kernel** before moving on to the next notebook. You can view and shut down all running kernels at once in **Running Terminals and Kernels** in the left sidebar.
