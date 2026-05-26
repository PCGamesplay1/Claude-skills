---
title: "Master: AI Image and Video Creation Guide 2026"
ingested: 2026-05-26
tags: [ai-video, ai-image, prompting, model-stack, nlm-master, ingest]
source_notebook: https://notebooklm.google.com/notebook/69fa8912-f30b-45c8-a5b3-694e2dfec5f8
source_count: 100
drive_file: https://drive.google.com/file/d/1Tzvy9_n2DXZUWE-CiJy6eUFSgjHd5xpY/view
phase: 4
version: "1.3"
---

# Source: Master AI Image and Video Creation Guide 2026

> 100-source NotebookLM. Phase 4 output — 26 raw model variants collapsed to 14 canonical via Temporal Dominance rule. Re-uploaded as single source of truth into NLM 69fa8912.

---

## Key Reference: 14-Model Canonical Stack

### Tier 1 — Flagship Cloud (Multimodal / Dialogue-Native)

| Model | Owner | Signature Capability | Access |
|---|---|---|---|
| **Veo 3.1** | Google DeepMind | 4K native, dialogue + Foley in-generation, Scene Builder, 3 tiers: Standard / Fast / Lite | Google Ultra $250/mo · API `veo-3.1-generate-preview` |
| **Sora 2** | OpenAI | 16s standard / 25s Pro, Cameo likeness, storyboard mode | ChatGPT Plus/Pro |
| **Kling 3.0** | Kuaishou | Motion king — Character Binding, time-coded multi-shot lists, voice elements | kling.ai |
| **Seedance 2.0** | ByteDance | Thinking model with RAG — plans physics + story before rendering | seaart.ai |

### Tier 2 — Specialised & Open Source (Video)

| Model | Owner | Signature |
|---|---|---|
| **LTX-2.3** | Lightricks | Open weights, 4K/50fps/HDR, local-runnable (32GB VRAM req) |
| **WAN 2.6** | Alibaba | Audio-to-video lip sync, bilingual, subject referencing |
| **Luma Ray 3** | Luma AI | Modify tool (motion transfer), EXR transparency, video-to-video |
| **Runway** | Runway AI | Story Panels, script-to-storyboard, commercial-safe training |
| **Pika** | Pika Labs | Real-time avatar chat, agentic personality (Pika Me) |

### Tier 3 — Image Generation & Editing

| Model | Signature |
|---|---|
| **Nano Banana 2** (Gemini Flash Image) | Conversational segmentation, consistent multi-character referencing |
| **FLUX.1** | JSON/hex precision, 8.4GB VRAM (Klein variant), 4MP detail, open source |
| **Midjourney V8** | SREF style codes, 360° turnarounds, lookbook consistency |
| **Stable Diffusion** | Local ControlNet, IP-Adapter, LoRA training |

### Tier 4 — Infrastructure

| Tool | Role |
|---|---|
| **ComfyUI** | Node-based local orchestration, App Mode, Comfy Cloud GPU |

---

## Master 4-Step Prompt Workflow

```
Step 1 — DRAFT    : Describe scene in plain English to Claude / Gemini
Step 2 — TRANSLATE: Ask: "Convert to JSON with Camera, Subject, Environment, Lighting, Action buckets"
Step 3 — REFINE   : Replace glue words with technical terms (e.g. "AR Alexa 35", "14mm fisheye", "#FF4400")
Step 4 — EXECUTE  : Paste final JSON or expanded text into target video generator
```

## Master JSON Prompt Template

```json
{
  "CAMERA": {
    "lens": "24mm wide-angle",
    "movement": "slow dolly forward",
    "framing": "medium shot",
    "depth_of_field": "shallow, subject sharp, background bokeh"
  },
  "SUBJECT": {
    "description": "[CHARACTER — age, ethnicity, costume, expression]",
    "action": "[VERB — what they are doing]",
    "position": "[SPATIAL — left/center/right, foreground/mid/background]",
    "hands": "[EXPLICIT — e.g. 'left hand holds one cup, right hand at side']"
  },
  "ENVIRONMENT": {
    "location": "[SETTING]",
    "time_of_day": "[LIGHTING CONDITION]",
    "weather": "[IF RELEVANT]",
    "background": "[DISTANCE — what's behind the subject]"
  },
  "LIGHTING": {
    "type": "[e.g. Rembrandt, high-key, neon, golden hour]",
    "direction": "[from left, from above, rim light]",
    "color_temp": "[warm/cool/neutral or hex]"
  },
  "STYLE": {
    "aesthetic": "[cinematic, documentary, anime, etc.]",
    "color_grade": "[e.g. teal-orange, desaturated, film grain]",
    "ar": "[16:9, 9:16, 2.39:1]",
    "fps": "[24, 30, 60]"
  },
  "AUDIO": {
    "dialogue": "[Character: 'spoken line']",
    "sfx": "[sound effects]",
    "ambient": "[background sound]"
  },
  "NEGATIVE": ["blurry", "distorted hands", "watermark", "text"]
}
```

---

## Temporal Dominance Collapses Applied

| Canonical Kept | Variants Dropped |
|---|---|
| Veo 3.1 | Veo, Veo 2, Veo 3 |
| WAN 2.6 | WAN, WAN 2.5 |
| LTX-2.3 | LTX, LTX-2 |
| Kling 3.0 | Kling, Kling 01 |
| Seedance 2.0 | Seedance |
| Midjourney V8 | Midjourney |
| Sora 2 | Sora, Sora 1 |

---

## Cross-links

- [[nlm-master-veo-professional-2026]] — detailed Veo 3.1 prompting
- [[nlm-master-veo3-april-2026]] — Sonic Landscaping, timestamp syntax
- [[nlm-master-comfyui-2026]] — local pipeline (LTX-2.3)
- [[higgsfield]] — Seedance 2.0 / I2V workflow (Higgsfield platform)
