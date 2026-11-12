# QUALITY RULES — GHOST PORTFOLIO 2.0

1. **Three-State Reporting Mandate:** Every validation check (`QG-01` through `QG-15`) must report `PASS`, `FAIL`, or `NOT VERIFIED`.
2. **Zero Unverified Claims:** Never report a test, build, Lighthouse score, or accessibility audit as `PASS` without attaching actual command execution output.
3. **Mandatory Pre-Confirmation Pipeline:** Before transitioning any workflow to `HUMAN_CONFIRMATION`, verify:
   - `QG-01`: `pnpm typecheck` (`0` errors)
   - `QG-02`: `pnpm lint` (`0` errors)
   - `QG-03` & `QG-04`: `pnpm test` (`100%` pass)
   - `QG-05` & `QG-06`: `pnpm test:e2e` & multi-viewport responsive check (`375px–1920px`)
   - `QG-07` & `QG-13`: WCAG 2.2 AA & `prefers-reduced-motion` check
   - `QG-15`: `pnpm build` succeeds cleanly

