---
name: agile-story-estimation
description: "Trigger: user stories, backlog sizing, story points, Planning Poker. Estimate only ready stories with local calibration."
license: Apache-2.0
metadata:
  author: gentleman-programming
  version: "1.0"
---

## Activation Contract

Load this skill for backlog, user-story, Planning Poker, sprint sizing, story point, or agile estimate requests.

## Hard Rules

- Do not size stories that fail INVEST or Definition of Ready checks; mark them `NOT READY`.
- Treat story points and velocity as team-local calibration only; never compare points across teams.
- Product Owners may clarify scope but must not override implementer-led estimates.
- Include Definition of Done scope before finalizing: tests, integration, infrastructure, deployment, and documentation.
- Flag uncalibrated estimates with `[LOCAL CALIBRATION REQUIRED]`.

## Decision Gates

| Condition | Action |
|---|---|
| Missing acceptance criteria or unclear outcome | Block sizing; ask for clarification |
| Estimates diverge by two or more card values | Ask each outlier for rationale before converging |
| Cross-team point comparison requested | Block comparison; explain team-local calibration |
| No historical team data | Produce relative size only with `[LOCAL CALIBRATION REQUIRED]` |

## Execution Steps

1. Read `references/planning-poker-checklist.md`.
2. Check each story against INVEST, DoR, and DoD scope.
3. Collect implementer estimates and rationale; preserve disagreement explicitly.
4. Resolve divergence through discussion, not authority override.
5. Output story sizes only after readiness passes.

## Output Contract

Return per story: readiness, blockers, size or `NOT READY`, rationale, DoD inclusions, calibration source, unresolved disagreements, and `> [HUMAN REVIEW REQUIRED]` for any estimate used outside team discussion.

## References

- `references/planning-poker-checklist.md`
