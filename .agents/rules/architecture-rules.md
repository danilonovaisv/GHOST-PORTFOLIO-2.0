# ARCHITECTURE RULES — GHOST PORTFOLIO 2.0

1. **Server Components by Default:** Every route `page.tsx`, `layout.tsx`, and editorial block in `src/` must be a React Server Component unless browser APIs/hooks require `'use client'` in a leaf component.
2. **Error Boundary Mandate:** Every route segment under `src/app/(website)/` must include an `error.tsx` client boundary, and every WebGL `<Canvas>` must be wrapped in `<WebGLBoundary fallback={...}>`.
3. **Strict Data Validation:** All content loaded from Supabase or local snapshots must pass Zod validation (`src/lib/validation/`) before rendering.
4. **Zero Unapproved Dependencies:** Do not add packages to `package.json` without architectural justification in `.context/DECISION-LOG.md` and human approval.
5. **Context7 Verification:** Always query Context7 when implementing Next.js 16, React 19, Tailwind CSS v4, or Supabase SSR patterns.

