# Junyu25.github.io

Personal website of Junyu Chen — bioinformatics, microbiome research, and a bilingual (English/中文) blog.

Built with [Jekyll](https://jekyllrb.com/) and the [al-folio](https://github.com/alshedivat/al-folio) academic theme, and deployed automatically to GitHub Pages with GitHub Actions.

## How it works

You write Markdown; GitHub Actions builds and deploys the site. You never have to build locally.

- **Blog posts** live in `_posts/` as `YYYY-MM-DD-title.md`.
- **Publications** are generated from `_bibliography/papers.bib`.
- **CV** is generated from `_data/cv.yml`.
- **Projects** live in `_projects/`.
- **Site config** (name, links, navbar, features) is in `_config.yml`; social links are in `_data/socials.yml`.

## Adding a blog post

Create a file in `_posts/`, for example `_posts/2026-06-12-my-post.md`:

```markdown
---
layout: post
title: "My Post Title"
date: 2026-06-12
description: "One-line summary"
tags: BioInfo Python
categories: Note
---

Write your content in Markdown. Images go in `assets/img/` and are referenced as
`/assets/img/your-image.png`.
```

Commit and push to the default branch — the **Deploy site** workflow
(`.github/workflows/deploy.yml`) builds the site and publishes it.

## Deployment

On every push to the default branch, GitHub Actions builds the site and pushes the
rendered output to the `gh-pages` branch. GitHub Pages then serves that branch.

**One-time setup:** in the repository **Settings → Pages**, set
*Build and deployment → Source* to **Deploy from a branch**, branch **`gh-pages`** (root).

## Local preview (optional)

```bash
bundle install
npm ci
bundle exec jekyll serve
```

Rendering Jupyter notebooks and responsive images locally also needs `nbconvert`
and ImageMagick (`convert`); the GitHub Actions workflow installs these automatically.
