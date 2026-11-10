# gcube-edu-examples

gcube EDU 템플릿용 실습 예제 모음입니다. EDU 템플릿 컨테이너로 워크로드를 배포한 뒤 이 저장소를 받으면, 바로 노트북 실습을 시작할 수 있습니다.

11개 EDU 템플릿에 1:1로 대응하는 11개 폴더로 구성되며, 각 폴더는 노트북 3개와 폴더별 안내(README)를 담고 있습니다.

## 사용 방법

1. 사용하려는 EDU 템플릿으로 gcube 워크로드를 배포합니다.
   실습 저장소를 받는 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 이 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. 배포한 템플릿과 같은 이름의 폴더를 열어 `01`부터 순서대로 실행합니다.

각 폴더는 해당 템플릿에 맞는 노트북만 담고 있습니다. 예를 들어 `edu-cv-pytorch` 템플릿을 배포했다면 `edu-cv-pytorch` 폴더를 사용합니다.

## 템플릿 목록

| 폴더 (= 템플릿) | 도메인 | 노트북 주제 |
|---|---|---|
| edu-cv-pytorch | 컴퓨터비전 | 이미지 분류(CNN) · 전이학습 · 데이터 증강 |
| edu-dl-tensorflow | TensorFlow 딥러닝 | 이미지 분류(Keras) · 전이학습 · 과적합 제어 |
| edu-ml-data | 기초 ML · 데이터분석 | EDA · 회귀 · 분류와 군집화 |
| edu-nlp-hf | 자연어처리 | pipeline 추론 · 텍스트 분류 파인튜닝 · 임베딩 검색 |
| edu-rl-pytorch | 강화학습 | gymnasium 기초 · PPO 학습 · 알고리즘 비교 |
| edu-genai-sd | 생성형 AI | text-to-image · 프롬프트와 파라미터 · img2img |
| edu-llm-train | LLM 파인튜닝 · RAG | LoRA · QLoRA · RAG(FAISS) |
| edu-audio-pytorch | 음성 · 오디오 | 오디오 특징(librosa) · 음성인식(Whisper) · 오디오 분류 |
| edu-medical-monai | 의료영상 | DICOM · NIfTI I/O · MONAI 변환 · UNet 분할 |
| edu-geo-gdal | 원격탐사 · 지리공간 | 래스터(rasterio) · 벡터(geopandas) · NDVI |
| edu-gnn-pyg | 그래프 신경망 | 그래프 기초(PyG) · 노드 분류(GCN) · 그래프 분류 |

## 폴더 구조

```
gcube-edu-examples/
├─ edu-cv-pytorch/
│  ├─ 01_image_classification_cnn.ipynb
│  ├─ 02_transfer_learning.ipynb
│  ├─ 03_data_augmentation.ipynb
│  └─ README.md
├─ edu-dl-tensorflow/        # 위와 동일하게 노트북 3개 + README.md
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

각 폴더의 README에 해당 템플릿의 실습 순서, 권장 GPU 사양, 포함 환경이 정리되어 있습니다.

## 공통 사항

- 모든 노트북은 JupyterLab에서 위에서 아래로 순서대로 실행하도록 구성되어 있습니다.
- 시각화는 한글 폰트(NanumGothic)를 사용합니다.
- 템플릿 이미지는 CUDA 버전별 태그로 제공되며, 패키지 버전이 고정되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](VERSIONS.md)를 참고하세요.
- 데이터셋·모델은 노트북 실행 시 자동 다운로드되어 `/workspace/.cache`에 저장됩니다. (일부 노트북은 합성 데이터를 사용해 다운로드가 필요 없습니다.)
- 노트북마다 커널이 따로 실행되며, 실행이 끝나도 커널을 종료하기 전까지 GPU 메모리를 계속 사용합니다. 여러 노트북을 함께 열어두면 GPU 사양(VRAM)에 따라 메모리가 부족해 커널이 종료될 수 있습니다. 특히 `edu-genai-sd`, `edu-llm-train`처럼 큰 모델을 다루는 노트북은 다음 노트북으로 넘어가기 전에 **Kernel → Shut Down Kernel**로 이전 노트북의 커널을 종료하세요. 실행 중인 커널은 왼쪽 사이드바의 **Running Terminals and Kernels**에서 한 번에 확인하고 종료할 수 있습니다.