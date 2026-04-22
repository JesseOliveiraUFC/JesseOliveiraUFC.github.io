# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Static single-page portfolio for Jessé Oliveira (Data Engineer & AI). No framework, no build step — three files: `index.html`, `style.css`, `script.js`.

## Preview locally

Open `index.html` directly in a browser, or start a local server:

```bash
python -m http.server 8080
# or
npx serve .
```

## Deployment options

- **GitHub Pages**: push repo → Settings → Pages → branch `master`, root `/`
- **Netlify / Vercel**: drag-and-drop the folder, or connect the GitHub repo

## Architecture

All content is in `index.html` as a single page with anchor-linked sections:
`#hero` → `#sobre` → `#experiencia` → `#competencias` → `#formacao` → `#contato`

`style.css` uses CSS custom properties (`:root`) for the entire design system — colors, radius, timing. Change `--accent` / `--accent-2` to retheme the whole site.

`script.js` provides three behaviors:
1. Navbar `.scrolled` class on scroll (adds blur/background)
2. Mobile hamburger menu toggle
3. `IntersectionObserver` that adds `.visible` to `[data-animate]` elements for scroll-reveal animations

## Scroll-reveal pattern

Any element with `data-animate` starts at `opacity: 0` / `transform: translateY/X(...)` via CSS, and transitions to its final state when `.visible` is added by the observer. Stagger delays for grid children are set via `nth-child` transition-delay in CSS.

## Adding / editing content

- **New experience role**: copy a `.timeline-item` block in `index.html`, update text and `.tag` chips
- **New skill category**: copy a `.skill-card` block; the grid auto-fills columns
- **Colors**: edit `--accent` and `--accent-2` in `:root` in `style.css`
- **Contact links**: update `href` on `.contact-card` anchors in the `#contato` section
