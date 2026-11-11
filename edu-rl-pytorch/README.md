# edu-rl-pytorch — Reinforcement learning labs

**English** | [한국어](README.ko.md)

Lab examples for the `edu-rl-pytorch` container. Using Gymnasium and Stable-Baselines3, they cover reinforcement learning from basic concepts to agent training and algorithm comparison. The environment is CartPole, built into Gymnasium, so no separate download is needed.

## Lab order

We recommend going through the notebooks in numbered order.

| Notebook | Description |
|---|---|
| `01_gymnasium_basics.ipynb` | Learn the observation, action, and reward structure of a Gymnasium environment and how to interact with it, and measure the performance of a random policy as a baseline. (CartPole) |
| `02_train_ppo_cartpole.ipynb` | Train CartPole with PPO from Stable-Baselines3, and compare the mean reward before and after training to see the improvement. |
| `03_compare_algorithms.ipynb` | Train PPO, A2C, and DQN under the same conditions and compare their performance, learning the characteristics of each algorithm and why the choice matters. |

## How to run

1. Deploy a workload with the `edu-rl-pytorch` template (GPU with 8 GB+ VRAM recommended).
   You need to clone the lab GitHub repo. There are two ways to do this.
- Automatic clone — set the environment variable `GIT_CLONE_REPO` to the repository URL, and it is cloned automatically when the workload is deployed.
- Manual clone — after deployment, run `git clone <repo URL>` in the workload container's terminal.
2. Open JupyterLab.
3. Open the `edu-rl-pytorch` folder and run the notebooks in order, starting with `01`.

To visualize training logs, set a log path when creating the model, such as `tensorboard_log="/workspace/runs"`, and view it with tensorboard. (These notebooks compare results with Matplotlib bar charts, so they do not include tensorboard setup.)

## Environment

- **CartPole-v1** — a classic control problem: move a cart left and right to keep a pole from falling. It is built into Gymnasium, so no download is needed.

## Installed packages

Based on PyTorch 2.11 (CUDA 13.0 and 12.8 images available), with the packages needed for reinforcement learning labs preinstalled.

These examples are based on the `ghcr.io/data-alliance/edu-rl-pytorch:torch2.11-cuda13.0` image. The CUDA 12.8 image (`:torch2.11-cuda12.8`) has the same package versions. See [VERSIONS.md](../VERSIONS.md) for how to choose a tag and how versions are pinned.

**As of:** 2026-11-10

The versions below are a snapshot of this image. Package versions are pinned in the template's `requirements.txt`. Run `pip show <package>` in the container terminal to check the exact installed version.

| Package | Version | Role |
|---|---|---|
| gymnasium | 1.3.0 | Reinforcement learning environments (observation, action, reward interface) |
| stable-baselines3 | 2.9.0 | Proven reinforcement learning algorithm implementations (PPO, A2C, DQN, etc.) |
| tensorboard | 2.20.0 | Training log and curve visualization |
| Matplotlib | 3.11.0 | Visualization (includes the Korean font NanumGothic) |
| NumPy | 2.4.3 | Numerical array operations |
| tqdm | 4.68.3 | Training progress display |
| ipywidgets | 8.1.8 | Widget-based progress bars and UI rendering (displays tqdm progress bars) |