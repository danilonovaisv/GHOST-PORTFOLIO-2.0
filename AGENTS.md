# AGENTS.md — GHOST PORTFOLIO 2.0 (Universal Multi-IDE Entry Point)

> **System:** GHOST-PORTFOLIO-2.0 — Executive Digital Portfolio Ecosystem for Danilo Novais  
> **Supported Environments:** Google Antigravity, Claude Code, Cursor, OpenAI Codex  
> **Governance Protocol:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`)

---

## 1. Single Source of Truth (Architecture & Intelligence)

This repository uses a unified, IDE-agnostic intelligence architecture. Do not duplicate rules across IDE-specific files; always load from `.context/` and `.agents/`:

1. **Constitutional Charter & Current State:**
   - [`.context/PROJECT-CONSTITUTION.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/PROJECT-CONSTITUTION.md)
   - [`.context/active-state.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/active-state.md)
   - [`.context/DECISION-LOG.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/DECISION-LOG.md)
2. **Strategy, UX & Design System 2.0:**
   - [`.context/PRODUCT-STRATEGY.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/PRODUCT-STRATEGY.md)
   - [`.context/CREATIVE-DIRECTION.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/CREATIVE-DIRECTION.md)
   - [`.context/CONTENT-STRATEGY.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/CONTENT-STRATEGY.md)
   - [`.context/INFORMATION-ARCHITECTURE.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/INFORMATION-ARCHITECTURE.md)
   - [`.context/DESIGN-SYSTEM.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/DESIGN-SYSTEM.md)
3. **Technical, Data, Security & Media Architecture:**
   - [`.context/TECHNICAL-ARCHITECTURE.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/TECHNICAL-ARCHITECTURE.md)
   - [`.context/COMPONENT-ARCHITECTURE.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/COMPONENT-ARCHITECTURE.md)
   - [`.context/DATABASE-SCHEMA.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/DATABASE-SCHEMA.md)
   - [`.context/SECURITY-ARCHITECTURE.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/SECURITY-ARCHITECTURE.md)
   - [`.context/MEDIA-ARCHITECTURE.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/MEDIA-ARCHITECTURE.md)
   - [`.context/QUALITY-GATES.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/QUALITY-GATES.md)
4. **Multi-Agent Battalion & Skills:**
   - [`.agents/AGENTS_MANIFEST.md`](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.agents/AGENTS_MANIFEST.md) (19 Specialized Agents in `.agents/agents/`)
   - `.agents/skills/` (17 Progressive-Disclosure Skills)
   - `.agents/rules/` (6 Canonical Rule Sets)
   - `.agents/workflows/` (15 PREVC Workflows)

---

## 2. Non-Negotiable Operational Rules

1. **Never touch production (`https://portfoliodanilo.com`) or `PORTFOLIO-DANILO-FINAL`.**
2. **Never fabricate client names, metrics, or project results.**
3. **Always query Context7 before implementing Next.js 16, React 19, Tailwind CSS v4, or Supabase SSR patterns.**
4. **Never report a Quality Gate (`QG-01`–`QG-15`) as `PASS` without command execution evidence.**
5. **Respect Human Approval Gates (`REVIEW_REQUIRED` and `HUMAN_CONFIRMATION`).**

