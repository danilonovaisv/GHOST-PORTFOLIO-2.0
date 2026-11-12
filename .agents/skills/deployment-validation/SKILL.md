---
name: deployment-validation
version: 2.0.0
origin: Consolidated from verification-before-completion & deployment-procedures in Agent-Skills-Knowledge-Hub
description: Executes the 15 Quality Gates (QG-01 to QG-15), validates production build integrity, and enforces the human approval gate before release.
---

# Deployment Validation Skill (`deployment-validation`)

## 1. Purpose
Guarantee that no code is marked complete and no release is promoted without complete, evidence-backed verification of all 15 Quality Gates (`QG-01` through `QG-15`) and explicit human sign-off.

## 2. When to Use
- At the transition from `VALIDATION` to `HUMAN_CONFIRMATION` in the PREVC protocol, and during `13-pre-release.md` / `14-deployment.md`.

## 3. When Not to Use
- Never use this skill to auto-deploy to production without explicit human authorization.

## 4. Input Contract
- `release_candidate`: Current git branch/commit and Quality Gate reports from `AG-13` through `AG-17`.

## 5. Operational Instructions (Progressive Disclosure)
1. **Execute Core Verification Pipeline:**
   - `pnpm typecheck` (`QG-01`)
   - `pnpm lint` (`QG-02`)
   - `pnpm test` (`QG-03`, `QG-04`)
   - `pnpm build` (`QG-15`)
   - `pnpm test:e2e` (`QG-05`, `QG-06`, `QG-07`, `QG-08`, `QG-13`)
2. **Aggregate Gate Statuses:** Record exact `PASS`, `FAIL`, or `NOT VERIFIED` states in `docs/release/RELEASE-DOSSIER.md`.
3. **Enforce Stop Gate:** If any gate is `FAIL`, transition state to `FIX_REQUIRED`. If all gates pass, transition to `HUMAN_CONFIRMATION` and present the Release Dossier to Danilo Novais.

## 6. Output Contract
- Complete `docs/release/RELEASE-DOSSIER.md` with execution evidence for `QG-01` through `QG-15`.

## 7. Validation Criteria
- Zero `FAIL` gates; explicit human approval recorded prior to any production cutover.

