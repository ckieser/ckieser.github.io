# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Personal portfolio/CV website for Christoph Kieser, hosted on GitHub Pages at `ckieser.io`. No build tools or frameworks — purely static vanilla HTML/CSS/JS. The only external dependency is Google Fonts (Inter + JetBrains Mono), loaded via CDN in `<head>`.

## Files

- `index.html` — the entire site: all HTML structure, CSS styles, and JavaScript in one self-contained file
- `llms.txt` — plain-text bio for AI/LLM discoverability (mirrors the content shown on the site)
- `photo.jpg` — profile photo referenced in `index.html`
- `CNAME` — custom domain (`ckieser.io`) for GitHub Pages

## Development

Open `index.html` directly in a browser — no server or build step required. Changes deploy automatically when pushed to the `main` branch via GitHub Pages.

## Architecture

Everything lives in `index.html`:
- **CSS**: CSS custom properties (`--bg`, `--bg-alt`, `--surface`, `--surface-2`, `--surface-3`, `--cyan`, `--indigo`, `--muted`, etc.) define a deep-navy theme with cyan/indigo accents. 18+ labeled CSS sections.
- **Fonts**: Inter (sans) + JetBrains Mono (mono) via Google Fonts CDN.
- **Favicon**: Inline SVG data-URI in `<head>` — "ck" monogram in cyan on dark square.
- **Sections**: `#hero`, `#about`, `#skills`, `#experience`, `#education`, `#contact` — anchor-linked from a fixed nav with hamburger on mobile.
- **JavaScript** (7 labelled sections at bottom of `<body>`):
  1. rAF-throttled scroll handler — scroll progress bar, nav `.scrolled` class, back-to-top visibility
  2. Back-to-top button click handler
  3. Hamburger menu toggle (overlay, Escape key, link-click close)
  4. Typing animation — cycles 5 phrases inside the terminal window component
  5. Staggered IntersectionObserver reveal — `data-delay` on individual cards for offset entry
  6. Language bar animations — separate observer triggers bar width transitions
  7. Active nav highlighting via IntersectionObserver

## Key UI Components

- **Terminal window** (hero): macOS-style chrome with red/yellow/green dots, typing animation inside
- **Scroll progress bar**: 3px fixed bar at very top (z-index 200), gradient cyan→indigo
- **Mobile hamburger**: animates to ✕, opens full-screen overlay with staggered nav links
- **Back-to-top button**: fixed bottom-right, fades in after 400px scroll
- **Stats strip** (hero): inline pipe-separated monospace values below CTAs
- **Glassmorphism stat cards** (about): `backdrop-filter: blur(8px)` with top cyan accent border
- **Skill groups**: left `3px` accent border alternating cyan/indigo; emoji in square badge
- **Timeline**: 3px gradient rail, 24px dots, pulse-ring on current role, `→` bullets, period date pills
- **Education section**: 3 labelled subsections — Education cards, Languages, Certifications (active with green left border; expired at 0.65 opacity under "Previously Held" label)

## Content Synchronisation

When updating professional content (job titles, dates, certifications, skills, bio text), keep `index.html` and `llms.txt` in sync — they contain the same factual information in different formats.

Certification validity dates in both files follow the Red Hat certification system: RHCE and RHCSA expiry is tied to the most recent Red Hat exam passed (currently the OpenShift Developer cert, valid until Aug 2028).
