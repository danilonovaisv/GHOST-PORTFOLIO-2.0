---
name: portfolio-context
version: 2.0.0
origin: Adapted from Portfolio Design Auditor (portfolio-context-analyst) in Agent-Skills-Knowledge-Hub
description: Maps GHOST-PORTFOLIO-2.0 architecture, route dependencies, design tokens, and documented vs. implemented state before any design or code modification.
---

# Portfolio Context Skill (`portfolio-context`)

## 1. Purpose
Construct an evidence-based map of the target route, component tree, data dependencies, and Ghost Design System tokens before planning or executing any modification.

## 2. When to Use
- At the start of any `DISCOVERY` or `PLANNING` step in the PREVC protocol.
- Before auditing or refactoring any route under `src/app/` or component under `src/components/`.

## 3. When Not to Use
- Do not use this skill to modify application source code directly; it is strictly read-and-map.

## 4. Input Contract
- `target`: Route path (e.g., `/projetos/[slug]`), component name, or architectural domain.
- `context_docs`: Relevant files in `.context/` (`INFORMATION-ARCHITECTURE.md`, `DESIGN-SYSTEM.md`, `TECHNICAL-ARCHITECTURE.md`).

## 5. Operational Instructions (Progressive Disclosure)
1. **Check Graph / Context First:** Read `.context/active-state.md` and the domain's specification in `.context/` (or run `graphify query "<target>"` when `graphify-out/graph.json` is present).
2. **Trace Component Tree:** Map `Route Page → Section → Feature Component → UI Primitive → Motion Wrapper → Media Asset`.
3. **Compare Spec vs. Implementation:** Explicitly separate **Documented Specification** (`.context/`) from **Actual Code** (`src/`).
4. **Load Deep References Only as Needed:** Consult `.context/COMPONENT-ARCHITECTURE.md` or `.context/DATABASE-SCHEMA.md` only when data/component boundaries are involved.

## 6. Output Contract
- **Target Route / Module**
- **Specification Sources Consulted**
- **Component & Data Dependency Chain**
- **Spec vs. Implementation Deltas**
- **Verification Risks**

## 7. Validation Criteria
- Every referenced file path and symbol must be verified to exist; zero unverified assumptions.

