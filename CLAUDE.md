# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the NA-MIC ProjectWeek repository - a Jekyll-based static site hosting documentation for semi-annual medical imaging research hackathons. Events are organized in directories like `PW44_2026_GranCanaria/` containing project pages, photos, and event details.

## Build and Development Commands

```bash
# Install dependencies (requires Ruby 3.3+)
bundle install

# Run local development server
jekyll serve
# or
bundle exec jekyll serve

# Build site (outputs to _site/)
jekyll build
```

The site is automatically deployed via Netlify when changes are merged to master.

## Architecture

### Directory Structure
- `PW##_YEAR_Location/` - Event directories (PW26 through PW44+)
  - `Projects/` - Individual project pages with YAML front matter
  - `Projects/Template/README.md.j2` - Jinja2 template for auto-generated pages
- `_layouts/` - Jekyll page layouts (e.g., `pw44-project.html`)
- `_includes/` - Reusable components (`projects.md`, `calendar.md`)
- `.github/workflows/` - GitHub Actions for automated project page creation

### Automated Project Page Creation
When a GitHub issue is created using the project template and labeled `project:create`:
1. `.github/workflows/project-page-pull-request.yml` extracts issue form data
2. Renders `Projects/Template/README.md.j2` with Jinja2
3. Creates a PR with the new project page

### Project Page Format
Project pages use YAML front matter:
```yaml
layout: pw44-project
permalink: /:path/
project_title: My Project
category: Segmentation  # Options: DICOM, VR/AR, IGT, Segmentation, Quantification, Cloud/Web, Infrastructure, Other
key_investigators:
  - name: Firstname Lastname
    affiliation: Institution
    country: Country
```

## Key Files
- `_config.yml` - Jekyll configuration, plugins, and exclusions
- `Gemfile` - Ruby dependencies (github-pages, jemoji)
- `netlify.toml` - Netlify build settings
- `MAINTAINERS.md` - Reference commits for setting up new events
- `.github/ISSUE_TEMPLATE/project.yml` - Project creation form schema

## Conventions
- No spaces or special characters in folder/file names
- Key investigators format: `- Firstname Lastname (Affiliation, Country)`
- Videos need `<video>` tags for GitHub uploads, `<iframe>` for YouTube embeds
- Don't reuse project templates from previous years - use current event's template
