# edu-audio-pytorch — Speech and audio labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-audio-pytorch` container. Extract audio features with librosa, recognize speech with Whisper, and classify audio with a CNN on mel spectrograms.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_audio_features_librosa.ipynb` | Extract and visualize waveforms, spectrograms, mel spectrograms, and MFCCs with librosa. Learn the basic features used in audio deep learning. |
| `02_speech_recognition_whisper.ipynb` | Convert speech to text with OpenAI Whisper. Get the full transcript and per-segment timestamps. |
| `03_audio_classification.ipynb` | Convert audio to mel spectrograms and classify them with a CNN. Walk through the full pipeline using synthetic audio. |

## How to run

1. Deploy a workload with the `edu-audio-pytorch` template (GPU with 8 GB+ VRAM recommended; Whisper models of size medium or smaller recommended).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-audio-pytorch` folder and run the notebooks in order, starting with `01`.

## Models and data

- The example audio for 01 and 02 is included with librosa and is downloaded automatically on first run. In the labs, you can also use your own recordings.
- The Whisper model is downloaded automatically on first run.
- 03 generates synthetic audio, so no download is needed.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages and system tools (ffmpeg) needed for audio processing preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-audio-pytorch:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| torchaudio | 2.11.0 (+cu130 / +cu128) | PyTorch audio processing (transforms, I/O) |
| librosa | 0.11.0 | Audio analysis and feature extraction (spectrograms, MFCCs, etc.) |
| soundfile | 0.14.0 | Reading and writing audio files |
| openai-whisper | 20250625 | Speech recognition (speech-to-text) |
| ffmpeg (system) | System package | Decoding of various audio/video formats |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic) |
| tqdm | 4.68.3 | Progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |