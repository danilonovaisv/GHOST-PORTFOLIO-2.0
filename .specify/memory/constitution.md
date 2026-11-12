# SPEC-DRIVEN DEVELOPMENT CONSTITUTION (`.specify/memory/constitution.md`)

**System:** GHOST-PORTFOLIO-2.0  
**Methodology:** Spec-Kit + PREVC Protocol

1. **Specification Before Code:** No component, route, or migration script may be implemented without an approved specification in `.context/` or `.specify/specs/`.
2. **Single Source of Tokens:** All visual styling must consume CSS variables defined in `@theme` (`src/styles/globals.css`) per `.context/DESIGN-SYSTEM.md`.
3. **Strict Type & Schema Contracts:** All data entering the UI must be validated by Zod schemas in `src/lib/validation/`.
4. **Evidence-Based Verification:** No task reaches `COMPLETED` until its applicable Quality Gates (`QG-01` through `QG-15`) report `PASS` with execution logs.

