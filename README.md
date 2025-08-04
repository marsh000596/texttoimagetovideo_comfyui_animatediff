# 🤖 ComfyUI + AnimateDiff Setup Guide for custom texttoimagetovideo_comfyui_animatediff

A comprehensive setup guide and environment structure for using **ComfyUI** with **AnimateDiff** for animation generation workflows.

---

## 🌐 Recommended Directory Structure

```
A:/OPENAI/
└── ComfyUI/
    ├── main.py
    ├── requirements.txt
    ├── comfyenv/              ← your virtual environment
    └── custom_nodes/
```

---

## ✅ Prerequisites

### 1. Install Python

Download and install **Python 3.10** or **3.11** from:
[https://www.python.org/downloads/](https://www.python.org/downloads/)

---

## ⚡ Clone and Setup ComfyUI

```bash
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
```

### Optional: Install Video Helper Extension

```bash
cd custom_nodes
git clone https://github.com/comfyanonymous/ComfyUI-VideoHelperExtension.git
```

---

## 📚 Setup Virtual Environment

```bash
python -m venv comfyenv
.\comfyenv\Scripts\activate
pip install -r requirements.txt
deactivate
```

---

## 👨‍💨 Install AnimateDiff Node

```bash
cd ComfyUI/custom_nodes
# Pick one of the working repos

git clone https://github.com/Kosinkadink/ComfyUI-AnimateDiff-Evolved.git
cd ComfyUI-AnimateDiff-Evolved
pip install -r requirements.txt
```

---

## 📂 Add Models

### 1. AnimateDiff Model (v3.1 recommended)

* Download: `v3_sd15_mm.ckpt`
* Place into: `ComfyUI/models/animatediff_models/`

### 2. Stable Diffusion Base Model

* Recommended: `RealisticVisionV60B1_v51HyperVAE.safetensors`
* Place into: `ComfyUI/models/checkpoints/`

### 3. VAE (optional)

* File: `vae-ft-mse-840000-ema-pruned.safetensors`
* Place into: `ComfyUI/models/vae/`

---

## 👩‍💳 Install ComfyUI Manager

```bash
cd ComfyUI/custom_nodes/
git clone https://github.com/ltdrdata/ComfyUI-Manager.git
```

---

## 🔄 Workflow Build Order

1. Prompt Generator
2. AnimateDiff Loader
3. KSampler / Euler
4. Checkpoint Loader
5. Conditioning + Latent Input
6. AnimateDiff Video Frame Node
7. VAE Decoder
8. Save Image / MP4

> Save the workflow JSON into: `ComfyUI/workflows/`

---

## 🧪 CUDA Fix (if required)

```bash
pip uninstall torch torchvision torchaudio -y
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121

python
>>> import torch
>>> print(torch.cuda.is_available())  # Should return True
```

---

## 🕹️ Launch the App

```bash
# From the ComfyUI folder:
python main.py
```

Visit in browser: [http://127.0.0.1:8188](http://127.0.0.1:8188)

---

## 📖 JSON Node Requirement (Post-May 2024)

Every node must include:

* `mode`
* `order`
* `flags`
* `properties`
* `inputs` (array)
* `outputs` (array)

---

## 🎓 AnimateDiff Quick Start (Alt Script)

```bash
git clone https://github.com/guoyww/AnimateDiff.git
cd AnimateDiff
pip install -r requirements.txt
```

### Run Samples:

```bash
python -m scripts.animate --config configs/prompts/1_animate/1_1_animate_RealisticVision.yaml
```

---

## 📆 Recommended Files Checklist

| Type             | File                                     | Location                    |
| ---------------- | ---------------------------------------- | --------------------------- |
| Base Model       | realisticVisionV51.safetensors           | models/checkpoints/         |
| VAE (optional)   | vae-ft-mse-840000-ema-pruned.safetensors | models/vae/                 |
| Motion Module    | v3\_sd15\_mm.ckpt                        | models/animatediff\_models/ |
| AnimateDiff Node | ComfyUI-AnimateDiff-Evolved              | custom\_nodes/              |

---

## 🔎 Useful Repos and Extensions

* [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
* [AnimateDiff Evolved](https://github.com/continue-revolution/AnimateDiff)
* [ComfyUI Manager](https://github.com/ltdrdata/ComfyUI-Manager)
* [VHS](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
* [WAS Node Suite](https://github.com/WASasquatch/was-node-suite-comfyui)

---

## 📋 License

MIT License. Refer to individual repositories for original licenses.

---

## ✅ Summary: What You Should Have

```
ComfyUI/      # here my directory name is texttoimagetovideo
├── models/
│   ├── animatediff_models/       ✓ v3_sd15_mm.ckpt
│   ├── checkpoints/              ✓ RealisticVisionV51.safetensors
│   ├── vae/                      ✓ VAE (optional)
│
├── custom_nodes/
│   ├── ComfyUI-AnimateDiff-Evolved/
│   ├── ComfyUI-VideoHelperSuite/
│   ├── ComfyUI-Manager/
│   └── (optional control net)
│
├── input/
├── output/
├── main.py
```

<img width="797" height="266" alt="Screenshot 2025-08-04 020706" src="https://github.com/user-attachments/assets/35da536d-6906-494c-81ea-74954b323ce8" />

##


<img width="1481" height="546" alt="image" src="https://github.com/user-attachments/assets/2a12ccf8-7437-406e-b3ca-130a7a923810" />

##
<img width="1913" height="879" alt="Screenshot 2025-08-04 020600" src="https://github.com/user-attachments/assets/bbe52bbc-146a-4c18-8df8-3d728cd72603" />

##
<img width="1913" height="879" alt="Screenshot 2025-08-04 020600" src="https://github.com/user-attachments/assets/85c66c7f-2b28-405a-be5e-cdb6bf76f751" />

##



<img width="1119" height="542" alt="image" src="https://github.com/user-attachments/assets/af15ad57-cb4f-46e9-8c65-758b2e201160" />


# This project represents a cutting-edge AI video generation system built using ComfyUI as the foundational node-based interface and AnimateDiff-Evolved for dynamic animation capabilities. The goal is to create a modular, customizable pipeline that enables users to generate high-quality, frame-consistent animations from text or image prompts using state-of-the-art models like Realistic Vision v5.1 and AnimateDiff v3.1+.

✅ What We’ve Achieved So Far
✅ Core Integration:

Set up ComfyUI with custom nodes like AnimateDiff-Evolved, ComfyUI-Manager, VideoHelperSuite, and deforum.

Verified GPU acceleration via CUDA + PyTorch + NVIDIA driver pipeline.

✅ Animation Workflows Built:

Text-to-Video Pipeline: From prompt → latent render → video synthesis.

Image-to-Video Pipeline: Conditioned animation from base image + prompt.

Realistic Vision Integration: Seamless use of RV5.1 as the base checkpoint for lifelike visuals.

Prompt Interpolation & keyframe animation with Deforum-like camera effects.

✅ Manual & JSON Workflow Creation:

Built reusable .json workflows for AnimateDiff with specific frame rates, resolution presets, and conditioning settings.

Custom prompt engineering enabled via token sliders and scheduling.

✅ UI Portal Setup:

An interactive ML prediction UI (FastAPI + Jinja2 + Docker) for easier model experimentation.

🧪 Ongoing & In-Progress Work
🚧 Advanced Workflow Variants under development:

Anime-focused pipelines (AnimeDiff v1.1 + MMDET tokenizer).

Cinematic prompt-to-video stories with frame stitching and voiceover.

Style-transfer workflows that mix Stable Diffusion XL + AnimateDiff.

🚧 n8n Automation Integration:

Prompt generation automation + render queuing for continuous batch video generation.

🚧 Post-Processing Additions:

Audio syncing (via TTS or external WAV input).

Upscaling pipeline with Real-ESRGAN or Topaz AI for 2K/4K exports.

Video stabilization and noise removal.

📈 Future Goals
One-Click Video Studio Setup: Pre-built Docker container or EXE installer for all workflows + models.

Community Workflow Library: Public gallery of .json workflows for plug-and-play use.

ComfyUI Web Interface: Expose the UI via browser for remote rendering.

Render Farm Compatibility: Batch video generation across multiple GPUs or machines.

AI Director System: Automatically generate scene flows, camera paths, and prompts from a single story input.

🎯 Why This Project Matters
Enables non-programmers, artists, and creators to harness generative video tools with no coding required.

Acts as a foundation for future AI-powered storytelling, cinematic production, and real-time rendering.

Bridges the gap between local AI deployment and cloud video generation platforms.

Highly adaptable — anyone from students to indie game studios can use this as a launching pad.

🧰 Tools & Technologies Used
ComfyUI, AnimateDiff, Deforum, RealisticVision

PyTorch, CUDA, xformers

Docker, FastAPI, Python

JSON workflows, Jinja2 UI Templates

GitHub, VSCode, ffmpeg, Web UI

📦 Current Repository Highlights
/ComfyUI/: Core UI + nodes

/custom_nodes/: AnimateDiff, Manager, VideoHelperSuite, Deforum, etc.

/models/: Stable Diffusion checkpoints, motion modules

/workflows/: Ready-to-run AnimateDiff .json files

/app/: API + prediction interface (under development)

/README.md: Full setup instructions (just published)

Ready to Animate! 🚀



