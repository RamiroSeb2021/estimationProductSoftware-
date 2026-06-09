# agile-story-estimation Specification

## Purpose

Guides backlog and story estimation using INVEST readiness checks, Planning Poker reasoning, and team-local calibration. Blocks cross-team story-point comparisons.

## Requirements

### Requirement: INVEST and DoR Readiness Check

The skill MUST validate each story against INVEST criteria and a supplied or inferred DoR before producing a size estimate. Stories that fail readiness MUST NOT be estimated as if ready.

#### Scenario: Story passes readiness check

- GIVEN a story has acceptance criteria, independence, and estimated scope
- WHEN the skill checks INVEST and DoR
- THEN it proceeds to estimation and outputs a size with rationale

#### Scenario: Story fails readiness — missing acceptance criteria

- GIVEN a story has no acceptance criteria
- WHEN the skill checks INVEST and DoR
- THEN it marks the story as `NOT READY`, lists missing criteria, and blocks sizing output

---

### Requirement: Implementer-Led Sizing

The skill MUST require that size estimates come from team members who will implement the work. The Product Owner MAY clarify scope but MUST NOT override implementer size decisions.

#### Scenario: PO attempts to override estimate

- GIVEN implementers produced an estimate and a PO role proposes a lower number
- WHEN the skill processes the interaction
- THEN it flags the override attempt, preserves the implementer estimate, and surfaces the disagreement for discussion

#### Scenario: Planning Poker divergence

- GIVEN two implementers produce estimates two or more card values apart
- WHEN the skill processes the estimates
- THEN it requests an explanation from each outlier before converging on a final estimate

---

### Requirement: Team-Local Calibration

The skill MUST anchor story points and velocity to team-local historical data. It MUST NOT compare points across teams as absolute units.

#### Scenario: Cross-team comparison attempted

- GIVEN a user asks to compare this team's velocity to another team's velocity
- WHEN the skill processes the request
- THEN it blocks the comparison and explains that points are team-local calibration units

#### Scenario: No historical data available

- GIVEN no team historical estimates or actuals are provided
- WHEN the skill produces an estimate
- THEN it outputs the estimate as relative and flags it with `[LOCAL CALIBRATION REQUIRED]` before using it for capacity planning

---

### Requirement: DoD Completeness

The skill MUST surface the Definition of Done and include tests, integration, infrastructure, and documentation in scope before finalizing a story estimate.

#### Scenario: DoD not supplied

- GIVEN a user asks to estimate stories but provides no DoD
- WHEN the skill processes the request
- THEN it prompts for DoD and provides a default checklist covering: unit tests, integration, deployment, and documentation
