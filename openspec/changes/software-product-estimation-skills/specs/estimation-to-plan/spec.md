# estimation-to-plan Specification

## Purpose

Converts a validated size estimate into a forecast range for duration, cost, and staffing. Exposes uncertainty, capacity constraints, and staffing risks. Never produces deterministic commitments.

## Requirements

### Requirement: Uncertainty Range Output

The skill MUST produce a forecast as a range (optimistic/expected/pessimistic) with explicit assumptions. It MUST NOT emit a single-point duration or cost without a confidence qualifier.

#### Scenario: Valid forecast with all inputs

- GIVEN size, productivity baseline, DoD, team capacity, and technology context are supplied
- WHEN the skill produces a forecast
- THEN it returns three scenarios (optimistic/expected/pessimistic) with assumption list and `[HUMAN REVIEW REQUIRED]` block

#### Scenario: Incomplete inputs

- GIVEN size is available but productivity baseline is missing
- WHEN the skill processes the request
- THEN it surfaces the missing inputs, refuses to emit duration, and returns a `[HUMAN REVIEW REQUIRED — productivity baseline required]` block

---

### Requirement: DoD and Quality Scope Inclusion

The skill MUST include QA/UAT, infrastructure, documentation, and non-functional work as explicit line items in the forecast. It MUST NOT reduce forecast scope to implementation-only effort.

#### Scenario: DoD includes UAT and infra

- GIVEN the DoD specifies UAT, infrastructure provisioning, and documentation
- WHEN the skill builds the forecast model
- THEN QA/UAT, infra, and docs appear as separate effort line items in the forecast

---

### Requirement: Brooks's Law Staffing Guard

The skill MUST surface onboarding, knowledge-transfer, and communication overhead costs when a user proposes adding staff to accelerate a late or large project. It MUST NOT recommend adding people without quantifying the communication overhead.

#### Scenario: Add staff to compress timeline

- GIVEN a user asks to halve duration by doubling team size
- WHEN the skill processes the request
- THEN it explains the communication overhead increase, estimates onboarding cost, and presents the staffing scenario with caveats rather than a simple multiplier

---

### Requirement: No Cross-Team Point Comparison

The skill MUST NOT use story-point velocity comparisons across teams when computing forecasts. Velocity inputs MUST be team-local.

#### Scenario: Cross-team velocity provided

- GIVEN a user provides a velocity figure sourced from a different team
- WHEN the skill processes the input
- THEN it flags the input as cross-team, explains the calibration risk, and requests team-local data
