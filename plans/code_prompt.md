# Portfolio-First Jekyll Site: Implementation Plan

This document defines the implementation plan for upgrading `torenunez.github.io` into a portfolio-first personal website.

---

## Objective

Transform the site into a portfolio-first personal website that:
- Communicates engineering maturity, technical competence, and long-term reliability in under 10 seconds
- Makes it easy for recruiters and peers to understand who you are, what you build, and why you're credible
- Remains simple to deploy (Jekyll + GitHub Pages) and easy to maintain
- Is structured so new content can be added without redesigning the layout
- Supports future design assets (images, textures, icons) via plug-and-play slots

---

## Brand Context

### Primary Audience
- Hiring managers
- Engineering leaders
- Technical recruiters
- Developers reviewing code and projects

### Brand Goals
- Technical credibility and clarity
- Professional confidence without corporate stiffness
- Modern, intentional taste
- Serious engineering competence

### Core Brand Keywords
**futuristic, minimal, balanced, sustainable, data-driven**

### Visual DNA (from reference imagery)
The personal brand draws from Mesoamerican geometric patterns:
- Step-fret (grecas) motifs
- Radial symmetry
- High contrast (light/dark)
- Angular, precise shapes
- Textured stone/wood materiality

These patterns will inform future design assets. The MVP uses a clean, neutral foundation that these assets can layer onto.

---

## Maintenance Philosophy

### Primary: Easy deployment and maintenance via Claude Code
- All changes should be achievable by describing what you want in plain English
- File structure is flat and predictable — no hunting for where things live
- Content lives in YAML (like Django fixtures) — edit data, not templates
- CSS uses variables — change once, applies everywhere

### Secondary: Code you can understand
- All code will be commented explaining *why*, not just *what*
- No JavaScript frameworks — vanilla JS only for minimal interactivity
- SCSS is just CSS with variables and nesting — nothing exotic

---

## Design Principles

- **Clarity over decoration** — every element earns its place
- **Systemized aesthetic** — consistent grids, predictable spacing, strong hierarchy
- **Futuristic but restrained** — subtle geometric cues, neutral colors, timeless typography
- **Light mode** — light backgrounds with dark text
- **External linking strategy** — projects link to GitHub repos, experience links to LinkedIn
- **Asset-ready** — CSS and HTML structured for easy asset integration later

---

## MVP Sections (4 total)

```
Homepage (single page, anchored)
├── Hero (#hero)
│   └── Name, role, value prop, "View Projects" CTA
├── Projects (#projects)
│   └── 3-4 featured cards → GitHub repos
├── Experience (#experience)
│   └── CV timeline → LinkedIn CTA at bottom
└── Contact (#contact)
    └── "Get in Touch" with email + LinkedIn + GitHub
```

**Deferred for later:** About, Skills, Blog

---

## Architecture (Built to Extend)

### Content extensibility
- All content lives in `_data/*.yml` — add projects/jobs by editing YAML only
- Each section is a standalone `_includes/*.html` — drop new ones in, reference in layout

### Design extensibility
- Tokens in `_tokens.scss` — change colors/spacing globally
- Asset paths defined as CSS custom properties — swap images without touching HTML
- Optional asset slots with solid-color fallbacks for MVP

> **Remember:** The MVP ships clean with solid colors. When you're ready with design assets, drop them in and update one line in `_tokens.scss`.

### To add a new section later
1. Create `_data/[section].yml`
2. Create `_includes/[section].html`
3. Add `{% include [section].html %}` to `home.html`

### To add design assets later
1. Drop assets into `assets/images/[category]/`
2. Update CSS custom properties in `_tokens.scss`
3. Assets automatically apply via existing CSS rules

---

## File Structure

```
torenunez.github.io/
├── _config.yml                     # Site metadata (modified)
├── _data/
│   ├── profile.yml                 # Name, title, value prop, links
│   ├── projects.yml                # Array of featured projects
│   └── experience.yml              # Array of jobs/roles
├── _includes/
│   ├── head.html                   # Meta tags, fonts, CSS links
│   ├── nav.html                    # Sticky navigation
│   ├── hero.html                   # Hero section
│   ├── projects.html               # Projects section wrapper
│   ├── project_card.html           # Single project card component
│   ├── experience.html             # Experience section wrapper
│   ├── experience_item.html        # Single timeline entry component
│   ├── contact.html                # Get in Touch section
│   └── footer.html                 # Minimal footer
├── _layouts/
│   ├── default.html                # Base HTML wrapper (modified)
│   └── home.html                   # Assembles sections (new)
├── _sass/
│   ├── _tokens.scss                # Design tokens + asset path variables
│   ├── _base.scss                  # Reset, body styles, typography
│   ├── _layout.scss                # Container, section, grid utilities
│   └── _components.scss            # Cards, buttons, links
├── assets/
│   ├── css/
│   │   └── main.scss               # Imports all partials
│   └── images/                     # Asset slots (empty for MVP)
│       ├── hero/                   # Hero backgrounds
│       ├── backgrounds/            # Section backgrounds, textures
│       ├── icons/                  # Custom icons (SVG)
│       ├── social/                 # OG image, LinkedIn banner
│       └── favicon/                # Favicon set
├── index.html                      # Entry point, uses home layout
└── _posts/                         # Preserved, unlinked for now
```

---

## Design Tokens

### Colors (Light Mode)

```scss
// Core palette
$color-bg: #FAFAFA;
$color-surface: #FFFFFF;
$color-text: #1A1A1A;
$color-text-muted: #6B6B6B;
$color-border: #E5E5E5;
$color-border-strong: #D0D0D0;
$color-accent: #2563EB;
$color-accent-hover: #1D4ED8;
```

### Typography

```scss
// Font stacks
$font-sans: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
$font-mono: 'JetBrains Mono', 'SF Mono', 'Fira Code', monospace;

// Scale
$font-size-xs: 0.75rem;    // 12px - micro labels
$font-size-sm: 0.875rem;   // 14px - small text
$font-size-base: 1rem;     // 16px - body
$font-size-lg: 1.125rem;   // 18px - lead
$font-size-xl: 1.5rem;     // 24px - h3
$font-size-2xl: 2rem;      // 32px - h2
$font-size-3xl: 2.5rem;    // 40px - h1 / hero
$font-size-4xl: 3rem;      // 48px - hero name (desktop)
```

### Spacing (8px base)

```scss
$space-1: 0.25rem;   // 4px
$space-2: 0.5rem;    // 8px
$space-3: 0.75rem;   // 12px
$space-4: 1rem;      // 16px
$space-6: 1.5rem;    // 24px
$space-8: 2rem;      // 32px
$space-12: 3rem;     // 48px
$space-16: 4rem;     // 64px
$space-24: 6rem;     // 96px
```

### Layout

```scss
$container-max: 1120px;
$container-narrow: 720px;
$radius-sm: 4px;
$radius-md: 8px;
```

### Asset Paths (CSS Custom Properties)

These are defined as CSS custom properties so assets can be swapped without recompiling SCSS:

```scss
:root {
  // Hero
  --hero-bg-image: none;                    // Future: url('/assets/images/hero/hero.webp')
  --hero-bg-color: #{$color-bg};

  // Section backgrounds
  --section-projects-bg: #{$color-bg};
  --section-experience-bg: #{$color-surface};
  --section-contact-bg: #{$color-bg};

  // Textures (optional overlays)
  --texture-subtle: none;                   // Future: url('/assets/images/backgrounds/texture.webp')
  --texture-opacity: 0.03;

  // Decorative
  --divider-pattern: none;                  // Future: url('/assets/images/backgrounds/divider.svg')
}
```

---

## Data Schemas

### `_data/profile.yml`

```yaml
name: Salvador J. Nunez
title: "[Your Role]"
value_prop: "[One sentence: what you do + why it matters]"
cta_text: View Projects
cta_link: "#projects"
links:
  github: https://github.com/torenunez
  linkedin: https://linkedin.com/in/[handle]
  email: your@email.com
```

### `_data/projects.yml`

```yaml
- title: Project Name
  description: One-line description of what it does and why it matters
  tags:
    - Python
    - ML
  repo_url: https://github.com/torenunez/repo-name
  featured: true

- title: Another Project
  description: Brief description
  tags:
    - SQL
    - Data
  repo_url: https://github.com/torenunez/another-repo
  featured: true
```

### `_data/experience.yml`

```yaml
- company: Company Name
  role: Senior Engineer
  dates: 2022 – Present
  bullets:
    - Led initiative that achieved X outcome
    - Built system handling Y scale

- company: Previous Company
  role: Engineer
  dates: 2019 – 2022
  bullets:
    - Accomplishment with measurable impact
    - Technical contribution

linkedin_cta: View full history on LinkedIn
linkedin_url: https://linkedin.com/in/[handle]
```

---

## Visual Language

### Section Headers

Monospace micro-labels for futuristic feel:

```html
<span class="section-label">01</span>
<h2 class="section-title">Projects</h2>
```

Renders as: `01` (muted) + `Projects` (bold)

### Cards

- White background (`$color-surface`) on page background (`$color-bg`)
- 1px border (`$color-border`)
- Subtle shadow on hover
- Minimal radius (4-8px)
- Ready for optional background images via `--card-bg-image`

### Interactions

- Hover: `translateY(-2px)` + shadow increase
- Links: accent color, underline on hover
- Focus: visible outline for accessibility (3px solid accent)

### JavaScript (Minimal)

No frameworks. Vanilla JS only for:
- Smooth scroll to anchor links (progressive enhancement — works without JS)
- Mobile nav toggle (if needed)

That's it. All animations are CSS-only. If JS fails to load, site still works perfectly.

### Social Icons (GitHub & LinkedIn)

Clean, professional approach using inline SVGs:

**Why inline SVG?**
- Crisp at any size (vector, not raster)
- No external requests (faster load)
- Styleable with CSS (color matches your theme)
- No icon library overhead

**Appearance:**
- Monochrome (uses `$color-text-muted`, not brand colors)
- 24px default size
- Hover: transitions to `$color-accent`
- Consistent with overall minimal aesthetic

**Placement:**
- Hero section: small, next to or below CTAs
- Contact section: prominent, with labels
- Nav (optional): icon-only in header

**Implementation:**
```html
<!-- GitHub icon — inline SVG for crisp rendering and CSS styling -->
<a href="{{ site.data.profile.links.github }}" class="social-link" aria-label="GitHub">
  <svg>...</svg>
</a>
```

```scss
.social-link {
  color: $color-text-muted;
  transition: color 0.2s ease;

  &:hover {
    color: $color-accent;
  }
}
```

**Icons included:**
- GitHub (Octicon or Simple Icons version)
- LinkedIn
- Email (envelope icon for mailto: links)

### Responsive Breakpoints

```scss
$breakpoint-sm: 640px;
$breakpoint-md: 768px;
$breakpoint-lg: 1024px;
$breakpoint-xl: 1280px;
```

Mobile-first approach: base styles for mobile, `@media (min-width: $breakpoint-*)` for larger.

---

## Execution Order

Each phase ends with a local preview so you can test and give feedback before proceeding.

**Local preview command:** `bundle exec jekyll serve`
**View at:** `http://localhost:4000`

---

### Phase 1: Setup ✅
1. ✅ Create branch: `upgrade-portfolio-system`
2. ✅ Verify existing site builds successfully
3. ✅ Create empty asset directories

**Test:** Run `bundle exec jekyll serve` — existing site should still work unchanged.
**You'll see:** The old blog-style site (confirms nothing is broken).

**Note:** Required Ruby 4.0+ via Homebrew (`brew install ruby`) since system Ruby 2.6 was incompatible with modern Jekyll.

---

### Phase 2: Design System ✅

**Issue found:** GitHub Pages uses older Sass that doesn't support `@use` directive. Fixed by using `@import` instead in all SCSS files.
4. ✅ Create `_sass/_tokens.scss` (colors, type, spacing, asset variables)
5. ✅ Create `_sass/_base.scss` (reset, typography, links)
6. ✅ Create `_sass/_layout.scss` (container, section, grid)
7. ✅ Create `_sass/_components.scss` (cards, buttons, tags)
8. ✅ Update `assets/css/main.scss` to import partials

**Test:** Site builds without errors. Old site still displays (new CSS exists but isn't applied yet).
**You'll see:** Same old site — this phase is foundation work.

---

### Phase 3: Data ✅
9. ✅ Create `_data/profile.yml` (with placeholders)
10. ✅ Create `_data/projects.yml` (with placeholders)
11. ✅ Create `_data/experience.yml` (with placeholders)

**Test:** Site builds without errors.
**You'll see:** Still the old site — data files exist but aren't used yet.

---

### Phase 4: Includes ✅
12. ✅ Create `_includes/head.html` (meta, fonts, CSS)
13. ✅ Create `_includes/nav.html`
14. ✅ Create `_includes/hero.html`
15. ✅ Create `_includes/projects.html` + `_includes/project_card.html`
16. ✅ Create `_includes/experience.html` + `_includes/experience_item.html`
17. ✅ Create `_includes/contact.html`
18. ✅ Create `_includes/footer.html`

**Test:** Site builds without errors.
**You'll see:** Still the old site — includes exist but aren't assembled yet.

---

### Phase 5: Assembly (The Big Reveal) ✅
19. ✅ Create `_layouts/home.html`
20. ✅ Update `_layouts/default.html`
21. ✅ Update `index.html` to use home layout
22. ✅ Update `_config.yml` with new metadata

**Test:** Run `bundle exec jekyll serve` and refresh browser.
**You'll see:** The new portfolio site with all 4 sections (Hero, Projects, Experience, Contact) using placeholder content.

**This is the main feedback point.** Review:
- Overall layout and spacing
- Section order and flow
- Typography and colors
- Responsive behavior (resize browser or use phone)

---

### Phase 6: QA & Polish
23. Incorporate your feedback from Phase 5
24. Test responsive behavior (mobile, tablet, desktop)
25. Verify all links work
26. Check accessibility (contrast, focus states)
27. Final build verification

**Test:** Full review across devices.
**You'll see:** Polished site ready for real content.

---

### Phase 7: Your Content
28. Replace placeholder data in `_data/*.yml` with your real info

**Test:** Refresh browser to see your actual content.
**You'll see:** Your finished portfolio.

---

## Code Documentation Standards

All generated code will include comments explaining *why*, not just *what*:

### SCSS files
```scss
// ==============================================
// TOKENS: Design system variables
// Single source of truth — change here, applies everywhere
// ==============================================

// Why this blue? Passes WCAG AA contrast on white, feels professional not playful
$color-accent: #2563EB;

// Why 62.5%? Sets 1rem = 10px for easier mental math (16px = 1.6rem)
html { font-size: 62.5%; }
```

### HTML/Liquid templates
```html
<!--
  hero.html — First thing visitors see
  Why a separate include? Keeps home.html clean, makes hero reusable if needed
-->
<section class="hero">
  <!-- Why id="hero"? Creates defined anchor for nav links to scroll to -->
  <h1>{{ site.data.profile.name }}</h1>
</section>
```

### Non-obvious decisions get explained
```scss
// Why translateY instead of margin? GPU-accelerated, won't cause layout reflow
.card:hover { transform: translateY(-2px); }
```

---

## Acceptance Criteria

- [ ] Hero visible immediately with name, role, value prop, CTA
- [ ] Projects section shows 3-4 cards linking to GitHub repos
- [ ] Experience section shows CV timeline with LinkedIn CTA
- [ ] Contact section has email + social links
- [ ] Light, clean aesthetic with no visual clutter
- [ ] Responsive on mobile, tablet, desktop
- [ ] Adding new content requires only YAML edits
- [ ] Site builds and deploys via GitHub Pages
- [ ] Asset directories exist and are ready for future images

---

## Common Maintenance Tasks (Claude Code Prompts)

Copy-paste these prompts to Claude Code for common updates:

### Add a new project
> "Add a new project to my portfolio: [title], [one-line description], tags: [X, Y, Z], repo: [GitHub URL]"

### Update experience
> "Add a new job to my experience: [Company], [Role], [Dates], bullets: [achievement 1], [achievement 2]"

### Change accent color
> "Change the accent color to [#hexcode]"

### Update contact info
> "Update my email to [new@email.com]"

### Add a new section
> "Add an About section to my portfolio with these focus areas: [X, Y, Z]"

### Preview locally
> "Run the Jekyll dev server so I can preview changes"

### Deploy
> "Commit these changes and push to deploy"

---

## Adding Design Assets Later

When design assets are ready, follow this process:

### Hero Background
1. Add `hero.webp` (2560x1440) to `assets/images/hero/`
2. Update `_tokens.scss`:
   ```scss
   --hero-bg-image: url('/assets/images/hero/hero.webp');
   ```

### Section Textures
1. Add `texture.webp` (tileable) to `assets/images/backgrounds/`
2. Update `_tokens.scss`:
   ```scss
   --texture-subtle: url('/assets/images/backgrounds/texture.webp');
   ```

### Favicon
1. Add files to `assets/images/favicon/`:
   - `favicon.svg`
   - `favicon-32.png`
   - `apple-touch-icon-180.png`
2. Update `_includes/head.html` to reference them

### Social/OG Image
1. Add `og.png` (1200x630) to `assets/images/social/`
2. Update `_includes/head.html` meta tags

### Asset Manifest

Track assets in `assets/images/MANIFEST.md`:

```markdown
| File | Dimensions | Format | Usage |
|------|------------|--------|-------|
| hero/hero.webp | 2560x1440 | WEBP | Hero background |
| backgrounds/texture.webp | 512x512 | WEBP | Tileable texture overlay |
| favicon/favicon.svg | - | SVG | Browser favicon |
| social/og.png | 1200x630 | PNG | Open Graph image |
```

---

## Future Extensions (Post-MVP)

### Sections
- About section with focus areas
- Skills section with grouped tags
- Blog integration at /blog/

### Features
- Dark mode toggle
- Project filtering by tag
- Resume PDF download
- Animated geometric accents (CSS-only)

### Design Assets
- Hero imagery incorporating Mesoamerican geometric patterns
- Custom icon set (step-fret inspired)
- Textured section dividers
- Subtle grid/pattern overlays
