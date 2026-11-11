# edu-geo-gdal — Remote sensing and geospatial labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-geo-gdal` container. Learn the basic remote sensing workflow: handle satellite imagery (rasters) with rasterio and vector data with geopandas, and compute the NDVI vegetation index.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_raster_rasterio.ipynb` | Understand how a raster (satellite image) is structured (bands, CRS, transform), and save, load, and visualize GeoTIFFs with rasterio. |
| `02_vector_geopandas.ipynb` | Create geometries with shapely, manage them with geopandas, and perform spatial operations (area, intersection) and coordinate system transformations. |
| `03_ndvi_remote_sensing.ipynb` | Compute the NDVI vegetation index from the near-infrared and red bands, then classify and visualize land cover types. |

## How to run

1. Deploy a workload with the `edu-geo-gdal` template (GPU with 8 GB+ VRAM recommended; process large images in tiles/patches).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-geo-gdal` folder and run the notebooks in order, starting with `01`.

## Data

- All notebooks generate synthetic rasters and vectors, so no download is needed.
- In real labs, load satellite imagery such as Landsat or Sentinel with `rasterio.open('image.tif')` and analyze it the same way.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for geospatial analysis preinstalled. (rasterio bundles GDAL in its wheel.)

These examples are based on the `ghcr.io/data-alliance/edu-geo-gdal:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| rasterio | 1.5.0 | Raster (satellite imagery, DEM) I/O and processing (GDAL-based) |
| geopandas | 1.1.3 | Vector data (points, lines, polygons) management and spatial operations |
| shapely | 2.1.2 | Geometric operations (area, distance, intersection, etc.) |
| pyproj | 3.7.2 | Coordinate reference system (CRS) transformation and projection |
| scikit-image | 0.26.0 | Image processing |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic) |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |