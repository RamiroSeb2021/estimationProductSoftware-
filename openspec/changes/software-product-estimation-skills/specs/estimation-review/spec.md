# estimation-review Specification

## Purpose

Audits existing estimates for missing scope, hidden complexity, invalid assumptions, and false precision. Returns severity-ordered findings with correction recommendations.

## Requirements

### Requirement: Severity-Ordered Findings

The skill MUST rank audit findings as Critical, High, Medium, or Low and present them in descending severity order. Each finding MUST include: what is wrong, why it matters, and a recommended correction or question.

#### Scenario: Missing non-functional requirements found

- GIVEN an existing estimate covers implementation but omits security, performance, and infrastructure
- WHEN the skill audits the estimate
- THEN it surfaces each omission as a High finding with a recommended question to the team

#### Scenario: Clean estimate

- GIVEN an estimate includes scope, DoD, assumptions, confidence range, and method used
- WHEN the skill audits the estimate
- THEN it returns no Critical or High findings and confirms which criteria passed

---

### Requirement: False Precision Detection

The skill MUST flag any estimate that lacks an uncertainty range, assumption list, or confidence qualifier as false precision. It MUST NOT accept a single-point estimate as valid for downstream use without flagging it.

#### Scenario: Single-point estimate in proposal

- GIVEN a project proposal states "delivery in 6 weeks" with no assumptions or range
- WHEN the skill reviews the estimate
- THEN it produces a Critical finding: false precision — no uncertainty range or assumptions provided

---

### Requirement: Modified-Code Comprehension Check

The skill MUST check whether estimates for modified or refactored code account for comprehension overhead. Work on existing code MUST NOT be estimated at the same rate as new development.

#### Scenario: Modified code estimated as new

- GIVEN an estimate treats refactored modules at the same rate as new features
- WHEN the skill audits the estimate
- THEN it raises a High finding: modified-code comprehension cost missing

---

### Requirement: Transcript vs External Source Boundary

The skill MUST distinguish findings derived from the internal Tech Talk transcript from those backed by externally validated method references (Scrum Guide, INVEST, ISO/IEC 20926, Fowler, Brooks). Transcript-derived findings MUST be marked as illustrative; external-source findings MUST cite the source.

#### Scenario: Audit cites transcript rule

- GIVEN a finding is based solely on the internal Tech Talk
- WHEN the skill outputs the finding
- THEN it includes a note: "(Source: internal Tech Talk — illustrative; verify against formal method reference)"
