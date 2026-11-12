# QUALITY GATES & VERIFICATION PROTOCOL — GHOST PORTFOLIO 2.0

**Phase:** 08 — Quality Gates & Verification  
**Active Personas:** QA Engineer (`AG-16`), Accessibility Auditor (`AG-13`), Performance Auditor (`AG-14`), Visual QA Agent (`AG-17`), Security Auditor (`AG-15`), Release Manager (`AG-18`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Evidence-First Reporting Rule

Every quality gate evaluation across all workflows MUST report one of three explicit states:
- **`PASS`** — Verified by actual command execution, test output, or browser inspection log attached to the report.
- **`FAIL`** — Execution failed or threshold was not met; blocks transition to `HUMAN_CONFIRMATION`.
- **`NOT VERIFIED`** — Gate could not be executed in the current environment; requires explicit disclosure and human sign-off.

> **Non-Negotiable Rule:** Never report a test or audit as `PASS` without execution evidence.

---

## 2. The 15 Mandatory Quality Gates

| Gate ID | Dimension | Command / Verification Tool | Acceptance Threshold (`PASS` Criteria) | Owner Agent |
| :--- | :--- | :--- | :--- | :--- |
| **QG-01** | **TypeScript Strictness** | `pnpm typecheck` (`tsc --noEmit --strict`) | `0` errors, `0` implicit `any`, `0` `@ts-ignore` without documented justification | `AG-06` / `AG-16` |
| **QG-02** | **ESLint & Code Hygiene** | `pnpm lint` | `0` errors, `0` warnings, no raw `z-[nnn]` tokens, no `console.log` in `src/` | `AG-07` / `AG-16` |
| **QG-03** | **Unit Tests & Schema Validation** | `pnpm test:unit` & `pnpm validate:content` | `100%` pass rate; all project & experience records pass Zod schema validation | `AG-10` / `AG-16` |
| **QG-04** | **Integration Tests** | `pnpm test:integration` | Data repository, snapshot fallback, and component block renderers pass | `AG-16` |
| **QG-05** | **Playwright E2E Journeys** | `pnpm test:e2e` | All 9 routes render `200 OK`; filter bar, case navigation, mobile menu, and contact flow pass | `AG-16` |
| **QG-06** | **Responsive Viewports** | Playwright Visual Matrix (`375px`, `768px`, `1024px`, `1440px`, `1920px`) | Zero horizontal overflow (`scrollWidth <= clientWidth`), `.std-grid` alignment intact | `AG-17` |
| **QG-07** | **Accessibility (WCAG 2.2 AA)** | `@axe-core/playwright` + Keyboard Tab Audit | `0` critical/serious Axe violations; contrast ≥ `4.5:1`; touch targets ≥ `48x48px`; focus ring visible | `AG-13` |
| **QG-08** | **Technical SEO** | `pnpm validate:seo` + Playwright meta check | Unique `<title>`, `<meta name="description">`, canonical URL, OpenGraph, JSON-LD `Person`/`CreativeWork`, valid `/sitemap.xml` & `/robots.txt` | `AG-12` |
| **QG-09** | **Core Web Vitals** | Lighthouse CI (Mobile & Desktop) | Performance ≥ `90`, Accessibility ≥ `95`, Best Practices ≥ `95`, SEO ≥ `95`; LCP < `2.5s`, INP < `200ms`, CLS < `0.1` | `AG-14` |
| **QG-10** | **Image Optimization** | Asset Audit Script + Network Inspection | All images serve `AVIF`/`WebP`, explicit `width`/`height` or `aspectRatio`, correct `sizes`, only Hero has `priority` | `AG-11` |
| **QG-11** | **Video Loading Lifecycle** | Network & DOM Inspection | `preload="none"` by default; off-screen videos paused; valid WebP `poster` defined on 100% of videos | `AG-11` |
| **QG-12** | **WebGL Performance & Fallback** | Chrome DevTools FPS Meter + Context Loss Test | Sustained `60 FPS` on desktop / `≥ 50 FPS` on mobile; `dpr` capped; graceful CSS fallback when WebGL disabled | `AG-09` / `AG-14` |
| **QG-13** | **Reduced Motion Compliance** | Playwright `emulateMedia({ reducedMotion: 'reduce' })` | All parallax, `translateY`, blur reveals, and continuous shader loops disabled cleanly | `AG-08` / `AG-13` |
| **QG-14** | **Security & Secret Hygiene** | Secret Scan + HTTP Header Check | `0` leaked credentials; `server-only` boundaries intact; CSP, HSTS, `X-Frame-Options` headers verified | `AG-15` |
| **QG-15** | **Production Build Integrity** | `pnpm build` | Clean production build with `0` errors; route bundle sizes within budget (`< 180KB` First Load JS for editorial routes) | `AG-18` |

---

## 3. Standard Quality Gate Report Template

```markdown
## Quality Gate Execution Report
- **Workflow / Phase:** [Name]
- **Timestamp:** [ISO-8601]
- **Commit / Branch:** [Ref]

| Gate ID | Dimension | Status (`PASS` / `FAIL` / `NOT VERIFIED`) | Execution Evidence / Command Output |
| :--- | :--- | :--- | :--- |
| QG-01 | TypeScript | [STATUS] | [Command & Summary] |
| ... | ... | ... | ... |
```

