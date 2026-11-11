# edu-cv-pytorch — 컴퓨터비전 실습

[English](README.md) | **한국어**

`edu-cv-pytorch` 컨테이너용 실습 예제입니다. PyTorch를 사용해 이미지 분류부터 전이학습, 데이터 증강까지 컴퓨터비전의 표준 흐름을 다룹니다. 모든 노트북은 **CIFAR-10** 데이터셋을 사용하며, 실행 시 Hugging Face Hub에서 자동으로 내려받아 `/workspace/.cache/huggingface`에 저장됩니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_image_classification_cnn.ipynb` | CNN을 직접 설계해 CIFAR-10 이미지를 분류합니다. 데이터 로드·시각화, CNN 구조 설계, 학습, 평가까지 딥러닝 컴퓨터비전의 기본 흐름을 익힙니다. |
| `02_transfer_learning.ipynb` | ImageNet 사전학습 ResNet18을 가져와 CIFAR-10에 미세조정합니다. 적은 학습으로 더 높은 정확도를 얻는 **전이학습**을 다룹니다. |
| `03_data_augmentation.ipynb` | albumentations로 데이터 증강을 적용하고, 증강 전후의 정확도를 비교해 일반화 성능 향상 효과를 확인합니다. |

## 실행 방법

1. `edu-cv-pytorch` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 시작과 동시에 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-cv-pytorch` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 데이터셋

- **CIFAR-10** — 10개 클래스(비행기, 자동차, 새, 고양이, 사슴, 개, 개구리, 말, 배, 트럭)의 32×32 컬러 이미지 6만 장.
- 노트북 실행 시 Hugging Face Hub(`uoft-cs/cifar10`)에서 자동으로 내려받아 `/workspace/.cache/huggingface`에 저장됩니다.
- CIFAR-10을 Hugging Face Hub에서 받기 위해 `datasets` 패키지가 필요합니다. 이 패키지는 컴퓨터비전 이미지 기본 구성에는 포함되지 않으므로, **각 노트북 첫 셀에서 `%pip install datasets`로 설치**합니다(한 번 설치하면 같은 세션에서는 다시 설치할 필요가 없습니다).

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 컴퓨터비전 실습에 필요한 패키지가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-cv-pytorch:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.ko.md)를 참고하세요.

**기준일:** 2026-11-10

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| torch, torchvision | 2.11.0, 0.26.0 (+cu130 / +cu128) | 딥러닝 프레임워크 및 비전 모델·데이터셋·이미지 변환 |
| opencv-python-headless | 4.13.0.92 | 이미지 읽기·처리 (GUI 없는 서버용 빌드) |
| albumentations | 2.0.8 | 데이터 증강 (회전·반전·밝기 변화 등) |
| Pillow | 12.1.1 | 기본 이미지 입출력 |
| scikit-learn | 1.9.0 | 평가 지표·전처리 등 보조 머신러닝 도구 |
| SciPy | 1.18.0 | 과학 연산 |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함 — 그래프 제목·라벨에 한글 사용 가능) |
| tqdm | 4.68.3 | 학습 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |