# OpenAI Codex Instructions — GHOST-PORTFOLIO-2.0

Always consult `AGENTS.md` and `.context/active-state.md` at session start.

- **Architecture & Specifications:** `.context/`
- **Agents, Skills, Rules & PREVC Workflows:** `.agents/`
- **Quality Gates (`QG-01`–`QG-15`):** `.context/QUALITY-GATES.md`
- **Non-Negotiable Constraints:**
  1. Never touch production (`portfoliodanilo.com`) or `PORTFOLIO-DANILO-FINAL`.
  2. Enforce TypeScript strictness, Next.js 16 Server Components by default, and Zod 4 validation on all content payloads.
  3. Require explicit human approval at `REVIEW_REQUIRED` and `HUMAN_CONFIRMATION` gates.

