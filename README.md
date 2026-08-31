# 🌐 suresh.dev

[![GitHub Workflow Status][gha_badge]][gha_url]

Home for https://suresh.dev, built with [Zola](https://www.getzola.org/)

## Dev

```bash
$ brew install zola

$ zola serve   # preview at http://localhost:1111 with live reload
$ zola check   # validate internal links & assets
$ zola build   # build the static site into public/
```

## New Post

Create a new file under `content/blog/`, e.g. `content/blog/my-post.md`:

```markdown
+++
title = "My Post"
date = 2026-01-01
+++

Post content goes here.
```

`zola serve` picks it up automatically.

## Deployment

Pushes to `main` are built with Zola and deployed to GitHub Pages by [GitHub Actions][gha_url].

[gha_url]: https://github.com/sureshg/sureshg.github.io/actions/workflows/deploy.yml
[gha_badge]: https://img.shields.io/github/actions/workflow/status/sureshg/sureshg.github.io/deploy.yml?branch=main&color=green&label=Build&logo=Github-Actions&logoColor=green
