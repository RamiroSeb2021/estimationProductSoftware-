# Forecast Model Reference

Use this checklist before converting size into a plan. If any required input is missing, return the missing-input gate instead of inventing a forecast.

## Required Inputs

| Input | Required evidence |
|---|---|
| Validated size | Story points, proxy worksheet, or approved FP output with assumptions. |
| Productivity baseline | Team-local throughput, comparable delivery history, or approved organizational baseline. |
| Capacity | Availability, holidays, support load, ceremonies, interruptions, and allocation percentage. |
| Definition of Done | Coding, tests, review, integration, deployment, docs, QA, and acceptance expectations. |
| Technology context | Novelty, dependencies, integrations, NFRs, and operational constraints. |

## Forecast Shape

Return ranges only:

| Scenario | Purpose |
|---|---|
| Optimistic | Known path, low interruption, assumptions hold. |
| Expected | Normal delivery with likely clarification and integration cost. |
| Pessimistic | Rework, dependency delay, hidden complexity, or capacity loss. |

Every scenario includes assumptions, confidence, and `> [HUMAN REVIEW REQUIRED]`.

## DoD and Quality Line Items

Include separate line items for implementation, unit/integration testing, QA, UAT, infrastructure, release/deployment, documentation, security/performance work, and contingency.

## Brooks's Law Guard

Adding staff is not a simple multiplier. Show:

| Staffing change | Required caveat |
|---|---|
| Add one person | Onboarding time, pairing/review load, domain transfer. |
| Double team size | Communication paths increase, coordination work rises, delivery may slow first. |
| Add late in project | Highest risk; likely re-planning and rework before benefit. |

## Cross-Team Boundary

Never convert another team's points or velocity into this team's duration. Flag it as cross-team data and request team-local productivity history.
