# DISCOVERY REPORT — GHOST PORTFOLIO 2.0

**Phase:** 00 — Discovery & Ecosystem Audit  
**Date:** 2026-11-12  
**Active Personas:** Portfolio Context Analyst, Creative Strategist, UX Architect, Technical Architect  
**Target Production URL:** https://portfoliodanilo.com (Read-Only Inspection)  
**Source Code Repository:** `danilonovaisv/PORTFOLIO-DANILO-FINAL` (Read-Only Inspection)  
**Knowledge Repository:** `danilonovaisv/Agent-Skills-Knowledge-Hub` (Read-Only Inspection)  
**Target Blueprint Repository:** `GHOST-PORTFOLIO-2.0`

---

## 1. Evidence & Verification Ledger (Facts vs. Assumptions)

### 1.1 Verified Facts (Directly Inspected via GitHub MCP, Context7 & Web Index)

1. **Framework & Runtime (`package.json`):**
   - `next`: `16.4.6` (App Router, `output: 'standalone'`, Turbopack raw GLSL loader rules + Webpack fallback).
   - `react` & `react-dom`: `19.3.1`.
   - `typescript`: `~7.0.2` (strict mode, `NODE_OPTIONS='--max-old-space-size=8192'`).
   - `tailwindcss`: `4.3.5` with `@tailwindcss/postcss` `4.3.5` (CSS-first `@theme` configuration in `src/app/globals.css`).
   - `packageManager`: `pnpm@12.18.0`, Node engine `22`.
2. **Motion & 3D Stack (`package.json`):**
   - `three`: `^0.187.0`, `@react-three/fiber`: `^9.8.2`, `three-stdlib`: `^2.36.1`, `ogl`: `^1.0.11`.
   - `gsap`: `^3.15.1`, `motion`: `^14.12.0`, `lenis`: `^1.3.27`.
3. **Backend, Storage & Infrastructure (`package.json`, `next.config.mjs`, `supabase/schema.sql`):**
   - Supabase (`@supabase/supabase-js` `^2.119.0`, `@supabase/ssr` `0.12.7`) hosted at `umkmwbkwvulxtdodzmzf.supabase.co`.
   - Dual-cloud storage footprints: Supabase Storage buckets (`site-assets`, `portfolio-media`) + Cloudflare R2 (`@aws-sdk/client-s3`, `assets.portfoliodanilo.com`, `*.r2.dev`).
   - Dual deployment adapters present in repository: Firebase Hosting (`firebase.json`, `scripts/firebase-next-adapter.cjs`) and Cloudflare Workers/OpenNext (`@opennextjs/cloudflare` `^1.20.16`, `open-next.config.ts`, `wrangler.toml`).
4. **Public Website Structure (`src/app/` & Live Search Index):**
   - Public routes: `/` (Home), `/sobre` (About), `/portfolio` (Showcase), `/projects/[slug]` (Project Case detail), `/o-que-me-move` (Manifesto/Editorial), `/contato` (Contact), `/privacidade`, `/qr-scanner` (PWA utility).
   - Admin & Auth routes tightly coupled in the same app: `/admin` and `/auth`.
   - Central narrative motto on live site: *"Você não vê tudo o que eu faço. Mas sente quando funciona."* / Ghost System motto: *"You don't see design. But it sees you."*
   - Three current portfolio showcase categories on live site: **Brand & Campaigns**, **Videos & Motions**, **Websites & Tech** (15 published projects).
   - Verified client roster referenced in public portfolio: Swift, Nestlé, Nivea, Ambev, Zé Delivery, Pernod Ricard, Algar Telecom, Mapfre, AON, O Boticário, Grupo Iguatemi, Unilever.
5. **Existing Design System (`.context/GHOST-DESIGN-SYSTEM.md` v3.2 & `src/app/globals.css`):**
   - Palette: `bluePrimary` (`#0048ff`), `blueAccent` (`#4fe6ff`), `pinkDetails` (`#f501d3`), `purpleDetails` (`#8705f2` hover/anomaly only), `background` / Void Black (`#040013`), `neutral` (`#0b0d3a`), `text` (`#fcffff`), `textSecondary` (`#a1a3a3`), `redAccent` (`#e50914`), `abyssStart` (`#0c1445`), `abyssMid` (`#08031f`).
   - Typography: `Manrope` Variable (200–800) as primary font and `PPSupplyMono` for metadata/code (note: legacy rules in `GEMINI.md` and `design-auditor.md` still mention `'TT Norms Pro'`, `'Outfit'`, or `'Playfair Display'`, whereas `globals.css` and `GHOST-DESIGN-SYSTEM.md` v3.2 standardized on `Manrope` + `PPSupplyMono`).
   - Z-index governance: 19 semantic layers (`--z-layer-base: 0` through `--z-layer-cursor: 110`, plus `--z-layer-preloader: 1000`).
   - Motion constants: `GHOST_EASE` (`[0.22, 1, 0.36, 1]`), `GHOST_EASE_SOFT` (`[0.25, 1, 0.5, 1]`), `GHOST_EASE_HEAVY` (`[0.43, 0.13, 0.23, 0.96]`), `GHOST_EASE_AMBIENT` (`[0.17, 0.55, 0.55, 1]`).
6. **Existing Data Model Fragmentation (`supabase/schema.sql` & `src/types/`):**
   - Coexistence of overlapping tables: `portfolio_projects`, `projects`, `landing_pages`, `experiences`, `site_assets`, `portfolio_tags`, `portfolio_project_tags`, `client_errors`, `audit_log`.
   - Coexistence of 5 case template schemas in `src/types/project-template.ts`: `legacy-blocks`, `master-project-v1`, `master-project-v2`, `master-project-v3-alpa`, and `master-project-v3-alpa-hero`.

### 1.2 Documented Assumptions (Requiring Validation Before Content Migration)

1. **Case Study Strategic Depth:** While 15 projects exist in Supabase (`portfolio_projects` / `landing_pages`), we assume not all 15 currently contain structured fields for *Challenge*, *Strategic Thinking*, *Creative Direction*, and *Verified Impact*—meaning Phase 01/09 content curation will need to enrich priority flagship cases without inventing metrics.
2. **Hosting Consolidation:** The current repo contains both Firebase Hosting adapters and OpenNext Cloudflare configs alongside Vercel conventions; we assume `GHOST-PORTFOLIO-2.0` will deploy to an isolated staging environment first (Vercel or Cloudflare Workers) before any DNS cutover of `portfoliodanilo.com`.
3. **Media Asset Source of Truth:** Both Supabase Storage (`site-assets`, `portfolio-media`) and Cloudflare R2 (`assets.portfoliodanilo.com`) are referenced in `next.config.mjs`. We assume existing media URLs remain read-accessible and will be cataloged via a read-only manifest script before migration.

---

## 2. Current Website & Repository Diagnosis

### 2.1 Existing Capabilities (What Works Well)

| Dimension | Verified Capability | Evidence |
| :--- | :--- | :--- |
| **Visual Identity** | Distinctive "Ghost Era" dark-mode atmospheric aesthetic (`#040013` Void Black + `#0048ff` Brand Blue + `#4fe6ff` Ghost Cyan) | `.context/GHOST-DESIGN-SYSTEM.md`, `src/app/globals.css` |
| **Fluid Typography & Mobile Safety** | Comprehensive `clamp()` scale with dedicated `--font-body-mobile` (20–22px) and iOS notch safe-area insets | `src/app/globals.css` lines 105–218 |
| **Z-Index Discipline** | Strict 19-layer CSS variable stacking system preventing modal/header/canvas collisions | `src/app/globals.css` lines 71–92 |
| **Security Headers** | Strict Content-Security-Policy (CSP), `X-Frame-Options: DENY`, `nosniff`, and domain allowlists | `next.config.mjs` lines 70–250 |
| **Multi-Agent Foundation** | 18 documented agents in `.agents/AGENTS_MANIFEST.md` and mature audit skills (`auditoria-estrategica-portfolio`, `design-auditor`) | `.agents/AGENTS_MANIFEST.md` |

### 2.2 Technical Limitations & Architectural Debt in `PORTFOLIO-DANILO-FINAL`

1. **Monolithic Coupling of Admin CMS & Public Experience:**
   - `/admin`, `/auth`, `/qr-scanner`, and CRUD mutation scripts live inside the same runtime bundle and dependency tree as the public portfolio, inflating dependencies (`react-hook-form`, `html5-qrcode`, `openai`, `@aws-sdk/client-s3`, `pg`) and complicating SSR caching.
2. **Schema & Template Fragmentation (5 Template Versions + 3 Project Tables):**
   - `src/types/project-template.ts` maintains five different template schemas (`legacy-blocks`, `v1`, `v2`, `v3-alpa`, `v3-alpa-hero`), while `supabase/schema.sql` contains both `portfolio_projects` + `landing_pages` AND a separate `projects` table.
3. **Infrastructure & Tooling Sprawl:**
   - Root directory contains 15+ hidden agent/tool folders (`.1code`, `.Jules`, `.claude-flow`, `.qwen`, `.serena`, `.squirrel_home`, `.firebase-cache`), SQL dumps in git root (`backup.sql`, `migration-backup.sql`, `migration-d1-full.sql`), and overlapping deployment targets (Firebase + Cloudflare OpenNext).
4. **TypeScript Memory Overhead:**
   - `typecheck` requires `NODE_OPTIONS='--max-old-space-size=8192'` due to massive dependency graphs (Three.js + R3F + OpenAI + AWS SDK + Playwright + Admin types in a single tsconfig scope).
5. **WebGL vs. Editorial Hierarchy:**
   - As documented in `.agents/skills/auditoria-estrategica-portfolio/SKILL.md`, the WebGL layer in the Hero can compete with editorial legibility and impact Mobile LCP/INP if not strictly budget-gated and isolated.
6. **Documentation Drift on Typography:**
   - Older agent rules (`GEMINI.md`, `design-auditor.md`) reference `'TT Norms Pro'`, `'Inter Tight'`, and `'Playfair Display'`, whereas the actual production code (`tailwind.config.ts`, `globals.css`, `GHOST-DESIGN-SYSTEM.md` v3.2) uses `Manrope` Variable + `PPSupplyMono`.

### 2.3 Creative & Strategic Opportunities

1. **Repositioning from "Portfolio Showcase" to "Executive Creative & Tech Ecosystem":**
   - Shift the immediate narrative from a catalog of deliverables to **Strategic Thinking**, **Creative Leadership (Head of Creation / Creative Director)**, and **Creative Technology & Generative AI**.
2. **Modular Editorial Case Architecture:**
   - Replace fragmented v1/v2/v3 JSON blobs with a single, strongly typed, composable **8-Stage Editorial Case System** (Hero → Overview → Strategic Thinking → Creative Development → Experience → Results → Credits → Next Project).
3. **Dedicated Executive & Innovation Territories:**
   - Introduce `/expertise` (Strategic Leadership & Operations), `/creative-technology` (Generative AI, WebGL, Agentic Systems), `/curriculo` (Executive CV), and `/lab` (Experimental R&D) alongside `/sobre` and `/portfolio`.
4. **Static-First Public Rendering with On-Demand Revalidation:**
   - Decouple public rendering from live database latency using Next.js 16 `generateStaticParams` + tagged cache (`unstable_cache` / `revalidateTag`) + validated local/snapshot fallback so the public site renders instantaneously even if Supabase is unreachable.

---

## 3. Reusable Assets & Knowledge Hub Inventory

### 3.1 Reusable Creative & Data Assets (`PORTFOLIO-DANILO-FINAL`)

- **Supabase Storage Buckets (Read-Only Reuse):** `site-assets` and `portfolio-media` on `umkmwbkwvulxtdodzmzf.supabase.co` and `assets.portfoliodanilo.com`.
- **15 Published Projects & Brand Logos:** Existing project metadata, covers, landscape/square variants, video previews, and client logos (Swift, Nestlé, Nivea, Ambev, Zé Delivery, Pernod Ricard, Algar Telecom, Mapfre, AON, O Boticário, Grupo Iguatemi, Unilever).
- **Ghost Design System v3.2 Tokens:** Color palette (`#040013`, `#0048ff`, `#4fe6ff`, `#0b0d3a`, `#fcffff`), `GHOST_EASE` curves, 19-layer z-index scale, and `<AntigravityCTA />` interaction choreography.
- **Custom Shaders & 3D Primitives:** GLSL shaders (`*.glsl`, `*.vert`, `*.frag`), `Grainient.tsx`, and `GhostCursor.tsx` (to be refactored with strict performance budgets and reduced-motion guards).

### 3.2 Reusable Capabilities from `Agent-Skills-Knowledge-Hub`

We inspected `REPOSITORY_INDEX.md`, `SKILLS-E-AGENTS/`, and `.agents/` in `Agent-Skills-Knowledge-Hub`. The following high-priority packages will be reused and adapted rather than reinvented:

| Knowledge Hub Package | Source Path | Application in `GHOST-PORTFOLIO-2.0` |
| :--- | :--- | :--- |
| **Portfolio Design Auditor Suite** | `portfolio-context-analyst.md`, `design-auditor.md`, `implementation-planner.md`, `audit-validator.md`, `auditoria-estrategica-portfolio` | Direct foundation for `portfolio-context`, `portfolio-ux-audit`, and `visual-regression` skills |
| **Taste Skill (Anti-Slop Frontend)** | `curated-knowledge/taste-skill/` & `design-taste-frontend` | Enforces editorial minimalism, anti-generic layout rules, and purposeful motion in `art-direction` and `component-engineering` |
| **Spec-Kit (Spec-Driven Development)** | `curated-knowledge/spec-kit/` & `SKILLS-E-AGENTS/projetos especiais/SPDD/` | Powers `.specify/` directory structure and the PREVC workflow specification gates |
| **Superpowers (TDD & Verification)** | `curated-knowledge/superpowers/` & `verification-before-completion` | Enforces evidence-based quality gates (`PASS` / `FAIL` / `NOT VERIFIED`) |
| **Crear Design System (DTCG / OKLCH)** | `SKILLS-E-AGENTS/plugins/criar-design-system/` | Guides token governance and contrast validation in Ghost Design System 2.0 |
| **GSAP & Motion Choreography Suite** | `gsap-core`, `gsap-scrolltrigger`, `framer-motion`, `animation-vocabulary` | Consolidated into the `motion-engineering` skill with progressive disclosure references |
| **Three.js & R3F Optimization Suite** | `ghost-r3f-optimization`, `threejs-shaders`, `3d-webgl-scene` | Consolidated into the `threejs-experience` skill with 60fps and fallback mandates |
| **Supabase Core & Media Pipeline** | `supabase-auth-storage-realtime-core`, `supabase-media-pipeline` | Consolidated into `media-optimization` and backend data access patterns |

---

## 4. Migration Risks & Mitigation Matrix

| Risk ID | Risk Description | Severity | Mitigation Strategy |
| :--- | :--- | :--- | :--- |
| **RISK-01** | **Production Contamination:** Accidental writes to production Supabase tables or buckets used by `portfoliodanilo.com`. | **CRITICAL** | `GHOST-PORTFOLIO-2.0` uses a strictly read-only/snapshot data layer in Phase 1 or isolated `v2_*` schema/views; zero destructive SQL or storage mutations without human approval. |
| **RISK-02** | **Case Content Thinness:** Existing projects in DB have visual galleries but lack structured narrative fields (Challenge, Strategy, Concept). | **HIGH** | Design the Case Study Builder schema with optional progressive blocks so existing visual-heavy cases render cleanly while flagship cases showcase full strategic depth. |
| **RISK-03** | **WebGL Mobile Thermal/LCP Degradation:** Heavy shaders blocking main thread on mid-tier mobile devices. | **HIGH** | Isolate `<Canvas>` in lazy-loaded boundaries, cap `dpr={[1, 1.5]}` on mobile, pause off-screen loops via `IntersectionObserver`, and provide instant CSS/poster fallback. |
| **RISK-04** | **Font & Token Drift:** Conflicting references to `TT Norms Pro` vs `Manrope` across legacy agent prompts. | **MEDIUM** | Standardize Ghost Design System 2.0 on `Manrope Variable` + `PPSupplyMono` (matching live v3.2 CSS) with explicit token lint rules. |
| **RISK-05** | **IDE Configuration Sprawl:** 10+ hidden agent directories polluting repository root as seen in `PORTFOLIO-DANILO-FINAL`. | **MEDIUM** | Centralize all canonical intelligence in `.agents/` and `.context/`, using lightweight root adapter pointers (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `.cursorrules`). |

