# galileo-framework-ways-of-work Development Guidelines

Static HTML/CSS/JS microsite visualizing Galileo Platform's socio-technical operating system.
No build tools, no package manager - runs directly in browser.

Auto-generated from all feature plans. Last updated: 2025-01-12

## Tech Stack

- HTML5 semantic markup with ARIA accessibility
- CSS3 with custom properties + Tailwind CDN (utilities only)
- Vanilla JavaScript (ES6+) - config-driven SVG generation
- GSAP 3.12.2 (CDN) for animations
- Google Fonts: Space Grotesk, Inter, Material Symbols Outlined

## Development Commands

### Local Development

#### Start local server:
```bash
python3 -m http.server 8000
# Open: http://localhost:8000/index.html
```

#### Or direct file open:
```bash
open index.html
```

### Validation & Quality

#### HTML validation:
Paste index.html into: https://validator.w3.org/

#### CSS validation:
Paste style.css into: https://jigsaw.w3.org/css-validator/

#### JavaScript validation:
Use browser DevTools console for runtime errors

#### Accessibility audit:
Browser extensions: axe DevTools, WAVE, or Lighthouse

### Manual Testing Checklist

- [ ] All 4 views render correctly (WOW, POM, STA, POV)
- [ ] Keyboard navigation: Tab, Enter, Space work on all interactive elements
- [ ] Mode toggles function (insight/stability loops, team overlays, residuality)
- [ ] Context map interactions (hover, click, detail panel)
- [ ] Mobile responsive behavior (640px, 768px, 1024px breakpoints)
- [ ] Browser compatibility: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+

## Code Style Guidelines

### HTML

- Use semantic HTML5 elements: `<section>`, `<article>`, `<nav>`, `<header>`
- Indentation: **4 spaces** (enforce consistently)
- ARIA attributes for interactive elements:
  - `role="button"` for clickable non-button elements
  - `aria-label` for icon-only buttons or SVG diagrams
  - `data-focusable="true"` for keyboard-accessible custom elements
- Use `data-*` attributes for JavaScript hooks, not classes
- Inline event handlers for simple toggles: `onclick="switchView('wow', event)"`
- Complex event logic: use `addEventListener` in script.js
- Close all tags properly; maintain consistent quote style (double quotes)

### CSS

- Indentation: **4 spaces**
- Define reusable values in `:root` custom properties (see Color Palette below)
- Use Tailwind CDN classes for layout/spacing; custom CSS for components
- Component naming: `.component-modifier` pattern (e.g., `.view-btn.active`)
- State classes: `.active`, `.revealed`, `.hidden`, `.opacity-0`
- Colors: Reference CSS variables (`var(--blue)`, `var(--slate-200)`)
- Transitions: `0.2s ease` for hover/focus; `0.5s` for view changes
- Focus states: **Required** - use `:focus-visible` with 2px cyan outline
- Avoid `!important` unless overriding CDN defaults
- Media queries: Target 640px (mobile), 768px (tablet), 1024px (desktop)
- Group styles: layout → colors → typography → interactive states
- Maintain existing glass-morphism design system:
  ```css
  .glass-panel {
      background: rgba(15, 23, 42, 0.78);
      backdrop-filter: blur(16px);
      border: 1px solid rgba(148, 163, 184, 0.35);
  }
  ```

### JavaScript

- Indentation: **4 spaces**
- **Semicolons: Required** (enforce on all statements)
- Function naming: `verbNoun` pattern (e.g., `buildWowDiagram`, `renderContextStressGrid`, `staSetMode`)
- Constants: `SCREAMING_SNAKE_CASE` (e.g., `TRACK_COLORS`, `ENABLE_FOCUS`)
- Config objects: `camelCase` (e.g., `wowConfig`, `contextStressModel`)
- Use `const` by default; `let` only when reassignment needed; avoid `var`
- Template literals for HTML/SVG generation
- Arrow functions for callbacks; named functions for top-level/exported functions
- Comments: Explain "why" not "what"; use `// Section dividers` liberally
- Event handlers:
  - Simple: inline `onclick="functionName()"`
  - Complex: `element.addEventListener('click', handler);`
- Async operations: Use promises, avoid callback hell
- Error handling: Defensive checks (`if (!container) return;`)

#### Config-Driven Architecture Pattern

**ALL diagram data lives in config objects.** Never hardcode content in rendering functions.

- `wowConfig`: Discovery/Delivery/Operations tracks, loops, residual zones
- `pomConfig`: POM tracks and feedback loops
- `staLayers`: 5-layer architecture model definitions
- `contextStressModel`: Context cards with stress scores and behavioral modes
- `ctxLayers`, `ctxDependencies`, `ctxFrictionIndicators`: Ownership & friction data
- `journeyStepDetails`: Customer value stream journey steps
- `roleActivitiesData`: POV model role contributions per DDO track

**To modify content**: Edit config objects at top of script.js, not rendering functions.

#### SVG Generation Pattern

1. Define data structure (config object)
2. Create `build*Diagram()` function
3. Use template literals with `map()` for repeated elements
4. Define `<defs>` for reusable gradients, markers, filters
5. Add interactivity via `addEventListener` or `data-focusable`

## Design System - Color Palette

### CSS Custom Properties (`:root`)

```css
--bg: #0b0f19;                    /* Background dark */
--panel: rgba(15, 23, 42, 0.78);  /* Glass panel background */
--stroke: rgba(148, 163, 184, 0.35); /* Border/stroke */
--blue: #3b82f6;                  /* Discovery track */
--green: #10b981;                 /* Delivery track */
--rose: #ec4899;                  /* Operations track */
--cyan: #06b6d4;                  /* Platform, stability loop */
--amber: #fbbf24;                 /* Enabling teams, warnings */
--purple: #a855f7;                /* Complicated subsystem */
--slate-100: #e2e8f0;             /* Primary text */
--slate-200: #cbd5e1;             /* Secondary text */
--slate-300: #94a3b8;             /* Tertiary text */
```

### JavaScript Color Constants (`TRACK_COLORS`)

```javascript
const TRACK_COLORS = {
    discovery: { base: '#3b82f6', light: '#60a5fa', text: '#bfdbfe' },
    delivery: { base: '#10b981', light: '#34d399', text: '#bbf7d0' },
    operations: { base: '#ec4899', light: '#f472b6', text: '#fbcfe8' }
};
```

**Usage**: Colors auto-propagate through SVG gradients, strokes, and text when referenced from config.

## File Organization

### Project Structure

```text
index.html          # Page structure, 4 view containers, CDN links
style.css           # Custom properties, glass-panel system, component styles
script.js           # Config objects → rendering → event handlers
specs/              # Feature planning documents (not loaded by app)
  001-context-map-ownership/
    spec.md
    plan.md
    data-model.md
    contracts/
.specify/           # Spec system templates and scripts
```

### index.html
- Semantic structure: `<nav>` → view containers → modals
- 4 main views: `#wow-view`, `#pom-view`, `#sta-view`, `#pov-view`
- CDN links: Tailwind, GSAP, Google Fonts
- Modal/overlay markup for journey detail, context detail

### style.css
- `:root` custom properties (lines 1-14)
- Utility classes: `.glass-panel`, `.text-gradient`, `.view-switcher`
- View switching: `.view-container`, `.view-btn`
- Component styles: `.journey-card`, `.ctx-card`, `.ctx-pill`
- Responsive: `@media (max-width: 640px)` for mobile

### script.js (organized in sequential sections)
1. **Lines 1-46**: Tailwind config, utilities, view switcher
2. **Lines 88-321**: WOW diagram (config, build, modes, sequences)
3. **Lines 323-586**: POM diagram (tracks, loops, team overlays, behavior modes)
4. **Lines 588-895**: STA diagram (5 layers, DDO/teams/residuality modes, context map)
5. **Lines 897+**: POV system (role bubbles, activities, contributions)
6. **Bottom**: `DOMContentLoaded` initialization

### specs/ folder
- Feature plans following the Specify framework
- Each spec has: `spec.md`, `plan.md`, `tasks.md`, `checklists/`, `contracts/`
- Not loaded by the application; for documentation and planning only

## How to Extend

### Adding a New View

1. **HTML**: Add view container in `index.html`
   ```html
   <div id="new-view" class="view-container">
       <!-- content -->
   </div>
   ```

2. **Navigation**: Add button to `.view-switcher`
   ```html
   <button class="view-btn" onclick="switchView('new', event)">New View</button>
   ```

3. **Config**: Create config object in `script.js`
   ```javascript
   const newConfig = {
       items: [...],
       modes: [...]
   };
   ```

4. **Build function**: Generate SVG or HTML
   ```javascript
   function buildNewDiagram() {
       const container = document.getElementById('new-diagram');
       if (!container) return;
       container.innerHTML = `<svg>...</svg>`;
   }
   ```

5. **Initialize**: Call in `DOMContentLoaded`
   ```javascript
   document.addEventListener('DOMContentLoaded', () => {
       buildNewDiagram();
       // ... other init
   });
   ```

### Modifying Existing Diagrams

**Change track labels or colors:**
Edit the config object (e.g., `wowConfig.tracks[0].label`) - colors auto-propagate through gradients and markers.

**Add feedback loops:**
Add to `loops` array in config with path data (`from`, `cp`, `to`), color, and marker ID.

**Update context data:**
Edit `contextStressModel` or `ctxLayers` - rendering functions automatically update based on config.

**Modify journey steps:**
Edit `journeyStepDetails` object with new steps, perspectives, signals, exceptions.

### Adding Interactive Overlays

1. Add SVG `<g>` layer in build function with `opacity-0` class
2. Create toggle function:
   ```javascript
   function diagramSetMode(mode) {
       document.querySelectorAll('.overlay-layer').forEach(l => l.classList.add('opacity-0'));
       const target = document.getElementById(`layer-${mode}`);
       if (target) target.classList.remove('opacity-0');
   }
   ```
3. Add mode buttons in HTML
4. Bind to button click events

### Modifying the Context Map

- Contexts defined in `buildStaContextMap()` function
- Layout uses calculated positions: `y = startY + layerIndex * layerHeight`
- To add context: Extend config and add to appropriate layer
- Hover states bound via `.forEach()` loop after render
- Click handlers open detail panel with DDO contributions

## Accessibility Guidelines

Follow WCAG 2.1 AA standards as minimum.

### Keyboard Navigation

- All interactive elements must be keyboard-accessible
- SVG elements: use `data-focusable="true"` attribute
- Support Tab (focus), Enter (activate), Space (activate)
- Call `ENABLE_FOCUS()` utility after rendering interactive diagrams
- Ensure logical tab order (matches visual layout)

### Focus States

- All buttons/links must have `:focus-visible` styles
- Standard: 2px cyan outline with 2px offset
- Never remove focus outlines with `outline: none` without custom replacement

### ARIA & Semantic Markup

- `role="button"` for clickable non-button elements (e.g., SVG groups)
- `aria-label` for icon-only buttons and SVG diagrams
- `role="img"` for complex SVG visualizations
- Maintain heading hierarchy: h1 → h2 → h3 (no skipping)
- Use `<section>` with `aria-labelledby` for major page regions

### Screen Readers

- Use descriptive labels: "Discovery track - Clarify problem and context"
- Avoid generic text like "Click here" - use descriptive link text
- Ensure dynamic content changes are announced (use `aria-live` if needed)
- Test with VoiceOver (macOS), NVDA (Windows), or JAWS

## Browser Compatibility

### Supported Browsers (Modern evergreen)

- Chrome 90+ (recommended for development)
- Firefox 88+
- Safari 14+
- Edge 90+

### Required Features

- CSS Custom Properties (variables) - no fallback
- ES6+ JavaScript: `const`, `let`, arrow functions, template literals, `Map`, `Set`
- SVG 1.1 with inline styles
- IntersectionObserver API (with scroll fallback)

### Graceful Degradation

- `IntersectionObserver` fallback: uses `checkReveal()` on scroll event
- CSS animations degrade gracefully if not supported (no FOUC)
- GSAP animations are progressive enhancement (site works without)

## Git Workflow: Ship - Show - Ask

Use [Conventional Commits](https://www.conventionalcommits.org/) format.

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`

**Examples**:
```
feat(wow): add residuality overlay mode to continuous flow diagram
fix(sta): correct context map click handler for mobile touch events
docs(agents): document SVG generation patterns and config structure
style(css): update glass-panel opacity for better readability
refactor(script): extract common SVG gradient generation to utility
```

### Decision Framework

- **Ship**: Small fixes, documentation updates, obvious improvements (commit & push)
- **Show**: New features, refactoring, style changes (commit, push, notify team)
- **Ask**: Breaking changes, architecture decisions, major features (discuss before implementing)

### Code Review

- Another agent or team member should review before merging to main
- Review checklist:
  - [ ] Code follows style guidelines (indentation, semicolons, naming)
  - [ ] Accessibility requirements met (keyboard nav, ARIA, focus states)
  - [ ] Browser compatibility maintained
  - [ ] Config-driven pattern respected (no hardcoded content)
  - [ ] Manual testing checklist completed

## Spec System (Specify Framework)

This project uses the Specify framework for feature planning and documentation.

### Structure

Each feature lives in `specs/<feature-id>/`:
- `spec.md`: Feature specification (problem, solution, constraints)
- `plan.md`: Implementation plan (phases, tasks, risks)
- `tasks.md`: Granular task breakdown
- `checklists/requirements.md`: Requirements checklist
- `contracts/`: API contracts, data models (YAML/JSON)

### Templates

Located in `.specify/templates/`:
- `spec-template.md`
- `plan-template.md`
- `tasks-template.md`
- `checklist-template.md`
- `agent-file-template.md`

### Scripts

Located in `.specify/scripts/bash/`:
- `create-new-feature.sh`: Scaffold new feature from templates
- `setup-plan.sh`: Initialize planning artifacts
- `update-agent-context.sh`: Update AGENTS.md with plan insights

### Usage

```bash
# Create new feature spec
./.specify/scripts/bash/create-new-feature.sh <feature-id>
```

Specs are documentation artifacts - they are not loaded or executed by the application.

## Recent Changes

- 001-context-map-ownership: Added plan artifacts and static-stack guidance
- 2025-01-12: Enhanced AGENTS.md with comprehensive code style, accessibility, and extension guides

<!-- MANUAL ADDITIONS START -->
<!-- Add custom project-specific guidelines below this line -->
<!-- MANUAL ADDITIONS END -->
