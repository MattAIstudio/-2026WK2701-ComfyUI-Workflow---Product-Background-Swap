# MattAIStudio FLUX.2 Product Background Replacement Workflows v3.0
Two optimized ComfyUI pipelines for commercial product background replacement powered by FLUX.2 Klein. This repository includes two separate workflows optimized for different GPU VRAM capacities.
More info you can refer to my Youtube channel:https://www.youtube.com/@MattAIstudio

## Overview
These ComfyUI JSON workflows automatically cut out products from white backgrounds with RMBG-2.0, then generate brand-new custom scenes while keeping the product’s position, scale and size unchanged for commercial e-commerce rendering.

## Workflow Differences
### 1. MattAIStudio_ChangeBackground_v3.0-A5000-16G.json
**Target Hardware**: 16GB VRAM GPUs (RTX A5000 Laptop, mid-range notebooks)
#### VRAM Optimization Settings
- Qwen CLIP text encoder offloaded to CPU to reduce GPU memory consumption
- UNET uses `fp8_e4m3fn` quantization
- Maximum supported resolution capped at 1024px
- VRAM cleanup node pre-sampling to prevent OOM errors
#### Suitable Scenarios
Laptops, workstations and all GPUs with less than 24GB VRAM.

### 2. MattAIStudio_ChangeBackground_v3.0-RTX5090-32G.json
**Target Hardware**: Flagship 32GB VRAM GPUs (RTX 5090 high-end desktop)
#### Performance & Quality Improvements
- CLIP encoder runs fully on GPU for faster prompt processing
- UNET uses faster `fp8_e4m3fn_fast` precision
- Supports high-res output up to 1536 × 2048
- Only lightweight cache clearing instead of full model offloading
#### Suitable Scenarios
Desktop flagship GPUs, high-detail commercial product photography rendering.

## Shared Core Features
- Locked product subject: no deformation or position drift after background swap
- RMBG-2.0 intelligent automatic matting
- Optimized FLUX.2 Klein distilled model (Recommended Steps: 4–6, CFG Scale = 1.0)
- Built-in image comparer to preview original vs generated result
- Color-coded node groups for intuitive editing and debugging

## Required Models
| Model File | Storage Folder |
|------------|----------------|
| flux-2-klein-9b-fp8.safetensors | diffusion_models |
| qwen_3_8b_fp8mixed.safetensors | text_encoders |
| flux2-vae.safetensors | vae |
| RMBG-2.0 | models/RMBG |

## How to Use
1. Download the `.json` workflow matching your GPU VRAM size
2. Drag and drop the JSON file directly into ComfyUI canvas
3. Upload your white-background product image
4. Modify the background prompt text to customize scene styles
5. Queue prompt to render commercial product images

## Important Notes
- Running the 32G workflow on 16GB GPUs will cause out-of-memory crashes
- For ultra-high fidelity visuals, replace with `flux-2-klein-base-9b-fp8` and set sampling steps to 20–30
- Launch parameter for low VRAM machines:
```bash
python main.py --reserve-vram 0.6 --lowvram
