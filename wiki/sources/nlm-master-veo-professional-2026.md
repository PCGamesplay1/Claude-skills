---
title: "Master: Veo Professional Prompting — May 2026"
ingested: 2026-05-26
tags: [veo, ai-video, prompting, json-schema, nlm-master, ingest]
source_notebook: https://notebooklm.google.com/notebook/09b39c77-cbe4-483c-b890-2476b3f67bef
source_count: 49
drive_file: https://drive.google.com/file/d/1FvKSW_KX9MnHrbNZsNhDb3SlYzMDlmRN/view
---

# Source: Veo Professional Prompting — May 2026

> 49-source NotebookLM — Veo 3.1 ecosystem: model IDs, exact syntax, JSON schemas, continuity workflows, troubleshooting trees, industry templates.

---

## Model Line (as of 2026-05)

| Model | API ID | Status |
|---|---|---|
| Veo 3.1 Standard | `veo-3.1-generate-preview` | Preview |
| Veo 3.1 Fast | `veo-3.1-fast-generate-preview` | Preview |
| Veo 3.1 Lite | `veo-3.1-lite-generate-preview` | Preview (2026-03-31) |
| Veo 3 / Veo 3 Fast | — | Stable |
| Veo 2 | — | Being phased out |

---

## Prompting Frameworks

### 5-Part Foundational Formula (DeepMind Standard)
```
[Cinematography] + [Subject] + [Action] + [Context] + [Style & Ambiance]
```

### 7-Component Production Framework
```
[Subject] + [Action] + [Scene] + [Style] + [Dialogue] + [Sounds] + [Technical/Negatives]
```

### 8-Component Master Formula
```
Subject + Context + Action + Style + Camera + Composition + Ambiance + Audio
```

---

## JSON vs Natural Language: Controlled Test Results

50 generations each, same semantic goal:

| Metric | Natural Language | JSON Structure |
|---|---|---|
| First-try success rate | 34% | **78%** |
| Avg iterations to approval | 4.2 | **1.6** |
| Token cost | 1.0x | **0.7x** |
| Temporal consistency | 23% | **71%** |

**Rule**: Use JSON for anything requiring consistency across shots or multiple takes.

---

## Continuity Workflows

### Identity Anchor Protocol
To maintain character consistency across clips:
1. Generate reference frame (face, costume, environment)
2. Extract exact appearance description (hair color, clothing hex codes, physical markers)
3. Open new generation with identical reference block before any action description
4. Lock the "anchor" — never alter reference block between clips

### Scene-to-Scene Transition Syntax
```
[SCENE A END]: Subject walks left, exits frame right at [00:07-00:08]
[SCENE B START]: Same subject enters from frame left, continues motion
→ Maintains physics continuity at cut point
```

---

## Cinematography Lexicon

Veo 3.1 responds to professional terms as architectural triggers:

| Term | Effect |
|---|---|
| `Dolly Zoom` | Zoom-while-dollying, Vertigo effect |
| `Rack Focus` | Shift focus plane mid-shot |
| `Dutch Angle` | Tilted frame, psychological unease |
| `Anamorphic Lens` | Widescreen, cinematic flares |
| `Telephoto compression` | 85mm+, isolates subject |
| `Handheld micro-stabilization` | Controlled shake, documentary feel |

---

## Troubleshooting Tree

| Symptom | Root Cause | Fix |
|---|---|---|
| Hand distortion | Subject description too vague | Explicit: "left hand holds X, right hand at side" |
| Scene drift across clips | No identity anchor | Add reference block at scene start |
| Audio-visual desync | Audio cues after visual description | Put `Ambient:` and `SFX:` before action description |
| Temporal inconsistency | Natural language prompt | Convert to JSON structure |
| Watermarks/text appearing | Missing negative prompt | Add `"NEGATIVE": ["text", "watermark", "logo"]` |

---

## Cross-links

- [[nlm-master-veo3-april-2026]] — community techniques + Sonic Landscaping
- [[nlm-master-ai-creation-guide-2026]] — model stack context
- [[ai-video-prompting]] — synthesis concept
