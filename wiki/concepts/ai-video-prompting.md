---
title: AI Video Prompting — Synthesis
created: 2026-05-26
tags: [ai-video, veo, prompting, sonic-landscaping, json-prompt, synthesis]
sources: [nlm-master-ai-creation-guide-2026, nlm-master-veo-professional-2026, nlm-master-veo3-april-2026, nlm-master-comfyui-2026]
---

# AI Video Prompting — Synthesis

> Cross-source synthesis from 4 Master NLM guides (247 total sources). Covers model selection, prompt architecture, audio-first techniques, and local pipeline setup.

---

## Model Selection Decision Tree

```
Need dialogue/Foley in-generation?  → Veo 3.1 (Standard or Fast)
Need max motion quality?            → Kling 3.0 (Character Binding, multi-shot lists)
Want planning/physics reasoning?    → Seedance 2.0 (thinking model + RAG)
Cinematic + storyboard mode?        → Sora 2
Open source, local, 4K?             → LTX-2.3 via ComfyUI (32GB VRAM req)
Image generation, hex precision?    → FLUX.1 (Klein variant, 8.4GB VRAM)
Style consistency + reference?      → Midjourney V8 (SREF codes)
```

---

## Universal Prompt Architecture

### The 4-Step Workflow (works across all platforms)

```
1. DRAFT     : Plain English to Claude/Gemini — describe scene, mood, intention
2. TRANSLATE : "Convert to JSON: Camera, Subject, Environment, Lighting, Action, Audio"
3. REFINE    : Replace vague words with technical terms and exact values
4. EXECUTE   : Paste into target model
```

### JSON vs Natural Language (Veo 3.1 controlled test, 50 runs each)

| Metric | Natural Language | JSON |
|---|---|---|
| First-try success | 34% | **78%** |
| Avg iterations | 4.2 | **1.6** |
| Token cost | 1.0x | **0.7x** |
| Temporal consistency | 23% | **71%** |

**Use JSON whenever consistency matters.** Natural language for one-off experimental shots.

---

## Sonic Landscaping — Audio-First Prompting (Veo 3.1)

Veo 3.1 is audio-visual simultaneous — sound and visuals generated in one pass. Describing audio forces physically correct visuals.

```
Footsteps  → surface material, character weight
Wind       → outdoor scale, weather severity
Glass      → physics shards, spatial echo
Machinery  → industrial environment, distance

Bad:  "A man walks through a busy street."
Good: "A man walks through a busy street. Ambient noise: traffic, distant construction,
       a food vendor calling out. SFX: his footsteps on wet pavement."
```

Audio cue syntax:
```
Character: "spoken dialogue"
SFX: sound effect description
Ambient noise: background environment
[00:04-00:06] SFX: timed sound event
```

---

## Timestamp Multi-Shot Syntax (Veo 3.1)

One prompt, 4 shots in 8 seconds:
```
[00:00-00:02] Medium shot from behind, [action]. [Camera note].
[00:02-00:04] Reverse shot, [expression]. SFX: [sound].
[00:04-00:06] Tracking shot, [continuation]. Emotion: [note].
[00:06-00:08] Wide crane up, pulls back. Ambient: [sound].
```

---

## Character Continuity Across Clips

**Identity Anchor Protocol:**
1. Generate reference frame
2. Extract exact appearance (hex colors, physical markers, costume detail)
3. Begin every new clip with identical reference block
4. Never alter the reference block — add action description after it

**Hand-Over-Hand Chaining:**
```
Clip N:   "[00:06-00:08] Subject reaches for door handle."
Clip N+1: "[00:00-00:02] [CONTINUATION] Hand on door handle, pushes open..."
```

---

## Edit-Don't-Re-roll

When output is 80% correct:
1. Identify the failing element specifically
2. Add one explicit corrective constraint for that element
3. Re-generate — don't start from scratch
4. Stack constraints progressively (each iteration locks solved elements)

---

## Local Pipeline: ComfyUI + LTX-2.3

**Two-Stage Production:**

| Stage | Purpose | VRAM | CFG | Steps |
|---|---|---|---|---|
| Draft (distilled) | Motion blocking, timing | 12GB+ | 1.5–2.0 | 8–12 |
| Refine (full BF16) | Final 720p–1080p output | 24GB+ | 3.0–4.5 | 20–30 |

**Critical launch flags:**
```bash
--lowvram              # streams to VRAM as needed
--disable-pinned-memory # fixes "pixel mush" glitch
--reserve-vram 5        # keeps 5GB for system
```

---

## Common Failure Modes + Fixes

| Symptom | Fix |
|---|---|
| Hand distortion | Explicit: "left hand holds X, right hand at side" |
| Scene drift across clips | Identity anchor block at every clip start |
| Audio-visual desync | Put audio cues before action description |
| Temporal inconsistency | Switch from NL to JSON prompt |
| Watermarks/text | Add `NEGATIVE: ["text", "watermark", "logo"]` |
| Pixel mush (local) | Add `--disable-pinned-memory` flag |
| VRAM crash (local) | Add `--reserve-vram 5` + enable CPU offload for VAE |

---

## Cross-links

- [[nlm-master-ai-creation-guide-2026]] — full model stack
- [[nlm-master-veo-professional-2026]] — Veo schemas + troubleshooting
- [[nlm-master-veo3-april-2026]] — Sonic Landscaping + timestamp syntax
- [[nlm-master-comfyui-2026]] — local pipeline detail
- [[higgsfield]] — Seedance 2.0 / I2V / Ref2V workflow
