# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static website built with [Zola](https://www.getzola.org/), a fast static site generator written in Rust. The site uses the "no style, please!" theme (customized as "default"), which is a minimalist, nearly no-CSS theme focused on speed and readability.

## Development Commands

### Running the Site Locally
```bash
zola serve
```
The site will be available at http://localhost:1111 with live reloading.

### Building the Site
```bash
zola build
```
Always run this after making changes to verify the site builds successfully.

### Checking the Build
```bash
zola check
```
Validates configuration and content without building.

## Site Architecture

### Directory Structure

- **content/**: Markdown content files organized by sections
  - `_index.md`: Homepage content
  - Subdirectories like `essays/` and `2026-year-resolution/` for organized content
  - Each content file has YAML frontmatter with metadata (title, date, description, taxonomies)

- **templates/**: Custom Zola templates (in the root for overrides)
- **themes/default/**: The "no style, please!" theme
  - `templates/`: Theme templates (base.html, page.html, section.html, etc.)
  - `sass/`: SASS stylesheets (compiled automatically when `compile_sass = true`)
  - `static/`: Theme static assets

- **static/**: Root static assets (images, favicon.ico)
  - Files here are served directly at the site root

- **public/**: Generated site output (git-ignored)

### Configuration

`config.toml` contains:
- Base URL (currently set to localhost:1111)
- Taxonomies: tags, categories, contexts
- Theme selection: `theme = "default"`
- Markdown settings (syntax highlighting enabled)
- Extra variables like logo path

### Content Frontmatter

Pages use YAML frontmatter with these common fields:
```yaml
---
title: "Page Title"
date: 2026-01-04
description: "Page description for meta tags"
extra:
    add_toc: true  # Optional: adds table of contents
[taxonomies]
tags = ["tag1", "tag2"]
categories = ["category1"]
contexts = ["context1"]
---
```

### Theme Features

The "no style, please!" theme supports:
- Three default taxonomies: tags, categories, contexts
- Optional page list on homepage (configured via `extra.list_pages`)
- Header/footer navigation links (configured in `extra` section)
- Table of contents per page (`extra.add_toc = true`)
- Two custom shortcodes:
  - `{{ hr(data_content="text") }}`: Horizontal rule with text
  - `{{ iimg(src="...", alt="...") }}`: Invertable images for dark mode
- Twitter card metatags (enabled by default)

### Templates Hierarchy

- `base.html`: Base template with HTML structure
- `index.html`: Homepage template
- `page.html`: Individual page template
- `section.html`: Section listing template
- `taxonomy_list.html` / `taxonomy_single.html`: Taxonomy templates
- Specialized taxonomy templates in `categories/`, `contexts/`, `tags/` subdirectories
