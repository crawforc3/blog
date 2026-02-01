# Blog Project

Personal blog built with [Quartz](https://quartz.jzhao.xyz/), a static site generator for digital gardens.

## Quick Reference

- **Framework:** Quartz v4 (TypeScript, Preact)
- **Node:** v22+ required
- **Site URL:** https://crawforc3.github.io/blog

## Commands

```bash
npm run docs      # Build and serve locally (http://localhost:8080)
npm run check     # TypeScript check + formatting
npm run format    # Auto-format code
```

## Project Structure

```
content/          # Markdown content (posts, pages)
  index.md        # Homepage
  resume.md       # Resume page (print-friendly)
  images/         # Images for posts
quartz/           # Framework source
  styles/         # SCSS styles (custom.scss for overrides)
  components/     # Preact components
quartz.config.ts  # Site configuration
quartz.layout.ts  # Layout configuration
```

## Adding Content

Create `.md` files in `content/` with frontmatter:

```markdown
---
title: Page Title
tags: [tag1, tag2]
---

Content here...
```

- Links: `[[page-name|Display Text]]` (Obsidian syntax)
- Images: `![alt](images/filename.png)`

## Resume

The resume page (`content/resume.md`) has print-friendly styles. To export as PDF:
1. Navigate to the resume page
2. Use browser print (Ctrl+P / Cmd+P)
3. Save as PDF

## Ignored Directories

These are excluded from the build (see `quartz.config.ts`):
- `private/`, `templates/`, `.obsidian/`, `logseq/`
