# 이미지 태그와 패키지 버전 안내

이 저장소의 노트북은 EDU 템플릿 이미지의 **고정된 패키지 버전**을 기준으로 작성·검증되었습니다. 이 문서는 어떤 이미지 태그를 사용해야 하는지, 왜 버전을 고정했는지, 버전과 관련해 주의할 점을 정리합니다.

## 어떤 태그를 사용하나요

템플릿 이미지는 CUDA 버전별 태그로 제공됩니다. 배포할 노드의 **NVIDIA 드라이버 버전**에 맞는 태그를 선택합니다. 드라이버 버전은 컨테이너 터미널이나 노트북 셀에서 `nvidia-smi`로 확인할 수 있습니다.

| 템플릿 | CUDA 13.0 (드라이버 580 이상) | CUDA 12.8 (드라이버 570 이상) |
|---|---|---|
| edu-dl-tensorflow | — | `tf2.17-cuda12.8` |
| edu-ml-data | `ubuntu24.04-cuda13.0` | `ubuntu24.04-cuda12.8` |
| PyTorch 템플릿 9종 | `torch2.11-cuda13.0` | `torch2.11-cuda12.8` |

- 이미지 주소 형식은 `ghcr.io/data-alliance/<템플릿>:<태그>`입니다. 예: `ghcr.io/data-alliance/edu-cv-pytorch:torch2.11-cuda12.8`
- 같은 이미지가 Docker Hub [`gcubeai`](https://hub.docker.com/u/gcubeai)에도 같은 이름·태그로 있습니다. 예: `gcubeai/edu-cv-pytorch:torch2.11-cuda12.8`
- PyTorch 템플릿 9종: edu-cv-pytorch, edu-nlp-hf, edu-rl-pytorch, edu-genai-sd, edu-llm-train, edu-audio-pytorch, edu-medical-monai, edu-geo-gdal, edu-gnn-pyg
- 같은 템플릿이라면 CUDA 버전과 관계없이 **패키지 버전은 동일**하므로, 어떤 태그를 사용해도 같은 노트북을 그대로 실행할 수 있습니다.
- `latest` 태그는 가장 최신 조합을 가리키며, 새 조합이 나오면 옮겨질 수 있습니다. 실습 환경을 일정하게 유지하려면 `latest` 대신 위 태그를 사용하세요.

## 왜 버전을 고정하나요

- 노트북은 특정 패키지 버전의 API와 동작을 기준으로 작성되었습니다. 패키지가 바뀌면 함수 이름·인자·출력 형식이 달라져 노트북이 동작하지 않거나 결과가 달라질 수 있습니다.
- 버전을 고정하지 않으면 이미지를 다시 빌드할 때마다 그 시점의 최신 버전이 설치되어, 같은 태그라도 내용이 달라질 수 있습니다.
- 그래서 각 템플릿의 패키지 버전은 템플릿 저장소의 `requirements.txt`로 고정되어 있으며, 버전을 올릴 때는 노트북을 다시 확인한 뒤 반영합니다.

## 템플릿별 주요 버전

전체 버전 목록은 [gcube-edu-templates](https://github.com/Data-Alliance/gcube-edu-templates) 저장소의 각 템플릿 폴더에 있는 `requirements.txt`와 README의 "포함 환경"을 참고하세요.

| 템플릿 | 주요 버전 |
|---|---|
| edu-dl-tensorflow | TensorFlow 2.17, NumPy 1.26.4, scikit-learn 1.5.2 |
| edu-ml-data | NumPy 2.5.0, pandas 3.0.3, scikit-learn 1.9.0 |
| edu-cv-pytorch | PyTorch 2.11.0, albumentations 2.0.8, OpenCV 4.13 |
| edu-nlp-hf | PyTorch 2.11.0, transformers 5.12.1, datasets 5.0.0 |
| edu-rl-pytorch | PyTorch 2.11.0, gymnasium 1.3.0, stable-baselines3 2.9.0 |
| edu-genai-sd | PyTorch 2.11.0, diffusers 0.38.0, transformers 5.12.1 |
| edu-llm-train | PyTorch 2.11.0, transformers 5.12.1, peft 0.19.1, trl 1.6.0, bitsandbytes 0.49.2 |
| edu-audio-pytorch | PyTorch 2.11.0, librosa 0.11.0, openai-whisper 20250625 |
| edu-medical-monai | PyTorch 2.11.0, MONAI 1.6.0 |
| edu-geo-gdal | PyTorch 2.11.0, rasterio 1.5.0, geopandas 1.1.3 |
| edu-gnn-pyg | PyTorch 2.11.0, PyTorch Geometric 2.8.0 |

## 주의할 점

- **컨테이너 안에서 `pip install -U`로 기존 패키지를 올리지 마세요.** 노트북이 동작하지 않을 수 있습니다. 노트북에 없는 패키지를 새로 설치하는 것은 괜찮습니다.
- **PyTorch 템플릿은 torch 버전이 잠겨 있습니다.** torch를 다른 CUDA 빌드로 바꾸면 GPU를 사용할 수 없게 되므로, torch·torchvision·torchaudio·triton은 이미지에 설치된 버전에서 바뀌지 않도록 막혀 있습니다. 다른 torch 버전을 요구하는 패키지를 설치하면 `ResolutionImpossible` 오류가 나며 설치되지 않습니다.

## 다른 Python 버전이 필요할 때

이미지는 Ubuntu 24.04, Python 3.12 기준입니다. 다른 Python 버전이 필요하면 컨테이너 안에서 [uv](https://docs.astral.sh/uv/)로 별도 환경을 만들어 사용할 수 있습니다.

```bash
pip install uv
uv venv -p 3.10 /workspace/py310        # Python 3.10 환경 생성 (Python도 자동으로 내려받음)
source /workspace/py310/bin/activate
uv pip install ipykernel numpy pandas    # 필요한 패키지를 새 환경에 설치
python -m ipykernel install --user --name py310 --display-name "Python 3.10"
```

새 환경에는 패키지가 설치되어 있지 않으므로 torch 등 필요한 패키지를 다시 설치해야 합니다. 새 환경에서는 위 예시처럼 `uv pip`를 사용하세요. 일반 `pip`는 이미지에 설정된 torch 버전 잠금(`PIP_CONSTRAINT`)이 적용되어 새 환경에 다른 torch를 설치할 수 없습니다. 등록한 커널은 JupyterLab의 커널 선택에서 사용할 수 있습니다.
