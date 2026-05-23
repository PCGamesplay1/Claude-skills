---
name: vault
description: Read and write the AI LLM Wiki stored in the PCGamesplay1/Claude-skills GitHub repository. Use when the user invokes /vault, asks to read the wiki, append a log entry, or check open items. Works on any platform (Mac, Windows, Linux, web, mobile) via GitHub MCP — no local filesystem required.
---

# Vault Skill

The AI LLM Wiki lives in the `wiki/` directory of the `PCGamesplay1/Claude-skills` GitHub repository (branch: `main`). This skill reads and writes it via the GitHub MCP tools.

## Key files

| File | Purpose |
|------|---------|
| `wiki/index.md` | Master index of all wiki pages |
| `wiki/log.md` | Append-only operation log, newest entries at the top |

## Commands

When the user invokes `/vault`, check their message for a subcommand:

### `/vault` or `/vault read`
Fetch and display both files:
1. Use `mcp__github__get_file_contents` with `owner=PCGamesplay1`, `repo=Claude-skills`, `ref=refs/heads/main`
2. Fetch `wiki/index.md` and `wiki/log.md` in parallel
3. Display the index first, then the most recent 3–5 log entries
4. Show the raw GitHub URLs for Claude.ai WebFetch access:
   - `https://raw.githubusercontent.com/PCGamesplay1/Claude-skills/main/wiki/index.md`
   - `https://raw.githubusercontent.com/PCGamesplay1/Claude-skills/main/wiki/log.md`

### `/vault log`
Append a new entry to `wiki/log.md`:
1. Ask the user for the log entry content if not already provided
2. Fetch the current `wiki/log.md` using `mcp__github__get_file_contents` — note the file's SHA from the response
3. Insert the new entry **at the top**, immediately after the header `---` divider and before any existing entries
4. Use the entry format:
   ```
   ## [YYYY-MM-DD] CATEGORY — Title

   **content here**

   ---
   ```
   Use today's date. Category should match existing ones (INGEST, ARCHITECTURE, WORKFLOW, BASELINE, etc.)
5. Push the updated file using `mcp__github__create_or_update_file` with the SHA from step 2
6. Confirm the commit URL to the user

### `/vault index`
Fetch and display only `wiki/index.md`.

### `/vault status`
Fetch both files and summarise:
- Total sections in index (Concepts, Entities, Sources, Syntheses counts)
- Most recent log entry date and category
- Any open items listed in the most recent log entries

### `/vault sync`
This command requires the local Mac vault. Explain:
- On **Mac**: run `vault github sync` in Terminal (or `vault ingest all` for the full pipeline)
- On **Windows/Linux/web**: not available — the Obsidian vault is iCloud-only. Use `/vault log` to manually append entries instead.

## Notes

- Always fetch the current file SHA before writing — required by the GitHub API to prevent conflicts
- Log entries are newest-first; always insert at the top after the header block
- The header block ends at the first `---` divider after the frontmatter description line
- If the GitHub MCP tools are unavailable, fall back to providing the raw URLs and asking the user to fetch manually
