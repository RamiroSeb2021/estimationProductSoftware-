---
name: software-product-estimation
description: "Trigger: software estimation, sizing, roadmap forecasts, planning poker, function points. Route requests to one estimation workflow."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill for software product estimation requests: sizing, forecasts, cost, staffing, Planning Poker, function points, proxy sizing, or estimate review.

## Hard Rules

- Select exactly one focused workflow; do not run multiple methods in one response.
- Block false precision: never emit a single-point size, date, cost, or staffing answer without assumptions, uncertainty range, confidence, and `> [HUMAN REVIEW REQUIRED]`.
- Keep size separate from duration, cost, and staffing. Produce or validate size first; route conversion to `estimation-to-plan` as a distinct step.
- Treat transcript-derived ideas as illustrative only unless backed by an external method reference.
- Do not invent business rules, baselines, productivity rates, DoR/DoD, cost rates, or function-point weights.

## Decision Gates

| User intent | Route |
|---|---|
| Audit an existing estimate, proposal, roadmap, or timeline | `estimation-review` |
| Formal functional size, FP, IFPUG/ISO, ILF/EIF/EI/EO/EQ | `function-point-estimation` |
| Backlog, user stories, Planning Poker, points, sprint sizing | `agile-story-estimation` |
| Conceptual design, modules, components, S/M/L proxy size | `proxy-component-estimation` |
| Duration, cost, people, or dates from an already validated size | `estimation-to-plan` |
| Ambiguous notes, transcript, missing scope boundary, unclear method | `estimation-discovery` |

## Execution Steps

1. Read `references/router-decision-tree.md`.
2. Classify the request into one route and list the evidence used.
3. If inputs are missing, route to `estimation-discovery` and ask only for minimum required inputs.
4. If size and forecast are both requested, handle size first, then hand off to `estimation-to-plan`.
5. Load the selected specialized skill before producing method-specific output.

## Output Contract

Return: selected route, why that route fits, missing inputs, safety gates triggered, and the exact specialized skill to load next. Include `> [HUMAN REVIEW REQUIRED]` whenever any size or forecast leaves the router.

## References

- `references/router-decision-tree.md`
- `references/meeting-notes.md`
