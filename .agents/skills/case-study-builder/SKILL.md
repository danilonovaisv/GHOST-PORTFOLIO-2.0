---
name: case-study-builder
version: 2.0.0
origin: Adapted from review-project-case-page in PORTFOLIO-DANILO-FINAL & content-creator in Agent-Skills-Knowledge-Hub
description: Structures and validates modular 8-stage portfolio case studies (/projetos/[slug]) using composable editorial blocks and Zod schemas.
---

# Case Study Builder Skill (`case-study-builder`)

## 1. Purpose
Transform raw project data and legacy templates (`v1`, `v2`, `v3-alpa`, `v3-alpa-hero`) into cohesive, modular 8-stage editorial case studies.

## 2. When to Use
- When creating, migrating, or auditing project case studies under `/projetos/[slug]` and `src/lib/data/content/projects/`.

## 3. When Not to Use
- Never fabricate project challenges, strategies, or metrics not supported by source records or human authorship.

## 4. Input Contract
- `project_source`: Legacy `portfolio_projects` + `landing_pages` record or author brief.
- `case_tier`: `'flagship'` (full 8-stage narrative) or `'showcase'` (streamlined 5-stage visual narrative).

## 5. Operational Instructions (Progressive Disclosure)
1. **Map the 8 Stages:**
   - `01. Hero` → Title, Client, Territory, Year, Hero Media
   - `02. Overview` → Executive summary, Context, Challenge
   - `03. Strategic Thinking` *(Flagship)* → Insights, Strategy, Direction
   - `04. Creative Development` *(Flagship)* → Concept, Art Direction, Execution
   - `05. Experience Showcase` → Composable `ProjectSection[]` blocks (`fullbleed-media`, `narrative-split`, `media-grid`, `video-showcase`, `quote-band`, `interactive-embed`)
   - `06. Results & Deliverables` *(When verified)* → Shipped scope & factual outcomes
   - `07. Credits` → Role & partner credits
   - `08. Next Project` → Curated sequential slug
2. **Validate Schema:** Run Zod validation (`ProjectSchema.parse()`) on the resulting structure.
3. **Deep Reference:** Load `.context/CONTENT-STRATEGY.md` and `.context/DATABASE-SCHEMA.md` for TypeScript contracts.

## 6. Output Contract
- Schema-valid `Project` object ready for rendering by `<CaseBlockRenderer />`.

## 7. Validation Criteria
- Passes `QG-03` (`pnpm validate:content`) with 100% valid asset references and zero fabricated claims.

