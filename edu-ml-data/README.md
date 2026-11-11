# edu-ml-data — Basic machine learning and data analysis labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-ml-data` container. Using pandas and scikit-learn, they cover the basic machine learning workflow, from exploratory data analysis (EDA) to regression, classification, and clustering. All data comes from scikit-learn built-in datasets, so no separate download is needed.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_eda_visualization.ipynb` | Learn the basics of exploratory data analysis (EDA): handle data with pandas and visualize distributions and correlations with seaborn. (Wine dataset) |
| `02_regression.ipynb` | Predict continuous values with linear regression and evaluate with R², RMSE, and MAE. Visualize the results with a predicted-vs-actual scatter plot. (Diabetes dataset) |
| `03_classification_clustering.ipynb` | Compare classification (logistic regression, random forest) and clustering (K-means + PCA visualization) on the same data to learn the difference between supervised and unsupervised learning. (Wine dataset) |

## How to run

1. Deploy a workload with the `edu-ml-data` template (GPU with 8 GB+ VRAM recommended).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-ml-data` folder and run the notebooks in order, starting with `01`.

## Datasets

- **Wine dataset** — distinguishes 3 wine types using 13 chemical properties (for classification and clustering).
- **Diabetes dataset** — predicts disease progression from 10 health indicators (for regression).
- Both are scikit-learn built-in datasets (`sklearn.datasets`), so they are available immediately without download.

## Installed packages

The packages needed for basic machine learning and data analysis are preinstalled. (This is an introductory environment that does not rely heavily on the GPU. If you need PyTorch or TensorFlow, use another template.)

These examples are based on the `ghcr.io/data-alliance/edu-ml-data:ubuntu24.04-cuda13.0` image. The CUDA 12.8 image (`:ubuntu24.04-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| NumPy | 2.5.0 | Numerical array operations |
| pandas | 3.0.3 | Tabular data processing and analysis |
| scikit-learn | 1.9.0 | Machine learning (regression, classification, clustering), preprocessing, evaluation, built-in datasets |
| SciPy | 1.18.0 | Scientific and statistical computing |
| statsmodels | 0.14.6 | Statistical modeling and testing |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic) |
| seaborn | 0.13.2 | Statistical visualization (heatmaps, distributions, etc.) |
| Plotly | 6.8.0 | Interactive visualization |
| openpyxl | 3.1.5 | Excel file I/O |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |