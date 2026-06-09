# Function Point Counting Workbook

`[STUB — approved tables required before FP counts are emitted]`

This file is intentionally not an IFPUG/ISO counting table. Replace it only with an organization-approved workbook before calculated Function Point counts are allowed.

## Current Mode

`[COUNTING WORKBOOK REQUIRED — no calculated FP emitted]`

The skill may produce a worksheet of candidate functions and evidence. It must not calculate adjusted or unadjusted FP totals from this stub.

## Worksheet Fields

| Field | Purpose |
|---|---|
| Candidate name | Business-facing function or data group. |
| Candidate type | ILF, EIF, EI, EO, or EQ. |
| Boundary evidence | Why the item belongs inside or outside the application boundary. |
| DET evidence | Data elements observed or `[UNKNOWN]`. |
| RET evidence | Record element types observed or `[UNKNOWN]`. |
| FTR evidence | File types referenced or `[UNKNOWN]`. |
| Source | Story, mockup, transcript, API, report, user-provided rule. |
| Review gate | `[HUMAN REVIEW REQUIRED — AI-extracted count]` when AI assisted extraction. |

## Classification Reminders

- ILF: internal logical data maintained by the application boundary.
- EIF: external logical data referenced but maintained outside the boundary.
- EI: external input that changes application state or maintained data.
- EO: external output with derived data, calculations, or processing logic.
- EQ: external inquiry that retrieves data without significant derived processing.
- Navigation-only UI elements, menus, cancel buttons, and plain links are excluded from transactional function candidates.

## Approval Gate

Calculated FP output requires an approved workbook containing local counting rules, complexity tables, weights, and review process. Until then, use worksheet-only output and keep size separate from productivity, duration, cost, and staffing.
