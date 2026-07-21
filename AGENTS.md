# Bloom — Flower Landing Page

## Project Overview
A premium Astro landing page for flower lovers. Awwwards-tier design with floating pill nav, editorial typography, bento grid, and dark mode support.

## Quick Start
```bash
npm run dev          # Start dev server (http://localhost:4321)
npm run build        # Build to dist/
npm run preview      # Preview production build
```

## Tech Stack
- **Framework:** Astro 7.1.1 (static output)
- **Node:** >= 22.12.0 (required by Astro 7)
- **Fonts:** Cormorant Garamond (headings) + Plus Jakarta Sans (body) via Google Fonts
- **CSS:** Vanilla CSS with custom properties, no framework
- **JS:** Vanilla IntersectionObserver for scroll reveals
- **Images:** Unsplash URLs (verified working)
- **Deploy:** GitHub Pages via GitHub Actions

## Project Structure
```
flower-bloom/
├── src/
│   ├── layouts/
│   │   └── Layout.astro          # Base HTML + all CSS (is:global)
│   ├── components/
│   │   ├── Nav.astro             # Floating pill navigation
│   │   ├── Hero.astro            # Editorial split hero
│   │   ├── Marquee.astro         # Flower variety marquee
│   │   ├── Features.astro        # Asymmetric bento grid
│   │   ├── Gallery.astro         # Dark gallery section
│   │   ├── Testimonials.astro    # Testimonial cards
│   │   ├── CTA.astro             # Email signup section
│   │   ├── Footer.astro          # Footer with links
│   │   └── ScrollReveal.astro    # IntersectionObserver script
│   └── pages/
│       └── index.astro           # Main page (imports all components)
├── public/
│   ├── favicon.ico
│   └── favicon.svg
├── .github/workflows/
│   └── gh-pages.yml              # GitHub Actions deployment
├── astro.config.mjs
├── package.json
└── tsconfig.json
```

## Key Conventions
- All CSS lives in `Layout.astro` with `is:global` — no component-scoped styles
- Components are pure HTML markup (no props, no logic)
- Scroll reveal via `.reveal` class + IntersectionObserver
- Dark mode via `prefers-color-scheme: dark` media query
- Custom easing curves: `--ease-out-expo`, `--ease-out-quart`, `--ease-spring`

## Deployment
- Push to `main` triggers GitHub Actions workflow
- Builds with Node 22, deploys to GitHub Pages
- Site URL: https://zorrme.github.io/flower-bloom/
- Repo: https://github.com/zorrme/flower-bloom

## Development Notes
- The `.netlify/` directory can be ignored (from earlier Netlify deploy attempt)
- `node_modules/` is gitignored
- All Unsplash image URLs are verified working — replace carefully if updating
