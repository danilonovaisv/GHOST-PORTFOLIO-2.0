# WORKFLOW 05 — PROTOTYPING & VISUAL VALIDATION

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/prototype` or Phase 04 Visual Validation.
- **Required Context:** `.context/DESIGN-SYSTEM.md`, `.context/CREATIVE-DIRECTION.md`, `.context/INFORMATION-ARCHITECTURE.md`.
- **Participating Agents:** `AG-03` (Art Director), `AG-07` (UI Engineer), `AG-08` (Motion Engineer), `AG-17` (Visual QA Agent).
- **Required Skills:** `art-direction`, `ghost-design-system`, `component-engineering`, `visual-regression`.
- **Tools:** `read_file`, `write_file`, `edit_file`, Playwright MCP / Chrome DevTools MCP.
- **Execution Sequence:**
  1. `PLANNING`: Select key archetype views to prototype first: Home Hero + Selected Works (`/`), Portfolio Exhibition (`/portfolio`), and 1 Flagship Case Study (`/projetos/[slug]`).
  2. `REVIEW`: Review layout grid proportions and typographic hierarchy with `AG-03`.
  3. `EXECUTION`: Build interactive layout prototypes using real assets from `.context/ASSET-MANIFEST.md`.
  4. `VALIDATION`: Inspect across `375px`, `768px`, and `1440px` viewports with `AG-17` (`QG-06`).
  5. `CONFIRMATION`: Present visual prototypes to Danilo Novais for approval before scaling across all routes.
- **Dependencies:** `04-design-system.md`.
- **Approval Gates:** **Mandatory Human Visual Gate** — Do not proceed to full multi-route engineering until the visual prototype of Home and Case Study is approved.
- **Failure Conditions:** Generic layout feel, WebGL obscuring text, or broken mobile proportions.
- **Recovery Strategy:** Refine grid asymmetry, negative space, and z-layer opacity per `AG-03` critique.
- **Validation:** `QG-06` & `QG-07` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** Human sign-off on visual prototype fidelity.

