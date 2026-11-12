# CONTENT MODEL — GHOST PORTFOLIO 2.0

> Canonical reference for content entities. For full TypeScript interfaces and PostgreSQL DDL, see [DATABASE-SCHEMA.md](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/DATABASE-SCHEMA.md) and [CONTENT-STRATEGY.md](file:///Users/danilonovais/GHOST-PORTFOLIO-2.0/.context/CONTENT-STRATEGY.md).

## Entity Hierarchy

1. **`Profile` (`src/lib/data/content/profile.ts`)**
   - Executive positioning, manifesto, short & extended biography, contact coordinates (`danilo@portfoliodanilo.com`, WhatsApp, LinkedIn), location (`São Paulo, BR`).
2. **`Experience[]` (`src/lib/data/content/experiences.ts`)**
   - Career leadership roles, companies, periods, executive summary, and verified achievements.
3. **`Territory[]` (`src/lib/data/content/territories.ts`)**
   - The 5 Strategic Territories: `branding`, `campaign`, `motion`, `web`, `creative-technology`.
4. **`Project[]` (`src/lib/data/content/projects/`)**
   - 15 curated portfolio projects structured with metadata, `MediaAsset` covers, `ProjectCaseNarrative`, and composable `ProjectSection[]` blocks.
5. **`ClientBrand[]` (`src/lib/data/content/clients.ts`)**
   - Verified brand roster (Swift, Nestlé, Nivea, Ambev, Zé Delivery, Pernod Ricard, Algar Telecom, Mapfre, AON, O Boticário, Grupo Iguatemi, Unilever) with monochrome SVG emblems.
6. **`LabExperiment[]` (`src/lib/data/content/lab.ts`)**
   - Interactive shaders, Generative AI studies, and agentic engineering explorations.

