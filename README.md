# Project Planner

A lightweight, Markdown-first repo for planning many projects with AI assistance. Each project lives in its own folder and follows a simple three-step workflow: Requirements → Technical Design → Tasks. You can also keep any supporting files (JSON, data dumps, notes) alongside those core docs.

## Folder Structure

```
projects/
  example-project/
    00-requirements.md
    01-technical-design.md
    02-tasks.md
    data/               # optional supporting data (JSON/CSV/etc.)
    notes.md            # optional notes or references
```

- One subfolder per project under `projects/`.
- Core docs are ordered and prefixed with `00`, `01`, `02` to make the flow explicit.
- Additional files are welcome (e.g., `data/*.json`, images, diagrams, exports).

## Workflow

Review gates are required between each phase to ensure correctness and allow user updates before moving on.

1) Requirements (`00-requirements.md`)
- Problem statement, goals, non-goals, scope, stakeholders.
- Constraints, assumptions, risks, success metrics, acceptance criteria.
- Inputs and references (links or files in `data/`).

Review Gate A — Requirements Approval
- Draft `00-requirements.md`, then pause for user review.
- Incorporate feedback/updates until approved before proceeding to design.

2) Technical Design (`01-technical-design.md`)
- Architecture overview, key components, data model, interfaces/APIs.
- Decisions and trade-offs, dependencies, risks and mitigations.
- Milestones and validation approach.

Review Gate B — Design Approval
- Draft `01-technical-design.md`, then pause for user review.
- Incorporate feedback/updates until approved before generating tasks.

3) Tasks (`02-tasks.md`)
- Convert requirements + design into actionable, prioritized tasks.
- Group into epics if helpful; note dependencies and owners.
- Use checkboxes for status with unique IDs (e.g., `TASK-001`).

## Conventions

- Naming: use `kebab-case` for project folders (e.g., `image-annotator`).
- Core files: `00-requirements.md`, `01-technical-design.md`, `02-tasks.md`.
- IDs: tasks use stable IDs like `TASK-001` that never change once issued.
- Status: `[ ]` Todo, `[~]` In Progress, `[x]` Done, `[!]` Blocked.
- Extra files: keep supporting artifacts under the project folder (e.g., `data/`, `notes/`).

## Quick Start

1. Create a new project folder under `projects/`.
2. Add `00-requirements.md` using the template below.
3. Ask for user review and approval of requirements (Review Gate A).
4. Derive `01-technical-design.md` from the approved requirements.
5. Ask for user review and approval of design (Review Gate B).
6. Generate `02-tasks.md` from both the approved requirements and design.

## Templates

You can copy these into each project and edit.

### 00-requirements.md

```markdown
# Requirements: <Project Name>

## Overview
- Problem:
- Goals:
- Non-goals:
- Stakeholders:

## Scope
- In scope:
- Out of scope:

## Constraints & Assumptions
- Constraints:
- Assumptions:

## Risks
-

## Success Metrics
-

## Acceptance Criteria
-

## Inputs & References
- Data files: `data/` (list files if any)
- External references:

## Open Questions
-

## Review & Sign-off
- Approved by:
- Date:
- Notes:
```

### 01-technical-design.md

```markdown
# Technical Design: <Project Name>

## Architecture Overview
- Summary diagram or description

## Components
-

## Data Model
- Entities / schemas / storage

## Interfaces / APIs
- Endpoints, events, contracts

## Decisions & Trade-offs
-

## Dependencies
-

## Risks & Mitigations
-

## Milestones
-

## Validation
- Test strategy / prototypes / metrics

## Open Questions
-

## Review & Sign-off
- Approved by:
- Date:
- Notes:
```

### 02-tasks.md

```markdown
# Tasks: <Project Name>

Legend: [ ] Todo, [~] In Progress, [x] Done, [!] Blocked

## Epics
- E-1: <Epic name>
- E-2: <Epic name>

## Open Tasks
- [ ] TASK-001 — <Task title> (Epic: E-1, Depends: -, Owner: -, Est: 2d, Priority: High)
  - Acceptance: <clear result>
- [ ] TASK-002 — <Task title> (Epic: E-1, Depends: TASK-001, Owner: -, Est: 1d, Priority: Medium)
  - Acceptance: <clear result>

## In Progress
- [~] TASK-003 — <Task title> (Epic: E-2, Depends: -, Owner: -, Est: 1d)

## Blocked
- [!] TASK-004 — <Task title> (Blocked by: <reason>)

## Done
- [x] TASK-000 — <Task title>

## Notes
-
```

## Working With AI

- See `AGENTS.md` for detailed guidance on how AI tools should use this repo.
- Typical flow: provide your high-level idea → AI drafts `00-requirements.md` → user reviews/approves (Gate A) → AI proposes `01-technical-design.md` → user reviews/approves (Gate B) → AI generates `02-tasks.md`.
- You can add any supporting files (datasets, json, diagrams) in the project folder; the AI will reference them from the docs.

### Using With Codex CLI and Other Tools

- Primary tooling: This repo is optimized for Codex CLI, which by default reads `AGENTS.md` first and follows it as the operating guide.
- Other agents/CLIs: Tools like Claude Code, Gemini CLI, Cline, Cursor, etc. can work too—as long as you explicitly instruct them to read `AGENTS.md` first and to follow it for the workflow and editing rules.
- Quick instruction to paste: "Open and read `AGENTS.md` first. Operate strictly within its guidelines for this repo."
- Consistency: Regardless of tool, keep each project self-contained under `projects/`, respect Review Gates (Gate A/B), and prefer additive, low‑risk edits.

## License

- Code and templates: MIT-style permissions with attribution; see `LICENSE`.
- Forks: You may fork this repo and use it for your own planning workflows.
- Documentation restriction: `AGENTS.md` and `README.md` may be used within this repo and its forks only. Do not copy, modify, or redistribute them outside this repo/forks, nor use them (in whole or substantial part) to build, train, or distribute software with planning features.
- Rights: All other rights reserved by Nimit Suwannagate <https://github.com/ethaizone/project-planner>.
