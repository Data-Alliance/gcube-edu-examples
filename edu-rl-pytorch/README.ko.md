# edu-rl-pytorch — 강화학습 실습

[English](README.md) | **한국어**

`edu-rl-pytorch` 컨테이너용 실습 예제입니다. Gymnasium과 Stable-Baselines3로 강화학습의 기본 개념부터 에이전트 학습, 알고리즘 비교까지 다룹니다. 환경은 Gymnasium에 내장된 CartPole을 사용하므로 별도 다운로드가 필요 없습니다.

## 실습 순서

번호 순서대로 진행하는 것을 권장합니다.

| 노트북 | 내용 |
|---|---|
| `01_gymnasium_basics.ipynb` | Gymnasium 환경의 관측·행동·보상 구조와 상호작용 방식을 익히고, 무작위 정책의 성능을 측정해 기준선을 잡습니다. (CartPole) |
| `02_train_ppo_cartpole.ipynb` | Stable-Baselines3의 PPO로 CartPole을 학습하고, 학습 전후 평균 보상을 비교해 향상 효과를 확인합니다. |
| `03_compare_algorithms.ipynb` | PPO·A2C·DQN을 동일 조건으로 학습해 성능을 비교하며, 알고리즘별 특성과 선택의 중요성을 익힙니다. |

## 실행 방법

1. `edu-rl-pytorch` 템플릿으로 워크로드 배포 (GPU VRAM 8GB 이상 권장).
   실습 github repo를 clone 받아야 하는데, 방법은 두 가지입니다.
- 자동 clone — 환경변수 `GIT_CLONE_REPO`에 저장소 주소를 입력하면 워크로드 배포 시 자동으로 받아집니다.
- 직접 clone — 배포 후 워크로드 컨테이너의 내부 터미널에서 `git clone <repo 주소>`를 실행합니다.
2. JupyterLab에 접속합니다.
3. `edu-rl-pytorch` 폴더를 열어 `01`부터 순서대로 실행합니다.

학습 로그를 시각화하려면, 모델 생성 시 `tensorboard_log="/workspace/runs"`처럼 로그 경로를 지정한 뒤 tensorboard로 확인할 수 있습니다. (이 예제 노트북들은 결과를 Matplotlib 막대그래프로 비교하므로 tensorboard 설정은 포함하지 않았습니다.)

## 환경

- **CartPole-v1** — 막대를 쓰러뜨리지 않게 카트를 좌우로 움직이는 고전 제어 문제. Gymnasium 내장이라 다운로드가 필요 없습니다.

## 포함 환경

PyTorch 2.11 기반(CUDA 13.0·12.8 이미지 제공)이며, 강화학습 실습에 필요한 패키지가 미리 설치되어 있습니다.

이 예제는 `ghcr.io/data-alliance/edu-rl-pytorch:torch2.11-cuda13.0` 이미지 기준이며, CUDA 12.8 이미지(`:torch2.11-cuda12.8`)도 같은 패키지 버전으로 구성되어 있습니다. 태그 선택과 버전 고정에 대한 안내는 [VERSIONS.md](../VERSIONS.ko.md)를 참고하세요.

**기준일:** 2026-11-10

아래 버전은 해당 이미지 기준 스냅샷입니다. 패키지 버전은 템플릿의 `requirements.txt`로 고정되어 있으며, 현재 설치된 정확한 버전은 컨테이너 터미널에서 `pip show <패키지>`로 확인할 수 있습니다.

| 패키지 | 버전 | 역할 |
|---|---|---|
| gymnasium | 1.3.0 | 강화학습 환경(관측·행동·보상 인터페이스) |
| stable-baselines3 | 2.9.0 | 검증된 강화학습 알고리즘 구현(PPO·A2C·DQN 등) |
| tensorboard | 2.20.0 | 학습 로그·곡선 시각화 |
| Matplotlib | 3.11.0 | 시각화 (한글 폰트 NanumGothic 포함) |
| NumPy | 2.4.3 | 수치 배열 연산 |
| tqdm | 4.68.3 | 학습 진행 상황 표시 |
| ipywidgets | 8.1.8 | 위젯 기반 진행바·UI 렌더(tqdm 진행바 표시) |