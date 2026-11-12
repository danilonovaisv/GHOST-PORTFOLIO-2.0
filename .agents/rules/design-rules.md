# DESIGN RULES — GHOST DESIGN SYSTEM 2.0

1. **Canonical Palette:** Use Void Black (`#040013`), Deep Neutral (`#0B0D3A`), Brand Blue (`#0048FF`), Ghost Cyan (`#4FE6FF`), Text Primary (`#FCFFFF`), and Text Secondary (`#B4B8C5`). Never use `#000000` or dominant purple surfaces (`#8705F2` is restricted to hover/anomaly states).
2. **Canonical Typography:** Use `Manrope` Variable (`--font-sans`) with fluid `clamp()` tokens and `PPSupplyMono` (`--font-mono`) for metadata/coordinates.
3. **Grid & Negative Space:** Wrap major sections in `<StandardGrid />` (`.std-grid`: `4 / 8 / 12` columns, `max-w-[1680px]`). Preserve `≥ 35%` negative space per viewport.
4. **Z-Index Discipline:** Never use raw `z-[nnn]` classes; always use semantic `--z-layer-*` tokens (`0`–`110`). WebGL canvases must stay behind `--z-layer-content: 20`.
5. **Motion Vocabulary:** Import `GHOST_EASE` (`[0.22, 1, 0.36, 1]`) from `src/config/motion.ts`. Respect `prefers-reduced-motion: reduce` on 100% of animations.

