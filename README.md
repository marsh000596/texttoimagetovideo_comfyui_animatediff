# texttoimagetovideo_comfyui_animatediff
This is a customized setup of ComfyUI with AnimateDiff-Evolved and several additional nodes, designed for anime and realistic video generation.

## Included Nodes
- AnimateDiff-Evolved
- ControlNet Auxiliary
- VHS (Video Helper Suite)
- WAS Node Suite
- ComfyUI Manager


##

Recommended Structure:
│
└───ComfyUI\
    │   main.py
    │   requirements.txt
    └───comfyenv\     ← your virtual environment lives here
    └───custom_nodes\

##

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


##

Note- If the git clone doesd not work, Pleasw refer to original git link and copy from there 

##

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

##
once run go to http://127.0.0.1:8188
##


optional - ComfyUI/models/vae/vae-ft-mse-840000-ema-pruned.safetensors # Create the vae/ folder if it doesn’t exist.
If your workflow doesn’t specify a VAE, ComfyUI may use the default or skip it — so explicitly adding the node is best.

##

How to Install ComfyUI Manager (Node Manager)
Go to your custom_nodes directory:
ComfyUI/custom_nodes/
git clone https://github.com/ltdrdata/ComfyUI-Manager.git

##

---------------------------------------------------

##

The latest versions of ComfyUI (after May 2024) require each node in the JSON to include:
Mandatory Fields per Node:
mode
order
flags
properties
inputs as an array
outputs as an array

##


Note: AnimateDiff is also offically supported by Diffusers. Visit AnimateDiff Diffusers Tutorial for more details. Following instructions is for working with this repository.
Note: For all scripts, checkpoint downloading will be automatically handled, so the script running may take longer time when first executed.

##


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



##

[wf3.json](https://github.com/user-attachments/files/21567897/wf3.json)
{
  "2": {
    "inputs": {
      "vae_name": "vae-ft-mse-840000-ema-pruned.safetensors"
    },
    "class_type": "VAELoader",
    "_meta": {
      "title": "Load VAE"
    }
  },
  "3": {
    "inputs": {
      "text": "1boy, solo, outdoors, city, dancing, jeans, dress shirt, blonde hair, long hair, brown eyes",
      "clip": [
        "4",
        0
      ]
    },
    "class_type": "CLIPTextEncode",
    "_meta": {
      "title": "CLIP Text Encode (Prompt)"
    }
  },
  "4": {
    "inputs": {
      "stop_at_clip_layer": -2,
      "clip": [
        "30",
        1
      ]
    },
    "class_type": "CLIPSetLastLayer",
    "_meta": {
      "title": "CLIP Set Last Layer"
    }
  },
  "6": {
    "inputs": {
      "text": "(worst quality, low quality: 1.4)",
      "clip": [
        "4",
        0
      ]
    },
    "class_type": "CLIPTextEncode",
    "_meta": {
      "title": "CLIP Text Encode (Prompt)"
    }
  },
  "7": {
    "inputs": {
      "seed": 44444444,
      "steps": 20,
      "cfg": 8,
      "sampler_name": "euler",
      "scheduler": "normal",
      "denoise": 1,
      "model": [
        "33",
        0
      ],
      "positive": [
        "24",
        0
      ],
      "negative": [
        "24",
        1
      ],
      "latent_image": [
        "9",
        0
      ]
    },
    "class_type": "KSampler",
    "_meta": {
      "title": "KSampler"
    }
  },
  "9": {
    "inputs": {
      "width": 512,
      "height": 768,
      "batch_size": [
        "50",
        2
      ]
    },
    "class_type": "EmptyLatentImage",
    "_meta": {
      "title": "Empty Latent Image"
    }
  },
  "10": {
    "inputs": {
      "samples": [
        "7",
        0
      ],
      "vae": [
        "2",
        0
      ]
    },
    "class_type": "VAEDecode",
    "_meta": {
      "title": "VAE Decode"
    }
  },
  "20": {
    "inputs": {
      "control_net_name": "control_v11p_sd15_openpose.pth"
    },
    "class_type": "ControlNetLoaderAdvanced",
    "_meta": {
      "title": "Load Advanced ControlNet Model 🛂🅐🅒🅝"
    }
  },
  "24": {
    "inputs": {
      "strength": 1,
      "start_percent": 0,
      "end_percent": 1,
      "positive": [
        "3",
        0
      ],
      "negative": [
        "6",
        0
      ],
      "control_net": [
        "20",
        0
      ],
      "image": [
        "50",
        0
      ]
    },
    "class_type": "ControlNetApplyAdvanced",
    "_meta": {
      "title": "Apply ControlNet"
    }
  },
  "30": {
    "inputs": {
      "ckpt_name": "cardosAnime_v20.safetensors"
    },
    "class_type": "CheckpointLoaderSimple",
    "_meta": {
      "title": "Load Checkpoint"
    }
  },
  "33": {
    "inputs": {
      "model_name": "temporaldiff-v1-animatediff.ckpt",
      "beta_schedule": "sqrt_linear (AnimateDiff)",
      "motion_scale": 1,
      "apply_v2_models_properly": true,
      "model": [
        "30",
        0
      ],
      "context_options": [
        "34",
        0
      ]
    },
    "class_type": "ADE_AnimateDiffLoaderWithContext",
    "_meta": {
      "title": "AnimateDiff Loader [Legacy] 🎭🅐🅓①"
    }
  },
  "34": {
    "inputs": {
      "context_length": 16,
      "context_stride": 1,
      "context_overlap": 4,
      "context_schedule": "uniform",
      "closed_loop": false,
      "fuse_method": "flat",
      "use_on_equal_length": false,
      "start_percent": 0,
      "guarantee_steps": 1
    },
    "class_type": "ADE_AnimateDiffUniformContextOptions",
    "_meta": {
      "title": "Context Options◆Looped Uniform 🎭🅐🅓"
    }
  },
  "39": {
    "inputs": {
      "images": [
        "50",
        0
      ]
    },
    "class_type": "PreviewImage",
    "_meta": {
      "title": "Preview Image"
    }
  },
  "40": {
    "inputs": {
      "upscale_method": "nearest-exact",
      "scale_by": 1.5,
      "samples": [
        "7",
        0
      ]
    },
    "class_type": "LatentUpscaleBy",
    "_meta": {
      "title": "Upscale Latent By"
    }
  },
  "41": {
    "inputs": {
      "seed": 44444444,
      "steps": 20,
      "cfg": 8,
      "sampler_name": "euler",
      "scheduler": "normal",
      "denoise": 1,
      "model": [
        "33",
        0
      ],
      "positive": [
        "24",
        0
      ],
      "negative": [
        "24",
        1
      ],
      "latent_image": [
        "40",
        0
      ]
    },
    "class_type": "KSampler",
    "_meta": {
      "title": "KSampler"
    }
  },
  "42": {
    "inputs": {
      "samples": [
        "41",
        0
      ],
      "vae": [
        "2",
        0
      ]
    },
    "class_type": "VAEDecode",
    "_meta": {
      "title": "VAE Decode"
    }
  },
  "50": {
    "inputs": {
      "directory": "openpose_full/",
      "image_load_cap": 48,
      "skip_first_images": 0,
      "select_every_nth": 1
    },
    "class_type": "VHS_LoadImages",
    "_meta": {
      "title": "Load Images (Upload) 🎥🅥🅗🅢"
    }
  },
  "51": {
    "inputs": {
      "frame_rate": 8,
      "loop_count": 0,
      "filename_prefix": "aaa_readme_cn",
      "format": "image/gif",
      "pingpong": false,
      "save_output": true,
      "images": [
        "10",
        0
      ]
    },
    "class_type": "VHS_VideoCombine",
    "_meta": {
      "title": "Video Combine 🎥🅥🅗🅢"
    }
  },
  "52": {
    "inputs": {
      "frame_rate": 8,
      "loop_count": 0,
      "filename_prefix": "aaa_readme_cn",
      "format": "image/gif",
      "pingpong": false,
      "save_output": true,
      "images": [
        "42",
        0
      ]
    },
    "class_type": "VHS_VideoCombine",
    "_meta": {
      "title": "Video Combine 🎥🅥🅗🅢"
    }
  }
}


##

[wf1.json](https://github.com/user-attachments/files/21567890/wf1.json)[wf3.json](https://github.com/user-attachments/files/21567872/wf3.json)

##

<img width="1481" height="546" alt="image" src="https://github.com/user-attachments/assets/f625d745-e8f3-47b3-b216-9bf4a9f98101" />

##

<img width="1913" height="879" alt="image" src="https://github.com/user-attachments/assets/5c7013e1-3e21-46ec-bf57-709e6595ba08" />


##
<img width="797" height="266" alt="image" src="https://github.com/user-attachments/assets/5745a6a6-dcd4-4df9-aa5b-904f845eaef6" />

##
│
└───ComfyUI\
    │
    └───custom_nodes\
    
    This folder custom_nodes is actually inside ComfyUI, texttoiagetovideo is the folder I personally created to contain all models altogether
<img width="1119" height="542" alt="image" src="https://github.com/user-attachments/assets/b1689b2b-e97f-4b33-9b8c-0f1d1e4a52d9" />

##

Credits
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
- [AnimateDiff-Evolved](https://github.com/continue-revolution/AnimateDiff)
- [VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
- [WAS Node Suite](https://github.com/WASasquatch/was-node-suite-comfyui)




