# Salvador J. Nunez - Portfolio

Personal portfolio website showcasing projects, experience, and skills. Built with Jekyll and hosted on GitHub Pages.

**Live site:** [torenunez.github.io](https://torenunez.github.io)

## Local Development

**Requirements:** Ruby 3.4+ (via Homebrew recommended; system Ruby 2.6 is incompatible)

```bash
# Install dependencies
bundle install

# Run local dev server (auto-rebuilds on changes)
bundle exec jekyll serve

# Build static site to _site/
bundle exec jekyll build
```

## Project Structure

```
_data/           # Content (YAML files)
  ├── profile.yml      # Name, title, social links
  ├── projects.yml     # Portfolio projects
  ├── experience.yml   # Work history
  └── education.yml    # Education entries

_includes/       # Reusable HTML components
_layouts/        # Page templates
_sass/           # SCSS partials
  ├── _tokens.scss     # Design system variables
  ├── _base.scss       # Reset & typography
  ├── _layout.scss     # Grid & sections
  └── _components.scss # Buttons, cards, tags

assets/          # Static files (CSS, images)
```

## Updating Content

**Add a project:**
```yaml
# _data/projects.yml
- title: Project Name
  description: Brief description
  tags: [Python, ML]
  repo_url: https://github.com/...
  featured: true  # Set to display on site
```

**Add work experience:**
```yaml
# _data/experience.yml - add to jobs array
- company: Company Name
  role: Your Role
  dates: 2022 – Present
  bullets:
    - Achievement with measurable impact
```

## License

MIT License
