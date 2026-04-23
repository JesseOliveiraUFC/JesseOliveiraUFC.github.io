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

- **GitHub Pages**: push repo → Settings → Pages → branch `main`, root `/`
- **Netlify / Vercel**: drag-and-drop the folder, or connect the GitHub repo

## Architecture

All content is in `index.html` as a single page with anchor-linked sections:
`#hero` → `#sobre` → `#experiencia` → `#competencias` → `#formacao` → `#contato`

`style.css` uses CSS custom properties (`:root`) for the entire design system — colors, radius, timing. Change `--accent` / `--accent-2` to retheme the whole site.

`script.js` provides five behaviors:
1. Navbar `.scrolled` class on scroll (adds blur/background)
2. Mobile hamburger menu toggle (also closes on outside click or nav-link click)
3. `IntersectionObserver` that adds `.visible` to `[data-animate]` elements for scroll-reveal animations (fires once, then unobserves)
4. Active nav-link highlight via a second `IntersectionObserver` on each `section[id]` (threshold 0.45)
5. Clients tooltip click-toggle on `#statClients` for touch/mobile (hover state is handled purely by CSS)

## Scroll-reveal pattern

Any element with `data-animate` starts at `opacity: 0` / `transform: translateY/X(...)` via CSS, and transitions to its final state when `.visible` is added by the observer. Stagger delays for grid children are set via `nth-child` transition-delay in CSS.

## Adding / editing content

- **New experience role**: copy a `.timeline-item` block in `index.html`, update text and `.tag` chips. Add `<span class="period current">` on the active role (renders a green dot).
- **New skill category**: copy a `.skill-card` block; the grid auto-fills columns
- **Colors**: edit `--accent` and `--accent-2` in `:root` in `style.css`
- **Contact links**: update `href` on `.contact-card` anchors in the `#contato` section. The first card uses `.contact-card--featured` for the primary call-to-action emphasis.
- **New education entry**: copy an `.edu-card` block. Add `<div class="edu-status ongoing">Em andamento</div>` as the first child for in-progress degrees.
- **New certification**: copy a `.cert-item` block inside `.cert-grid`; set `.cert-badge` text to the issuer name.
- **Alternating section backgrounds**: sections use `.section` by default; add `.section-alt` to alternate the background tone (experiência and formação use it).

## Client logo display classes

Logos live in `logos/`. Three CSS classes control how they render inside the 80×80 white-padded container:

| Class | Effect |
|---|---|
| *(none)* | White background, 8 px padding, `object-fit: contain` — safe default |
| `.logo-fit` | No background/padding, `object-fit: cover` — for photos or full-bleed logos |
| `.logo-clean` | Transparent background, no border/padding, `object-fit: contain` — for logos with their own padding baked in |
