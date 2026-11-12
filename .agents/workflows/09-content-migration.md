# WORKFLOW 09 — CONTENT MIGRATION & CASE CURATION

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/migrate-content` or Phase 12 Content & Asset Migration.
- **Required Context:** `.context/CONTENT-STRATEGY.md`, `.context/DATABASE-SCHEMA.md`, `.context/ASSET-MANIFEST.md`, `docs/research/DISCOVERY_REPORT.md`.
- **Participating Agents:** `AG-05` (Content Strategist), `AG-10` (Backend Engineer), `AG-11` (Media Pipeline Engineer).
- **Required Skills:** `case-study-builder`, `media-optimization`.
- **Tools:** `read_file`, `write_file`, `edit_file`, `run_command` (`tsx scripts/migrate-content.ts`, `tsx scripts/audit-assets.ts`).
- **Execution Sequence:**
  1. `PLANNING`: Read legacy project records (`portfolio_projects`, `landing_pages`, `experiences`, `site_assets`) in read-only mode.
  2. `REVIEW`: Classify the 15 projects into Flagship (8-stage) vs. Showcase (5-stage) tiers and verify zero fabricated metrics (`Law #4`).
  3. `EXECUTION`: Transform legacy v1/v2/v3 payloads into unified `Project` records (`src/lib/data/content/projects/`) and verify every asset URL via `scripts/audit-assets.ts`.
  4. `VALIDATION`: Run `QG-03` (`pnpm validate:content`) and `QG-10`/`QG-11` (100% of asset URLs return HTTP `200 OK`).
  5. `CONFIRMATION`: Present migrated case catalog for human review.
- **Dependencies:** `07-backend-development.md`.
- **Approval Gates:** Human review of curated case narratives before publishing.
- **Failure Conditions:** Any `404` asset URL, Zod schema failure, or unverified claim.
- **Recovery Strategy:** Map missing asset paths using `.context/ASSET-MANIFEST.md` and strip any unverified text fields.
- **Validation:** `QG-03`, `QG-10`, `QG-11` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** All 15 projects and career experiences validated and mapped into `GHOST-PORTFOLIO-2.0`.

