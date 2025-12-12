# Research Summary

## Decision: Keep current stack (HTML/CSS/vanilla JS), no new build tools
- **Rationale**: User requested “use the current stack”; existing repo is static. Keeps footprint minimal and aligns with performance/DevEx goals.
- **Alternatives considered**: Add a JS framework (adds complexity, unnecessary for static content); add build tooling (overhead without dynamic needs).

## Decision: Structure map as layered sections with ownership and dependency callouts
- **Rationale**: Clear sections per layer with owner/contact, scope, and dependency badges makes ownership discoverable in <30s and supports friction reduction.
- **Alternatives considered**: Single long list (harder to scan); modal-heavy UI (hurts mobile/responsiveness).

## Decision: Friction reporting via provided intake link/mailto plus inline confirmation
- **Rationale**: Static stack lacks backend; linking to an existing intake path (mail, form, ticket queue) satisfies “report/suggest” while keeping current stack. Inline “sent/opened” confirmation clarifies action.
- **Alternatives considered**: Build custom form + backend (not in scope/current stack); no reporting path (fails requirements).

## Decision: Performance/accessibility guardrails
- **Rationale**: Lean CSS/JS, no blocking assets, maintain semantic HTML and ARIA for clarity and fast load under ~1s.
- **Alternatives considered**: Heavy visualizations or external libs (risk bloat and slower loads).
