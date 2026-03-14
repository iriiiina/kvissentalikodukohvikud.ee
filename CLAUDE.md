# CLAUDE.md

## Project overview

Static website for **Kvissentali päev** (formerly "Kvissentali kodukohvikute päev") — an annual neighborhood event in Kvissentali, Tartu, Estonia. Hosted at https://kvissentalikodukohvikud.ee via GitHub Pages.

The current (upcoming) event is the 5th edition on May 30, 2026. Past events (2022–2025) are archived in year directories.

## Tech stack

- **Pure static site** — HTML5, CSS3, vanilla JavaScript. No frameworks, no build tools, no package manager.
- **Google Fonts** — Gayathri (400, 700)
- **Grid Gallery** — vendored JS/CSS library for photo lightboxes (`grid-gallery/`)
- **Hosting** — GitHub Pages with custom domain (CNAME)
- **PWA** — `manifest.json` with theme color `#405d27`

## Project structure

```
/                     → Current/upcoming event (index.html, style.css)
/2022/                → Archive: 1st event
/2023/                → Archive: 2nd event
/2024/                → Archive: 3rd event
/2025/                → Archive: 4th event
/{year}/pictures/     → Event photos (JPG)
/{year}/grid-gallery/ → Vendored gallery library (JS + CSS)
/{year}/img/          → Year-specific images and icons
/{year}/favicon/      → Favicons (duplicated per year)
/img/                 → Current event images, icons, marketing/
/favicon/             → Current event favicons
/qr/                  → QR code redirect pages
```

Each year directory is **self-contained** — a full copy of all assets. New years are created by duplicating the previous year's directory and updating content.

## Development

No build step. To run locally:

```sh
python -m http.server 8000
# or just open index.html in a browser
```

## Deployment

Push to `main` branch → GitHub Pages serves automatically.

## Design conventions

**Colors:**
- Grass Green: `#405d27` (primary — links, borders, nav)
- Light Green: `#6ab04c` (secondary)
- Orange: `#e58e26` (accents, hover states)
- Gray: `#3e4444` (body text)
- White: `#ffffff` (background)

**Responsive breakpoint:** 768px (mobile hamburger ↔ desktop horizontal nav)

**Icons:** SVG files in `img/`, colorized via CSS `filter`. Inline icons use class `.svg-in-text`.

## Git policy

**Do not** pull, commit, or push. Read-only git commands (`git status`, `git diff`, `git log`, etc.) are fine for gathering info.

## Code conventions

- **Language:** All content in Estonian (`lang="et-EE"`)
- **HTML:** Semantic elements (`header`, `nav`, `main`, `footer`, `section`). Schema.org microdata for SEO.
- **CSS:** No preprocessor. Flexbox layouts. Mobile-first. IDs and classes in kebab-case.
- **JS:** Minimal — only menu toggle and gallery. Inline `onClick`/`onchange` handlers.
- **Git commits:** Lowercase, present tense, no emoji (e.g., "add google form link", "remove program and map menu points")
