# ❯ terminal velocity_

I write about product, technology, leadership, and whatever is currently eating my brain. Occasionally about books. The goal was a minimal setup — write only in [Obsidian](https://obsidian.md), drop the finished Markdown file into the repo, and let everything else take care of itself. Published at [terminalvelocity.blog](https://terminalvelocity.blog).

## Stack

- **[Hugo](https://gohugo.io/)** — static site generator
- **[Bear Cub](https://github.com/clente/hugo-bearcub)** — minimal Hugo theme
- **[Cloudflare Pages](https://pages.cloudflare.com/)** — build, hosting, and deployment on every push to `main`
- **[Git](https://git-scm.com/) / GitHub** — version control and source of truth

## How it works

Posts are written in [Obsidian](https://obsidian.md) and dropped into `content/posts/` with minimal frontmatter. A push to `main` triggers Cloudflare Pages to rebuild and deploy. Nothing runs locally.

```
content/
└── posts/
    └── my-post.md
```

Frontmatter I use:

```yaml
---
title: Post title
date: 2026-05-04
---
```

That's it. If you're looking for a similar setup, the [Bear Cub README](https://github.com/clente/hugo-bearcub) is a good starting point.

## Contact

Find me on [Bluesky](https://bsky.app/profile/matoautomato.bsky.social).
