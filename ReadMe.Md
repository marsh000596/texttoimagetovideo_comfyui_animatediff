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
ComfyUI/
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

Ready to Animate! 🚀


