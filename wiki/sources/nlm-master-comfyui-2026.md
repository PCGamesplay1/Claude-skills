---
title: "Master: ComfyUI Complete Installation & Optimization Guide 2026"
ingested: 2026-05-26
tags: [comfyui, local-ai, ltx-video, flux, stable-diffusion, vram, nlm-master, ingest]
source_notebook: https://notebooklm.google.com/notebook/80eb9ef9-668c-472e-a54e-b5ab918daa2a
source_count: 58
drive_file: https://drive.google.com/file/d/1X_dUA_6QqPYPKHO5KJV58bxaeYt_5uiV/view
---

# Source: ComfyUI Complete Installation & Optimization Guide 2026

> 58-source comprehensive ComfyUI guide. Primary focus: LTX-2.3 video generation pipeline. Covers Windows/Mac/Linux/Docker/Cloud install, exact VRAM thresholds, CFG values, model file paths, launch flags, Two-Stage pipeline.

---

## Installation by Platform

### Windows
- **Desktop App (Recommended)** — Standalone installer, auto-configures Python and dependencies
- **Portable Version** — Pre-packaged ZIP with embedded Python
- **Manual**:
  ```bash
  git clone https://github.com/comfyanonymous/ComfyUI
  pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
  pip install -r requirements.txt
  ```

### Apple Silicon (M1/M2/M3/M4)
```bash
pyenv install 3.11 && pyenv local 3.11
python -m venv venv && source venv/bin/activate
pip install torch torchvision torchaudio  # MPS support included
```

### AMD (ROCm/Linux)
```bash
HSA_OVERRIDE_GFX_VERSION=11.0.0 python main.py
```

### Cloud Platforms (RunDiffusion, Vast.ai, RunPod)
Fix: Force venv injection for ModuleNotFoundError — all three platforms share this fix.

---

## VRAM Thresholds

| VRAM | Capability |
|---|---|
| 8GB | Entry baseline — SD 1.5, SDXL (tight), Flux FP8 (very tight) |
| 12GB | LTX-2.3 minimum — distilled model + FP8 offloading required |
| 16GB | LTX-2.3 comfortable — quantized models workable |
| 24GB | LTX-2.3 recommended — full BF16, no compromise |
| 48–80GB | Non-quantized two-stage pipelines at high resolution |

**Safety threshold**: Crash risk when VRAM hits **90–95%**.

---

## Launch Flags

```bash
# Memory management
--lowvram               # Most aggressive — streams to VRAM as needed
--medvram               # Balanced saving
--novram                # Smooths memory spikes during model swaps
--disable-pinned-memory # Fixes "pixel mush" glitches
--disable-async-offload # Stops memory corruption issues
--reserve-vram 5        # Reserve 5GB for system (adjust as needed)

# UI
--front-end-version comfy.org/comfyui_frontend@latest  # Force latest web UI
--listen                # Enable LAN access (http://[local-IP]:8188)
```

---

## Model File Paths

```
ComfyUI/
├── models/
│   ├── checkpoints/   ← SD 1.5, SDXL, Flux base models
│   ├── vae/           ← VAE decoders
│   ├── loras/         ← LoRA weights
│   ├── controlnet/    ← ControlNet models
│   ├── clip/          ← Text encoders (CLIP, T5)
│   └── unet/          ← Separate UNet weights (Flux)
└── custom_nodes/      ← Extension nodes
```

---

## LTX-2.3 Two-Stage Production Pipeline

**Stage 1 — Draft (Fast)**
- Model: LTX-2.3 distilled (lower VRAM)
- Resolution: 512×512 or 480p
- CFG: 1.5–2.0 (distilled models use low CFG)
- Steps: 8–12
- Purpose: Motion blocking, timing, composition check

**Stage 2 — Upscale/Refine (Pro)**
- Input: Stage 1 output as I2V seed
- Resolution: 720p or 1080p
- Model: LTX-2.3 full BF16 (or FP8 if VRAM-constrained)
- CFG: 3.0–4.5
- Steps: 20–30

---

## VRAM Management Techniques

- **CPU Offloading**: Move VAE decode or Gemma text encoder to RAM
- **"Clear VRAM and Cache" button**: Free memory without restart
- **SageAttention**: 2–3x attention speedup, minimal quality loss (Docker builds)
- **Quantization formats**: FP8, GGUF (Q3/Q4), NF4 — reduce VRAM footprint

---

## Key Nodes

| Node | Purpose |
|---|---|
| KSampler / KSamplerAdvanced | Core sampler — controls CFG, steps, scheduler |
| VAEDecode / VAEEncode | Convert between latent and pixel space |
| ControlNetApplyAdvanced | Apply conditioning (OpenPose, Depth, etc.) |
| VideoLinearCFGGuidance | LTX-specific guidance for video |
| SageAttentionNode | Inject 2-3x attention speedup |

---

## Cross-links

- [[nlm-master-ai-creation-guide-2026]] — LTX-2.3 position in model stack
- [[ai-video-prompting]] — prompting after generation
