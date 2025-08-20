# AGENTS Guide

This document describes how AI assistants should interact with this repo to plan projects. Follow the workflow, keep changes minimal and traceable, and never delete user content without explicit instruction.

## Objectives

- Use a consistent, repeatable flow per project: Requirements → Technical Design → Tasks.
- Keep each project self-contained in its own folder under `projects/`.
- Prefer additive, low-risk edits; preserve history and stability of IDs.

## Tooling Compatibility

- Codex CLI: This repo is designed for Codex CLI, which reads `AGENTS.md` first and uses it as the operating guide.
- Other tools: Claude Code, Gemini CLI, Cline, Cursor, and similar tools can be used if the user instructs them to read `AGENTS.md` first and follow it exactly.
- Instruction snippet: "Read `AGENTS.md` first and operate within its rules for this repo."

## Project Lifecycle

1) New Project
- Create a folder under `projects/` using `kebab-case` (e.g., `image-annotator`).
- Add the three core files using the templates in `README.md`:
  - `00-requirements.md`
  - `01-technical-design.md`
  - `02-tasks.md`
- Place any provided artifacts in the project folder (e.g., `data/`, `notes.md`).

2) Requirements → Review → Design
- Draft `00-requirements.md` and pause for explicit user review.
- Incorporate updates until the user approves Requirements (Gate A).
- Only after approval, draft `01-technical-design.md` referencing the requirements and any data files.
- Capture assumptions, alternatives, and risks explicitly in the design.

3) Design → Review → Tasks
- Draft `01-technical-design.md` and pause for explicit user review.
- Incorporate updates until the user approves Design (Gate B).
- Generate `02-tasks.md` from BOTH the approved `00-requirements.md` and `01-technical-design.md`.
- Tasks must be actionable, independently verifiable, and include acceptance criteria.
- Group tasks under Epics when useful; include dependencies and estimates where appropriate.

## Review Gates

- Gate A — Requirements Approval: Do not proceed to Technical Design until the user confirms approval or provides updates that are incorporated.
- Gate B — Design Approval: Do not proceed to Tasks until the user confirms approval or provides updates that are incorporated.
- Record approvals in the respective docs under "Review & Sign-off" sections in each template.
  - Approval recording (required): After the user approves Gate A/B, assistants must fill the "Review & Sign-off" section of the corresponding doc with:
    - Approved by: the Git committer name from `git config user.name` (fallback to user-provided name if unavailable)
    - Date: current local date in ISO `YYYY-MM-DD`
    - Notes: "Gate A: Requirements approved" or "Gate B: Design approved" as appropriate

## Editing Rules

- Scope: Operate within one project directory unless explicitly asked to touch others.
- Preservation: Do not remove or rename user files unless explicitly instructed.
- Clarity: Prefer small, incremental diffs; avoid reformatting unrelated content.
- Anchors: Keep section headers stable (`Overview`, `Risks`, `Open Questions`, etc.).
- Questions: If information is missing, add an `Open Questions` section with bullets.

## Task ID and Status Conventions

- IDs: Use `TASK-###` (e.g., `TASK-001`). Do not renumber existing IDs.
- Status: `[ ]` Todo, `[~]` In Progress, `[x]` Done, `[!]` Blocked.
- Placement:
  - New tasks → `Open Tasks` section.
  - Actively worked → `In Progress` section.
  - Completed → move to `Done` (keep the line; never delete).
  - Blocked → `Blocked` with a reason and upstream ID.
- Dependencies: Reference by ID (e.g., `Depends: TASK-004`).

## Supporting Files

- You may create project-local folders/files as needed:
  - `data/` for inputs (JSON/CSV), exports, or fixtures.
  - `notes.md` for research or scratchpad content.
  - `diagrams/` for images or architecture visuals.
- Always link or mention supporting files from the core docs so users can find them.

## Quality Bar for Generated Content

- Requirements: Clear problem statement, measurable success metrics, explicit acceptance criteria.
- Design: Architecture diagram or textual equivalent, component responsibilities, data model, interfaces, risks, and milestones.
- Tasks: Specific, testable outcomes with acceptance bullets and clear dependencies.

## Example Task Entry

```
- [ ] TASK-007 — Implement auth middleware (Epic: E-2, Depends: TASK-006, Owner: -, Est: 1d, Priority: High)
  - Acceptance:
    - Requests without valid token are rejected with 401
    - Valid tokens attach `userId` to request context
```

## When to Ask Questions

- Missing constraints, unclear scope, or conflicting goals → add bullets under `Open Questions` and ask the user.
- If estimates or priorities are unknown, set reasonable placeholders and flag with `(Needs input)`.

## Safety & Boundaries

- Do not fetch external resources unless explicitly provided by the user as files or text.
- Do not remove content; mark deprecated ideas clearly instead of deleting.
- Keep edits within the project folder; avoid cross-project changes unless asked.

## Commit Style & Versioning

- Standard: Use Conventional Commits for all commits.
- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
- Scope: Use the project folder (e.g., `projects/sample-project`) or a broad scope like `repo`, `templates`, `agents`.
- Subject: Imperative mood, 50 chars max, no trailing period (e.g., `feat(projects/foo): add tasks file`).
- Body (optional, keep brief): Only add when it materially helps. Prefer up to 3 bullet lines, each ≤ 72 chars. Avoid paragraphs and repetition.
- References: Add `Refs TASK-###` or `Closes TASK-###` as a final short line when relevant.
- Breaking changes: Add a single `BREAKING CHANGE:` line describing the impact.
- Granularity: One logical change per commit; avoid mixing formatting-only edits with content changes.

### Assistant Commit Behavior

- When the user asks to "create a commit", squash the current session's changes into a single commit unless they request multiple commits.
- Use a concise Conventional Commit subject (≤50 chars). If multiple areas are touched, pick a broad scope like `repo`.
- Add a short multi-line body (≤3 bullets, ≤72 chars each) summarizing key changes; include `Refs/Closes` lines only if relevant.
- Ask for approval before running `git` commands when sandboxing requires it.
- Do not amend or rewrite history unless explicitly requested by the user.

Examples (concise):
```
feat(projects/sample-project): add initial requirements and design

Refs TASK-001.

docs(templates): clarify task legend and epics usage

fix(projects/foo): correct acceptance criteria wording

chore(projects/sample-project): add .gitkeep to data directory

docs(agents): tighten commit message guidelines

docs(repo): add review gates and commit rules

- README: add review gates, sign-off sections
- AGENTS: add review gates + squash policy and concise rules
```

Tags (optional): If you wish to tag releases of templates or process, use semantic version tags like `v1.0.0` and note changes in `README.md`.

## Handy Prompts (for users)

- "Create a new project folder for <idea> and draft requirements."
- "Using the requirements, produce a technical design and note risks."
- "From requirements and design, generate a prioritized task list with estimates."
- "Review tasks and flag missing dependencies or open questions."

By following this guide, AI assistants can collaborate effectively and predictably within this repo.
