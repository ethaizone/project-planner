# Technical Design: TODO SPA (React)

## Architecture Overview
- Single-page React application rendering two grouped lists (In Progress, Done) with client-side state and required `localStorage` persistence.
- Single view (no router). Derived views for grouping/sorting; core state is a flat todos array managed via a reducer to centralize logic and keep updates predictable.

## Components
- App: application shell; initializes state from `localStorage`; provides handlers; layout.
- TodoInput: add new item control with validation and feedback (length limit, cap reached).
- TodoList: renders a section (title, count, items) for a filtered/sorted subset.
- TodoItem: displays label and controls (toggle, inline rename, delete) with keyboard support.
- UI primitives (shadcn/ui): `Input`, `Button`, `Checkbox`, `Card`/`Separator`, and `Toast`/`Alert` for feedback.
- Storage util: load/save state to `localStorage` under versioned key.

## Data Model
- Todo: `{ id: string, title: string, done: boolean, createdAt: number, updatedAt: number, completedAt?: number }`
- AppState: `{ todos: Todo[] }`
- LocalStorage shape: `{ version: 1, todos: Todo[] }` under key `todo-spa-react:v1`.

## Interfaces / APIs
- No backend APIs.
- Component props/events:
  - TodoInput: `onAdd(title: string)`, `atCap: boolean`, `error?: string`
  - TodoList: `items: Todo[]`, `title: string`, `count: number`, `onToggle(id)`, `onRename(id, title)`, `onDelete(id)`
  - TodoItem: `todo`, `onToggle`, `onRename`, `onDelete`
- Reducer actions:
  - `ADD(title)` — validate (non-empty, ≤250 chars, cap < 30), create todo (id via `crypto.randomUUID()` or fallback), push; set timestamps.
  - `TOGGLE(id)` — flip `done`; set `completedAt` when true, unset when false; update `updatedAt`.
  - `RENAME(id, title)` — validate (non-empty, ≤250 chars); update `title`, `updatedAt`.
  - `DELETE(id)` — remove from array.

## Behavior & Ordering
- In Progress: derived as `todos.filter(!done)` sorted by `createdAt` desc (newest first).
- Done: derived as `todos.filter(done)` sorted by `completedAt` desc (most recent completion first; fallback to `updatedAt` if missing for resilience).
- Movement: `TOGGLE` re-renders with the item appearing in the other list based on `done` state.
- Limits:
  - Title: 1–250 chars (trimmed). Disallow empty/whitespace-only titles.
  - Count: Maximum 30 items total; block `ADD` when at cap with clear inline feedback.

## Persistence
- Load: on initial render, read key `todo-spa-react:v1`; if version matches, hydrate `todos`.
- Save: `useEffect` on `todos` to serialize and store `{ version: 1, todos }`.
- Corruption handling: try/catch on parse; if invalid, start with empty state.

## Styling & Accessibility
- Styling: Tailwind CSS with shadcn/ui components; light spacing, readable typography; responsive single-column layout.
- Accessibility: labels for inputs, focus outlines, checkbox toggles via Space/Enter, inline rename uses input with accessible name; ensure color contrast meets WCAG AA.

## Decisions & Trade-offs
- `useReducer` centralizes state transitions vs multiple `useState` calls; simpler to test manually and reason about.
- Client-only persistence via `localStorage` meets demo needs without backend complexity.
- Flat array with derived sorts is simpler than normalized store for this scope.

## Dependencies
- React + Vite (or CRA) for scaffold.
- Tailwind CSS + shadcn/ui for UI components.
- Optional: `nanoid` if `crypto.randomUUID` unsupported; otherwise use native.

## Risks & Mitigations
- Accessibility gaps: define keyboard flows and verify manually per acceptance criteria.
- Local storage limits/corruption: small payload; handle parse errors gracefully and reset.
- Overflows of title text: enforce limit and truncate visually with title attribute for full text.

## Milestones
- M1: Scaffold app with Vite, Tailwind, shadcn/ui; layout shell.
- M2: Implement reducer, add flow with validation and cap.
- M3: Grouped rendering with counts and empty states.
- M4: Toggle movement + ordering; delete.
- M5: Inline rename; keyboard/a11y polish; persistence wiring.
- M6: Lighthouse pass and minor UI polish.

## Validation
- Manual validation against acceptance criteria:
  - Add/remove/rename/toggle; movement between groups; counts and limits.
  - Persistence across reload; invalid storage resets gracefully.
  - Keyboard flows: Enter to add/save, Space/Enter to toggle.
  - Lighthouse ≥ 90 for PWA page (Perf/A11y/BP).

## Open Questions
- None at this time.

## Review & Sign-off
- Approved by: EThaiZone
- Date: 2025-08-21
- Notes: Gate B: Design approved
