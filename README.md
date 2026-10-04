# Progress Review

**English | [中文](README.zh-CN.md)**

An AirJelly-only skill that uses the current user's AirJelly profile, memory, and recorded events to turn context-supported work into two matching views — a timeline and a project line — with every item labelled by ownership and result state.

Its hard requirement is a closed evidence boundary: it must not use the workspace, Git, the web, external documents, other MCP sources, or the current conversation to supplement evidence. The same AirJelly Context snapshot, subject, and time window should produce the same classifications and output structure.

## What it does

Given a person's AirJelly Context, it produces a self-contained HTML with:

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

## Data source

The only allowed sources are profile facts, memory, and events already stored in AirJelly, plus `airjelly_context` injected into the current session.

An event may identify Feishu, ChatGPT, Claude, Chrome, or another app as its original `source_app`, but it is usable only after AirJelly has recorded it. The skill never revisits those applications to supplement evidence. Missing AirJelly evidence remains a gap; the skill does not read local repositories, GitHub, web pages, or temporary user-supplied materials. If AirJelly Context is unavailable, no review is generated.

## Install

Put the `progress-review/` folder into AirJelly's skills directory:

- AirJelly: `~/Library/Application Support/AirJelly/skills/progress-review/`

## Use

```text
Give me a progress review for the past three months.
```

## Minimum input

The review subject, time window, intended use, and publication boundary. All work claims come from AirJelly Context. Missing evidence remains an explicit gap; the skill does not request supplementary work materials or fall back to another source.

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
| 1.1.0 | 2026-10-04 | Made the skill AirJelly-only with a closed evidence boundary and fail-closed behavior when Context is unavailable. |
| 1.0.0 | 2026-10-04 | First release: closed dual-axis taxonomy, two-line output, fixed template, QA. |
