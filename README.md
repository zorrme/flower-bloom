# Bloom — For Flower Lovers

A premium Astro landing page with Awwwards-tier design: floating pill navigation, editorial typography, asymmetric bento grid, film grain overlay, blur-up scroll reveals, and automatic dark mode.

**Live:** https://zorrme.github.io/flower-bloom/

## Tech Stack

- **Astro 7.1.1** — Static site generation
- **Vanilla CSS** — Custom properties, no framework
- **Vanilla JS** — IntersectionObserver scroll reveals
- **GitHub Actions** — CI/CD to GitHub Pages

## Quick Start

```bash
npm install
npm run dev        # → http://localhost:4321
```

## Commands

| Command | Action |
|---------|--------|
| `npm install` | Install dependencies |
| `npm run dev` | Start dev server at localhost:4321 |
| `npm run build` | Build production site to `dist/` |
| `npm run preview` | Preview production build locally |

## Project Structure

```
src/
├── layouts/Layout.astro       # Base HTML + all global CSS
├── components/
│   ├── Nav.astro              # Floating pill navigation
│   ├── Hero.astro             # Editorial split hero section
│   ├── Marquee.astro          # Infinite flower name scroll
│   ├── Features.astro         # Asymmetric bento grid
│   ├── Gallery.astro          # Image gallery section
│   ├── Testimonials.astro     # Testimonial cards
│   ├── CTA.astro              # Email signup section
│   ├── Footer.astro           # Footer with links
│   └── ScrollReveal.astro     # Scroll animation logic
└── pages/index.astro          # Main page
```

## Design Features

- **Floating pill navigation** with glassmorphism effect
- **Cormorant Garamond + Plus Jakarta Sans** typography pairing
- **Asymmetric bento grid** with double-bezel cards
- **Film grain overlay** via SVG noise texture
- **Blur-up scroll reveals** with IntersectionObserver
- **Dark mode** via `prefers-color-scheme` media query
- **Custom easing curves** for premium motion

## Deployment

Push to `main` triggers automatic deployment via GitHub Actions.

## Documentation

- [Design System](design.md) — Colors, typography, spacing, motion
- [Architecture](architecture.md) — Technical structure and build pipeline
