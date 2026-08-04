# Megamind

A starter repository for running an **AI-managed wiki** on top of an [Obsidian](https://obsidian.md) vault, using [Claude Code](https://claude.com/claude-code) as the maintainer.

You keep capturing raw material — clippings, papers, daily notes. Claude turns it into a linked, structured wiki of concepts and entities, and keeps that wiki in sync as new material comes in.

![Megamind](megamind.png)

## Concept

The vault is split into three zones with different editing rules, enforced via `CLAUDE.md`:

| Zone    | Who owns it                | What lives there                                                         |
| ------- | -------------------------- | ------------------------------------------------------------------------ |
| `raw/`  | You (read-only for Claude) | Clipped articles, papers, books, daily notes, fleeting thoughts          |
| `wiki/` | Claude (LLM-maintained)    | Concepts, entities, syntheses, indices — generated and refactored freely |
| `dev/`  | Both (collaborative)       | ADRs, debriefs, projects, snippets                                       |

Claude never edits or moves anything in `raw/` — it only reads, cites, and links to it. `wiki/` is Claude's own territory: every page there gets frontmatter (`title`, `type`, `tags`, `sources`) and at least one `[[wikilink]]` to another page, so the wiki stays a connected graph instead of a pile of orphaned notes. `dev/` is a shared workspace — Claude can suggest edits but won't touch an existing ADR without explicit confirmation.

## Getting started

1. Clone this repo and open it as a vault in Obsidian.
2. Open the same folder with Claude Code.
3. Drop material into `raw/` (or let `/wiki-ingest` fetch and save it for you), then run the commands below to grow the wiki.
4. Read and adjust `CLAUDE.md` — it's the contract Claude follows for this vault. Zone rules, frontmatter conventions, and the ingestion workflow all live there.

## Slash commands

- **`/wiki-ingest <url-or-file>`** — Pull in a source (via the `defuddle` skill for URLs), save it to `raw/clippings/`, identify key concepts and entities, and propose a plan for creating/updating `wiki/` pages. Nothing is written until you approve the plan.
- **`/wiki-lint [focus area]`** — Health-check the wiki for contradictions, stale claims, orphan pages, missing pages, and missing cross-references. Reports findings first; only fixes what you approve.
- **`/wiki-query <question>`** — Search the vault and answer a question in prose, citing every page consulted via `[[wikilinks]]`, prioritizing `wiki/` over `dev/` and `raw/`.

## Skills

Loaded from `.claude/skills/`:

- `obsidian-markdown` — Obsidian-flavored markdown: wikilinks, callouts, embeds, properties
- `obsidian-bases` — `.base` database views
- `json-canvas` — `.canvas` visual whiteboards
- `obsidian-cli` — vault automation via the `obsdmd` command
- `defuddle` — clean content extraction from URLs
- `adr-writing` — the vault's Architecture Decision Record pattern
- `debrief-writing` — the vault's post-mortem / debrief pattern

## Requirements

- [Obsidian](https://obsidian.md) for browsing and editing the vault
- [Claude Code](https://claude.com/claude-code) for the AI maintainer
- [Defuddle CLI](https://github.com/kepano/defuddle) (`npm install -g defuddle`) for clean web extraction during ingestion

## Guardrails

Some hard rules Claude follows in this vault (full list in `CLAUDE.md`):

- Never edits or renames files in `raw/`
- Never deletes files without explicit confirmation
- Never runs `git add`, `git commit`, or `git push` — version control stays in your hands
- Never edits an existing ADR without you explicitly confirming
- Shows a plan before any operation touching more than 5 files
