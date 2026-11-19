# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A static documentation site, the "GitHub Copilot Onboarding Hub": HTML guides and interactive simulators teaching GitHub Copilot in VS Code and the Copilot CLI. There is no build step, package manager, linter or test suite. It is published by GitHub Pages from the root of `main` (`.nojekyll` is present). `README.md` has the page index (numbered 1–10 plus Training and Onboarding Kit).

## Running locally

```bash
python -m http.server 8000   # then open http://localhost:8000
```

Use a server rather than `file://`, since pages load `assets/` via relative paths.

## Architecture

Every page is a self-contained HTML file at the repo root that links the shared assets (no inline framework, no bundler):

- `assets/copilot-sim.css` / `assets/copilot-sim.js` — layout, theme and behaviour for the step-based simulator pages.
- `assets/copilot-kit.css` / `assets/copilot-kit.js` — quizzes and persisted checklists. It must load **after** `copilot-sim.js`.
- Asset links carry a cache-busting query (`?v=1`). Bump it in the pages when you change an asset.

### Simulator page contract (driven by `copilot-sim.js`)

Content is declarative markup; the JS generates the chrome from it:

- Each step is `<section class="step-panel" data-section="…" data-title="…" data-sub="…">`. The script builds the sidebar (`#steps-nav`, grouped by `data-section`), progress bar (`#progress`, `#progress-label`), Back/Next rows (appended to each panel), `#step-N` deep links and arrow-key navigation. A page needs those container IDs in its header and `main-area` skeleton. Copy an existing `Copilot_Sim_*.html` as a template.
- Tabs: `[data-tabs]` containing `.tab-btn[data-tab]` and `.tab-pane[data-pane]`.
- Animated terminal: `.terminal.typer` with a `.run-btn` and `.l` lines (optional `data-wait` ms per line).
- Step-through chat: `.chat.reveal` containing `.msg` elements.
- Quizzes (`copilot-kit.js`): `.quiz` > `.q` (optional `data-why`) > `.qo` options, with `data-ok` on the correct one. The pass mark is 80%.
- Checklists (`copilot-kit.js`): `.track` lists, with `data-key` and `data-meter` (id of a counter element). Progress is saved in `localStorage` under `gh-copilot-track:<key>`.

### Content conventions

- The simulator pages share a running story (Northwind Logistics, new hire Leo, mentor Marco, the "ShipTrack" project). Keep new content consistent with it.
- Headers show an "Updated <Month Year>" pill. Update it when you revise facts.
- When adding a page, also add it to `index.html` and the README table, and add the nav or link wiring the other pages use.
