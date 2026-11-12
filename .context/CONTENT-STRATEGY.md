# CONTENT STRATEGY — GHOST PORTFOLIO 2.0

**Phase:** 01 — Creative Strategy & Narrative Architecture  
**Active Personas:** Content Strategist (`AG-05`), Creative Strategist (`AG-01`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Core Editorial Principle: Strategy Before Aesthetics

In `PORTFOLIO-DANILO-FINAL`, several projects functioned primarily as visual galleries or modal previews. In `GHOST-PORTFOLIO-2.0`, every project and institutional page is structured to answer **why** a decision was made, **how** creative leadership shaped the outcome, and **what** tangible value was delivered—while strictly obeying **Rule #6: Never invent project results, clients, metrics, or professional achievements.**

---

## 2. Voice, Tone & Editorial Taxonomy

### 2.1 Voice Attributes
- **Executive & Articulate:** Speaks the language of business transformation, brand equity, and creative operations—not just software tools.
- **Minimal & Precise:** Short, high-density paragraphs. Zero fluff, zero clichés, zero AI-generated filler adjectives.
- **Reflective & Authorial:** Preserves Danilo's authentic voice (*"Você não vê tudo o que eu faço. Mas sente quando funciona."*).

### 2.2 Language Strategy
- **Primary Language:** Portuguese (`pt-BR`), matching the current production portfolio and core executive market, with architecture prepared for optional `en-US` internationalization dictionary support in `src/lib/i18n/` without restructuring routes.

---

## 3. The 8-Stage Modular Case Study Framework

Every case study under `/projetos/[slug]` is composed from an 8-stage narrative arc. Because existing legacy projects have varying levels of text vs. visual documentation, stages 01, 02, 05, 07, and 08 are **Mandatory Core Stages**, while stages 03, 04, and 06 are **Composable Narrative Modules** that render when verified data is present:

```text
PROJECT CASE ARCHITECTURE
│
├── 01. HERO (Mandatory)
│   ├── Project Title & Subtitle
│   ├── Client Name & Official Brand Emblem
│   ├── Strategic Territory & Year (PPSupplyMono)
│   ├── Services / Role Tags (e.g., Creative Direction, Brand Strategy, Motion)
│   └── Hero Media Stage (Image, Video Loop, or Isolated Interactive HTML/WebGL)
│
├── 02. PROJECT OVERVIEW (Mandatory)
│   ├── Executive Summary (2–3 sentences)
│   ├── Context & Market Moment
│   └── The Core Challenge & Objectives
│
├── 03. STRATEGIC THINKING (Composable — Flagship Cases)
│   ├── Cultural / Business Insights
│   ├── Strategic Proposition
│   └── Creative Direction Mandate
│
├── 04. CREATIVE DEVELOPMENT (Composable — Flagship Cases)
│   ├── Core Concept & Manifesto
│   ├── Art Direction & Visual System
│   └── Technical / Craft Execution
│
├── 05. EXPERIENCE & MEDIA SHOWCASE (Mandatory)
│   ├── Full-Bleed Cinematic Frames
│   ├── Asymmetric 2-Column & 3-Column Editorial Grids
│   ├── On-Demand Video Showcases & Motion Breakdowns
│   ├── Typography / Identity Specimens
│   └── Interactive / WebGL Embeds
│
├── 06. DELIVERABLES & VERIFIED IMPACT (Composable)
│   ├── Scope of Deliverables Shipped
│   └── Verified Qualitative / Quantitative Outcomes (Strictly factual; zero fabricated KPIs)
│
├── 07. CREDITS & GOVERNANCE (Mandatory)
│   ├── Danilo's Role (e.g., Creative Direction, Art Direction, Motion)
│   └── Agency / Partner / Production Credits
│
└── 08. NEXT PROJECT CONTINUITY (Mandatory)
    └── Curated Next Case Teaser with Instant Preload
```

---

## 4. Content Curation & Migration Policy (15 Existing Projects)

### Tier 1 — Flagship Strategic Cases (Featured on Home & Top of Portfolio)
Projects with rich strategic context and multi-disciplinary execution (e.g., *Magic — Devolvendo a magia ao rádio*, major brand campaigns, interactive web experiences) receive full 8-stage editorial treatment.

### Tier 2 — Visual & Craft Showcases
Projects focused on specific craft excellence (e.g., *Key Visuals*, *Motion Pieces*, *Specific Identity Explorations*) use a streamlined 5-stage composition (`01. Hero` → `02. Overview` → `05. Experience Showcase` → `07. Credits` → `08. Next Project`) so they feel intentionally concise rather than incomplete.

---

## 5. Content Governance Rules

1. **Fact-Only Rule:** Every client name, year, role, and outcome must trace directly to `PORTFOLIO-DANILO-FINAL` database records (`portfolio_projects`, `landing_pages`, `experiences`) or explicit author input.
2. **Confidential Client Handling:** Projects marked as *Cliente Confidencial* preserve confidentiality while clearly articulating the industry sector, strategic challenge, and creative solution.
3. **Structured Content Validation:** All content files and Supabase payloads must pass Zod schema validation (`src/lib/validation/content-schema.ts`) at build time before any page is generated.

