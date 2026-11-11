# edu-gnn-pyg — Graph neural network labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-gnn-pyg` container. Using PyTorch Geometric, they cover the standard graph neural network (GNN) workflow, from graph data structures to node classification and graph classification.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_graph_basics_pyg.ipynb` | Represent a graph as a PyG `Data` object (node features, edges), visualize it with networkx, and understand message passing in a GCN layer. |
| `02_node_classification_gcn.ipynb` | Classify nodes in the Cora citation network with a 2-layer GCN. Covers the core idea of GNNs: using information from neighboring nodes. |
| `03_graph_classification.ipynb` | Cover graph classification, where each graph is one sample. Build graph representations with `global_mean_pool` and train in batches. |

## How to run

1. Deploy a workload with the `edu-gnn-pyg` template (GPU with 8 GB+ VRAM recommended).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-gnn-pyg` folder and run the notebooks in order, starting with `01`.

## Data

- The Cora dataset for 02 is downloaded automatically when the notebook runs.
- 01 and 03 generate synthetic graphs, so no download is needed.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for graph neural network labs preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-gnn-pyg:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| torch-geometric | 2.8.0 | Graph neural network library (layers such as GCNConv, Data, datasets, pooling) |
| networkx | 3.6.1 | Graph creation, analysis, and visualization |
| scikit-learn | 1.9.0 | Auxiliary tools for evaluation, preprocessing, dimensionality reduction, etc. (not used directly in these notebooks) |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic) |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |