---
name: debrief-writing
description: Debrief / post-mortem pattern of this vault. Consult BEFORE creating
    or editing files in dev/debriefs/. Focuses on facts, not blame, and forces
    identification of generalizable learning.
---

# Skill: Debrief / Post-mortem Writing

Debriefs document incidents or significant events. The goal is **learning**,
not blame attribution. Each debrief is blameless.

## When to create

- Production incident (any severity)
- Bug that took >2h to diagnose
- Technical decision that proved wrong and had to be reverted
- Sprint or project ended (retrospective debrief)

## Numbering and name

`dev/debriefs/YYYY-MM-DD-short-slug.md`

## Frontmatter

```yaml
---
title: <What happened, in one sentence>
type: debrief
incident-date: 2026-04-28
severity: low | medium | high | critical
duration-minutes: 45
tags: [tag1, tag2]
related-projects: ["[[Project-X]]"]
related-adrs: ["[[ADR-0007]]"]
---
```

## Structure

```markdown
# Debrief: <title>

## TL;DR

3 sentences. What, impact, root cause.

## Timeline

Chronological list of events. Use UTC or explicit timezone.

- 14:32 — Alarm fires
- 14:35 — On-call investigates
- 14:48 — Root cause identified
- ...

## Root cause

Honest technical analysis. No softened reformulations.

## What worked

3-5 bullet items.

## What didn't work

3-5 bullet items. No people names — describe the system/process.

## Action items

Numbered list with [[wikilinks]] to projects where action will be executed.

- [ ] 1. Add timeout in [[Service-X]] for external calls
- [ ] 2. Update [[ADR-0003]] with new constraint

## Generalizable learning

1-2 paragraphs. **This is the most important section.** What goes beyond this
incident? What pattern applies to other systems? One-sentence answer:
"Systems that X must Y" — something that could become a future skill rule.
```

## Rules

- Debriefs are blameless: focus on system/process, not individuals.
- Always link to related ADRs and projects for context.
- Keep the timeline accurate and in chronological order with explicit timezones.
- Action items should be actionable and linked to relevant projects.
