# 🐺 fenrir-progress

Source for the **[Fenrir progress log](https://javierspn.github.io/fenrir-progress)** — a public,
running record of the [Fenrir](https://github.com/javierspn/fenrir-agent) experiment: cohort numbers,
learning curves, and screenshots.

Built with GitHub Pages' native Jekyll — **no local build needed**. Push to `main`, the page rebuilds.

## Add a progress entry

Drop a file in `_posts/` named `YYYY-MM-DD-slug.md`:

```markdown
---
layout: post
title: "What happened"
---

Body in Markdown. Reference a screenshot:

<figure class="shot">
  <img src="{{ '/assets/img/my-shot.png' | relative_url }}" alt="...">
  <figcaption>caption</figcaption>
</figure>
```

## Add a screenshot

1. Save the PNG into `assets/img/` (e.g. a Grafana panel export).
2. Reference it as `{{ '/assets/img/NAME.png' | relative_url }}`.
3. The three `PLACEHOLDER-*.png` files are stand-ins — overwrite them with real Grafana exports
   (same names) and the latest post updates automatically.

## Update the headline metrics

Edit the `.metrics` block in `index.md`.

## Layout

- `index.md` — home (hero + metric strip + post list + support).
- `_posts/` — dated entries.
- `_layouts/` — `default.html` (dark hero) + `post.html`.
- `assets/css/style.css` — the dark theme.
- `assets/img/` — screenshots.

Apache-2.0.
