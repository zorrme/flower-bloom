# Design System — Bloom

## Color Palette

### Light Mode
| Token | Hex | Usage |
|-------|-----|-------|
| `--sage-900` | `#1a2e1f` | Deep accents |
| `--sage-800` | `#2a4a33` | Dark text on light backgrounds |
| `--sage-700` | `#3a6547` | Icons, active states |
| `--sage-600` | `#4a7d5b` | Hover states |
| `--sage-500` | `#6b9e7a` | Links, secondary actions |
| `--sage-400` | `#8fb89e` | Subtle accents |
| `--sage-100` | `#dce8df` | Light backgrounds |
| `--sage-50` | `#eef5f0` | Soft tints |
| `--cream` | `#f8f6f1` | Page background |
| `--cream-warm` | `#f2efe8` | Card backgrounds |
| `--blush` | `#c4877a` | Accent, CTAs |
| `--blush-soft` | `#e8c4bb` | Soft accent backgrounds |
| `--ink` | `#1a1a18` | Primary text |
| `--ink-muted` | `#7a7a76` | Secondary text |
| `--ink-faint` | `#b0afa8` | Tertiary text, borders |
| `--white` | `#fefefe` | Pure white |
| `--white-warm` | `#faf8f4` | Warm white |

### Dark Mode (`prefers-color-scheme: dark`)
| Token | Hex | Mapping |
|-------|-----|---------|
| `--cream` | `#0c0f0d` | Dark background |
| `--cream-warm` | `#111613` | Dark card background |
| `--sage-50` | `#1a2e1f` | Dark surface |
| `--sage-100` | `#1e3524` | Dark elevated surface |
| `--white` | `#151b17` | Dark white |
| `--white-warm` | `#1a221d` | Dark warm white |
| `--ink` | `#e4e2dc` | Light text on dark |
| `--ink-muted` | `#8a8a86` | Secondary text |
| `--ink-faint` | `#5a5a56` | Tertiary text |
| `--blush-soft` | `#3a2a26` | Dark accent |

## Typography

### Font Families
- **Headings:** `'Cormorant Garamond', Georgia, serif`
  - Weights: 300 (light), 400 (regular), 500 (medium), 600 (semibold), 700 (bold)
  - Italic weights: 300, 400, 500
- **Body:** `'Plus Jakarta Sans', system-ui, sans-serif`
  - Weights: 300 (light), 400 (regular), 500 (medium), 600 (semibold), 700 (bold)
  - Italic weight: 400

### Type Scale
```css
h1, h2, h3, h4 {
  font-family: 'Cormorant Garamond', Georgia, serif;
  font-weight: 400;
  line-height: 1.05;
}
```

## Spacing & Radius

### Border Radius
| Token | Value | Usage |
|-------|-------|-------|
| `--radius-lg` | `24px` | Large cards, modals |
| `--radius-xl` | `32px` | Extra large containers |
| `--radius-pill` | `100px` | Buttons, nav pill, tags |

## Motion

### Easing Curves
| Token | Value | Usage |
|-------|-------|-------|
| `--ease-out-expo` | `cubic-bezier(0.16, 1, 0.3, 1)` | Main transitions, reveals |
| `--ease-out-quart` | `cubic-bezier(0.25, 1, 0.5, 1)` | Secondary transitions |
| `--ease-spring` | `cubic-bezier(0.32, 0.72, 0, 1)` | Bouncy interactions |

### Scroll Reveal System
- Elements with class `.reveal` are hidden by default
- IntersectionObserver (threshold: 0.12, rootMargin: `0px 0px -30px 0px`) triggers `.visible` class
- Delay modifiers: `.reveal-d1` through `.reveal-d5` for staggered entrance
- Once revealed, element is unobserved (one-shot animation)

## Layout Patterns

### Floating Pill Navigation
- Fixed position, centered horizontally
- Glassmorphism: `backdrop-filter: blur(24px) saturate(1.4)`
- Semi-transparent background with subtle border and inset shadow
- Border radius: pill (100px)

### Bento Grid (Features)
- Asymmetric grid layout using CSS Grid
- Mix of text cells and image cells
- Spanning cells for emphasis
- Double-bezel card architecture (inner border effect)

### Section Pattern
Each section follows:
1. Eyebrow label (small caps, muted)
2. Section title (Cormorant Garamond)
3. Section description (Plus Jakarta Sans)
4. Content (grid, gallery, cards)

## Visual Effects

### Film Grain Overlay
```css
body::after {
  content: '';
  position: fixed;
  inset: 0;
  z-index: 9999;
  pointer-events: none;
  opacity: 0.025;
  background-image: url("data:image/svg+xml,...fractalNoise...");
  background-size: 200px;
}
```

### Glassmorphism (Nav)
```css
backdrop-filter: blur(24px) saturate(1.4);
background: rgba(248, 246, 241, 0.8);
border: 1px solid rgba(26, 46, 31, 0.08);
box-shadow: 0 1px 2px rgba(26,46,31,0.04), 
            0 8px 32px rgba(26,46,31,0.06), 
            inset 0 1px 0 rgba(255,255,255,0.6);
```

## Image Treatment
- All images use Unsplash URLs with specific crop parameters
- Eager loading for above-the-fold (hero)
- Lazy loading for below-the-fold
- `fetchpriority="high"` for hero main image

## Responsive Behavior
- Single-column layout on mobile
- Multi-column grids on desktop
- Mobile nav toggle with hamburger menu
- Fluid typography and spacing
