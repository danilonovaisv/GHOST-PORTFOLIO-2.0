# CREATIVE DIRECTION — GHOST PORTFOLIO 2.0

**Phase:** 01 — Creative Strategy & Art Direction  
**Active Personas:** Art Director (`AG-03`), Creative Strategist (`AG-01`), Design System Architect (`AG-04`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Aesthetic Vision: The Evolved "Ghost Era"

`GHOST-PORTFOLIO-2.0` preserves the unmistakable DNA of the Ghost System—**deep void darkness pierced by spectral electric blue and cyan**—while elevating the layout from a showcase grid to a **cinematic editorial monograph**.

### Core Creative Tenets
1. **Presence Without Noise:** Every pixel of WebGL, motion, or glow exists to frame the work and amplify the narrative, never to compete with project imagery or typography.
2. **Editorial Asymmetry:** Inspired by Swiss editorial grids and high-fashion/architectural monographs, pairing bold `Manrope` display statements with technical `PPSupplyMono` coordinates and generous negative space.
3. **Motion as Breath:** Movement follows the canonical `GHOST_EASE` (`cubic-bezier(0.22, 1, 0.36, 1)`)—fast initial impulse with a long, weightless deceleration. No bouncy springs, no gratuitous scaling, no visual anxiety.
4. **Tactile Digital Craft:** Subtle glassmorphic depth (`rgba(255, 255, 255, 0.05)` with `1px` spectral borders), controlled atmospheric grain, and seamless media transitions.

---

## 2. Visual Territories & Mood Direction

### Territory A — The Void Stage (Global Canvas)
- **Atmosphere:** Infinite `#040013` (Void Black) transitioning subtly through `#08031f` (Abyss Mid) and `#0c1445` (Abyss Start).
- **Rule:** Never use flat `#000000` or muddy gray backgrounds. The background is a living atmospheric stage.

### Territory B — Spectral Light (Interactive & Brand Signals)
- **Primary Signal:** Electric Ghost Blue (`#0048FF`) for primary actions, active states, and structural anchors.
- **Ethereal Highlight:** Ghost Cyan (`#4FE6FF`) for data coordinates, subtle focus rings, and secondary spectral accents.
- **Controlled Anomaly:** Purple (`#8705F2`) and Pink (`#F501D3`) are strictly reserved for micro-interactions (such as the `<AntigravityCTA />` hover separation or Lab shader anomalies)—never used as dominant surface fills.

### Territory C — Editorial Authority (Typography & Negative Space)
- **Contrast & Legibility:** `#FCFFFF` (Ghost White) for primary headlines and narrative copy, paired with `#B4B8C5` (elevated from legacy `#A1A3A3` where needed to guarantee WCAG 2.2 AA contrast on `#0B0D3A` surfaces).
- **Spatial Rhythm:** Minimum 35% of any viewport must remain open Void Black / Abyss negative space to preserve luxury editorial pacing.

---

## 3. Page-by-Page Art Direction Guidelines

### 3.1 Home (`/`) — The Executive Manifesto
- **Hero Section:** Editorial manifesto typography in the foreground (`--z-layer-content: 20`) with an isolated, low-opacity interactive WebGL/shader field in the background (`--z-layer-base: 0` / `--z-layer-3d: 15`) that never obscures headline legibility.
- **Featured Cases:** Large-scale editorial cards (full-bleed or asymmetric 7/5 column split) with instant video/image hover previews, client emblem, strategic category tag, and concise executive thesis.
- **Leadership & AI Sections:** Structured architectural blocks with monochrome client wall (Swift, Nestlé, Nivea, Ambev, Zé Delivery, Pernod Ricard, Algar Telecom, Mapfre, AON, O Boticário, Grupo Iguatemi, Unilever) that illuminate on hover.

### 3.2 Portfolio Index (`/portfolio`) — Curated Exhibition
- **Filter Architecture:** Instant, zero-layout-shift filtering across the 5 Strategic Territories (`All`, `Branding`, `Campaigns`, `Motion`, `Web & Digital`, `Creative Tech & AI`) with live item count in `PPSupplyMono`.
- **View Modes:** Editorial Asymmetric Grid (default) + Executive Index List view (for rapid scanning by recruiters/CMOs).

### 3.3 Case Studies (`/projetos/[slug]`) — Immersive Monograph
- **Dynamic Accent Adaptation:** While the global shell remains Void Black (`#040013`), each case study can inject a scoped `--case-accent` token for subtle ambient glows and eyebrow metadata without breaking the Ghost System identity.
- **Pacing:** Alternates between constrained editorial reading columns (`max-w-3xl` / 8 columns) for Strategy/Challenge text and full-bleed (`100vw` or 12-column) media stages for visual impact.

### 3.4 Creative Technology & Lab (`/creative-technology` & `/lab`)
- **Visual Language:** Higher density of `PPSupplyMono` telemetry, interactive shader canvases, generative AI workflow breakdowns, and live interactive sandboxes.

---

## 4. Anti-Patterns (Strictly Forbidden)

1. **No Visual Competition:** WebGL particles or shaders must never render *on top* of body copy or reduce text contrast below WCAG AA (`4.5:1`).
2. **No Generic SaaS Templates:** Forbidden to use standard 3-column icon-card feature grids, generic pricing-style boxes, or stock illustrations.
3. **No Uncontrolled Motion:** Forbidden to use `scale > 1.04` on cards, elastic/bouncy easings, or continuous off-screen animations.
4. **No Placeholder Media:** Every visual slot must bind to a verified asset from the asset manifest (`site-assets` / `portfolio-media`) or render a typographic architectural frame—never `lorem ipsum` or stock unsplash URLs.

