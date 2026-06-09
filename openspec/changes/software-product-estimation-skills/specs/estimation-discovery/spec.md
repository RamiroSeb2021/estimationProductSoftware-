# estimation-discovery Specification

## Purpose

Extracts estimation-ready facts from ambiguous product material. Produces a structured estimation brief before any sizing method is applied.

## Requirements

### Requirement: Estimation Brief Output

The skill MUST produce a structured brief containing: problem space, solution space, scope/bounded context, actors, capabilities, entities, transactions, integrations, non-functional drivers, assumptions, unknowns, and readiness warnings.

#### Scenario: Brief from vague requirements

- GIVEN a user provides a short product description with no structure
- WHEN the skill processes the input
- THEN it returns a brief with all mandatory sections and flags any section that could not be populated as `[UNKNOWN]`

#### Scenario: Brief from transcript or meeting notes

- GIVEN a user provides a raw VTT or meeting transcript
- WHEN the skill processes the input
- THEN it separates business problem from proposed solution and lists extracted entities, transactions, and open questions

---

### Requirement: Readiness Assessment

The skill MUST assess whether the extracted scope is ready for sizing and MUST recommend a method (agile, proxy, function-point, or clarification-needed) at the end of every brief.

#### Scenario: Scope ready for agile sizing

- GIVEN extracted artifacts include defined stories with acceptance criteria and a team context
- WHEN the skill evaluates readiness
- THEN it recommends `agile-story-estimation` and lists the stories available for sizing

#### Scenario: Scope not ready — missing boundary

- GIVEN extracted artifacts lack a clear bounded context or application boundary
- WHEN the skill evaluates readiness
- THEN it marks readiness as `NOT READY`, lists clarification questions, and withholds a method recommendation

---

### Requirement: No Invented Business Rules

The skill MUST NOT fabricate business logic, acceptance criteria, or functional rules absent from the provided artifacts. Gaps MUST be surfaced as open questions, not assumed values.

#### Scenario: Missing acceptance criteria

- GIVEN a feature description contains no acceptance criteria
- WHEN the skill builds the estimation brief
- THEN it lists the missing criteria as open questions and does NOT invent criteria
