# :herb: My Home Page

[![GitHub Workflow Status][gha_badge]][gha_url]

Home for https://suresh.dev, built with [Zola](https://www.getzola.org/) using the
[apollo](https://github.com/not-matthias/apollo) theme.

## Dev

```bash
brew install zola

zola serve   # preview at http://127.0.0.1:1111 with live reload
zola check   # validate internal links & assets
zola build   # build the static site into public/
```

Requires Zola **0.23.0+** (tested with 0.23.4).

## New Post

Create a new file under `content/blog/`, e.g. `content/blog/my-post.md`:

```markdown
+++
title = "My Post"
date = 2026-01-01
+++

Post content goes here.
```

`zola serve` picks it up automatically, no other wiring needed.

## Deployment

Pushing to `main` triggers [`.github/workflows/deploy.yml`][gha_url], which uses [`getzola/github-pages`][zola_action],
the official action linked from [Zola's own deployment docs][zola_docs], to build the site and upload it as a Pages
artifact, then `actions/deploy-pages` publishes it. No generated files are ever committed back to `main`.

[gha_url]: https://github.com/sureshg/sureshg.github.io/actions/workflows/deploy.yml
[gha_badge]: https://img.shields.io/github/actions/workflow/status/sureshg/sureshg.github.io/deploy.yml?branch=main&color=green&label=Build&logo=Github-Actions&logoColor=green
[zola_action]: https://github.com/getzola/github-pages
[zola_docs]: https://www.getzola.org/documentation/deployment/github-pages/
