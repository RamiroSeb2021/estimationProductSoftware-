# Software Product Estimation Skills

This repository is a documentation and AI-skill workspace for software product estimation. It provides project-local `SKILL.md` instructions that help AI coding assistants route estimation requests, extract missing scope, choose an estimation method, and protect teams from false precision.

It is **not** a runnable product or estimation calculator. The current artifacts are Markdown skills, local references, OpenSpec planning documents, and Bash setup/test helpers for skill installation.

## Current status

| Area | Status |
|------|--------|
| Estimation skills | 7 project-local skills implemented under `skills/` |
| Runtime application | Not present |
| Package manifest | Not present |
| Build step | Not applicable |
| Tests | `bash skills/setup_test.sh` validates the setup helper, not estimation behavior |
| Spec trail | OpenSpec change artifacts live under `openspec/changes/software-product-estimation-skills/` |

## What is included

The skill suite covers these workflows:

| Skill | Purpose |
|-------|---------|
| `software-product-estimation` | Router skill for choosing the right estimation workflow |
| `estimation-discovery` | Turns unclear notes, transcripts, or scope fragments into an estimation brief |
| `agile-story-estimation` | Supports backlog readiness and Planning Poker style reasoning |
| `proxy-component-estimation` | Sizes conceptual components with local proxy calibration guards |
| `function-point-estimation` | Provides an IFPUG-style worksheet/review flow without fabricating official tables |
| `estimation-to-plan` | Converts validated size into guarded duration, cost, and staffing ranges |
| `estimation-review` | Audits existing estimates for gaps, false precision, and unsafe assumptions |

Every output-producing estimation workflow is designed to surface assumptions, uncertainty, confidence, and a human-review gate before estimates are used as commitments.

## Repository structure

```text
.
├── docs/
│   └── skill-style-guide.md
├── openspec/
│   ├── config.yaml
│   └── changes/software-product-estimation-skills/
├── skills/
│   ├── software-product-estimation/
│   ├── estimation-discovery/
│   ├── agile-story-estimation/
│   ├── proxy-component-estimation/
│   ├── function-point-estimation/
│   ├── estimation-to-plan/
│   ├── estimation-review/
│   ├── setup.sh
│   └── setup_test.sh
└── README.md
```

## Using the skills

AI assistants that understand Agent Skills can read the relevant `SKILL.md` file directly. Start with the router:

```text
Read skills/software-product-estimation/SKILL.md
```

For local assistant setup, run the helper from the repository root:

```bash
bash skills/setup.sh --all
```

The setup script can configure links or instruction files for Claude Code, Gemini CLI, Codex, and GitHub Copilot. Use `bash skills/setup.sh --help` to see targeted options.

## Verification

There is no application build. The available executable check validates the setup helper:

```bash
bash skills/setup_test.sh
```

The estimation skills themselves are verified through static/manual review documented in:

- `openspec/changes/software-product-estimation-skills/verify-report.md`
- `openspec/changes/software-product-estimation-skills/static-verification.md`

## Important guardrails

- Do not treat AI-generated estimates as commitments without human review.
- Do not emit single-point dates, costs, or staffing claims without assumptions and uncertainty ranges.
- Do not compare story points or velocity across teams as absolute units.
- Do not produce formal function-point counts until approved counting tables/workbooks are supplied.
- Keep transcript-derived concepts separate from externally validated estimation rules.

## Deeper references

- `docs/skill-style-guide.md` — authoring contract for LLM-first skills.
- `openspec/changes/software-product-estimation-skills/proposal.md` — scope, rationale, and risks.
- `openspec/changes/software-product-estimation-skills/tasks.md` — completed work plan and review slicing.
- `skills/*/references/` — method-specific checklists, worksheets, and supporting notes.
