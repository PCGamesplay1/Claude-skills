---
title: "Master: Veo 3 Prompting — April 2026"
ingested: 2026-05-26
tags: [veo, ai-video, sonic-landscaping, timestamp-syntax, community, nlm-master, ingest]
source_notebook: https://notebooklm.google.com/notebook/3c5a93bf-12d8-46d5-9f6c-d9fb57a3ba21
source_count: 49
drive_file: https://drive.google.com/file/d/1we8TBNrCi8MJKGJGVEXEAakbyi1XsJpE/view
---

# Source: Veo 3 Prompting — April 2026 (Community Techniques)

> 49-source community-heavy corpus. Focus: audio-first philosophy (Sonic Landscaping), timestamp multi-shot syntax, hand-over-hand chaining, Edit-Don't-Re-roll workflow, @-mention API slots. Complements the Professional notebook.

---

## The Omni Model Paradigm

**3D Latent Diffusion Architecture**: Model treats **time as a spatial dimension** — works in spatio-temporal patches, not raw pixels. Enforces physical consistency and reduces "AI shimmer" across frames.

**Audio-visual simultaneity** = sound and visuals generated in single pass through joint latent processing.

Mental model: *"Think of Veo 3.1 as a blind director who needs to hear the scene to visualize it."*

---

## Sonic Landscaping — Audio-First Prompting

**Core principle**: Describing sounds forces more physically accurate visuals than describing visuals alone. Audio anchors weight of the scene and masks subtle visual artifacts.

### Audio Cue Syntax

| Audio Type | Syntax | Example |
|---|---|---|
| Dialogue | `Character: "..."` | `Professor: "The results are unprecedented."` |
| Sound Effects | `SFX:` | `SFX: The metallic click of a typewriter key.` |
| Ambient | `Ambient noise:` | `Ambient noise: The quiet hum of a server room.` |
| Timed SFX | `[HH:MM-HH:MM] SFX:` | `[00:04-00:06] SFX: A sudden thunderclap.` |

### Realism Anchoring via Audio
- Footsteps → weight and surface material
- Environmental wind → outdoor scale
- Glass breaking → accurate physics shards
- Door opening → spatial context

**Audio masking**: High-quality audio cues mask subtle visual artifacts — strong audio environment reduces viewer perception of visual glitches.

---

## Timestamp Multi-Shot Syntax

Divide 8-second clip into timed segments. Each segment = distinct shot direction.

```
[00:00-00:02] Medium shot from behind subject, action description. Camera notes.
[00:02-00:04] Reverse shot, subject expression, emotional note. SFX: description.
[00:04-00:06] Tracking shot, continued action. Emotion: note.
[00:06-00:08] Wide crane up, pulls back to establish. Ambient: sound.
```

---

## Hand-Over-Hand Chaining

Use the last 2 seconds of clip N as the opening context for clip N+1:

```
Clip 1: "[00:06-00:08] Subject reaches for door handle."
Clip 2: "[00:00-00:02] [CONTINUATION] Hand on door handle, pushes open..."
```

Maintains motion physics across generation boundaries.

---

## Edit-Don't-Re-roll Workflow

When output is 80% correct but one element fails:
1. Identify failing element (hands, background, timing)
2. Add explicit corrective constraint for that element only
3. Re-generate with constraint — don't regenerate from scratch
4. Stack constraints progressively: each iteration locks the solved elements

---

## @-Mention API Syntax

Veo 3.1 API supports reference slots:
- `@character_1`, `@character_2` — character identity anchors
- `@location_ref` — environment anchor
- `@style_ref` — visual style anchor

Inject references at the top of the prompt before scene description.

---

## Cross-links

- [[nlm-master-veo-professional-2026]] — JSON schemas, troubleshooting trees
- [[ai-video-prompting]] — synthesis concept
- [[sonic-landscaping]] — concept page
