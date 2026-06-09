---
name: estimation-to-plan
description: "Trigger: forecast ranges, duration, cost, staffing, roadmap dates. Convert validated size into a guarded plan range."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill when a user has a validated size estimate and asks for duration, cost, staffing, roadmap dates, or delivery forecast ranges.

## Hard Rules

- Require validated size, assumptions, Definition of Done, team capacity, and a productivity baseline before emitting duration or cost.
- Produce optimistic/expected/pessimistic ranges only; never output a single-point date, cost, or staffing commitment.
- Include QA, UAT, infrastructure, documentation, integration, and non-functional work as explicit forecast line items.
- Apply Brooks's Law guard when adding people is proposed: show onboarding, knowledge-transfer, and communication overhead.
- Do not compare story points or velocity across teams; request team-local productivity data.
- Add `> [HUMAN REVIEW REQUIRED]` to every forecast.

## Decision Gates

| Condition | Action |
|---|---|
| Missing size, capacity, DoD, or productivity baseline | Refuse forecast; list missing inputs |
| Cross-team velocity or point conversion supplied | Block conversion; request team-local baseline |
| Staffing increase requested | Add Brooks's Law overhead scenario before forecast |
| Only size is available | Route back to sizing skill; do not infer duration |

## Execution Steps

1. Read `references/forecast-model.md`.
2. Validate size source, assumptions, DoD, capacity, and productivity baseline.
3. Build optimistic, expected, and pessimistic scenarios with explicit assumptions.
4. Itemize QA/UAT, infra, docs, integration, NFRs, and risk buffers separately.
5. If staffing changes are requested, show overhead and caveats before any compression claim.

## Output Contract

Return input readiness, missing inputs, forecast range table, assumptions, capacity and productivity baseline, DoD/quality line items, staffing caveats, confidence level, and `> [HUMAN REVIEW REQUIRED]`.

## References

- `references/forecast-model.md`
