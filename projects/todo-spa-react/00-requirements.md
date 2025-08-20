# Requirements: TODO SPA (React)

## Overview
- Problem: Provide a simple, single-user TODO app as a browser-based SPA where users can add, remove, rename, check, and uncheck items. Checked items move to a Done group; unchecked items appear under In Progress.
- Goals: Fast, intuitive React UI; clear two-group list (In Progress, Done); reliable state updates; basic accessibility and keyboard support; responsive layout.
- Non-goals: Server-side rendering, authentication, multi-user sync, real-time collaboration, backend API, cloud storage, advanced filtering/search beyond the two groups.
- Stakeholders: Requester/product owner; front-end developer(s); end users.

## Scope
- In scope: React SPA with components for input/form, list rendering, item controls (rename, delete, toggle complete); automatic movement between groups on toggle; basic empty-state and error UI.
- Out of scope: Backend services, user accounts, cross-device sync, push notifications, i18n, complex theming, drag-and-drop reordering (unless prioritized later).

## Constraints & Assumptions
- Constraints: Implemented as a standalone React SPA; no network requirements; runs in modern desktop and mobile browsers (evergreen; no specific minimums requested).
- Assumptions: Single user; client-only state with required persistence via `localStorage`. No router beyond a single view. Styling with Tailwind CSS and shadcn/ui components. No unit or e2e tests needed as this is a demo.

## Risks
- Accessibility gaps (keyboard navigation, labels) if not addressed early.
- State consistency bugs (e.g., rename and toggle racing) without clear single source of truth.
- Over-expanding scope (filters, tags, due dates) can delay delivery.

## Success Metrics
- All core actions (add/remove/rename/check/uncheck) work without console errors.
- Toggling instantly moves items between In Progress and Done groups.
- Page reload preserves items using `localStorage`.
- Basic keyboard support: add via Enter, rename via keyboard, toggle via Space/Enter.
- Title length enforced to ≤ 250 chars with clear validation.
- Total item cap enforced at 30 with clear feedback when reached.
- Lighthouse (Performance/Accessibility/Best Practices) scores ≥ 90 on a sample page.

## Acceptance Criteria
- UI shows two sections: "In Progress" and "Done". Each displays the correct items based on completion state.
- Add: entering text and pressing Enter (or clicking Add) creates a new In Progress item at the top of the list. In Progress is ordered by `createdAt` descending (newest first).
- Remove: an item can be deleted; list updates immediately.
- Rename: an item label can be edited inline and saved via Enter/blur; validation prevents empty titles and titles > 250 chars with clear inline error.
- Check/Uncheck: toggling completion moves the item between groups while preserving its title.
- Done ordering: Done list is ordered by `completedAt` descending (most recently completed first).
- Counts: each section displays an item count.
- Empty states: clear messaging when a section has no items.
- Accessibility: form controls have labels; items are reachable by keyboard; Space/Enter toggles checkbox; color contrast is sufficient.
- Persistence: items persist across refresh using `localStorage` under a versioned key.
- Limits: Total items capped at 30 (adding is blocked with a helpful message once the cap is reached). Toggling does not affect the cap (since total count is unchanged).

## Inputs & References
- Data files: `data/` (none currently)
- External references: None

## Open Questions
- None at this time.

## Review & Sign-off
- Approved by: EThaiZone
- Date: 2025-08-21
- Notes: Gate A: Requirements approved
