# AGENTS.md

## Project Overview

Tesla DCF Valuation Model — a single-file, browser-based interactive tool for discounted cash flow valuation of Tesla (2025-2035). No build process, no framework, no server. Just open `index.html`.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| UI | Single `index.html`, CSS Grid/Flexbox |
| Charts | Chart.js (CDN) |
| Logic | Pure vanilla JavaScript (client-side) |
| Export | CSV download |

## Build / Run / Test Commands

```bash
# Run: just open in browser (no build step)
open index.html

# No package manager — no npm, no bundler, no transpiler
# No test framework configured yet
# No linter configured yet
```

There is no build system, no package.json, no node_modules. Everything lives in one HTML file. If adding dev tooling (linter, formatter), keep it optional and non-breaking — the file must always work by opening directly in a browser.

## Project Structure

```
tesla-dcf-model/
├── index.html          # THE file — HTML + CSS + JS all-in-one
├── plan.md             # Full implementation plan with data, pseudocode, UI spec
├── README.md           # User-facing docs (German)
├── AGENTS.md           # This file
└── .gitignore
```

`plan.md` is the source of truth for implementation. Read it before making changes.

## Code Style

### General

- All code lives inside `index.html` — HTML structure, `<style>`, and `<script>` sections
- Keep the single-file constraint: do NOT split into separate .js/.css files unless explicitly asked
- Use German for UI labels and comments visible to users; use English for code logic and variable names
- No external dependencies beyond Chart.js CDN

### JavaScript

- Use `const` by default, `let` when reassignment needed, never `var`
- Use arrow functions for callbacks and short helpers
- Use template literals for string interpolation
- Use `Math.max(0, ...)` to guard against negative values in financial calculations
- Prefer `for` loops for year-range projections (2026-2035 pattern seen throughout plan)
- Group related logic into named functions (e.g., `calculateAutomotiveRevenue()`, `calculateDCF()`)
- Use descriptive variable names: `wacc`, `terminalGrowth`, `fairValuePerShare`, not abbreviations
- Format numbers with `toLocaleString('en-US', { style: 'currency', currency: 'USD' })` for display
- Store percentages as decimals internally (0.11 for 11%), display as percentages in UI

### CSS

- Use CSS custom properties (variables) for colors, spacing, and the sidebar width (~300px)
- Use CSS Grid for the main layout (sidebar + content), Flexbox for internal components
- Color-code segments consistently: Automotive (blue), Energy (green), Services (gray), FSD (orange), Robotaxi (red), Optimus (purple), Terafab (dashed/gray)
- Responsive: ensure it works on 1280px+ screens; mobile is secondary

### HTML

- Use semantic elements where practical (`<nav>`, `<main>`, `<section>`)
- Sidebar uses accordion structure with one section per business segment
- Main area uses tab navigation: Dashboard, Revenue Detail, DCF Calculation, Sensitivity

## Error Handling & Defensive Coding

- Guard all financial calculations against division by zero (especially `wacc - terminalGrowth`)
- Clamp slider inputs to min/max bounds before using in calculations
- Use `Math.max(0, ...)` for any value that cannot be negative (FCF, revenue, margins)
- Validate user input: parse with `parseFloat()`, fall back to defaults on `NaN`
- Wrap chart updates in try/catch to prevent a bad data point from crashing the UI

## Financial Model Conventions

- Projection range: 2025 (base year) through 2035 (10-year forecast)
- Currency: USD, display in billions with one decimal (e.g., "$94.8B")
- DCF formula: `fairValuePerShare = (sum(PV(FCFs)) + PV(terminalValue) + netCash) / sharesOutstanding`
- Three scenarios: Bull / Base / Bear — see `plan.md` for exact parameters
- Terminal value: `FCF_final * (1 + g) / (WACC - g)`

## Key Data Points (from plan.md)

- Tesla 2025 revenue: $94.8B, shares outstanding: 3.216B, net cash: ~$32B
- FSD subscribers: 1.1M at $99/month, 38% YoY growth
- Robotaxi: Austin start June 2025, ~7,200 fleet in 2026
- Energy: 46.7 GWh deployed in 2025, $12.8B revenue

## When Making Changes

1. Read `plan.md` first — it contains the full spec, data, and pseudocode
2. Test by opening `index.html` in a browser after every change
3. Verify sliders update charts in real-time; DCF must recalculate on every input change
4. CSV export must include all projection years and segments
5. Do not add build steps, package managers, or frameworks without explicit approval
6. Keep the disclaimer visible: "Dies ist kein Investment-Rat."
7. After implementing a feature, verify the full flow: input change → calculation → chart update → CSV export
8. Check that all three scenarios (Bull/Base/Bear) produce reasonable values across the sensitivity range

## Common Patterns

- **Slider binding**: attach `input` event listener → update state → call `recalculate()` → call `updateCharts()`
- **Number display**: internal values in raw numbers, display via `formatCurrency()` / `formatPercent()` helpers
- **Chart updates**: destroy old chart instance before creating new one to prevent memory leaks
- **CSV export**: build array of rows, join with commas, create Blob, trigger download via hidden `<a>` element

## Things to Avoid

- Do not use `innerHTML` for user-facing content (use `textContent` for safety)
- Do not hardcode magic numbers — extract to named constants at the top of the script
- Do not add dependencies without explicit approval — the single-file constraint is sacred
- Do not break the accordion/tabs when adding new sidebar sections
