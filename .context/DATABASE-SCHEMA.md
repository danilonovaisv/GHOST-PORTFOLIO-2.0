# DATABASE SCHEMA & CONTENT MODEL — GHOST PORTFOLIO 2.0

**Phase:** 02 — Data Architecture & Content Model  
**Active Personas:** Backend Engineer (`AG-10`), Content Strategist (`AG-05`), Security Auditor (`AG-15`)  
**Status:** Blueprint Specification (Pending Human Approval)

---

## 1. Non-Destructive Coexistence & Migration Principle

> [!CAUTION]
> **Rule #1 & #2 Enforcement:** `GHOST-PORTFOLIO-2.0` must **never** alter, drop, or overwrite existing tables (`public.portfolio_projects`, `public.landing_pages`, `public.site_assets`, `public.experiences`) used by the live `portfoliodanilo.com` production site.

### Strategy for Safe Coexistence
1. **Phase 1 (Read-Only Adapter + Local Validated Snapshot):**
   - `GHOST-PORTFOLIO-2.0` reads existing records from `public.portfolio_projects`, `public.landing_pages`, `public.experiences`, and `public.site_assets` via a **Read-Only Mapper (`scripts/migrate-content.ts`)** that transforms legacy rows (including `master-project-v1/v2/v3` JSON payloads) into the unified `GHOST-PORTFOLIO-2.0` schema and enriches them with curated strategic narratives in `src/lib/data/content/`.
2. **Phase 2 (Isolated `v2` Schema / Views in Supabase):**
   - When dynamic database persistence is enabled for `GHOST-PORTFOLIO-2.0`, all new tables use an isolated namespace (`ghost_v2` schema or `v2_*` prefixed tables) with strict Row Level Security (RLS).

---

## 2. Canonical TypeScript & Zod Content Model (`src/types/content.ts`)

```typescript
export type StrategicTerritory =
  | 'branding'
  | 'campaign'
  | 'motion'
  | 'web'
  | 'creative-technology';

export type MediaKind = 'image' | 'video' | 'html' | 'webgl';

export interface MediaAsset {
  id?: string;
  kind: MediaKind;
  src: string;
  poster?: string;
  alt: string;
  width?: number;
  height?: number;
  aspectRatio?: '16/9' | '4/3' | '1/1' | '9/16' | '21/9' | string;
  caption?: string;
}

export interface ProjectCaseNarrative {
  summary: string;          // Executive summary (Mandatory)
  context?: string;         // Market & brand context
  challenge?: string;       // Business / creative problem
  objectives?: string[];    // Key objectives
  insights?: string;        // Strategic insights
  strategy?: string;        // Strategic approach
  concept?: string;         // Creative concept & art direction
  execution?: string;       // Craft & technological execution
  deliverables?: string[];  // Shipped artifacts
  impact?: string[];        // Verified factual outcomes only (Zero fabricated metrics)
}

export type ProjectSection =
  | {
      id: string;
      type: 'narrative-split';
      data: {
        eyebrow?: string;
        headline: string;
        body: string[];
        media?: MediaAsset;
        mediaAlign?: 'left' | 'right';
      };
    }
  | {
      id: string;
      type: 'fullbleed-media';
      data: {
        media: MediaAsset;
        caption?: string;
        contained?: boolean;
      };
    }
  | {
      id: string;
      type: 'media-grid';
      data: {
        columns: 1 | 2 | 3;
        items: MediaAsset[];
      };
    }
  | {
      id: string;
      type: 'quote-band';
      data: {
        quote: string;
        attribution?: string;
      };
    }
  | {
      id: string;
      type: 'video-showcase';
      data: {
        video: MediaAsset;
        autoplayLoop?: boolean;
        provider?: 'native' | 'youtube';
        youtubeId?: string;
      };
    }
  | {
      id: string;
      type: 'metrics-deliverables';
      data: {
        deliverables: string[];
        verifiedOutcomes?: Array<{ label: string; description: string }>;
      };
    }
  | {
      id: string;
      type: 'interactive-embed';
      data: {
        title: string;
        sandboxHtml?: string;
        sceneId?: string;
        fallbackMedia: MediaAsset;
      };
    };

export interface Project {
  id: string;
  slug: string;
  legacySlug?: string;
  title: string;
  subtitle?: string;
  client: string;
  clientSlug: string;
  clientLogo?: MediaAsset;
  territory: StrategicTerritory;
  tags: string[];
  services: string[];
  year: number;
  featuredOnHome: boolean;
  featuredOrder?: number;
  portfolioOrder: number;
  published: boolean;
  caseTier: 'flagship' | 'showcase';
  accentColor: string; // Default: '#0048FF'
  coverLandscape: MediaAsset;
  coverSquare?: MediaAsset;
  heroMedia: MediaAsset;
  narrative: ProjectCaseNarrative;
  sections: ProjectSection[];
  credits: Array<{ role: string; name: string }>;
  externalUrl?: string;
  nextProjectSlug?: string;
  seo: {
    title: string;
    description: string;
    ogImage: string;
    keywords?: string[];
  };
}
```

---

## 3. Target PostgreSQL Schema (`ghost_v2` Namespace)

When persisted to Supabase in Phase 2, the clean schema consolidates the legacy `portfolio_projects` + `landing_pages` + `projects` tables into four normalized, strictly-typed tables:

```sql
-- Isolated schema so production public.* tables remain 100% untouched
CREATE SCHEMA IF NOT EXISTS ghost_v2;

-- 1. Projects & Case Studies (Unified Table)
CREATE TABLE IF NOT EXISTS ghost_v2.projects (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug TEXT UNIQUE NOT NULL,
  legacy_slug TEXT,
  title TEXT NOT NULL,
  subtitle TEXT,
  client_name TEXT NOT NULL,
  client_slug TEXT NOT NULL,
  territory TEXT NOT NULL CHECK (territory IN ('branding', 'campaign', 'motion', 'web', 'creative-technology')),
  case_tier TEXT NOT NULL DEFAULT 'showcase' CHECK (case_tier IN ('flagship', 'showcase')),
  year INTEGER NOT NULL,
  tags TEXT[] NOT NULL DEFAULT '{}',
  services TEXT[] NOT NULL DEFAULT '{}',
  featured_on_home BOOLEAN NOT NULL DEFAULT false,
  featured_order INTEGER,
  portfolio_order INTEGER NOT NULL DEFAULT 0,
  is_published BOOLEAN NOT NULL DEFAULT true,
  accent_color TEXT NOT NULL DEFAULT '#0048FF',
  cover_landscape JSONB NOT NULL,
  cover_square JSONB,
  hero_media JSONB NOT NULL,
  narrative JSONB NOT NULL DEFAULT '{}'::jsonb,
  sections JSONB NOT NULL DEFAULT '[]'::jsonb,
  credits JSONB NOT NULL DEFAULT '[]'::jsonb,
  seo JSONB NOT NULL DEFAULT '{}'::jsonb,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- 2. Executive Experience & Career Timeline
CREATE TABLE IF NOT EXISTS ghost_v2.experiences (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  company TEXT NOT NULL,
  role TEXT NOT NULL,
  period_label TEXT NOT NULL,
  start_date DATE,
  end_date DATE,
  summary TEXT NOT NULL,
  highlights TEXT[] NOT NULL DEFAULT '{}',
  sort_order INTEGER NOT NULL DEFAULT 0,
  is_published BOOLEAN NOT NULL DEFAULT true,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- 3. Lab & Creative Tech Experiments
CREATE TABLE IF NOT EXISTS ghost_v2.lab_experiments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  slug TEXT UNIQUE NOT NULL,
  title TEXT NOT NULL,
  category TEXT NOT NULL CHECK (category IN ('webgl-shader', 'generative-ai', 'agentic-system', 'motion-study')),
  summary TEXT NOT NULL,
  tech_stack TEXT[] NOT NULL DEFAULT '{}',
  preview_media JSONB NOT NULL,
  interactive_config JSONB,
  is_published BOOLEAN NOT NULL DEFAULT true,
  sort_order INTEGER NOT NULL DEFAULT 0,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- 4. Verified Media Asset Catalog
CREATE TABLE IF NOT EXISTS ghost_v2.media_assets (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  asset_key TEXT UNIQUE NOT NULL,
  storage_provider TEXT NOT NULL CHECK (storage_provider IN ('supabase', 'r2', 'local')),
  bucket TEXT,
  file_path TEXT NOT NULL,
  public_url TEXT NOT NULL,
  mime_type TEXT NOT NULL,
  width INTEGER,
  height INTEGER,
  size_bytes BIGINT,
  alt_text TEXT NOT NULL,
  created_at TIMESTAMPTZ NOT NULL DEFAULT now()
);

-- Row Level Security (RLS)
ALTER TABLE ghost_v2.projects ENABLE ROW LEVEL SECURITY;
ALTER TABLE ghost_v2.experiences ENABLE ROW LEVEL SECURITY;
ALTER TABLE ghost_v2.lab_experiments ENABLE ROW LEVEL SECURITY;
ALTER TABLE ghost_v2.media_assets ENABLE ROW LEVEL SECURITY;

-- Public Read-Only Policies (Anon & Authenticated can only read published rows)
CREATE POLICY "Public read published projects" ON ghost_v2.projects
  FOR SELECT USING (is_published = true);

CREATE POLICY "Public read published experiences" ON ghost_v2.experiences
  FOR SELECT USING (is_published = true);

CREATE POLICY "Public read published lab experiments" ON ghost_v2.lab_experiments
  FOR SELECT USING (is_published = true);

CREATE POLICY "Public read media assets" ON ghost_v2.media_assets
  FOR SELECT USING (true);
```

