# COMPONENT ARCHITECTURE — GHOST PORTFOLIO 2.0

**Phase:** 02 — Component & Modular Case Engine Architecture  
**Active Personas:** Frontend Architect (`AG-06`), Design System Architect (`AG-04`), UI Engineer (`AG-07`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Component Taxonomy & Directory Hierarchy

Components in `src/components/` are organized by architectural responsibility and enforces strict **Server vs. Client Component** boundaries:

```text
src/components/
├── ui/                    # Atomic Design System primitives (Button, Badge, Tag, Divider, IconCircle)
├── typography/            # Fluid editorial typography (<DisplayHeading>, <SectionHeader>, <MonoMeta>, <GhostText>)
├── layout/                # Structural wrappers (<StandardGrid>, <Container>, <Section>, <PageShell>)
├── navigation/            # Wayfinding (<Header>, <MobileMenuCurtain>, <Footer>, <Breadcrumb>, <NextProjectBanner>)
├── motion/                # Reusable animation wrappers (<GhostReveal>, <ParallaxFrame>, <LenisProvider>, <AntigravityCTA>)
├── media/                 # Smart media renderers (<SmartImage>, <AdaptiveVideo>, <InteractiveEmbed>, <Lightbox>)
├── three/                 # Isolated WebGL islands (<WebGLBoundary>, <HeroAtmosphereCanvas>, <GrainientStage>)
├── home/                  # Home-specific editorial sections (HeroManifesto, SelectedWorks, TerritoriesGrid, BrandWall)
├── portfolio/             # Portfolio exhibition components (TerritoryFilterBar, ProjectCard, ProjectIndexRow)
└── projects/              # Modular 8-stage Case Study Block Engine
    ├── CaseHero.tsx
    ├── CaseOverview.tsx
    ├── CaseStrategyBlock.tsx
    ├── CaseCreativeBlock.tsx
    ├── CaseBlockRenderer.tsx
    ├── CaseCredits.tsx
    └── blocks/
        ├── FullBleedMediaBlock.tsx
        ├── SplitEditorialBlock.tsx
        ├── MediaGridBlock.tsx
        ├── QuoteBandBlock.tsx
        ├── MetricsHighlightBlock.tsx
        ├── VideoShowcaseBlock.tsx
        └── InteractiveStageBlock.tsx
```

---

## 2. Server vs. Client Component Boundary Rules

| Component Category | Default Boundary | Client Directive (`'use client'`) Allowed Only When |
| :--- | :--- | :--- |
| **Layout & Grid** (`StandardGrid`, `Section`, `Footer`) | **Server Component** | Never (must remain zero-JS Server Components) |
| **Typography & Copy** (`SectionHeader`, `MonoMeta`, `CaseOverview`) | **Server Component** | Wrapped by a thin `<GhostReveal>` client leaf if scroll-triggered animation is needed |
| **Case Block Renderer** (`CaseBlockRenderer`, `SplitEditorialBlock`) | **Server Component** | Individual interactive children (`AdaptiveVideo`, `InteractiveStageBlock`, `Lightbox`) are Client leaves |
| **Navigation** (`Header`, `MobileMenuCurtain`, `TerritoryFilterBar`) | **Client Component** | Requires scroll state, URL searchParams sync, or focus-trap keyboard handlers |
| **WebGL / 3D** (`HeroAtmosphereCanvas`, `GrainientStage`) | **Client Island (Lazy)** | Must be dynamically imported with `ssr: false` inside `<WebGLBoundary>` |

---

## 3. Core Structural Primitives

### 3.1 `<StandardGrid />` (`.std-grid`)
Enforces the canonical Ghost System 4 / 8 / 12 column responsive layout:
- **Mobile (`< 768px`):** 4 columns, `16px` (`gap-4`) gutter, `px-6` (`24px`) container padding.
- **Tablet (`768px – 1023px`):** 8 columns, `24px` (`gap-6`) gutter, `px-12` (`48px`) container padding.
- **Desktop (`≥ 1024px`):** 12 columns, `32px` (`gap-8`) gutter, `clamp(24px, 5vw, 96px)` padding, `max-w-[1680px]` centered.

### 3.2 `<AntigravityCTA />` & `<CompoundPillCTA />`
Preserves the signature Ghost interaction:
- **Structure:** Primary pill (`#0048FF`) paired with detached 48px circular icon node (`ArrowUpRight`).
- **Hover Choreography:** Circle shifts `8px` right, transitions background to `#8705F2` (Purple Anomaly), and rotates arrow from `-45deg` to `0deg` using `GHOST_EASE` (`[0.22, 1, 0.36, 1]`).
- **Accessibility:** Renders as a single semantic `<Link>` or `<button>` with `min-h-[48px]`, high-contrast `focus-visible:ring-2 focus-visible:ring-[#4FE6FF]`, and `prefers-reduced-motion` support.

---

## 4. The Composable Case Study Block Engine (`<CaseBlockRenderer />`)

Instead of maintaining 5 separate template files (`v1`, `v2`, `v3-alpa`, `v3-alpa-hero`, `legacy-blocks`) as in `PORTFOLIO-DANILO-FINAL`, `GHOST-PORTFOLIO-2.0` normalizes all case content into a discriminated union of strongly-typed editorial blocks (`ProjectSection`):

```tsx
// Conceptual Server Component Dispatcher
export function CaseBlockRenderer({ sections }: { sections: ProjectSection[] }) {
  return (
    <div className="flex flex-col gap-16 md:gap-24 lg:gap-32">
      {sections.map((section) => {
        switch (section.type) {
          case 'narrative-split':
            return <SplitEditorialBlock key={section.id} {...section.data} />;
          case 'fullbleed-media':
            return <FullBleedMediaBlock key={section.id} {...section.data} />;
          case 'media-grid':
            return <MediaGridBlock key={section.id} {...section.data} />;
          case 'quote-band':
            return <QuoteBandBlock key={section.id} {...section.data} />;
          case 'video-showcase':
            return <VideoShowcaseBlock key={section.id} {...section.data} />;
          case 'metrics-deliverables':
            return <MetricsHighlightBlock key={section.id} {...section.data} />;
          case 'interactive-embed':
            return <InteractiveStageBlock key={section.id} {...section.data} />;
        }
      })}
    </div>
  );
}
```
This guarantees that legacy v1/v2/v3 projects can be mapped 1:1 into `ProjectSection[]` via a deterministic adapter without touching component code.

