# Elementary Complexity — Writing

The public source for all writing published at [elementarycomplexity.com/writing](https://elementarycomplexity.com/writing).

Articles, think pieces, research notes, and governance proposal supplements live here as plain Markdown. The website is a derivative of these files; the files are sovereign.

## Why this repo exists

- **Canonical URLs for ideas.** A piece at `elementarycomplexity.com/writing/<slug>` is the public, durable address. The Markdown source in this repo is the version that survives any platform.
- **Forkable, citable, mirror-able.** Clone it. Fork it. PR a typo. Quote a paragraph with a permalink to a specific line.
- **Mirrored on-chain.** Pieces also get published to a [Simplepage](https://simplepage.eth.link) for ENS / IPFS provenance.
- **Plain markdown.** No proprietary CMS, no walled garden, no algorithmic feed. At build time, the `elementarycomplexity.com` site pulls the `posts/` folder from this repo, compiles each `.md` file through a pipeline called **Scriptorium** (part of the private site codebase), and outputs a fully rendered article page. Production builds read the exact commit pinned in the website repository’s `writing.lock.json`. Publishing is manual; pushing this repository does not rebuild or deploy the website.

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
3. Review the content, commit it, and push this repository’s `main`. Record the full
   40-character writing commit SHA (`git rev-parse HEAD`) and confirm it is on GitHub.
4. In `elementarycomplexitydotcom`, update `writing.lock.json` to that reviewed writing
   commit. Keep `repository` set to `elcocoel/elementarycomplexity-writing`.
5. Validate the website changes, then commit and push its `main`. Both repositories
   must be clean and pushed before deployment.
6. From the website repository, run `node scripts/deploy-site.mjs ec --check`, then
   `node scripts/deploy-site.mjs ec` for the intended production release. The helper
   exports committed website source; Vercel builds it with the pinned writing commit.
7. Confirm Vercel reports Ready and verify the article at
   `https://elementarycomplexity.com/writing/<slug>` and on the writing index.
8. (Optional) Mirror the same `.md` to Simplepage for ENS / IPFS provenance.

The website’s [production strategy](https://github.com/elcocoel/elementarycomplexitydotcom/blob/main/docs/PRODUCTION.md)
is the canonical deployment reference. Production ignores local writing paths and moving
branch overrides; local development can still read drafts from this checkout.

The automatic rebuild workflow has been removed, the `writing-repo-sync` Vercel deploy
hook revoked, and the `VERCEL_DEPLOY_HOOK` GitHub Actions secret removed. Do not restore
push-triggered deploy workflows or deploy hooks. A documentation-only writing commit does
not require changing the website’s content pin or deploying.

## License

Content is published under [CC BY 4.0](./LICENSE). Quote freely, attribute, link back.

## Citing a piece

```
Cocchia, E. (YYYY). "<title>." Elementary Complexity.
https://elementarycomplexity.com/writing/<slug>
```
