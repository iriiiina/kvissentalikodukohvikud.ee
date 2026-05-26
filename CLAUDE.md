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

## CI

- **Link checker** — `.github/workflows/links.yml` runs [lychee](https://github.com/lycheeverse/lychee) on every push to `main`, every PR, and weekly (Mondays 06:00 UTC). Hosts that block bots are skipped via `.lycheeignore`.

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

**Work directly on `main`.** Do not create feature branches or worktrees — make all edits in the main repo's working tree.

## Code conventions

- **Language:** All content in Estonian (`lang="et-EE"`)
- **HTML:** Semantic elements (`header`, `nav`, `main`, `footer`, `section`). Schema.org microdata for SEO.
- **CSS:** No preprocessor. Flexbox layouts. Mobile-first. IDs and classes in kebab-case.
- **JS:** Minimal — only menu toggle and gallery. Inline `onClick`/`onchange` handlers.
- **Git commits:** Lowercase, present tense, no emoji (e.g., "add google form link", "remove program and map menu points")

## Sitemap

Whenever you make any content change to a file in this project, update the `<lastmod>` value of the **first `<url>` entry** (the current event at `/`) in `sitemap.xml` to today's date in `YYYY-MM-DD` format. Do not touch the `<lastmod>` values of archived year entries — they should stay frozen at the date of that year's event.
