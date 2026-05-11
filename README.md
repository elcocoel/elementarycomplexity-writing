# Elementary Complexity — Writing

The public source for all writing published at [elementarycomplexity.com/writing](https://elementarycomplexity.com/writing).

Articles, think pieces, research notes, and governance proposal supplements live here as plain Markdown. The website is a derivative of these files; the files are sovereign.

## Why this repo exists

- **Canonical URLs for ideas.** A piece at `elementarycomplexity.com/writing/<slug>` is the public, durable address. The Markdown source in this repo is the version that survives any platform.
- **Forkable, citable, mirror-able.** Clone it. Fork it. PR a typo. Quote a paragraph with a permalink to a specific line.
- **Mirrored on-chain.** Pieces also get published to a [Simplepage](https://simplepage.eth.link) for ENS / IPFS provenance.
- **Plain markdown.** No proprietary CMS, no walled garden, no algorithmic feed. At build time, the `elementarycomplexity.com` site pulls the `posts/` folder from this repo, compiles each `.md` file through a pipeline called **Scriptorium** (part of the private site codebase), and outputs a fully rendered article page. Push to `main` here → site rebuilds within ~60 seconds.

## Structure

```
posts/
  YYYY-MM-DD-slug.md      # one article per file
media/
  <any image, asset, or file referenced by a post>
```

## Frontmatter contract

Every post starts with a YAML block:

```yaml
---
title: The Loyalty-Gated Redemption Protocol
slug: loyalty-gated-redemption           # optional; defaults to filename minus the YYYY-MM-DD- prefix
date: 2026-05-15                         # ISO date; the canonical publication day
excerpt: A counter-proposal to GIP-150.  # 1–2 sentence summary for the index card + RSS
cover: ./media/lgrp-cover.png            # optional hero image (relative path, resolved at build time)
ogImage: ./media/lgrp-og.png             # optional OG image override
tags: [governance, gnosis, zk-proofs]    # free-form, lowercase
pinned: false                            # if true, floats to the top of /writing
status: published                        # draft | scheduled | published
publishedAt: 2026-05-15T10:00:00Z        # optional explicit timestamp; defaults to `date`
simplepage: https://writing.eth.link/loyalty-gated-redemption   # optional "also at" link
---
```

## Renderer capabilities

The Scriptorium engine renders:

- CommonMark + GitHub Flavored Markdown (tables, footnotes, task lists, strikethrough, autolinks)
- GFM Alerts (`> [!NOTE]`, `> [!WARNING]`, etc.)
- Math (`$inline$` and `$$block$$` via KaTeX)
- Syntax-highlighted code blocks (Shiki, server-rendered)
- Mermaid diagrams (themed)
- Directive blocks for structured embeds:
  - `:::figure{src="..." caption="..." bleed="full"}` — figures with captions, optional full-bleed
  - `:::callout{type="note|tip|warning|danger|quote"}` — themed asides
  - `:::aside` — Tufte-style sidenotes
- Iframe passthrough with a sanitized allowlist (YouTube, X, Loom, Spotify, NotebookLM, Vimeo, Mirror, Paragraph, Figma, gists, CodePen, CodeSandbox). Paste any source's `<iframe>` share code directly.
- Auto-embed: a bare URL alone on its own line becomes an embed (no shortcode needed).

## How to publish

1. Add or edit a Markdown file in `posts/`.
2. Set `status: published` in frontmatter.
3. Commit + push to `main`.
4. The website rebuilds and the piece is live within ~30–60 seconds.
5. (Optional) Mirror the same `.md` to Simplepage for ENS / IPFS provenance.

## License

Content is published under [CC BY 4.0](./LICENSE). Quote freely, attribute, link back.

## Citing a piece

```
Cocchia, E. (YYYY). "<title>." Elementary Complexity.
https://elementarycomplexity.com/writing/<slug>
```
