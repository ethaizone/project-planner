# Tasks: TODO SPA (React)

Legend: [ ] Todo, [~] In Progress, [x] Done, [!] Blocked

## Epics
- E-1: Scaffold & UI primitives
- E-2: State management & persistence
- E-3: Core features (add/toggle/delete/rename)
- E-4: Grouping, ordering, and counts
- E-5: UX polish & accessibility
- E-6: QA & performance

## Open Tasks
- [ ] TASK-001 — Define UI layout and components (Epic: E-1, Depends: -, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Component tree matches design doc (`App`, `TodoInput`, `TodoList`, `TodoItem`).
    - Placeholder render shows sections without errors.
- [ ] TASK-002 — Implement add item flow (Epic: E-3, Depends: TASK-011, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Typing and Enter/Add creates a new In Progress item.
    - Validation: trimmed title 1–250 chars; errors shown inline.
    - Cap: adding blocked at 30 items with clear message.
    - New items appear at top (newest first) of In Progress.
- [ ] TASK-003 — Render grouped lists with counts (Epic: E-4, Depends: TASK-011, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Two sections: In Progress and Done.
    - Correct items in each section; counts displayed.
    - Empty states shown when a section has no items.
- [ ] TASK-004 — Toggle done/un-done with movement (Epic: E-3, Depends: TASK-003, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Toggling moves item between sections instantly.
    - Sets `completedAt` when done; clears when undone.
    - Ordering rules preserved after toggle.
- [ ] TASK-005 — Inline rename and save (Epic: E-3, Depends: TASK-003, Owner: -, Est: 0.5d, Priority: Medium)
  - Acceptance:
    - Click/keyboard to edit title; Enter/blur saves.
    - Validation: 1–250 chars; errors inline; no empty titles.
    - `updatedAt` refreshed on save.
- [ ] TASK-006 — Delete item with confirmation (Epic: E-3, Depends: TASK-003, Owner: -, Est: 0.25d, Priority: Medium)
  - Acceptance:
    - Confirm then delete removes item immediately from state.
    - No console errors; counts update correctly.
- [ ] TASK-007 — Styling with Tailwind + shadcn/ui (Epic: E-1, Depends: TASK-015, Owner: -, Est: 0.5d, Priority: Medium)
  - Acceptance:
    - shadcn/ui primitives used for inputs, buttons, checkbox, separators.
    - Consistent spacing, readable typography, responsive layout.
- [ ] TASK-008 — Implement localStorage persistence (Epic: E-2, Depends: TASK-012, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Items persist across reloads under key `todo-spa-react:v1`.
    - Versioned payload `{ version: 1, todos }` used.
    - Corruption handled (try/catch) falling back to empty state.
- [ ] TASK-009 — Accessibility pass + keyboard flows (Epic: E-5, Depends: TASK-002, Owner: -, Est: 0.5d, Priority: Medium)
  - Acceptance:
    - Labels for inputs; focus outlines visible.
    - Enter adds/saves rename; Space/Enter toggles checkbox.
    - Color contrast meets WCAG AA for text and controls.
- [ ] TASK-011 — Implement reducer and actions (Epic: E-2, Depends: -, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Actions: ADD, TOGGLE, RENAME, DELETE with timestamp updates.
    - IDs via `crypto.randomUUID()` or fallback.
    - Pure functions; no side effects inside reducer.
- [ ] TASK-012 — Storage utility with versioning (Epic: E-2, Depends: TASK-011, Owner: -, Est: 0.25d, Priority: Medium)
  - Acceptance:
    - `load()` returns valid state or empty on parse error.
    - `save()` serializes `{ version: 1, todos }`.
    - Key constant `todo-spa-react:v1` defined in one place.
- [ ] TASK-013 — Ordering logic for lists (Epic: E-4, Depends: TASK-011, Owner: -, Est: 0.25d, Priority: Medium)
  - Acceptance:
    - In Progress: sort by `createdAt` desc.
    - Done: sort by `completedAt` desc (fallback `updatedAt`).
    - Stable behavior verified after toggles and renames.
- [ ] TASK-014 — Feedback and toasts for validation (Epic: E-5, Depends: TASK-002, Owner: -, Est: 0.25d, Priority: Low)
  - Acceptance:
    - Inline errors for title length/empty; toast for cap reached.
    - Screen reader friendly messaging.
- [ ] TASK-015 — Tailwind + shadcn/ui setup (Epic: E-1, Depends: -, Owner: -, Est: 0.5d, Priority: High)
  - Acceptance:
    - Tailwind configured; shadcn/ui installed; base components available.
    - Build succeeds; styles load correctly.
- [ ] TASK-016 — Lighthouse and polish (Epic: E-6, Depends: TASK-007, Owner: -, Est: 0.25d, Priority: Low)
  - Acceptance:
    - Lighthouse scores ≥ 90 for Performance, Accessibility, Best Practices.
    - Minor UI tweaks applied as needed to meet scores.

## In Progress

## Blocked

## Done
- [x] TASK-010 — Confirm persistence and ordering preferences (Resolved by: Gate A approval and user answers)

## Notes
- Tasks derived from approved Requirements and Technical Design.
