# Token Migration Map — Ghost DS 2.0

Mapeamento entre os três sistemas de tokens atuais e o destino canônico Ghost DS 2.0.

**Fontes:**
- `A` = `src/app/globals.css` (`@theme` + `:root`)
- `B` = `src/config/colors.ts` (`COLORS`)
- `C` = `src/config/brand.ts` (`BRAND.colors`)

---

## 1. Cores — Conflitos e Destino

### 1.1 Nomenclatura duplicada (`--color-bluePrimary` vs `--color-ghost-*`)

| Token atual | Fonte | Valor | Ação Fase 1 |
|---|---|---|---|
| `--color-bluePrimary` | A | `#0048ff` | **MANTER** como alias canônico `@deprecated`; origem do Tailwind `text-bluePrimary` |
| `--color-ghost-deep-blue` | A | `#0048ff` | **REMOVER** — duplicata exata de `bluePrimary` |
| `--color-blueAccent` | A | `#4fe6ff` | **MANTER** (accent canônico) |
| `--color-ghost-text-primary` | A | `#fcffff` | **RENOMEAR** → aponta para `--color-text`; nome atual sugere que é um accent, gerando confusão |
| `--color-ghost-text-muted` | A | `#a1a3a3` | **REMOVER** — duplicata de `--color-textSecondary` |
| `--color-ghost-void-black` | A | `#040013` | **REMOVER** — duplicata de `--color-background` |
| `--color-ghost-surface` | A | `rgba(255,255,255,0.05)` | **RENOMEAR** → `--color-glass-surface` |
| `--color-primary` / `--color-accent` | A (aliases) | `#0048ff` / `#4fe6ff` | **MANTER** (compat Tailwind v4) |

### 1.2 Tokens DS 2.0 ausentes (a criar na Fase 1)

| Token | Valor | Origem |
|---|---|---|
| `--color-text-editorial` | `#E2E6F0` | DS 2.0 §2 |
| `--color-text-muted-aa` | `#B4B8C5` | DS 2.0 §2 |
| `--color-abyss-end` | `#040013` | DS 2.0 §2 (fecha a escala abyss) |
| `--color-glass-surface` | `rgba(255,255,255,0.05)` | rename de `ghost-surface` |
| `--color-glass-border` | `rgba(255,255,255,0.1)` | DS 2.0 §2 (border glass) |

### 1.3 Conflitos de valor entre fontes (CRÍTICO)

| Token | A (`globals.css`) | B (`colors.ts`) | C (`brand.ts`) | Resolução |
|---|---|---|---|---|
| `textSecondary` | `#a1a3a3` | `#a1a3a3` | **`#fcffff`** | **C está errado** → corrigir para `#a1a3a3` |
| `textEmphasis` | `#2e85f2` | `#2e85f2` | `#2E85F2` | OK (mesmo valor, caixa diferente) |

> ⚠️ `brand.ts` define `textSecondary: '#fcffff'` — branco puro. Isso **anula** a hierarquia de texto secundário em qualquer componente que leia de `BRAND.colors`. Correção obrigatória na Fase 1.4.

### 1.4 shadcn base (EX-01 — NÃO remover em massa)

| Token | `:root` | `.dark` | Decisão |
|---|---|---|---|
| `--primary` | `oklch(0.205 0 0)` | `oklch(0.922 0 0)` | Isolar em bloco `.shadcn-compat`; não remover (formulários dependem) |
| `--secondary`, `--muted`, `--accent` | tons neutros | tons neutros | Idem |
| `--card`, `--popover`, `--sidebar` | `oklch(1 0 0)` | `oklch(0.205 0 0)` | Idem |

---

## 2. Z-Index — Inventário Real

`src/constants/z-indices.ts` já é a fonte de verdade (19 camadas). O problema é **uso**, não definição.

| Uso hardcoded | Arquivo | Token correto já existente |
|---|---|---|
| `z-[1300]` | `src/app/layout.tsx:76` | `Z_INDEX.skipLink` (1300) ✅ já existe |
| `z-[9999]` | `src/components/ui/HTMLVideoBlock.tsx:174` | `Z_INDEX.debugTop` (9999) — mas semanticamente deveria ser `lightbox` (70) |
| `z-[9999]` | `src/components/sobre/origin/OriginComponents.tsx:138` | `Z_INDEX.debugTop` (9999) — scanlines deveriam ser `overlay` (50) ou `glass` (10) |

> **Nota de auditoria:** os dois usos de `9999` são semanticamente incorretos. Um lightbox deve usar `lightbox: 70`; um overlay de scanlines deve usar `overlay: 50`. O `debugTop: 9999` existe apenas para o debugger de desenvolvimento.

---

## 3. Tipografia — Lacunas

| Classe | Presente? | Problema |
|---|---|---|
| `.text-hero-manifesto` | ❌ | DS 2.0 §3.2 exige; não existe |
| `.text-display` | ✅ | OK (`clamp(2rem, 5vw, 4.5rem)`, weight 800, lh 1.1) |
| `.text-h1` / `.text-h2` / `.text-h3` | ✅ | OK |
| `.text-body-editorial` | ❌ | **Faltando** — lh 1.65, measure 60–72ch |
| `.text-body` | ✅ | OK (mas lh 1.5, não 1.55 do DS) |
| `.text-small` | ✅ | OK |
| `.text-micro-mono` | ⚠️ parcial | Existe `.text-micro` (mono), mas tracking `0.08em` e uppercase não são aplicados no CSS — só inline nos componentes |

**Fontes:**
- Manrope: self-hosted ✅ em `public/fonts/Manrope-VariableFont_wght.woff2`, com preload ✅
- PPSupplyMono: CDN `assets.codepen.io` ❌ — sem preload, sem self-host

---

## 4. Motion — Lacunas

| Token | Presente em `config/motion.ts` | Usado em componentes? |
|---|---|---|
| `MOTION_TOKENS.ease.*` | ✅ | ✅ (amplo) |
| `MOTION_TOKENS.duration.*` | ✅ | ✅ (amplo) |
| `MOTION_TOKENS.spring.*` | ✅ (4 presets stiffness/damping) | ❌ **ZERO usos** |
| `GHOST_SPRING_DEFAULT` | ❌ | — (a criar na Fase 2) |
| `GHOST_SPRING_MOMENTUM` | ❌ | — (a criar na Fase 2) |

**Busca por `type: 'spring'` em todo `src/`:** 0 resultados.

---

## 5. Hardcoded Hex — Inventário por Arquivo (Público)

| Arquivo | Ocorrências | Tokens de destino |
|---|---|---|
| `src/components/sobre/origin/OriginComponents.tsx` | ~18 | `--color-blueAccent`, `--color-background`, `--color-bluePrimary` |
| `src/components/sobre/beliefs/WhatMovesMeBackground.tsx` | 5 | `--color-bluePrimary`, `--color-blueAccent`, `--color-background` |
| `src/components/home/ShaderSection.tsx` | 2 | `--color-background` |
| `src/components/ui/shader-lines.tsx` | 2 | `--color-background` |
| `src/components/sobre/sections/ManifestoScrollSection.tsx` | 2 | `--color-background` |
| `src/components/layout/header/mobile/MobilePreLayers.tsx` | 3 | `--color-blueAccent`, `--color-purpleDetails`, `--color-pinkDetails` |
| `src/components/layout/header/DesktopFluidHeader.tsx` | 1 | `--color-bluePrimary` |
| `src/components/home/hero/VideoManifesto.tsx` | 1 | `--color-bluePrimary` |
| `src/components/home/featured-projects/FeaturedProjectAnimatedBackground.tsx` | 3 | `--color-bluePrimary`, `--color-purpleDetails` |
| `src/config/colors.ts` | (fonte — não migrar) | — |
| `src/config/brand.ts` | (fonte — não migrar) | — |
| `src/config/cta.ts` | (fonte — não migrar) | — |

> `src/config/*` e `src/lib/colors.ts` são **fontes de verdade legítimas** — hex ali é definição, não hardcode. O alvo da Fase 1.3 são os componentes de UI.

---

## 6. Ordem de Execução de Substituição

Para evitar quebra de regressão visual, a ordem é:

1. **Criar tokens faltantes** em `@theme` (não altera nada, só adiciona)
2. **Renomear/remover duplicatas** `ghost-*` → aliases canônicos (verificar cada uso)
3. **Corrigir `brand.ts` `textSecondary`** (mudança de valor, validar contraste)
4. **Substituir hex hardcoded** arquivo por arquivo (ordem: menor → maior ocorrência)
5. **Isolar shadcn** em bloco dedicado (não remover)
6. **Validar** com `pnpm typecheck && pnpm lint && pnpm build`