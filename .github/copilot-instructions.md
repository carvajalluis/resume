# Resume Generator - AI Agent Instructions

## Project Overview

This is a **Jekyll-based resume site** that renders markdown CVs to HTML/PDF using CSS. Currently deployed on GitHub Pages at `username.github.io/markdown-cv`. The project is forked from [elipapa/markdown-cv](https://github.com/elipapa/markdown-cv).

## Architecture & Key Files

### Content Structure
- **`index.md`**: Primary resume content in markdown format. All professional experience, skills, education, and certifications live here.
- **`cover_letter.md`**: Job-specific cover letters (currently contains an Oracle position example).
- **`_layouts/cv.html`**: Simple HTML wrapper that applies CSS styling to markdown content.
- **`_config.yml`**: Jekyll config defining the style theme (currently `davewhipp`).

### Styling System
- **`media/` directory**: Contains paired CSS files for screen and print rendering
  - `kjhealy-{screen,print}.css`: Original default style (academic CV format)
  - `davewhipp-{screen,print}.css`: Current style with larger fonts, right-aligned dates
  - `clean-{screen,print}.css`: Minimal clean style
- **Style selection**: Change `style: davewhipp` in `_config.yml` to switch themes
- **Print-to-PDF**: Media queries handle PDF export via browser print (⌘+P)

## Development Workflow

### Local Development
```bash
# Install Jekyll (one-time setup)
gem install bundler jekyll

# Start local server
jekyll serve
# or
bundle exec jekyll serve

# View at http://localhost:4000
# Live reload enabled - edit index.md and see changes instantly
```

### Deployment
- **Production branch**: `gh-pages` (this is the live branch, NOT main)
- **Auto-deploy**: Any push to `gh-pages` triggers GitHub Pages rebuild
- **Live URL pattern**: `username.github.io/markdown-cv`

### PDF Generation
Press ⌘+P (Mac) or Ctrl+P (Windows) in browser → Print CSS automatically applies → Save as PDF

## Future Enhancement Plan (AI-Driven Resume Targeting)

The codebase is planned to evolve into a job-focused resume generation system:

### Planned Architecture (see conversation history for full details)
1. **Data-driven structure**: Convert `index.md` to modular YAML files in `_data/`
   - `personal.yml`, `skills.yml`, `experience.yml`, `projects.yml`
   - Each item tagged with categories (frontend, backend, leadership, etc.)

2. **Job profile system**: `_data/profiles/` containing targeted configurations
   - Example: `frontend.yml` prioritizes React/JavaScript, reorders sections
   - AI-generated profiles based on job posting analysis

3. **AI integration** (planned `scripts/ai_resume/`):
   - Job posting analyzer (extract requirements, keywords, ATS terms)
   - Content matcher (score resume items by relevance to job)
   - Profile generator (auto-create optimal resume configuration)
   - Content optimizer (rewrite achievements for keyword/impact)

4. **Multiple resume outputs**: `/frontend/`, `/leadership/`, `/job-123/` URLs
   - Same core data, different filtering/emphasis per job type

### Current State vs Future
- **Now**: Single static resume, manual editing in `index.md`
- **Next**: Data-driven profiles with AI-assisted targeting
- **Key principle**: Keep Jekyll/GitHub Pages foundation, add smart layer on top

## Common Patterns & Conventions

### Resume Content Structure (in `index.md`)
```markdown
# **Name in Bold**
Contact links on separate lines
---
## **SECTION HEADERS IN CAPS**
- Bullet points for lists
- **Bold** for emphasis (roles, companies, keywords)
- Dates aligned right via CSS (no manual formatting needed)
```

### Adding New Styles
1. Create paired files: `media/stylename-screen.css` and `media/stylename-print.css`
2. Update `_config.yml`: `style: stylename`
3. Ensure print CSS handles page breaks, hides navigation, adjusts fonts

### Jekyll Specifics
- **No complex plugins**: Keep it GitHub Pages compatible (default Jekyll plugins only)
- **Markdown engine**: Kramdown (set in `_config.yml`)
- **Layout inheritance**: Single layout (`cv.html`), no complex templating currently

## Key Constraints & Decisions

1. **GitHub Pages limitations**: Can't use arbitrary Jekyll plugins, must stay in allowed set
2. **CSS print media queries**: Print styling is handled entirely via CSS `@media print`, not separate HTML
3. **Single-page focus**: Resume is one continuous page, not multi-page site (for now)
4. **Branch strategy**: `gh-pages` is production branch (unconventional but required by GitHub Pages setup)

## When Adding AI Features

Follow the architectural plan from the conversation:
- Start with data extraction from `index.md` to YAML
- Use Jekyll's `site.data` for content access
- Add Liquid templating logic for filtering (e.g., `{% if page.profile contains 'frontend' %}`)
- Create Python scripts in `scripts/` for AI integration (OpenAI, Anthropic, or Ollama)
- Store analyzed jobs in `_data/jobs/`, generated profiles in `_data/profiles/`
- Maintain backward compatibility: default profile = current `index.md` content

## Testing Changes

1. **Local preview**: Always test with `jekyll serve` before pushing
2. **Print test**: Check PDF output with browser print (CSS media queries must work)
3. **Style switching**: Test all themes in `_config.yml` still render correctly
4. **Mobile check**: Responsive CSS should work on small screens (screen.css files handle this)

## File Modification Cheat Sheet

- **Update resume content**: Edit `index.md`
- **Change visual theme**: Modify `style:` in `_config.yml`
- **Tweak styling**: Edit appropriate CSS in `media/` (remember screen + print pair)
- **Add new page**: Create markdown file with `layout: cv` front matter (not used currently)
- **Deploy**: Push to `gh-pages` branch

---

*Last updated based on codebase analysis and planned enhancements discussion (October 2025)*
