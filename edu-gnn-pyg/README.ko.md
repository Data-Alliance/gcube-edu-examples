# edu-gnn-pyg — 그래프 신경망 실습

[English](README.md) | **한국어**

`edu-gnn-pyg` 컨테이너용 실습 예제입니다. PyTorch Geometric으로 그래프 데이터 구조부터 노드 분류, 그래프 분류까지 그래프 신경망(GNN)의 표준 흐름을 다룹니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_graph_basics_pyg.ipynb` | 그래프를 PyG `Data`(노드 특징·엣지)로 표현하고 networkx로 시각화하며, GCN 레이어의 메시지 패싱을 이해합니다. |
| `02_node_classification_gcn.ipynb` | 인용 네트워크 Cora에서 2층 GCN으로 노드를 분류합니다. 그래프의 이웃 정보를 활용하는 GNN의 핵심을 다룹니다. |
| `03_graph_classification.ipynb` | 그래프 하나를 하나의 샘플로 보는 그래프 분류를 다룹니다. `global_mean_pool`로 그래프 표현을 만들고 배치 학습합니다. |

## 실행 방법

1. `edu-gnn-pyg` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-gnn-pyg` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 데이터

- 02의 Cora 데이터셋은 노트북 실행 시 자동 다운로드됩니다.
- 01·03은 합성 그래프를 생성하므로 다운로드가 필요 없습니다.

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 그래프 신경망 실습에 필요한 패키지가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-gnn-pyg:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.ko.md)를 참고하세요.

**기준일:** 2026-11-10

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| torch-geometric | 2.8.0 | 그래프 신경망 라이브러리(GCNConv 등 레이어·Data·데이터셋·풀링) |
| networkx | 3.6.1 | 그래프 생성·분석·시각화 |
| scikit-learn | 1.9.0 | 평가·전처리·차원축소 등 보조 도구 (이 예제 노트북에서는 직접 사용하지 않음) |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함) |
| tqdm | 4.68.3 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |