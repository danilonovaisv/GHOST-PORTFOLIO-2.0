---
name: threejs-experience
version: 2.0.0
origin: Consolidated from ghost-r3f-optimization, threejs-shaders & 3d-webgl-scene in PORTFOLIO-DANILO-FINAL and Agent-Skills-Knowledge-Hub
description: Architects isolated, GPU-budgeted Three.js / React Three Fiber scenes and GLSL shaders with mandatory WebGL fallback and 60fps enforcement.
---

# Three.js & WebGL Experience Skill (`threejs-experience`)

## 1. Purpose
Create atmospheric, high-performance 3D and shader experiences (`Grainient`, spectral fields, `/lab` studies) that elevate the Ghost aesthetic without degrading Core Web Vitals or crashing low-power devices.

## 2. When to Use
- When developing or auditing components in `src/components/three/`, custom GLSL shaders, or interactive 3D showcases in `/creative-technology` and `/lab`.

## 3. When Not to Use
- Never import `three` or `@react-three/fiber` directly into Server Components or global synchronous bundles.

## 4. Input Contract
- `scene_spec`: Target scene component, shader uniforms, z-layer placement, and fallback visual.

## 5. Operational Instructions (Progressive Disclosure)
1. **Dynamic Island Isolation:** Always load `<Canvas>` scenes via `next/dynamic(..., { ssr: false })` wrapped inside `<WebGLBoundary fallback={<AtmosphericCSSFallback />}>`.
2. **GPU & DPR Budgeting:** Set `dpr={[1, 1.5]}` on mobile and `dpr={[1, 2]}` on desktop; pause `useFrame` loops via `IntersectionObserver` when the canvas scrolls out of view.
3. **Z-Layer Discipline:** Position ambient canvases strictly at `--z-layer-base: 0` or `--z-layer-3d: 15–30` behind foreground text (`--z-layer-content: 20+`).
4. **Memory Hygiene:** Dispose geometries, materials, and textures on unmount; handle `webglcontextlost` events gracefully.
5. **Deep Reference:** Load `.context/MEDIA-ARCHITECTURE.md` (§4 WebGL Performance Budget).

## 6. Output Contract
- Lazy-loaded, context-loss-resilient R3F/Three.js scene component with verified HTML/CSS fallback.

## 7. Validation Criteria
- Passes `QG-12` (60fps desktop / ≥ 50fps mobile, graceful fallback on WebGL disable) and `QG-13` (pauses or falls back under `prefers-reduced-motion: reduce`).

