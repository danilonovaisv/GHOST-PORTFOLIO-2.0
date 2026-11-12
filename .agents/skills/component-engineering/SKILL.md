---
name: component-engineering
version: 2.0.0
origin: Adapted from tailwind-patterns, clean-code & react-best-practices in Agent-Skills-Knowledge-Hub
description: Guides modular React 19 + Tailwind CSS v4 component implementation with strict TypeScript contracts, accessibility states, and responsive grid alignment.
---

# Component Engineering Skill (`component-engineering`)

## 1. Purpose
Build reusable, composable, accessible React 19 components that strictly adhere to Ghost Design System 2.0 and `.context/COMPONENT-ARCHITECTURE.md`.

## 2. When to Use
- When implementing or refactoring components in `src/components/ui/`, `typography/`, `layout/`, `navigation/`, `home/`, `portfolio/`, or `projects/`.

## 3. When Not to Use
- Do not couple presentation components directly to Supabase client queries; pass validated data via props.

## 4. Input Contract
- `component_spec`: Component name, boundary (`Server` or `Client`), props interface, and visual/interaction states.

## 5. Operational Instructions (Progressive Disclosure)
1. **Boundary Discipline:** Default to Server Components. Add `'use client'` only to leaf components that require browser hooks (`useState`, `useEffect`, pointer/keyboard listeners, Motion/GSAP).
2. **Complete State Matrix:** Every interactive element must implement `default`, `hover`, `focus-visible` (`ring-2 ring-[#4FE6FF]`), `active`, and `disabled` states.
3. **Mobile-First Responsive Layout:** Build for `375px` (`4-col` `.std-grid`) first, scaling up via `md:` (`8-col`) and `lg:` (`12-col`). Include `.flex > * { min-width: 0 }` protection against text overflow.
4. **Deep Reference:** Load `.context/COMPONENT-ARCHITECTURE.md` and `.context/DESIGN-SYSTEM.md`.

## 6. Output Contract
- Clean, documented, strictly-typed `.tsx` component with zero ESLint or TypeScript warnings.

## 7. Validation Criteria
- Passes `QG-01` (TypeScript), `QG-02` (ESLint), `QG-06` (Responsive matrix), and `QG-07` (Accessibility).

