# Planning Poker Checklist

Use this checklist to keep story estimates ready, implementer-led, and locally calibrated.

## Readiness Gate

| Check | Pass condition |
|---|---|
| Independent | Story can be delivered without hidden coupling to unrelated work. |
| Negotiable | Scope can be discussed without rewriting the product goal. |
| Valuable | Outcome matters to a user, operator, business process, or platform capability. |
| Estimable | Acceptance criteria and technical unknowns are visible enough to discuss size. |
| Small | Story is not obviously an epic or multi-workflow package. |
| Testable | Acceptance criteria can be verified. |
| Definition of Ready | Team's DoR is supplied or explicitly accepted for this session. |

If any required check fails, mark the story `NOT READY` and do not provide points.

## Planning Poker Flow

1. Product Owner clarifies intent, constraints, and acceptance criteria.
2. Implementers estimate independently using the team's card scale.
3. Reveal estimates together.
4. If estimates differ by two or more card values, each high/low outlier explains assumptions and risks.
5. Re-estimate after clarifications; preserve unresolved disagreement instead of forcing false consensus.

## DoD Scope Inclusion

Before finalizing, confirm the estimate includes:

- Unit, integration, and acceptance test effort.
- Code review and rework.
- API/data migrations or deployment work.
- Observability, security, accessibility, and documentation when applicable.
- QA/UAT handoff support if part of the team's DoD.

## Local Calibration Block

`[LOCAL CALIBRATION REQUIRED]`

Story points are not universal units. Do not compare one team's points or velocity to another team's points or velocity. Without team-local historical estimates and actual outcomes, output relative size only and block capacity forecasting.
