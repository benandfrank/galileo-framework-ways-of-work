# Tasks: Context Map with Layer Ownership for Frictionless DevEx

**Input**: Design documents from `/specs/001-context-map-ownership/`  
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/

**Tests**: Not requested; focus on implementation and manual validation per quickstart.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Prepare page structure and styling foundations using the current static stack.

- [X] T001 [P] Create structural sections for summary, layers, dependencies, and friction containers in `index.html`
- [X] T002 [P] Add CSS variables, grid/layout, and badge styles to support ownership/dependency/friction views in `style.css`
- [X] T003 Add base script hooks (query selectors and empty render slots) for the new sections in `script.js`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Shared data scaffolding and legend needed before story-specific rendering.

- [X] T004 Seed placeholder data structures for layers, components, owners, dependencies, friction indicators, and executive summary in `script.js`
- [X] T005 Add shared render utilities for badges, lists, last-updated text, and responsive truncation in `script.js`
- [X] T006 Add legend/glossary section markup (stressors/ownership/dependency/friction keys) with anchors in `index.html`

**Checkpoint**: Foundation ready - user story implementation can now begin in parallel.

---

## Phase 3: User Story 1 - See ownership at a glance (Priority: P1) 🎯 MVP

**Goal**: Show each layer’s purpose and clear owner/contact so users can find ownership within 30s.

**Independent Test**: From the landing view, identify the owner for any layer/component in under 30 seconds.

### Implementation for User Story 1

- [X] T007 [US1] Populate layer/component ownership data (owners, contacts, engagement rules) aligned to entities in `script.js`
- [X] T008 [US1] Render ownership cards with layer purpose, scope, owner badges, and contact/engagement cues in `script.js` (using `index.html` containers)
- [X] T009 [P] [US1] Style ownership badges, focus states, and mobile readability for ownership sections in `style.css`

**Checkpoint**: User Story 1 independently deliverable (ownership clarity and contact paths visible).

---

## Phase 4: User Story 2 - Navigate dependencies with minimal friction (Priority: P2)

**Goal**: Let users trace upstream/downstream dependencies with engagement expectations visible.

**Independent Test**: Trace a dependency and find the owning team plus engagement/SLA info without external help.

### Implementation for User Story 2

- [X] T010 [US2] Extend data with dependencies and engagement expectations between components/layers in `script.js`
- [X] T011 [US2] Render dependency view with upstream/downstream cues, owner attribution, and SLA hints in `script.js` (using `index.html` containers)
- [X] T012 [P] [US2] Add cross-layer navigation anchors/jump links and inline labels to support dependency tracing in `index.html` and `style.css`

**Checkpoint**: User Story 2 independently deliverable (dependency tracing and engagement clarity).

---

## Phase 5: User Story 3 - Spot and fix friction points (Priority: P3)

**Goal**: Expose friction indicators and provide a clear reporting/action path with confirmation.

**Independent Test**: Click a friction indicator, see owner/action path, and submit/report with visible confirmation cue.

### Implementation for User Story 3

- [X] T013 [US3] Add friction indicator data (severity/status/owner) and link to affected layers/components in `script.js`
- [X] T014 [US3] Render friction indicators with owner, resolution path (mailto/intake link), and confirmation messaging in `script.js` (using `index.html` containers)
- [X] T015 [P] [US3] Update executive summary to surface top friction hotspots and timestamps in `index.html` and `script.js`

**Checkpoint**: User Story 3 independently deliverable (friction visibility and reporting path).

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final refinements across stories.

- [X] T016 [P] Refine copy and headings for ownership, dependency, and friction sections for executive readability in `index.html` (includes corrected owners and dependencies)
- [X] T017 Improve responsive spacing, contrast, and touch targets for all new elements in `style.css`
- [X] T018 Record manual validation notes (ownership findability, dependency trace, friction reporting flow) in `specs/001-context-map-ownership/quickstart.md`

---

## Dependencies & Execution Order

- Phase 1 → Phase 2 → User stories (US1 → US2 → US3 by priority; US2/US3 can run in parallel after Phase 2 if staffed).
- Polish after desired user stories are complete.

## Parallel Opportunities (examples)

- Phase 1: T001 (HTML scaffolding) and T002 (CSS tokens) in parallel.
- Phase 3 (US1): T009 styling in parallel with T007/T008 data+render.
- Phase 4 (US2): T012 navigation aids in parallel with T010/T011.
- Phase 5 (US3): T015 summary in parallel with T013/T014.

## Implementation Strategy

- MVP: Complete Phases 1–2, then deliver US1; validate ownership clarity before adding dependencies/friction.
- Incremental: Add US2 (dependency tracing), then US3 (friction/reporting), keeping each story independently testable per its checkpoint.
