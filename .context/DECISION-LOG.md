# ARCHITECTURAL DECISION LOG (ADR) — GHOST PORTFOLIO 2.0

| ADR ID | Date | Decision Title | Decision Summary | Status |
| :--- | :--- | :--- | :--- | :--- |
| **ADR-001** | 2026-11-12 | Clean-Room Repository (`GHOST-PORTFOLIO-2.0`) | Build in a dedicated repository rather than refactoring `PORTFOLIO-DANILO-FINAL` in-place to protect production (`portfoliodanilo.com`) and shed legacy config sprawl. | **PROPOSED (Gate 09)** |
| **ADR-002** | 2026-11-12 | Decouple Public Site from Admin CMS in Phase 1 | Prioritize the public executive portfolio using static generation + validated local/Supabase snapshots first; defer Admin CMS rebuild to Phase 2 after content schemas stabilize. | **PROPOSED (Gate 09)** |
| **ADR-003** | 2026-11-12 | Consolidate 5 Legacy Templates into 1 Block Engine | Replace `legacy-blocks`, `v1`, `v2`, `v3-alpa`, and `v3-alpa-hero` with a single discriminated-union `CaseBlockRenderer` supporting the 8-stage editorial narrative arc. | **PROPOSED (Gate 09)** |
| **ADR-004** | 2026-11-12 | Canonicalize Typography on `Manrope` + `PPSupplyMono` | Resolve documentation drift (`TT Norms Pro` vs `Manrope`) by standardizing on `Manrope Variable` + `PPSupplyMono`, matching the live Ghost System v3.2 CSS tokens. | **PROPOSED (Gate 09)** |
| **ADR-005** | 2026-11-12 | Logical 19-Agent Role Architecture with Selective Activation | Define 19 specialized agent personas organized in 4 tiers, activated on-demand by the Project Orchestrator rather than running 19 concurrent processes. | **PROPOSED (Gate 09)** |
| **ADR-006** | 2026-11-12 | Unified `.agents/` Intelligence with Thin IDE Adapters | Store all canonical agents, skills, rules, and workflows in `.agents/` and `.context/`, exposing thin root pointer files (`AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `.cursorrules`, `.codex/`). | **PROPOSED (Gate 09)** |

