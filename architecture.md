# Architecture — Bloom

## System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    GitHub Pages (CDN)                    │
│                   Static HTML/CSS/JS                    │
└─────────────────────────────────────────────────────────┘
                           ▲
                           │ git push main
┌─────────────────────────────────────────────────────────┐
│              GitHub Actions (CI/CD)                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌────────┐  │
│  │ Checkout │→ │Setup Node│→ │npm ci    │→ │astro   │  │
│  │          │  │  v22     │  │          │  │build   │  │
│  └──────────┘  └──────────┘  └──────────┘  └────────┘  │
│                                                         │
│  ┌──────────┐  ┌──────────────────────────────────┐    │
│  │ Upload   │→ │ Deploy to GitHub Pages            │    │
│  │ artifact │  │ (actions/deploy-pages@v4)         │    │
│  └──────────┘  └──────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
                           ▲
                           │ npm run build
┌─────────────────────────────────────────────────────────┐
│                    Astro (Build)                        │
│  ┌─────────────────────────────────────────────────┐   │
│  │ src/pages/index.astro                           │   │
│  │   └── imports Layout + 9 components             │   │
│  └─────────────────────────────────────────────────┘   │
│                           ↓                             │
│  ┌─────────────────────────────────────────────────┐   │
│  │ dist/                                           │   │
│  │   ├── index.html (minified, single-file)        │   │
│  │   └── _astro/index.[hash].css (extracted)       │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

## Component Architecture

### Component Tree
```
Layout.astro (base HTML + global CSS)
├── Nav.astro (floating pill nav)
├── Hero.astro (editorial split)
├── Marquee.astro (infinite scroll)
├── Features.astro (bento grid)
├── Gallery.astro (image grid)
├── Testimonials.astro (card carousel)
├── CTA.astro (email signup)
├── Footer.astro (links + socials)
└── ScrollReveal.astro (IntersectionObserver)
```

### Component Responsibilities

| Component | Type | Purpose |
|-----------|------|---------|
| `Layout.astro` | Layout | Base HTML shell, global CSS, `<slot />` |
| `Nav.astro` | UI | Fixed floating pill navigation with mobile toggle |
| `Hero.astro` | Section | Editorial split with images + CTA |
| `Marquee.astro` | UI | Infinite horizontal scroll of flower names |
| `Features.astro` | Section | Asymmetric bento grid with 6 feature cards |
| `Gallery.astro` | Section | Masonry-style image gallery |
| `Testimonials.astro` | Section | 3-column testimonial cards with stars |
| `CTA.astro` | Section | Email signup form |
| `Footer.astro` | Section | Multi-column footer with social links |
| `ScrollReveal.astro` | Logic | Client-side IntersectionObserver for animations |

### Data Flow
- **Zero props** — all components are static HTML markup
- **No state** — pure presentation layer
- **No client-side JS** except ScrollReveal (vanilla IntersectionObserver)
- **No API calls** — fully static site

## Build Pipeline

### Development
```bash
npm run dev          # Vite dev server with HMR
npm run dev --host   # Expose to network
```

### Production Build
```bash
npm run build        # Astro static build → dist/
npm run preview      # Preview production build locally
```

### Build Output
```
dist/
├── index.html           # Single HTML file (minified)
└── _astro/
    └── index.[hash].css # Extracted CSS bundle
```

## Deployment Architecture

### GitHub Actions Workflow
- **Trigger:** Push to `main` branch
- **Environment:** `ubuntu-latest`
- **Node Version:** 22 (required by Astro 7)
- **Build Command:** `npm run build`
- **Deploy Target:** GitHub Pages via `actions/deploy-pages@v4`

### Environment Configuration
- `github-pages` environment with branch policies for `main` and `gh-pages`
- `id-token: write` permission for Pages deployment
- `pages: write` permission for deployment

### Site Configuration
```javascript
// astro.config.mjs
{
  site: 'https://zorrme.github.io',
  base: '/flower-bloom',
  output: 'static'
}
```

## Performance Characteristics

### Static Generation
- Single HTML file with inlined critical path
- Extracted CSS bundle with content hash
- No JavaScript bundle (except inline ScrollReveal)
- No runtime server needed

### Image Strategy
- External Unsplash URLs (CDN-served)
- `loading="eager"` + `fetchpriority="high"` for hero
- `loading="lazy"` for below-fold images
- Specific crop parameters for consistent sizing

### CSS Architecture
- Single global stylesheet (24KB)
- CSS custom properties for theming
- No CSS preprocessors
- No utility framework
- Dark mode via `prefers-color-scheme` media query

### Animation Performance
- IntersectionObserver for scroll reveals (no scroll listeners)
- CSS transforms and opacity only (GPU-accelerated)
- `will-change` not used (avoided over-optimization)
- Film grain via CSS `background-image` (static SVG)

## Security Considerations
- No client-side secrets
- No API keys in codebase
- External resources: Google Fonts, Unsplash
- No cookies or local storage
- No forms that submit data (email form is demo only)

## Browser Support
- Modern browsers (Chrome, Firefox, Safari, Edge)
- CSS Grid, Flexbox, Custom Properties
- IntersectionObserver API
- `prefers-color-scheme` media query
- `backdrop-filter` for glassmorphism
