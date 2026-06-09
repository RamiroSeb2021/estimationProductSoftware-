---
name: proxy-component-estimation
description: "Trigger: component sizing, S/M/L estimates, conceptual modules. Build a calibrated proxy sizing worksheet."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill for conceptual designs, components, modules, services, screens, integrations, or S/M/L proxy sizing.

## Hard Rules

- Produce a component worksheet before any conversion to effort or duration.
- Classify every component as `new`, `modified`, or `refactor`.
- Add a comprehension-cost warning for `modified` and `refactor` work.
- Surface NFR drivers, integrations, and AI/LLM calls as sizing factors.
- Do not produce final effort without local comparable work; use `[LOCAL PROXY CALIBRATION REQUIRED]`.

## Decision Gates

| Condition | Action |
|---|---|
| No component boundary | Route back to `estimation-discovery` |
| No local proxy examples | Return relative S/M/L only with calibration gate |
| Modified/refactor work | Add comprehension-cost warning |
| AI, security, performance, or integration driver | Add complexity note before conversion |

## Execution Steps

1. Read `references/proxy-sizing-guide.md`.
2. Decompose the solution into reviewable components.
3. Assign S/M/L class with rationale and uncertainty.
4. Mark each component as new, modified, or refactor.
5. Attach local proxy reference when available; otherwise block effort conversion.

## Output Contract

Return a worksheet with component, size class, status, proxy rationale, NFR/integration flags, comprehension warnings, calibration source, open questions, and `> [HUMAN REVIEW REQUIRED]` for any sizing output.

## References

- `references/proxy-sizing-guide.md`
