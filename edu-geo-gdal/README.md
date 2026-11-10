# edu-geo-gdal — 원격탐사·지리공간 실습

`edu-geo-gdal` 컨테이너용 실습 예제입니다. rasterio로 위성영상(래스터)을, geopandas로 벡터 데이터를 다루고, NDVI 식생지수를 계산하는 원격탐사 기본 흐름을 익힙니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_raster_rasterio.ipynb` | 래스터(위성영상)의 구성(밴드·CRS·transform)을 이해하고, rasterio로 GeoTIFF를 저장·로드·시각화합니다. |
| `02_vector_geopandas.ipynb` | shapely로 도형을 만들고 geopandas로 관리하며, 공간 연산(면적·교집합)과 좌표계 변환을 수행합니다. |
| `03_ndvi_remote_sensing.ipynb` | 근적외선·빨강 밴드로 NDVI 식생지수를 계산하고, 토지 유형을 분류·시각화합니다. |

## 실행 방법

1. `edu-geo-gdal` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장. 대용량 영상은 타일/patch 단위 처리).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-geo-gdal` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 데이터

- 모든 노트북이 합성 래스터·벡터를 생성하므로 다운로드가 필요 없습니다.
- 실제 실습에서는 Landsat·Sentinel 등 위성영상을 `rasterio.open('영상.tif')`로 불러와 같은 방식으로 분석합니다.

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 지리공간 분석에 필요한 패키지가 미리 설치되어 있습니다. (rasterio가 GDAL을 wheel에 번들로 포함합니다.)

이 예제는 `ghcr.io/data-alliance/edu-geo-gdal:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.md)를 참고하세요.

**기준일:** 2026-11-10

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| rasterio | 1.5.0 | 래스터(위성영상·DEM) 입출력·처리(GDAL 기반) |
| geopandas | 1.1.3 | 벡터 데이터(점·선·면) 관리·공간 연산 |
| shapely | 2.1.2 | 기하 연산(면적·거리·교집합 등) |
| pyproj | 3.7.2 | 좌표계(CRS) 변환·투영 |
| scikit-image | 0.26.0 | 이미지 처리 |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함) |
| tqdm | 4.68.3 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |