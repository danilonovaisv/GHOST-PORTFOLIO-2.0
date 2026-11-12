# ASSET MANIFEST — GHOST PORTFOLIO 2.0

**Status:** Read-Only Catalog Blueprint (Populated automatically via `scripts/audit-assets.ts` in Phase 06/12)

## 1. Verified Storage Origins (Read-Only from `PORTFOLIO-DANILO-FINAL`)

| Source ID | Provider | Host / Endpoint | Buckets / Paths | Access Policy |
| :--- | :--- | :--- | :--- | :--- |
| **STORAGE-01** | Supabase Storage | `umkmwbkwvulxtdodzmzf.supabase.co` | `site-assets`, `portfolio-media` | Public Read-Only (`GET`) |
| **STORAGE-02** | Cloudflare R2 CDN | `assets.portfoliodanilo.com` | Root media mirror | Public Read-Only (`GET`) |
| **STORAGE-03** | Local Static Assets | `/public/fonts`, `/public/icons` | Self-hosted `Manrope` Variable & `PPSupplyMono` WOFF2 | Local Bundled |

## 2. Asset Governance Rules
1. **Zero Broken Links:** Every asset path referenced in `Project` or `Experience` records is verified via HTTP `HEAD` check in `scripts/audit-assets.ts`.
2. **Mandatory Metadata:** Every image asset must declare `src`, `alt`, `width`, `height`, and `aspectRatio`. Every video asset must declare `src`, `poster`, and `aspectRatio`.
3. **No Unverified External Hosts:** External hotlinking outside the CSP allowlist (`*.supabase.co`, `assets.portfoliodanilo.com`, `*.r2.dev`) is forbidden.

