# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page HTML portal for **Carconnect** — an internal training and operations reference for cabin agents of a satellite vehicle tracking company based in Ecuador. The site covers service protocols: vehicle blocking/unblocking, theft emergencies, GPS platform usage, and roadside assistance (Addiuva program).

Remote: `https://github.com/capacitacionVoccareSur/CapacitacionCarConnect.git`

## Development

No build tools, no package manager, no dependencies to install. To preview the site, open `index.html` directly in a browser or use any static file server:

```bash
# Python (if available)
python -m http.server 8080

# Or just open the file directly
start index.html
```

To deploy, commit and push to `main` — the repo is served as a static site from GitHub.

There are no tests, linters, CI/CD pipelines, or pre-commit hooks.

## Architecture

Everything lives in a single `index.html` file:

- **CSS** — all styles are in a `<style>` block in `<head>`. Uses CSS custom properties defined in `:root` for the color palette (dark navy `--ink`, cyan `--cyan`, amber `--amber`, etc.) and shared values (`--maxw`, `--r`, `--shadow`).
- **HTML content** — structured as named `<section>` anchors: `#saludo`, `#soa`, `#bloqueo`, `#plataforma`, `#addiuva`, `#robo`, `#plantilla`.
- **JS** — all inline in a `<script>` at the bottom. Three IIFEs handle: sticky nav highlighting (IntersectionObserver), back-to-top button, and the platform screenshot carousel (`car-plat`). One named function `copyPlantilla()` handles clipboard copy for the service template.
- **Analytics** — Google Analytics `G-98LCT43ENK` loaded in `<head>`.

### Asset structure

```
img/
  carconnect logo.jpg     # Header logo
  cap-01.png – cap-08.png # GPS platform screenshots (used in carousel)
  cap-soa.png             # SOA section screenshot
  "PROVY Y PROVINCIA .png"

*.pdf                     # Protocol and training PDFs embedded via <iframe> in the page
```

### UI component patterns

Reusable CSS classes used throughout the content:

| Class | Purpose |
|---|---|
| `.speech-block` | Styled "agent script" blocks with pulsing cyan dot |
| `.fase` / `.fase-big` | Numbered phase cards for step-by-step procedures |
| `.steps` / `.st` | Vertical numbered step list with connecting line |
| `.nota.warn/stop/go/info` | Callout boxes (amber/red/green/cyan) |
| `.esc-grid` / `.esc` | Scenario comparison cards |
| `.flow` / `.fnode` | Flowchart nodes (start, decision, action-g/r/b/a/v, end) |
| `.acc` (`<details>`) | Accordion sections |
| `.carousel` / `.car-track` | Image carousel (JS-controlled via `carMove()`) |
| `.pdf-viewer` | PDF embed with toolbar (download/open buttons + `<iframe>`) |
| `.tag.stop/go/neu` | Inline status badges |
| `.brand-card` | Insurance/service provider cards |
| `.lb` | Lightbox overlay for image zoom |
