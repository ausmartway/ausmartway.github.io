# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a GitHub Pages repository using Jekyll with the Cayman theme. It's a personal website hosted at `ausmartway.github.io`.

## Architecture

- **Static Site Generator**: Jekyll (configured via `_config.yml`)
- **Theme**: jekyll-theme-cayman
- **Hosting**: GitHub Pages
- **Content**: Simple HTML pages in the root directory

## Key Files

- `index.html`: Main landing page content
- `_config.yml`: Jekyll configuration and theme settings

## Development Commands

Since this is a Jekyll site using the al-folio theme, use these commands for local development:

```bash
# Install Jekyll and dependencies
bundle install

# Serve the site locally (with live reload)
bundle exec jekyll serve --livereload

# Build the site
bundle exec jekyll build

# Clean build artifacts
bundle exec jekyll clean
```

## Theme Structure

This site uses the **al-folio** theme, a modern Jekyll theme for portfolios:

- **Homepage**: `index.html` - Professional introduction and overview
- **Projects**: `_projects/` - Individual project showcase pages
- **Pages**: `_pages/` - Static pages (about, projects listing, CV)
- **Assets**: `assets/` - Images, CSS, and other static files
- **Configuration**: `_config.yml` - Site settings and theme configuration

## Content Management

### Adding New Projects
1. Create a new markdown file in `_projects/`
2. Use the front matter template from existing projects
3. Include categories and importance ratings for proper sorting

### Updating Professional Information
- Main details: Update `_config.yml`
- Homepage content: Edit `index.html`
- Detailed background: Edit `_pages/about.md`

## Deployment

The site automatically deploys to GitHub Pages when changes are pushed to the master branch. The al-folio theme is configured as a remote theme for GitHub Pages compatibility.