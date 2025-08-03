Recommended Structure:
│
└───ComfyUI\
    │   main.py
    │   requirements.txt
    └───comfyenv\     ← your virtual environment lives here
    └───custom_nodes\


Full structure:
|
|ComfyUI/
├── models/
│   ├── animatediff_models/               Motion modules (.ckpt)
│   ├── animatediff_motion_lora/          Optional: Motion LoRA
│   ├── stable-diffusion/                 SD1.5 or RealisticVision base model
│   ├── vae/                              VAE model (.ckpt or .safetensors)
│
├── custom_nodes/
│   ├── ComfyUI-AnimateDiff-Evolved/     AnimateDiff-Evolved core
│   ├── ComfyUI-Advanced-ControlNet/     Advanced ControlNet support
│   ├── ComfyUI-VideoHelperSuite/        VHS (video IO and composer)
│   └── (other optional custom nodes)
│
├── input/                                You can place your image input here
├── output/                               Final video gets saved here
├── main.py                               ComfyUI launcher


# ComfyUI Custom AnimateDiff Project

This is a customized setup of ComfyUI with AnimateDiff-Evolved and several additional nodes, designed for anime and realistic video generation.

## Included Nodes
- AnimateDiff-Evolved
- ControlNet Auxiliary
- VHS (Video Helper Suite)
- WAS Node Suite
- ComfyUI Manager

## Credits
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [AnimateDiff-Evolved](https://github.com/continue-revolution/AnimateDiff)
- [VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
- [WAS Node Suite](https://github.com/WASasquatch/was-node-suite-comfyui)

Note- If the git clone doesd not work, Pleasw refer to original git link and copy from there 

1. Install Python (3.10 or 3.11 recommended) From: https://www.python.org/downloads/

2. Clone ComfyUI & Install Dependencies-
git clone https://github.com/comfyanonymous/ComfyUI.git
cd ComfyUI
cd ComfyUI/custom_nodes
git clone https://github.com/comfyanonymous/ComfyUI-VideoHelperExtension.git


3. Setup a Virtual Environment
cd ComfyUI
python -m venv comfyenv
.\comfyenv\Scripts\activate
pip install -r requirements.txt
deactivate - EXIT OUT ON ENV


4. Install AnimateDiff Node - Type :   cd ..   # to move 1 step back in a directory but stay in env only and move to below floder
Clone into the custom_nodes folder:
cd ComfyUI/custom_nodes
git clone https://github.com/Kosinkadink/ComfyUI-AnimateDiff-Evolved.git
cd ComfyUI-AnimateDiff-Evolved
pip install -r requirements.txt
After pulling clone, Close the running ComfyUI window
Just press Ctrl + C in the terminal window where it's running.

5.Download AnimateDiff Model (v3.1 Recommended)=v3_sd15_mm.ckpt
Place the .ckpt file into:
ComfyUI/models/animatediff_models
Final Result Should Look Like:
ComfyUI\
└── custom_nodes\
    └── ComfyUI-AnimateDiff-Evolved\
        └── models\
            └── motion_modules\
                └── v3_sd15_mm.ckpt

6. Download Stable Diffusion Model (Base for Animation)= Realistic Vision V5.1 , realisticVisionV60B1_v51HyperVAE.safetensors
ComfyUI/models/checkpoints/
ComfyUI\
└── models\
    └── checkpoints\
        └── realisticVisionV60B1_v51HyperVAE.safetensors

optional - ComfyUI/models/vae/vae-ft-mse-840000-ema-pruned.safetensors # Create the vae/ folder if it doesn’t exist.
If your workflow doesn’t specify a VAE, ComfyUI may use the default or skip it — so explicitly adding the node is best.

How to Install ComfyUI Manager (Node Manager)
Go to your custom_nodes directory:
ComfyUI/custom_nodes/
git clone https://github.com/ltdrdata/ComfyUI-Manager.git


7.Build the ComfyUI Workflow (Node-Based)
Prompt Generator (Text input)
AnimateDiff Loader Node
Sampler (KSampler or Euler)
Checkpoint Loader (SD model)
Conditioning + Latent Input
AnimateDiff video frame node
VAE Decoder
Save Image / Save MP4 node

8.Place the workflow in ComfyUI/workflows/
 and go to directory with main.py file and run in terinal 
 if there is error for CUDA assertion -  AssertionError: Torch not compiled with CUDA enabled
pip uninstall torch torchvision torchaudio -y
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
or
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
run below-
import torch
print(torch.cuda.is_available())  # Should return True , 
9.rerun main.py file 

once run go to http://127.0.0.1:8188


---------------------------------------------------


The latest versions of ComfyUI (after May 2024) require each node in the JSON to include:
Mandatory Fields per Node:
mode
order
flags
properties
inputs as an array
outputs as an array

Note: AnimateDiff is also offically supported by Diffusers. Visit AnimateDiff Diffusers Tutorial for more details. Following instructions is for working with this repository.
Note: For all scripts, checkpoint downloading will be automatically handled, so the script running may take longer time when first executed.


TIP-
Generate animations with comunity models-
python -m scripts.animate --config configs/prompts/1_animate/1_1_animate_RealisticVision.yaml
python -m scripts.animate --config configs/prompts/1_animate/1_2_animate_FilmVelvia.yaml
python -m scripts.animate --config configs/prompts/1_animate/1_3_animate_ToonYou.yaml
python -m scripts.animate --config configs/prompts/1_animate/1_4_animate_MajicMix.yaml
python -m scripts.animate --config configs/prompts/1_animate/1_5_animate_RcnzCartoon.yaml
python -m scripts.animate --config configs/prompts/1_animate/1_6_animate_Lyriel.yaml
python -m scripts.animate --config configs/prompts/1_animate/1_7_animate_Tusun.yaml

Generate animation with MotionLoRA control=
python -m scripts.animate --config configs/prompts/2_motionlora/2_motionlora_RealisticVision.yaml

More control with SparseCtrl RGB and sketch
python -m scripts.animate --config configs/prompts/3_sparsectrl/3_1_sparsectrl_i2v.yaml
python -m scripts.animate --config configs/prompts/3_sparsectrl/3_2_sparsectrl_rgb_RealisticVision.yaml
python -m scripts.animate --config configs/prompts/3_sparsectrl/3_3_sparsectrl_sketch_RealisticVision.yaml

------------------------------------------------------

