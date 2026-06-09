---
name: function-point-estimation
description: "Trigger: function points, FP, IFPUG, ISO, ILF/EIF/EI/EO/EQ. Build worksheet-only FP analysis by default."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill for Function Point Analysis, functional size, IFPUG/ISO mentions, or ILF/EIF/EI/EO/EQ classification.

## Hard Rules

- Default to worksheet/review mode only.
- Do not emit adjusted or unadjusted FP counts unless `references/counting-workbook.md` is replaced with approved local counting tables.
- Do not fabricate complexity tables, weights, adjustment factors, productivity rates, duration, or cost.
- Add `[HUMAN REVIEW REQUIRED — AI-extracted count]` to every AI-assisted classification.
- Exclude navigation-only UI elements from transactional functions.
- Keep FP size separate from duration, cost, staffing, and productivity conversion.

## Decision Gates

| Condition | Action |
|---|---|
| Workbook is the stub or lacks approved tables | Return worksheet with `[COUNTING WORKBOOK REQUIRED — no calculated FP emitted]` |
| User asks timeline with FP | Produce FP worksheet first; hand conversion to `estimation-to-plan` |
| Classification comes from transcript/mockup/API scan | Require human review on each item |
| Navigation-only UI | Exclude from function candidates |

## Execution Steps

1. Read `references/counting-workbook.md`.
2. Identify candidate ILF, EIF, EI, EO, and EQ items using business-facing boundaries.
3. List DET, RET, and FTR evidence when available; mark missing evidence `[UNKNOWN]`.
4. Gate every AI-extracted candidate for human validation.
5. Emit counts only if an approved workbook explicitly authorizes them.

## Output Contract

Return worksheet mode, workbook status, candidate functions, evidence, exclusions, unknowns, human-review gates, and next step. Never return effort, duration, cost, or staffing.

## References

- `references/counting-workbook.md`
