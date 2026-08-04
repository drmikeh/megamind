---
description: Health-check the wiki for contradictions, staleness, orphans, and gaps
argument-hint: [optional focus area, e.g. "wiki/concepts" or "Claude Code"]
allowed-tools: Bash(grep:*), Bash(find:*), Bash(cat:*)
---

I'll health-check the wiki$ARGUMENTS, following the lint pass described in [[LLM Wiki Pattern]] and CLAUDE.md.

Check for:

1. **Contradictions** — pages that make conflicting claims about the same concept or entity.
2. **Stale claims** — notes superseded by a newer source already in `raw/clippings/` but never folded back in.
3. **Orphan pages** — pages in `wiki/` with no inbound `[[wikilinks]]` from any other page (violates the "every page needs ≥1 wikilink" rule in CLAUDE.md).
4. **Missing pages** — concepts or entities mentioned by name (via `[[wikilink]]`) but with no corresponding file, or referenced only as plain text where a page would be warranted.
5. **Missing cross-references** — pages that clearly relate (shared source, overlapping topic) but don't link to each other.
6. **Data gaps** — open questions or thin pages that a targeted `/wiki-ingest` could fill.

Process:

1. **Survey, don't rewrite.** Use `grep`/`find` to enumerate `wiki/concepts/`, `wiki/entities/`, and `wiki/index.md`. Do not open every file's full content unless needed to confirm a finding.
2. **Report findings** as a flat list, grouped by category above. For each: name the file(s), state the issue in one sentence, and suggest a concrete fix.
3. **Wait for confirmation** before editing anything. Findings are a report, not an action — mirror the `/wiki-ingest` approval gate. Don't fix orphans, add links, or edit frontmatter without the user picking which findings to act on.
4. **After approval:** apply only the approved fixes, and report each affected file in list format at the end.

Don't flag `raw/` files — that zone is read-only and out of scope for lint.
