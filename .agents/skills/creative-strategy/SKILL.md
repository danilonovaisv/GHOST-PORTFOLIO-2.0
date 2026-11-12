---
name: creative-strategy
version: 2.0.0
origin: Adapted from brand_strategist & auditoria-estrategica-portfolio in Agent-Skills-Knowledge-Hub
description: Aligns portfolio narratives, executive positioning, and value propositions with Danilo Novais's leadership pillars (Strategy, Creative Leadership, Creative Tech & AI).
---

# Creative Strategy Skill (`creative-strategy`)

## 1. Purpose
Ensure every page, headline, and case study positions Danilo Novais as a **Senior Creative Director, Head of Creation, Creative Strategist, and Creative Technologist** rather than merely a visual executor.

## 2. When to Use
- When drafting or reviewing positioning statements, Home manifesto sections, `/sobre`, `/expertise`, `/curriculo`, or case study strategic overviews.

## 3. When Not to Use
- Do not use for technical debugging, CSS token maintenance, or infrastructure deployment.
- Never use to fabricate metrics, client names, or unverified business outcomes.

## 4. Input Contract
- `target_page_or_case`: Route or project slug.
- `verified_facts`: Authentic project metadata, client context, and roles from `DISCOVERY_REPORT.md` or `src/lib/data/`.

## 5. Operational Instructions (Progressive Disclosure)
1. **Anchor in the 3 Executive Pillars:** Verify that the copy communicates (a) Strategic Thinking, (b) Creative Leadership/Operations, and (c) Technological Fluency.
2. **Audience Calibration:** Check alignment against the 4 target personas in `.context/PRODUCT-STRATEGY.md` (CMOs/C-Level, Founders/Tech Leaders, Agencies/Recruiters, Creative Peers).
3. **Territory Mapping:** Classify work accurately under `branding`, `campaign`, `motion`, `web`, or `creative-technology`.
4. **Deep Reference:** Load `.context/PRODUCT-STRATEGY.md` and `.context/CONTENT-STRATEGY.md` when structuring new narratives.

## 6. Output Contract
- **Positioning Thesis**
- **Headline & Narrative Copy (`pt-BR` / `en-US`)**
- **Pillar Alignment Check (Strategy / Leadership / Tech)**
- **Factual Traceability Confirmation**

## 7. Validation Criteria
- Zero generic clichés; 100% factual traceability; clear executive voice (*"Presence without noise"*).

