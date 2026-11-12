# WORKFLOW 08 — MOTION, INTERACTION & WEBGL DEVELOPMENT

**Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

- **Trigger:** `/motion-dev` or Phase 08 Motion & 3D Engineering.
- **Required Context:** `.context/DESIGN-SYSTEM.md` (§5 Motion), `.context/MEDIA-ARCHITECTURE.md` (§4 WebGL), `.context/CREATIVE-DIRECTION.md`.
- **Participating Agents:** `AG-08` (Motion Engineer), `AG-09` (Creative Tech Engineer), `AG-03` (Art Director), `AG-13` (Accessibility Auditor), `AG-14` (Performance Auditor).
- **Required Skills:** `motion-engineering`, `threejs-experience`, `accessibility-audit`, `performance-audit`.
- **Tools:** `read_file`, `write_file`, `edit_file`, Context7 MCP, Chrome DevTools MCP.
- **Execution Sequence:**
  1. `PLANNING`: Define motion choreography (`GHOST_EASE`, `<GhostReveal />`, `<AntigravityCTA />`, Lenis sync) and isolated R3F `<Canvas>` boundaries (`<WebGLBoundary />`).
  2. `REVIEW`: Verify z-layer separation (`--z-layer-3d < --z-layer-content`) with `AG-03` and reduced-motion fallbacks with `AG-13`.
  3. `EXECUTION`: Implement `src/components/motion/**` and `src/components/three/**` with `IntersectionObserver` loop pausing and `dpr` caps.
  4. `VALIDATION`: Execute `QG-12` (60fps frame rate & WebGL context-loss fallback) and `QG-13` (`prefers-reduced-motion: reduce` emulation).
  5. `CONFIRMATION`: Record motion & WebGL verification logs.
- **Dependencies:** `04-design-system.md`, `06-frontend-development.md`.
- **Approval Gates:** Human sign-off on Hero atmosphere and interaction feel.
- **Failure Conditions:** FPS drops `< 50fps` on mobile, missing WebGL fallback, or animations running under `prefers-reduced-motion: reduce`.
- **Recovery Strategy:** Reduce shader octaves/DPR, enforce `frameloop="demand"` when static, and bypass spatial motion when reduced-motion is active.
- **Validation:** `QG-12` & `QG-13` (`PASS` / `FAIL` / `NOT VERIFIED`).
- **Completion Criteria:** All animations and 3D scenes pass 60fps and reduced-motion gates.

