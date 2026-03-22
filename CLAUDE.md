# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

Personal GitHub Pages site for Yulei Liu (`ausmartway.github.io`) — a DevSecOps/Cloud Infrastructure portfolio. Uses Jekyll with the **minima** theme (dark skin).

## Development Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve --livereload

# Build only
bundle exec jekyll build

# Clean build artifacts
bundle exec jekyll clean
```

The site also works without Jekyll for the main page — `index.html` is a standalone HTML file and can be opened directly in a browser or served with:

```bash
python3 -m http.server 8080
```

## Architecture

### Two-tier content model

This repo has a deliberate split:

1. **`index.html`** — Standalone HTML (bypasses Jekyll entirely). Self-contained with inline `<style>` and `<script>`. Jekyll does not process it. This is the main landing page and the primary file for design work.

2. **Jekyll pages** (`about.md`, `projects.md`, `_pages/cv.md`, `_pages/aws-s3-security.md`) — Processed by Jekyll using the minima theme layout. These are separate from `index.html` and use Liquid templating.

3. **`_projects/` collection** — Individual project markdown files (currently `tfc-config-as-code.md`, `vault-config-as-code.md`). Referenced by `projects.md` via Liquid `site.projects` iteration.

### Key constraint

`index.html` and the Jekyll pages are **independent systems** — changes to nav or styling in `index.html` do not affect the Jekyll pages and vice versa.

### Configuration

- `_config.yml` — Jekyll config, theme (`minima`), social links, plugins (`jekyll-feed`, `jekyll-sitemap`, `jekyll-seo-tag`), and the `projects` collection definition
- Theme skin: `minima.skin: dark`

### Design specs and plans

Implementation specs and plans live in `docs/superpowers/specs/` and `docs/superpowers/plans/`. The `.superpowers/` directory (brainstorm session files) is gitignored.
