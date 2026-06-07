# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a zero-dependency static landing page for **LekAccount** (brand: SPD Advisory), a Thai professional accounting services company targeting SMEs. The entire site lives in a single file: `index.html`.

## Development

No build system, package manager, or tooling exists. Open `index.html` directly in a browser to preview. There are no lint, test, or build commands.

To serve locally with live reload you can use any static file server, e.g.:
```bash
python3 -m http.server 8080
```

## Architecture

Everything — HTML structure, all CSS, and all JavaScript — is embedded in `index.html` (~1100 lines), organized as:

1. `<style>` block — all styling via CSS custom properties (variables)
2. Semantic `<section>` elements — `#hero`, `#who-we-serve`, `#services`, `#pricing`, `#what-we-do`, `#testimonial`, `#why-us`, `#cta`, plus `<nav>` and `<footer>`
3. `<script>` block at bottom — vanilla JS (~60 lines)

## CSS Conventions

All colours are defined as CSS variables at the top of the `<style>` block:

```css
--navy: #0c1a35      /* primary dark */
--blue: #2952d9      /* primary accent */
--gold: #c8973a      /* secondary accent */
--gray-100 … --gray-800
```

Responsive breakpoints: `768px` (tablet) and `900px` (desktop). Layouts use CSS Grid with column counts that collapse on smaller screens.

Animation: elements receive a `fade-up` class and become visible when the Intersection Observer fires the `visible` class on scroll.

Typography uses Google Fonts: **Prompt** (headings/Thai display), **Sarabun** (Thai body), **Montserrat** (sans-serif), **Cormorant Garamond** (accent). Font sizes use `clamp()` for fluid scaling.

## JavaScript Features

- Nav shadow on scroll past 20 px
- Intersection Observer for `.fade-up` → `.visible` scroll animations
- Pricing tab toggle between three views: monthly / yearly / work-permit; active tab persisted in `localStorage`
- **Tweaks panel** — a hidden live-editing overlay (colour pickers + font selectors) for design iteration; toggled via a `postMessage` from a parent frame (edit-mode integration)

## Content Language

The page is in **Thai** (`lang="th"`). All copy, CTAs, and section headings are Thai. Keep this in mind when editing text content.
