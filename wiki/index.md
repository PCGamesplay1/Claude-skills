# AI Agentic Wiki — Index

> Master index of all wiki pages. Updated as new pages are created.

## Structure

- **[[concepts/]]** — Fundamental ideas: RAG, MCP, context windows, agent memory, semantic search, embeddings, etc.
- **[[entities/]]** — Tools, models, people, orgs: Claude Code, Karpathy, Smart Connections, Obsidian, etc.
- **[[sources/]]** — Summaries of ingested sources: papers, gists, articles, repos
- **[[syntheses/]]** — Cross-cutting analysis: comparisons, frameworks, emergent patterns

## Concepts

| Page | Summary |
|---|---|
| [[llm-wiki]] | Pattern: LLM builds persistent wiki layer over raw sources instead of re-deriving per query |
| [[rag]] | Retrieval-Augmented Generation — contrast with LLM Wiki |
| [[ingest]] | Operation: read source → update wiki pages → cross-link → log |
| [[query]] | Operation: answer from wiki, file good answers back as pages |
| [[lint]] | Operation: find orphans, contradictions, stale claims |
| [[token-compression]] | Techniques to cut LLM output tokens without losing accuracy |
| [[claude-code-skills]] | Claude Code plugin/skill system — markdown files extending agent behavior |
| [[ai-cost-observability]] | Tools + practices for measuring and optimizing AI token spend |
| [[skill-ecosystem]] | 4-marketplace Claude Code skill stack: superpowers, antigravity, karpathy, caveman |
| [[agent-native-cli]] | Design pattern for LLM-consumable CLIs: auto-JSON, typed exit codes, --compact, SQLite |
| [[demand-tree-knowledge-production]] | Demand map vs supply map — ROI-weighted gap map for self-directed AI knowledge production |
| [[ai-video-prompting]] | Cross-model synthesis — JSON vs NL, Sonic Landscaping, timestamp syntax, continuity protocols, ComfyUI VRAM |

## Entities

| Page | Summary |
|---|---|
| [[claude-code]] | Anthropic's agentic coding tool — recommended LLM writer for wiki pattern |
| [[karpathy-andrej]] | AI researcher, OpenAI co-founder, creator of LLM Wiki pattern |
| [[obsidian]] | Markdown IDE — reading interface for this vault |
| [[smart-connections-mcp]] | ~~MCP server~~ DEPRECATED 2026-05-22 — replaced by [[semantic-clip]] |
| [[semantic-clip]] | Node.js CLI — local semantic search via `.smart-env` vecs, zero MCP overhead |
| [[julius-brussee]] | Creator of caveman token compression skill and ecosystem |

## Sources

| Page | Summary |
|---|---|
| [[karpathy-llm-wiki-gist]] | April 2026 gist defining three-layer LLM Wiki architecture |
| [[dan6684-smart-connections-mcp]] | MCP server exposing Obsidian Smart Connections to Claude Code |
| [[caveman-julius-brussee]] | Claude Code skill — ~65% output token compression via caveman brevity |
| [[codeburn-getagentseal]] | TUI + menu bar for token cost observability across 19+ AI coding tools |
| [[design-extract-manavarya09]] | CLI + MCP server extracting website design systems — DTCG tokens, Tailwind, Figma vars |
| [[cloakbrowser-cloakhq]] | Stealth Chromium fork — drop-in Playwright replacement, passes bot detection (stub) |
| [[antigravity-awesome-skills]] | Community library of 1,431 Claude Code skills in 37 curated bundles across 9 categories |
| [[karpathy-guidelines-source]] | Karpathy coding guidelines plugin — 4 rules: think first, simplicity, surgical, goal-driven |
| [[vault-setup-session]] | Founding session: Obsidian vault structure, nested vault discovery, Smart Connections MCP setup |
| [[mcp-connector-management]] | MCP toggle patterns: disabled.json, SwiftBar plugin, Claude Desktop config race condition |
| [[cli-printing-press]] | Agent-driven Go CLI + MCP server generator from any API spec — printing-press v4.9.0 |
| [[nlm-master-ai-creation-guide-2026]] | 100-source Phase 4 master — 14-model canonical stack, Master JSON template, 4-step workflow |
| [[nlm-master-veo-professional-2026]] | 49-source Veo 3.1 professional guide — JSON schemas, continuity protocols, troubleshooting tree |
| [[nlm-master-veo3-april-2026]] | 49-source community Veo 3 guide — Sonic Landscaping, timestamp multi-shot, hand-over-hand chaining |
| [[nlm-master-comfyui-2026]] | 58-source ComfyUI guide — VRAM thresholds, LTX-2.3 two-stage pipeline, launch flags |
| [[nlm-master-facs-emotion-2026]] | 82-source FACS guide — AU reference, Universal Emotion combinations, VA model, micro-expression detection, AI animation pipeline |

## Syntheses

| Page | Summary |
|---|---|
| [[rag-vs-llm-wiki]] | Comparison of RAG and LLM Wiki knowledge architectures |

---

Last updated: 2026-05-26 (pass 2)
