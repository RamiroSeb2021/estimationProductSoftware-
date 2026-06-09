# proxy-component-estimation Specification

## Purpose

Estimates product size by decomposing a conceptual design into comparable components classified as small/medium/large. Requires calibrated local proxy examples for non-trivial forecasts.

## Requirements

### Requirement: Component Decomposition Worksheet

The skill MUST produce a worksheet listing each component, its size class (S/M/L), new-vs-modified classification, non-functional drivers, and proxy rationale. It MUST NOT produce a final effort estimate without a calibrated local proxy reference.

#### Scenario: Full worksheet with proxy reference

- GIVEN a component list, size-class definitions, and a local proxy reference (past comparable work)
- WHEN the skill produces the worksheet
- THEN each component row includes size class, classification, and a reference to the comparable item

#### Scenario: Worksheet without proxy reference

- GIVEN a component list but no local proxy reference
- WHEN the skill produces the worksheet
- THEN it outputs relative sizing only and flags the result with `[LOCAL PROXY CALIBRATION REQUIRED]`

---

### Requirement: New vs Modified Distinction

The skill MUST classify each component as new, modified, or refactor. Modified/refactor work MUST carry a comprehension-cost warning indicating that existing code understanding adds to the estimate.

#### Scenario: Modified component detected

- GIVEN a component is marked as modifying existing functionality
- WHEN the skill processes the component
- THEN it adds a comprehension-cost warning and does NOT treat the component as equivalent to new work

---

### Requirement: Non-Functional Cost Surfacing

The skill MUST identify non-functional drivers (performance, security, integrations, AI calls) per component and surface them as additional sizing factors before any conversion.

#### Scenario: AI integration component

- GIVEN a component includes an AI/LLM integration call
- WHEN the skill processes the component
- THEN it flags the component with an additional complexity note and does NOT treat it as a standard API call
