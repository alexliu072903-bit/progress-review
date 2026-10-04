# Progress Review

**English | [中文](README.zh-CN.md)**

A skill for AI coding agents (AirJelly, Claude Code, Codex, and others) that turns a person's real work into two matching views — a timeline and a project line — with every item labelled by ownership and result state.

Its one hard requirement is that the output is deterministic: send this skill to any colleague, run it with any agent, and the same person produces the same result.

## What it does

Given a person's memory or context, it produces a self-contained HTML with:

- **A timeline** — items in chronological order, to show trajectory.
- **A project line** — items grouped by theme, to show where the weight sits.
- **Four explicit lists** — done / not done, impact / no impact, closed / open.

Every item carries two labels:

- **Ownership** — lead / own / drive / influence / support
- **Result state** — delivered / impact / in progress / pending verification / open / stopped

The standard is an "effectiveness narrative": a stranger should see quickly what you owned, what changed, and what has verifiable evidence.

## Structure

```text
SKILL.md                                     main flow: purpose, naming boundary, determinism, two lines, output
references/taxonomy.md                       the closed vocabulary: ownership and result states, with tie-breakers
references/evidence.md                       fact / judgment / assumption; what counts as done
references/qa.md                             the pre-release consistency checks
assets/team-progress-review.template.html    the fixed output template
```

## Why the output is identical

1. **Closed vocabulary** — only the enumerated values, no invented labels.
2. **Decidable rules** — every value has a definition and a tie-breaker.
3. **Evidence required** — every item carries a source and a date; no evidence, no upgrade.
4. **Fixed order** — timeline ascending, project line by certainty.
5. **Fixed template** — same sections, classes, and legend.
6. **QA** — including a cross-run consistency check.

## Install

Put the `progress-review/` folder into your agent's skills directory:

- AirJelly: `~/Library/Application Support/AirJelly/skills/progress-review/`
- Claude Code: `~/.claude/skills/progress-review/`
- Codex: `~/.codex/skills/progress-review/`

## Use

```text
Give me a progress review for the past three months.
```

## Minimum input

A person's memory or context. If it is missing, the skill asks for the minimum: a factual bio, at least two outputs, one verifiable link per output, and a contact route for a public version.

## Boundary

- Do not call it a "performance review" or "technical review" on the surface.
- Do not invent data, dates, or titles.
- "Merged is not released; having data is not verified."
- Keep private or company-internal material out of anything published.

## License

MIT

## History

| Version | Date | Change |
| --- | --- | --- |
| 1.0.0 | 2026-10-04 | First release: closed dual-axis taxonomy, two-line output, fixed template, QA. |