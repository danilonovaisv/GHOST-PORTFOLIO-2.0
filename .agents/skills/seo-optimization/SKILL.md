---
name: seo-optimization
version: 2.0.0
origin: Adapted from seo-fundamentals in Agent-Skills-Knowledge-Hub & auditoria-estrategica-portfolio
description: Implements Next.js 16 Metadata API, Schema.org JSON-LD (Person, CreativeWork), OpenGraph cards, XML sitemaps, and canonical redirects.
---

# Technical SEO Optimization Skill (`seo-optimization`)

## 1. Purpose
Maximize organic discoverability and rich-result authority for Danilo Novais across executive roles (Creative Director, Head of Creation, Creative Strategist, Creative Technologist) and individual project cases.

## 2. When to Use
- When configuring route `generateMetadata`, JSON-LD structured data (`src/lib/seo/`), `sitemap.ts`, `robots.ts`, or legacy route redirects.

## 3. When Not to Use
- Never block `/_next/` static assets in `robots.txt` or generate duplicate `<h1>` tags on a single page.

## 4. Input Contract
- `route_metadata`: Title, description, canonical path, OG image, and structured entity data.

## 5. Operational Instructions (Progressive Disclosure)
1. **Route Metadata (`generateMetadata`):** Every page must export unique `title`, `description` (140–160 chars), `alternates.canonical`, `openGraph`, and `twitter` card metadata.
2. **Structured Data (`JSON-LD`):**
   - `/` & `/sobre` & `/curriculo`: `Person` + `ProfilePage` schema with `sameAs` links (LinkedIn, GitHub) and `knowsAbout` territories.
   - `/projetos/[slug]`: `CreativeWork` + `BreadcrumbList` schema citing client, year, creator, and summary.
3. **Sitemap & Redirects:** Auto-generate `/sitemap.xml` from all 9 static routes + all published project slugs; enforce `308` permanent redirects from `/projects/[slug]` to `/projetos/[slug]`.

## 6. Output Contract
- Valid Next.js `Metadata` objects, JSON-LD `<script type="application/ld+json">` payloads, and `sitemap.ts` / `robots.ts`.

## 7. Validation Criteria
- Passes `QG-08` (Lighthouse SEO ≥ `95`, valid XML sitemap, single `<h1>`, valid JSON-LD).

