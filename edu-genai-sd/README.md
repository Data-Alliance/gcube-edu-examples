# edu-genai-sd — 생성형 AI(Stable Diffusion) 실습

`edu-genai-sd` 컨테이너용 실습 예제입니다. Hugging Face `diffusers`로 Stable Diffusion을 사용해 텍스트→이미지 생성, 프롬프트·파라미터 실험, 이미지→이미지 변환을 다룹니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_text_to_image.ipynb` | StableDiffusionPipeline으로 텍스트 프롬프트에서 이미지를 생성합니다. 파이프라인 로드, 생성, 여러 프롬프트 비교. |
| `02_prompt_and_parameters.ipynb` | `guidance_scale`·`num_inference_steps`·네거티브 프롬프트가 결과에 미치는 영향을 같은 seed로 비교 실험합니다. |
| `03_img2img.ipynb` | 입력 이미지와 프롬프트로 새 이미지를 생성하는 img2img를 다루고, `strength`(변형 정도)를 비교합니다. |

## 실행 방법

1. `edu-genai-sd` 템플릿으로 워크로드 배포 (GPU VRAM 16GB 이상 권장. SDXL 등 대형 모델은 24GB 이상).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-genai-sd` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 모델

- Stable Diffusion v1.5 모델은 노트북 실행 시 Hugging Face Hub에서 자동 다운로드되어 `/workspace/.cache/huggingface`에 저장됩니다. GPU 환경에서는 절반 크기의 fp16 변형(`variant='fp16'`)을 받아 다운로드 용량을 줄입니다. 그래도 모델이 수 GB이므로 처음 실행 시 다운로드에 시간이 걸릴 수 있으며, 한 번 받으면 이후에는 캐시에서 빠르게 로드됩니다.
- 이미지 생성은 GPU 메모리를 많이 사용합니다. 메모리가 빠듯하면 `enable_attention_slicing()`을 사용하세요.
- 노트북 기본 모델(Stable Diffusion v1.5)은 VRAM 8GB에서도 동작합니다. 16GB 권장은 SDXL 등 대형 모델이나 LoRA 학습을 할 때 기준입니다.

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 생성형 AI 실습에 필요한 패키지가 미리 설치되어 있습니다. 어텐션 연산은 PyTorch 내장 SDPA를 사용합니다(별도 xformers 불필요).

이 예제는 `ghcr.io/data-alliance/edu-genai-sd:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.md)를 참고하세요.

**기준일:** 2026-06-19

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| diffusers | 0.38.0 | 확산 모델 파이프라인(text-to-image·img2img 등) |
| transformers | 5.12.1 | 텍스트 인코더(CLIP) 등 모델 구성 요소 |
| accelerate | 1.14.0 | 모델 로딩·실행 가속 |
| safetensors | 0.8.0 | 안전한 모델 가중치 포맷 |
| datasets | 5.0.0 | 데이터셋 로드(파인튜닝 시) |
| opencv-python-headless | 4.13.0.92 | 이미지 처리 |
| Pillow | 12.1.1 | 이미지 입출력 |
| tqdm | 4.68.3 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |