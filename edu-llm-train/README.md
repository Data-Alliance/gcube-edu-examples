# edu-llm-train — LLM 파인튜닝·RAG 실습

`edu-llm-train` 컨테이너용 실습 예제입니다. LoRA·QLoRA로 LLM을 효율적으로 파인튜닝하고, FAISS 기반 RAG(검색 증강 생성)를 구현합니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_lora_finetuning.ipynb` | LoRA로 원본 가중치는 고정하고 작은 추가 행렬만 학습합니다. `peft` + `trl` SFTTrainer로 작은 LLM을 instruction 데이터에 지도 파인튜닝합니다. |
| `02_qlora_4bit.ipynb` | bitsandbytes 4비트 양자화 + LoRA(QLoRA)로 더 적은 메모리에서 LLM을 파인튜닝합니다. 제한된 자원에서 LLM을 다루는 표준 기법. |
| `03_rag_faiss.ipynb` | 문서를 임베딩으로 변환해 FAISS로 색인·검색하고, 검색 결과를 LLM 프롬프트에 넣어 답변을 생성하는 RAG를 구현합니다. |

## 실행 방법

1. `edu-llm-train` 템플릿으로 워크로드 배포 (GPU VRAM 16GB 이상 권장. 7B 이상 모델 QLoRA 시 24GB 이상).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-llm-train` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 모델·데이터

- 모델(TinyLlama 등)과 데이터셋(Alpaca 등)은 노트북 실행 시 Hugging Face Hub에서 자동 다운로드되어 `/workspace/.cache/huggingface`에 저장됩니다.
- 4비트 양자화(bitsandbytes)와 QLoRA는 CUDA GPU가 필요합니다.
- 노트북 기본 모델(TinyLlama 1.1B)은 VRAM 8GB에서도 동작합니다. 16GB 권장은 7B 이상 대형 모델을 QLoRA로 학습할 때 기준입니다.

## 포함 환경

PyTorch 2.11 (CUDA 13.0) 기반이며, LLM 파인튜닝·RAG에 필요한 패키지가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-llm-train:20260619` 이미지 기준입니다.

**기준일:** 2026-06-19

아래 버전은 해당 이미지 기준 스냅샷입니다. 이미지 재빌드 시 일부 버전이 달라질 수 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| transformers | 5.12.1 | LLM·토크나이저·pipeline |
| datasets | 5.0.0 | 데이터셋 로드·전처리 |
| peft | 0.19.1 | LoRA 등 효율적 파인튜닝(PEFT) |
| trl | 1.6.0 | SFTTrainer 등 LLM 지도 파인튜닝 |
| bitsandbytes | 0.49.2 | 4비트/8비트 양자화(QLoRA) |
| accelerate | 1.14.0 | 학습 가속·분산 처리 |
| faiss-cpu | 1.14.3 | 벡터 색인·유사도 검색(RAG) |
| sentencepiece | 0.2.1 | 서브워드 토크나이저 |
| einops | 0.8.2 | 텐서 연산 표기 |
| evaluate, scikit-learn | 0.4.6, 1.9.0 | 평가 지표 |
| tensorboard | 2.20.0 | 학습 로그 시각화 |
| tqdm | 4.68.3 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |