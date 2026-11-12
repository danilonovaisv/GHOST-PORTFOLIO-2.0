# WORKFLOW 03 — UX & INFORMATION ARCHITECTURE

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/ux-architecture` or Phase 02 UX initialization.
- **Required Context:** `.context/PRODUCT-STRATEGY.md`, `.context/CONTENT-STRATEGY.md`.
- **Participating Agents:** `AG-02` (UX Architect), `AG-01` (Creative Strategist), `AG-12` (SEO Engineer).
- **Required Skills:** `portfolio-ux-audit`, `seo-optimization`.
- **Tools:** `read_file`, `write_file`, `edit_file`.
- **Execution Sequence:**
  1. `PLANNING`: Map the 9 core routes (`/`, `/sobre`, `/portfolio`, `/projetos/[slug]`, `/expertise`, `/creative-technology`, `/lab`, `/curriculo`, `/contato`) and legacy 308 redirects.
  2. `REVIEW`: Verify conversion paths (`≤ 2 clicks` to CV, cases, and contact) with `AG-01` and `AG-12`.
  3. `EXECUTION`: Author `.context/INFORMATION-ARCHITECTURE.md` with section flows and navigation state machines.
  4. `VALIDATION`: Verify mobile-first menu ergonomics and URL continuity for `/projects/[slug]`.
  5. `CONFIRMATION`: Submit `INFORMATION-ARCHITECTURE.md` for human approval.
- **Dependencies:** `02-creative-strategy.md`.
- **Approval Gates:** Human sign-off on route map and Home 9-section flow.
- **Failure Conditions:** Broken legacy URLs or Home page reduced to a mere thumbnail catalog.
- **Recovery Strategy:** Add explicit `308` redirect rules and restore the 9-section executive Home architecture.
- **Validation:** Route & redirect coverage check (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** `.context/INFORMATION-ARCHITECTURE.md` approved.

