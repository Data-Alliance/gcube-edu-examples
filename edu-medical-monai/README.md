# edu-medical-monai — 의료영상 실습

`edu-medical-monai` 컨테이너용 실습 예제입니다. 의료영상 포맷(DICOM·NIfTI) 처리부터 MONAI 전처리·증강, UNet 분할까지 의료영상 딥러닝의 표준 흐름을 다룹니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_medical_image_io.ipynb` | DICOM(pydicom)과 NIfTI(nibabel)로 의료영상을 읽고, 3D 볼륨을 단면으로 시각화하며, SimpleITK로 메타데이터를 확인합니다. |
| `02_monai_transforms.ipynb` | MONAI transforms로 의료영상을 전처리(강도 정규화 등)하고 증강(뒤집기·회전·잡음)하며, `Compose`로 파이프라인을 구성합니다. |
| `03_segmentation_unet.ipynb` | MONAI UNet과 DiceLoss로 분할 모델을 학습하고 Dice 점수로 평가합니다. 합성 데이터로 분할 전체 흐름을 경험합니다. |

## 실행 방법

1. `edu-medical-monai` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장. 3D 분할은 더 큰 VRAM 필요).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-medical-monai` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 데이터

- 01의 DICOM 예제는 pydicom에 내장되어 있습니다.
- 02·03은 합성 영상·볼륨을 생성하므로 다운로드가 필요 없습니다.
- 실제 실습에서는 MedNIST, MSD(Spleen·Liver 등) 같은 데이터셋이나 직접 보유한 DICOM/NIfTI를 사용합니다.

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 의료영상 처리에 필요한 패키지가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-medical-monai:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.md)를 참고하세요.

**기준일:** 2026-11-10

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| MONAI | 1.6.0 | 의료영상 딥러닝 프레임워크(전처리·증강·UNet 등 모델·손실·지표) |
| nibabel | 5.4.2 | NIfTI 등 신경영상 포맷 입출력 |
| pydicom | 3.0.2 | DICOM 파일 읽기·쓰기 |
| SimpleITK | 2.5.5 | 의료영상 I/O·처리(리샘플링·등록 등) |
| scikit-image | 0.26.0 | 일반 이미지 처리 |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함) |
| tqdm | 4.68.3 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |