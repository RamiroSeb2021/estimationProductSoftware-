# software-product-estimation Specification

## Purpose

Router skill — entry point for all estimation requests. Selects the appropriate estimation method, enforces false-precision guard, and keeps size separate from duration/cost/staffing.

## Requirements

### Requirement: Method Selection

The skill MUST classify each estimation request into exactly one method: discovery, agile-story, proxy-component, function-point, estimation-to-plan, or estimation-review. It MUST NOT attempt all methods in a single response.

#### Scenario: Router selects agile path

- GIVEN a user provides a backlog or stories and asks for estimation
- WHEN the skill evaluates available inputs
- THEN it routes to `agile-story-estimation` and lists required inputs

#### Scenario: Router selects function-point path

- GIVEN a user asks for formal functional size or mentions IFPUG/ISO
- WHEN the skill evaluates available inputs
- THEN it routes to `function-point-estimation` and confirms counting prerequisites

#### Scenario: Router receives ambiguous request

- GIVEN inputs are insufficient to determine a method
- WHEN the skill evaluates available artifacts
- THEN it invokes `estimation-discovery` and lists missing inputs before proceeding

---

### Requirement: False-Precision Guard

The skill MUST NOT produce a single-point estimate (e.g., "42 days") without accompanying assumptions, uncertainty range, and confidence level. It MUST surface a `[HUMAN REVIEW REQUIRED]` block for every size or forecast output.

#### Scenario: Single-point estimate attempt blocked

- GIVEN a user asks "how long will this take?" with no supporting inputs
- WHEN the skill processes the request
- THEN it returns a `[HUMAN REVIEW REQUIRED]` block listing missing inputs and refuses to emit a deterministic date

#### Scenario: Valid forecast with uncertainty

- GIVEN a size estimate, productivity baseline, and DoD are supplied
- WHEN the skill routes to `estimation-to-plan`
- THEN the response includes a range (optimistic/expected/pessimistic) and explicit assumptions

---

### Requirement: Size-Duration Separation

The skill MUST keep size estimation separate from duration/cost/staffing conversion. Size output MUST be produced first; conversion MUST be a distinct subsequent step.

#### Scenario: Size-only output requested

- GIVEN a user asks only "how big is this?"
- WHEN the skill processes the request
- THEN it returns a size result without attaching duration, cost, or team-size figures

#### Scenario: Full forecast requested

- GIVEN a user asks for size AND duration/cost
- WHEN the skill processes the request
- THEN it first surfaces size (with assumptions), then routes to `estimation-to-plan` as a separate step
