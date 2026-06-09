# function-point-estimation Specification

## Purpose

Produces or reviews an IFPUG-aligned Function Point Analysis. Defaults to worksheet/review mode. Full counting output requires a locally approved counting workbook.

## Requirements

### Requirement: Worksheet-Only Default Mode

The skill MUST default to worksheet/review mode. It MUST NOT produce adjusted or unadjusted Function Point counts unless a local `references/counting-workbook.md` with approved complexity/weight tables is present.

#### Scenario: Counting workbook absent

- GIVEN the user asks for a Function Point count and no approved counting workbook is present
- WHEN the skill processes the request
- THEN it returns a worksheet stub (ILF/EIF/EI/EO/EQ candidates identified, DETs/RETs/FTRs listed) with a `[COUNTING WORKBOOK REQUIRED — no calculated FP emitted]` notice

#### Scenario: Counting workbook present

- GIVEN an approved `references/counting-workbook.md` exists with complexity tables
- WHEN the skill processes the request
- THEN it produces unadjusted FP using the approved tables and surfaces adjustment factor notes

---

### Requirement: Function Classification

The skill MUST classify each candidate as ILF, EIF, EI, EO, or EQ using business-facing rules. It MUST NOT count navigation-only UI elements (menus, cancel buttons, navigation links) as transactional functions.

#### Scenario: Navigation element excluded

- GIVEN a mockup contains a sidebar menu and a cancel button
- WHEN the skill classifies transactional functions
- THEN neither the menu nor the cancel button appears in the count

#### Scenario: Report with multi-entity join

- GIVEN a report joins three data entities with derived calculations
- WHEN the skill classifies the function
- THEN it classifies it as EO and notes the FTR count and complexity driver

---

### Requirement: AI-Extracted Count Human Review Gate

The skill MUST flag any Function Point count that was assisted by AI extraction (from mockups, endpoints, transcripts) with `[HUMAN REVIEW REQUIRED — AI-extracted count]`.

#### Scenario: AI-extracted entities require review

- GIVEN entities and DETs were extracted from a transcript or mockup by the AI
- WHEN the skill produces the worksheet
- THEN every extracted element is flagged for human validation before the count is used

---

### Requirement: Size-Productivity Separation

The skill MUST keep FP counts separate from productivity, duration, and cost conversion. It MUST NOT attach a duration or effort estimate to the FP output.

#### Scenario: User asks for FP and timeline together

- GIVEN a user asks "how many function points and how long will it take?"
- WHEN the skill processes the request
- THEN it produces the FP worksheet first, then explicitly states that conversion to duration requires `estimation-to-plan`
