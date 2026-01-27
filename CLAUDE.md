# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Astro blog deployed to Cloudflare Workers. Uses MDX for blog content with type-safe frontmatter via Astro Content Collections.

## Commands

```bash
npm run dev          # Dev server at localhost:4321
npm run build        # Build to ./dist/
npm run preview      # Build and preview with Wrangler
npm run check        # Full check: build + tsc + deploy dry-run
npm run deploy       # Deploy to Cloudflare Workers
npm run cf-typegen   # Generate Cloudflare types (wrangler types)
```

## Architecture

- **Pages** (`src/pages/`): File-based routing. `index.astro`, `about.astro`, `blog/index.astro`, and `blog/[...slug].astro` for dynamic blog routes
- **Content Collections** (`src/content/blog/`): Markdown/MDX posts with schema-validated frontmatter (title, description, pubDate, updatedDate?, heroImage?)
- **Layouts** (`src/layouts/`): `BlogPost.astro` wraps blog post content
- **Components** (`src/components/`): `BaseHead.astro` (SEO/meta), `Header.astro`, `Footer.astro`, `FormattedDate.astro`, `HeaderLink.astro`
- **Constants** (`src/consts.ts`): `SITE_TITLE` and `SITE_DESCRIPTION` used across the site
- **Styles** (`src/styles/global.css`): Global CSS with CSS variables for theming

## Blog Post Frontmatter Schema

```yaml
title: string        # Required
description: string  # Required
pubDate: date        # Required
updatedDate: date    # Optional
heroImage: string    # Optional, path to image
```

## Cloudflare Configuration

- Wrangler config in `wrangler.json`
- Uses `@astrojs/cloudflare` adapter with platform proxy enabled
- Observability logging enabled
- Update `astro.config.mjs` site URL before production deploy
