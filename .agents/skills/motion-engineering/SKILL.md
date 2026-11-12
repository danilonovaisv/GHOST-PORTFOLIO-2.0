---
name: motion-engineering
version: 2.0.0
origin: Consolidated from framer-motion, gsap-core, gsap-scrolltrigger & animation-vocabulary in Agent-Skills-Knowledge-Hub
description: Orchestrates 60fps UI transitions, scroll reveals, Lenis smooth scrolling, and Ghost Easing choreography with 100% reduced-motion compliance.
---

# Motion Engineering Skill (`motion-engineering`)

## 1. Purpose
Deliver weightless, purposeful motion ("Motion as breath") across `GHOST-PORTFOLIO-2.0` using canonical Ghost easing curves and strict performance/accessibility guardrails.

## 2. When to Use
- When implementing `<GhostReveal />`, page transitions, `<AntigravityCTA />` micro-interactions, scroll-linked reveals, or Lenis smooth-scroll integration.

## 3. When Not to Use
- Never animate layout properties (`width`, `height`, `top`, `left`, `margin`) or apply `scale` / `bounce` / `rotate` to editorial cards.

## 4. Input Contract
- `target_interaction`: Component or transition type (`reveal`, `hover`, `curtain`, `parallax`).
- `motion_tokens`: Imported from `src/config/motion.ts`.

## 5. Operational Instructions (Progressive Disclosure)
1. **Use Canonical Constants Only:** Always import `GHOST_EASE` (`[0.22, 1, 0.36, 1]`), `GHOST_EASE_SOFT`, `GHOST_EASE_HEAVY`, or `GHOST_EASE_AMBIENT` from `src/config/motion.ts`.
2. **Enforce Content Reveal Limits:** Standard `<GhostReveal />` uses `opacity: 0 → 1`, `y: 18px → 0px` (hard max `18px`), `duration: 0.8s`, `stagger: 0.08s–0.1s`.
3. **Mandatory Reduced Motion Guard:** Check `useReducedMotion()` (Motion) or `window.matchMedia('(prefers-reduced-motion: reduce)')` (GSAP/Lenis). When active, disable spatial translation (`y: 0`), disable smooth-scroll inertia/parallax, and use simple opacity fades.
4. **Cleanup:** Always revert GSAP contexts (`useGSAP()` or `ctx.revert()`) and ScrollTriggers on unmount.
5. **Deep Reference:** Load `.context/DESIGN-SYSTEM.md` (§5 Motion Vocabulary).

## 6. Output Contract
- Compositor-friendly (`transform`, `opacity`), cleanup-safe motion components and hooks.

## 7. Validation Criteria
- `QG-12` (Sustained 60fps) and `QG-13` (`prefers-reduced-motion: reduce` verified via Playwright emulation).

