# edu-audio-pytorch — 음성·오디오 실습

`edu-audio-pytorch` 컨테이너용 실습 예제입니다. librosa로 오디오 특징을 추출하고, Whisper로 음성을 인식하며, 멜 스펙트로그램 기반 CNN으로 오디오를 분류합니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_audio_features_librosa.ipynb` | librosa로 파형, 스펙트로그램, 멜 스펙트로그램, MFCC를 추출·시각화합니다. 오디오 딥러닝의 기본 특징을 익힙니다. |
| `02_speech_recognition_whisper.ipynb` | OpenAI Whisper로 음성을 텍스트로 변환합니다. 전체 텍스트와 구간별 타임스탬프를 얻습니다. |
| `03_audio_classification.ipynb` | 오디오를 멜 스펙트로그램으로 변환해 CNN으로 분류합니다. 합성 오디오로 전체 파이프라인을 경험합니다. |

## 실행 방법

1. `edu-audio-pytorch` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장. Whisper는 medium 이하 모델 권장).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-audio-pytorch` 폴더를 열어 `01`부터 순서대로 실행합니다.

## 데이터·모델

- 01·02의 예제 오디오는 librosa에 포함되어 있으며 처음 실행 시 자동 다운로드됩니다. 실습에서는 직접 녹음한 파일을 사용할 수 있습니다.
- Whisper 모델은 처음 실행 시 자동 다운로드됩니다.
- 03은 합성 오디오를 생성하므로 다운로드가 필요 없습니다.

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 오디오 처리에 필요한 패키지와 시스템 도구(ffmpeg)가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-audio-pytorch:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.md)를 참고하세요.

**기준일:** 2026-06-19

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| torchaudio | 2.11.0 (+cu130 / +cu128) | PyTorch 오디오 처리(변환·I/O) |
| librosa | 0.11.0 | 오디오 분석·특징 추출(스펙트로그램·MFCC 등) |
| soundfile | 0.14.0 | 오디오 파일 읽기·쓰기 |
| openai-whisper | 20250625 | 음성 인식(speech-to-text) |
| ffmpeg (시스템) | 시스템 패키지 | 다양한 오디오/비디오 포맷 디코딩 |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함) |
| tqdm | 4.68.3 | 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |