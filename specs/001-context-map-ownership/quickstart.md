# Quickstart: Context Map with Layer Ownership

## Prereqs
- Modern browser (Chrome/Firefox/Safari/Edge)
- Optional: local HTTP server (`python3 -m http.server 8000`) for CORS-safe testing

## Run locally (current stack)
1) From repo root: `python3 -m http.server 8000`
2) Open `http://localhost:8000/index.html`
3) Verify ownership labels, dependency cues, friction indicators, and executive summary render on desktop and mobile sizes.

## Edit
- Content/UI: `index.html`, `style.css`, `script.js`
- Spec/plan artifacts: `specs/001-context-map-ownership/`
- Keep assets lean (<150KB gzip) and avoid new build tools.

## Validate
- Manual:
  - Ownership: pick any layer/component and find owner/contact in <30s.
  - Dependencies: trace a listed dependency and confirm owner + expectation/SLA is visible.
  - Friction: open a friction item, see action path, and trigger the mailto/intake link with confirmation cue.
  - Navigation: legend/jump links work; context map anchors reachable.
- Accessibility: headings order, labels, focus states, color contrast.
- Performance: load page; ensure no blocking external assets; basic Lighthouse or DevTools audit for quick check.
