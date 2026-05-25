# Demand Tree & AI-Directed Knowledge Production

**Created**: 2026-05-25  
**Source**: Analysis of Andy K's "The Right Problem" (thebooq.com / Medium) + Karpathy's LLM Wiki concept + personal vault pattern  
**Status**: Concept — not yet implemented

---

## Core Distinction: Supply Map vs Demand Map

Most wikis, RAG indices, and knowledge bases are **supply maps** — they record what exists. Obsidian vaults, Notion databases, GitHub wikis: the structure reflects the order content was produced, not the order it is needed.

A **demand map** (demand tree) is the inverse: it captures what people actually need to know, weighted by how much they need it. The shape is determined by usage patterns and consequence, not production history.

Andy K's insight from thebooq.com: the platform surfaced a demand tree for consumer information — questions people actually ask, not documents companies want to publish. The structure was often a tree (not flat search) because needs are hierarchical: broad intent → specific context → precise question.

---

## The Cognitive Skeleton Concept

For humans, a tree structure is useful navigation. For AI, it's something more fundamental: a **cognitive skeleton**.

AI systems can generate and synthesize content without effort. What they lack is a map of:
- What exists (supply map — current wikis provide this)
- What's missing (gap map — rarely explicit)
- What order those gaps matter in (priority signal — almost never encoded)

A demand tree with ROI weights on each branch gives an AI system a prioritized map of its own knowledge gaps. It transforms a passive index into an active production queue.

---

## ROI Weighting Formula

Each branch of the demand tree has a weight:

```
ROI = frequency_of_need × consequence_of_not_knowing
```

| Branch | Frequency | Consequence | ROI |
|--------|-----------|-------------|-----|
| Seedance prompt structure | High | High (blocks generation) | ★★★★★ |
| Claude API tool use | High | High (blocks automation) | ★★★★★ |
| Higgsfield model differences | Medium | Medium | ★★★ |
| HA PIR sensor config | Low | High (system breaks) | ★★★ |
| Stable Diffusion samplers | Low | Low | ★ |

The consequence dimension matters more than frequency for rare-but-critical knowledge. A node that's never needed until it is — and then blocks everything — has high consequence regardless of frequency.

---

## Three-Layer Architecture

### Layer 1 — Demand Tree (Intent Map)
The tree of what you need to know, organized by intent rather than topic:

```
I want to create AI video
├── with Higgsfield
│   ├── Seedance 2.0 (Ref2V / @mention tagging) ← FILLED
│   ├── I2V vs T2V (which model for what) ← PARTIAL
│   └── Prompt formulas (MCSLA / Five-Segment) ← FILLED
├── with other platforms
│   ├── Kling / Runway comparison ← MISSING
│   └── ComfyUI video nodes ← MISSING
└── ...
```

### Layer 2 — Gap Map
Each node tagged: `filled` / `partial` / `missing`. The gap map makes the holes visible. Currently this is implicit in what questions keep recurring in sessions.

### Layer 3 — Production Roadmap
Gap nodes sorted by ROI weight. This is the AI's work queue: "fill these gaps first because they block the most work."

---

## Practical Signal: Session Log Mining

The cheapest way to build a demand tree is to mine existing session logs. Every question you've asked Claude is a demand signal. Recurring questions = high frequency. Questions that blocked work = high consequence.

Session transcripts live in `~/.claude/projects/`. That's months of encoded demand data. A single pass extracting recurring question categories would produce a rough demand tree for free.

Steps:
1. Extract questions from session logs (grep or AI pass)
2. Cluster by intent (not topic — "how do I X" not "X docs")
3. Tag with consequence: did the session stall waiting for this answer?
4. Sort by `frequency × consequence`
5. Cross-reference against wiki to produce gap map

---

## Connection to Karpathy's LLM Wiki

Andrej Karpathy proposed maintaining a living wiki that an LLM keeps current — a document the AI can both read and update, validated by the human. This is the supply side.

The demand tree is the missing complement: it tells the LLM *what* to add next, and *why*, rather than leaving that to human curation instinct.

Combined:
- **Karpathy model**: LLM maintains the supply (wiki pages, accuracy, freshness)
- **Demand tree model**: Humans + session logs surface the demand (what's needed, priority)
- **ROI weights**: Connect the two — LLM produces what has highest demand × gap

---

## Synthesis: Self-Directed Knowledge Production System

```
Session logs → demand signal extraction
                        ↓
              Demand tree (intent-ordered)
                        ↓
              Gap map (filled / partial / missing)
                        ↓
    ROI sort (frequency × consequence) → Production queue
                        ↓
              LLM fills top gaps (Karpathy-style wiki update)
                        ↓
              Human validates → wiki grows
                        ↓
                [loop: new sessions → new demand signals]
```

This is a self-directed, demand-weighted knowledge production system. The AI doesn't wait to be told what to write. It reads the demand tree, checks the gap map, and fills the highest-ROI gaps.

---

## Current State of This Wiki

As of 2026-05-25, this vault is a **supply map** — pages added as knowledge was produced, not structured by demand.

To convert it:
- [ ] Mine session logs for recurring question clusters
- [ ] Build draft demand tree from clusters
- [ ] Tag existing wiki nodes as filled/partial/missing
- [ ] Assign ROI weights (manual first pass is fine)
- [ ] Use gap map to decide what to write next

This concept page is itself a test of the idea: it was logged because it scored high on the demand tree (high consequence — shapes how the wiki evolves) even though it was never explicitly requested.

---

## References

- Andy K, "The Right Problem" — thebooq.com / Medium, 2026
- Andrej Karpathy — LLM-maintained wiki concept (Twitter/X thread, ~2024)
- Personal vault: `wiki/index.md`, `wiki/log.md`
