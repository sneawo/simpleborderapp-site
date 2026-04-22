# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Marketing site for the **Simple Border** iOS/macOS app (App Store id `6451375021`), served as a static site at https://simpleborder.app via GitHub Pages (see `CNAME`). There is no app source code here — only the public website.

## Commands

No build, bundler, test runner, or linter. To preview locally:

```
python3 -m http.server 8000
```

Then open http://localhost:8000. Changes to `main` deploy automatically via GitHub Pages.

## Architecture

- **Pages are self-contained HTML files at the repo root** — each one inlines its own `<style>` and `<script>` blocks. There is no shared CSS/JS file. The dark-theme CSS variables (`--bg`, `--fg`, `--accent: #7ee787`, etc.) and the footer nav are duplicated across pages; when changing them, update every HTML file.
- **Pages currently shipped:** `index.html`, `changelog.html`, `how-to-add-borders-to-photos-on-iphone.html`, `how-to-prepare-instagram-carousel-photos-on-iphone.html`. Font Awesome is loaded from a CDN.
- **Assets live under `i/`** (`screenshots/`, `examples/`, `changelog/`, `how-to/`, plus `favicon.png`, `icon.png`, `og-image.png`, `demo.mp4`). Reference them with root-relative paths like `i/screenshots/1.jpeg`.
- **SEO surface** — `sitemap.xml`, `robots.txt`, `llms.txt`, and per-page `<meta>` / Open Graph / canonical tags. When adding or renaming a page, update `sitemap.xml` (including `lastmod`) and add any cross-links from the footers of existing pages.
- **Smart App Banner** is wired via `<meta name="apple-itunes-app" content="app-id=6451375021">` on `index.html`; keep the App Store id in sync if it ever changes.

## Conventions

- Keep the tone and visual style consistent with `index.html` — the dark theme, the green accent, and the existing section structure are the reference.
- Don't introduce a build step, framework, or package manager for small additions; prefer inline CSS/JS to match the rest of the site.
