# Prompt Stack

**Engineering knowledge through prompts**

Portfolio site showcasing AI-assisted development projects, technical guides, and insights on the shift from syntax to systems.

🌐 **Live Site**: [prompt-stack.github.io](https://prompt-stack.github.io)

## What This Is

A Jekyll-powered portfolio site documenting:
- **Guides** - Technical deep-dives on Claude, AI-assisted development, and engineering
- **Projects** - Production-ready applications (Content Engine, Content Stack, etc.)
- **Essays** - Philosophy and analysis on AI, accessibility, and systems thinking

## Tech Stack

- **Static Site Generator**: Jekyll
- **Hosting**: GitHub Pages
- **Design**: Custom CSS with dark mode support
- **Collections**: Guides, Essays, Projects

## Local Development

```bash
# Install dependencies
bundle install

# Run local server
bundle exec jekyll serve

# View at http://localhost:4000
```

## Site Structure

```
prompt-stack.github.io/
├── _config.yml          # Jekyll configuration
├── _layouts/            # Custom layouts
│   ├── default.html    # Base layout
│   ├── guide.html      # Guide layout
│   ├── essay.html      # Essay layout
│   └── project.html    # Project layout
├── _guides/             # Guide collection
├── _essays/             # Essay collection
├── _projects/           # Project collection
├── assets/css/          # Custom CSS
├── index.md             # Homepage
├── guides.md            # Guides listing
├── projects.md          # Projects listing
└── about.md             # About page
```

## Adding Content

### New Guide

Create a file in `_guides/` with frontmatter:

```markdown
---
title: "Your Guide Title"
date: 2025-10-18
summary: "Brief description"
tags: ["tag1", "tag2"]
---

# Content here
```

### New Project

Create a file in `_projects/` with frontmatter:

```markdown
---
title: "Project Name"
summary: "Brief description"
repo: "https://github.com/user/repo"
demo: "https://demo.url"
---

# Content here
```

## Design Philosophy

- **Clean & Minimal** - Focus on content, not chrome
- **Readable** - Optimized line length and spacing
- **Dark Mode** - Automatic based on system preference
- **Responsive** - Mobile-first design
- **Fast** - Static site, no JavaScript required

## Projects Featured

- [Content Engine](https://github.com/prompt-stack/content-engine) - AI content processing platform
- [Content Stack](https://github.com/prompt-stack/content-stack) - Media processing with strict architecture
- [Prompt Stack Lite](https://github.com/prompt-stack/prompt-stack-lite) - AI development starter

## License

MIT License - see LICENSE.md

---

**Built with AI-assisted development.** The code is real, the deployments work, and the insights are actionable.
