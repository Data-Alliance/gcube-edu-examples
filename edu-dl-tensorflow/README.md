# edu-dl-tensorflow — TensorFlow/Keras 딥러닝 실습

`edu-dl-tensorflow` 컨테이너용 실습 예제입니다. TensorFlow의 고수준 API인 Keras로 이미지 분류, 전이학습, 과적합 대응까지 딥러닝의 표준 워크플로를 다룹니다. 데이터셋은 실행 시 자동으로 다운로드됩니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_image_classification_keras.ipynb` | Fashion-MNIST를 Keras로 분류합니다. 데이터 로드·시각화, 모델 정의(Sequential), `model.fit`/`evaluate`, 학습 곡선·예측 결과 시각화까지 TensorFlow/Keras의 기본 워크플로를 익힙니다. |
| `02_transfer_learning.ipynb` | ImageNet 사전학습 MobileNetV2를 Fashion-MNIST에 전이학습합니다. 흑백 이미지를 3채널·96×96으로 변환한 뒤, 특징 추출(freeze) 후 미세조정(fine-tuning)하며 Keras 전처리 레이어로 데이터 증강을 적용합니다. |
| `03_overfitting_callbacks.ipynb` | 과적합을 학습/검증 곡선으로 진단하고, 데이터 증강·Dropout·EarlyStopping 콜백으로 완화하는 효과를 비교합니다. |

## 실행 방법

1. `edu-dl-tensorflow` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-dl-tensorflow` 폴더를 열어 `01`부터 순서대로 실행합니다.

> 폴더의 `gcube_quiet.py`는 TensorFlow가 GPU 초기화 시 출력하는 무해한 경고 메시지를 걸러 주는 보조 파일입니다. 각 노트북 첫 셀에서 자동으로 불러오며, 직접 실행할 필요는 없습니다.

## 데이터셋

- **Fashion-MNIST** — 10종류 의류(티셔츠, 바지, 신발 등)의 28×28 흑백 이미지 7만 장. 딥러닝 입문 표준 데이터셋.
- 모두 `tf.keras.datasets`로 노트북 실행 시 자동 다운로드됩니다. 별도 준비가 필요 없습니다.

## 포함 환경

TensorFlow 2.17 (CUDA 12.8) 기반이며, 딥러닝 실습에 필요한 패키지가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-dl-tensorflow:tf2.17-cuda12.8` 이미지 기준입니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.md)를 참고하세요.

**기준일:** 2026-06-19

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| TensorFlow (Keras 포함) | 2.17.0 | 딥러닝 프레임워크 및 고수준 API. 모델 정의·학습·평가, 사전학습 모델(applications), 전처리 레이어 |
| scikit-learn | 1.5.2 | 평가 지표·전처리 등 보조 머신러닝 도구 |
| SciPy | 1.12.0 | 과학 연산 |
| Pillow | 12.2.0 | 기본 이미지 입출력 |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함 — 그래프 제목·라벨에 한글 사용 가능) |
| tqdm | 4.67.1 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |