# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website built with Jekyll and GitHub Pages. The site follows a portfolio-first design, showcasing projects, experience, and contact information.

## Build Commands

```bash
# Install dependencies
bundle install

# Run local dev server (auto-rebuilds on changes)
bundle exec jekyll serve

# Build static site to _site/
bundle exec jekyll build

# Faster rebuilds during development
bundle exec jekyll serve --incremental
```

**System requirement:** Ruby 3.4+ via Homebrew (system Ruby 2.6 is incompatible).

## Architecture

### Content Model (Data-Driven)

All content lives in `_data/*.yml` files:
- `profile.yml` - Name, title, value prop, social links
- `projects.yml` - Projects array (use `featured: true` to display)
- `experience.yml` - Jobs array with achievements
- `education.yml` - Education entries

Update YAML → templates automatically render changes.

### Template Structure

```
_layouts/
  └── home.html          # Assembles all sections
_includes/
  ├── hero.html          # Hero section
  ├── projects.html      # Projects grid
  ├── project_card.html  # Individual project
  ├── experience.html    # Experience timeline
  └── ...                # One include per section
```

### Design System

All design tokens in `_sass/_tokens.scss`:
- Colors, spacing, typography, breakpoints, shadows
- CSS custom properties for asset paths (`--hero-bg-image`, etc.)

SCSS partials imported in order via `assets/css/main.scss`:
1. `_tokens.scss` - Design variables
2. `_base.scss` - Reset, typography, globals
3. `_layout.scss` - Container, sections, grids
4. `_components.scss` - Buttons, cards, tags

### Key Conventions

- **Mobile-first breakpoints:** Base styles for mobile, `@media (min-width: $breakpoint-*)` for larger screens
- **No JavaScript frameworks:** Vanilla JS only for smooth scroll (progressive enhancement)
- **Featured flag pattern:** Only items with `featured: true` display in lists
- **BEM-like naming:** `.section--hero`, `.hero__content`, etc.
- **Inline SVG icons:** Social links use inline SVG for styling and performance

## GitHub Pages Compatibility

**Critical:** GitHub Pages uses older Sass that doesn't support `@use`. Always use `@import` instead.

## Common Tasks

**Add a project:**
```yaml
# _data/projects.yml
- title: Project Name
  description: One-line description
  tags: [Python, ML]
  repo_url: https://github.com/...
  featured: true
```

**Add a job:**
```yaml
# _data/experience.yml - add to jobs array
- company: Company Name
  role: Senior Engineer
  dates: 2022 – Present
  bullets:
    - Achievement with impact
```

**Change accent color:** Update `$color-accent` in `_sass/_tokens.scss`

**Add images:** Place in `assets/images/[category]/`, update CSS custom properties in `_tokens.scss`
