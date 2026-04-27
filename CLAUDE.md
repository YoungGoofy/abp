# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-page static HTML website for ABP (Архитектор бизнес-проектов), a Russian-language business architecture consulting landing page. The entire site lives in one self-contained file.

## Project Structure

- `abp-site.html` — Single file containing all markup, CSS, and JavaScript (~1184 lines). No external assets except Google Fonts loaded via CDN.

## Running / Previewing

No build step or package manager. To preview:

```bash
# Option 1: open directly in browser
open abp-site.html

# Option 2: serve via any static server
npx serve .          # or python3 -m http.server 8000
```

## Architecture

The file is organized top-to-bottom as:

1. **`<head>`** — Google Fonts preload, inline `<style>` with CSS custom properties, global resets, and all component styles
2. **`<body>`** — Page sections in order:
   - Fixed `nav` with logo, links, and CTA
   - `section#hero` — Hero with monogram SVG, stats, dual CTAs
   - `section#pain` — Problem statement with numbered pain points
   - `section#solution` — Responsibility zone cards
   - `section#experience` — Track record with timeline items
   - `section#difference` — Comparison grid
   - `section#process` — 4-step process cards
   - `section#formats` — Engagement format cards
   - `section#cta` — Final call-to-action
   - `<footer>`
3. **`<script>`** (end of body) — Three behaviors:
   - Custom cursor: `cursorDot` + `cursorRing` with `requestAnimationFrame`-smoothed trailing
   - Scroll reveal: `IntersectionObserver` toggles `.visible` on `.reveal` elements at threshold `0.12`
   - Nav background: switches from gradient to solid + `backdrop-filter: blur(12px)` after `scrollY > 60`

## Design System

CSS custom properties (`:root`) define the palette:
- `--black: #0B0B0B` — page background
- `--graphite: #1F1F1F` — card backgrounds
- `--white: #F5F5F0` — primary text
- `--gold: #C2A36B` — accents, highlights, hover states
- Fonts: `Cormorant Garamond` (serif, headings), `DM Mono` (mono, labels), `Outfit` (sans, body)

## Editing Notes

- The grid background is rendered via CSS `linear-gradient` (`.grid-bg`), not an image.
- The noise overlay is an inline SVG data URI on `body::before`.
- The ABP monogram in the hero is an inline SVG.
- All animations are CSS-based (transitions on opacity/transform) except the cursor tracking loop.
- Content is in Russian; preserve Cyrillic copy when editing.
