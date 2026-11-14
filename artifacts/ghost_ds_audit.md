# Ghost Design System — Relatório de Auditoria

**Escopo da auditoria:** Camada de UI pública do `PORTFOLIO-DANILO-FINAL` (excluindo admin)
**Referências:** Ghost DS 2.0 / Apple Design Principles / Regras da Casa Design-Taste Frontend
**Data:** 2026-11-13
**Status:** Somente documentação — nenhuma alteração de código foi realizada

---

## I. Violações na Arquitetura de Tokens

### D-01 【Grave】Nomes duplicados de tokens de cor, semântica confusa

**Local:** `src/app/globals.css:4–8, 39–40`; `src/config/colors.ts`; `src/config/brand.ts`

| Nome antigo | Nome novo | Conflito |
|---|---|---|
| `--color-bluePrimary: #0048ff` | `--color-ghost-deep-blue: #0048ff` | Mesmo valor com duas variáveis; classes Tailwind `text-bluePrimary` e `bg-ghost-deep-blue` coexistem |
| `--color-blueAccent: #4fe6ff` | `--color-ghost-text-primary: #fcffff` (não é accent, gera confusão) | Sistema de aliases `ghost-*` não mapeia de forma clara para os nomes originais |
| `--color-purpleDetails` / `--color-pinkDetails` | Marcados como DEPRECATED nos comentários | Ainda utilizados em código ativo |

**Impacto:** Desenvolvedores novos têm dificuldade em distinguir os dois sistemas de nomenclatura, podendo usar variáveis já obsoletas. A especificação do DS 2.0 exige uma única fonte de verdade semântica.

---

### D-02 【Grave】Token Text Editorial ausente

**Local:** `src/app/globals.css`; `src/config/colors.ts`; `src/config/brand.ts`

O DS 2.0 §3 define explicitamente os tokens adicionais:
- `--color-text-editorial: #E2E6F0` (leitura prolongada, baixa halation)
- `--color-text-muted-aa: #B4B8C5` (garantia WCAG AA)

No código atual:
- CSS não possui definição de `--color-text-editorial`
- `textSecondary` é definido como `#a1a3a3` (DS v3.2) **e** `#fcffff` (brand.ts) — valores contraditórios
- Nenhuma classe `text-editorial` é referenciada em componentes; textos narrativos longos não recebem o tratamento tipográfico adequado

---

### D-03 【Médio】Variáveis shadcn/light poluem site dark-only

**Local:** `src/app/globals.css:152–183, 612–644`

As variáveis `--card`, `--popover`, `--sidebar` etc. são baseadas em tons de branco (ex: `oklch(1 0 0)`). Embora o bloco `.dark` sobrescreva alguns valores:
- `--primary` no `:root` recebe `oklch(0.205 0 0)` (cinza escuro), desconectado do azul da marca `#0048ff`
- No bloco `.dark`, `--primary: oklch(0.922 0 0)` (quase branco), mais uma vez desacoplado do design system

**Impacto:** Componentes que dependem das variáveis base shadcn (botões, inputs, cards) utilizam escala cinza no modo escuro em vez da paleta da marca, prejudicando a consistência visual.

---

### D-04 【Médio】Hex de cores da marca espalhados como strings hardcoded

**Local:** Lista abaixo

Aproximadamente **77 ocorrências** em JSX/TSX fora do contexto de admin:

| Arquivo | Valores hardcoded |
|---|---|
| `src/components/ui/shader-lines.tsx:360,376` | `#040013` (fundo) |
| `src/components/home/ShaderSection.tsx:197,212` | `#040013` |
| `src/components/sobre/origin/OriginComponents.tsx` | `#4fe6ff` ×10+, `#040013` ×2, `#0048ff` ×3 |
| `src/components/sobre/beliefs/WhatMovesMeBackground.tsx:21–35,46` | `#0048ff`, `#4fe6ff`, `#040013cc` |
| `src/components/layout/header/DesktopFluidHeader.tsx:132` | `'#0048ff'` (valor padrão de parâmetro) |
| `src/components/layout/header/mobile/MobilePreLayers.tsx:14–16` | `'#4fe6ff'` `'#8705f2'` `'#f501d3'` (array hardcoded) |
| `src/components/home/hero/VideoManifesto.tsx:154` | `focus-visible:outline-[#0048ff]` |
| `src/components/home/featured-projects/FeaturedProjectAnimatedBackground.tsx:114–115,143` | `'#0048ff'` `'#8705f2'` |
| `src/components/sobre/sections/ManifestoScrollSection.tsx:136,210` | `'#040013'` |

**Violação normativa:** DS 2.0 §2.2 determina "todas as cores devem ser referenciadas por variáveis CSS; hex hardcode é proibido na camada de UI".

---

## II. Violações na Arquitetura de Motion

### M-01 【Grave】Zero springs em interações de UI; todos usam tweens/CSS transitions

**Base:** Apple Design §4 "Comportamento antes de animação — use springs"; DS 2.0 §5.3 exige interruptibilidade em interações de UI.

| Local | Situação atual | Deveria ser |
|---|---|---|
| `AntigravityCTA.tsx:43–48, 70–72` | `{ duration: 0.2s, ease: GHOST_EASE }` + `whileTap={scale: 0.98}` | `type: 'spring', damping: 1.0` |
| `DesktopFluidHeader.tsx:103–114` | Largura do underline via `duration: 0.2, ease: GHOST_EASE` | transição spring |
| `ProjectCard.tsx:136` | `transition-[transform,box-shadow,...] duration-fast ease-out` (CSS transition) | Deve ser removido; hover gerenciado por framer-motion |
| `ContactForm.tsx:315–316` | `whileHover={y:-2}`, `whileTap={opacity:0.9}` (sem declaração spring type) | Adicionar `type: 'spring', damping: 1.0` |
| `globals.css:756–791` | `.cta-button { transition: ... }` + hover com `translateY(-1px)` (tween CSS puro) | Remover esta regra, transferir para motion |
| `globals.css:793–807` | `@keyframes button-animation` genérico (animação de entrada) | Tornar componente autônomo e usar spring |

**Defeito crítico:** Não existe nenhuma configuração de Motion com `type: 'spring'` — busca em toda a pasta `src/` retorna uso de spring igual a **zero**. Os tokens `spring.*` definidos em `config/motion.ts` (stiffness/damping) nunca foram referenciados em nenhum componente.

---

### M-02 【Grave】Menu mobile aberto/fechado usa GSAP — sem interruptibilidade nem herança de velocidade

**Local:** `src/hooks/useMobileMenuAnimation.ts` (GSAP Timeline completo)

Problemas:
- GSAP é biblioteca baseada em timeline; não suporta interrupção em tempo real pelo usuário durante a animação
- Não há passagem de velocidade do gesto → velocity do spring (Apple §5)
- Ao fechar, apenas opacidade + deslocamento Y simples (`gsap.to(all, { opacity: 0, y: 10, duration: 0.2 })`), sem projeção de momentum

---

### M-03 【Médio】Entrada de texto do Hero usa API animate() ao invés de Variants — não responde à interrupção

**Local:** `src/components/home/hero/HeroCopy.tsx:34–57`

```tsx
animate('.hero-line', { y: [standard, 0], opacity: [0, 1], filter: [...] }, { delay: stagger(0.04), duration: 0.6, ease: GHOST_EASE })
```

- Usa `useAnimate` + chamada imperativa `animate()`; uma vez iniciado, não pode ser interrompido do meio
- Deveria adotar o padrão `initial/animate/exit` com variants, permitindo cancelamento graceful caso o usuário saia da viewport antes do término

---

### M-04 【Médio】Estratégia de degradação para prefers-reduced-motion incompleta

**Local:** `src/app/globals.css:679–684`

```css
@media (prefers-reduced-motion: reduce) {
  .animate-marquee { animation: none !important; transform: none !important; }
}
```

- Apenas marquee possui tratamento reduced-motion
- Hero blur reveal, animações GSAP do menu e gatilhos `whileInView` **não** possuem alternativas dentro deste media query
- O hook `useMotionGate()` já bloqueia parcialmente animações no nível do componente, mas regras CSS independentes não foram tratadas em sincronia

---

### M-05 【Leve】Marquee usa linear infinite, incompatível com intuição física Apple

**Local:** `src/app/globals.css:674–677`

```css
.animate-marquee { animation: marquee 38s linear infinite; }
```

Rolagem linear e constante carece de realismo físico. Sugere-se transição ease-in-out no loop ou driving via WebGL/Canvas com inércia.

---

## III. Violações Tipográficas e de Fontes

### T-01 【Grave】Risco de FOUT: ambas as fontes utilizam font-display: swap

**Local:** `src/styles/fonts.css:11, 30`

```css
font-display: swap;  /* Manrope */
font-display: swap;  /* PPSupplyMono (referência CDN) */
```

Conforme a skill do Design System — *"Never let fonts pop in (no FOUT) — ever"* — `font-display: swap` é a causa direta do FOUT. Títulos display (hero, manifesto) que alternam para a fallback geram reflow visível.

Adicionalmente, PPSupplyMono carrega do CDN `assets.codepen.io`; preconnect existe mas preload não, tornando a carga imprevisível.

---

### T-02 【Médio】Ausência de token dedicado de line-height e letter-spacing editorial

**Local:** `src/app/globals.css:248–340`

O DS 2.0 determina:
- `.text-body-editorial`: line-height `1.65`, medida `60ch–72ch`
- Atualmente existem apenas `.text-body` (line-height 1.5) e `.text-body-enhanced` (line-height 1.5)

Textos narrativos longos de case studies não possuem classificação tipográfica própria e precisam recorrer ao body padrão, criando落差 de experiência para a proposta de plataforma de diretor criativo executivo.

---

### T-03 【Leve】Valores de tracking inconsistentes, alguns excessivamente apertados

**Local:** Diversos

- Hero desktop: `tracking-[-0.07em]` (maior tamanho, aceitável)
- Heading display AboutMethod: `tracking-[-0.03em]` (4.5rem, frouxo demais)
- Falta declaração de `font-optical-sizing`

Recomendação Apple: tracking negativo -0.02~–0.05em para títulos grandes, ajustando progressivamente conforme o tamanho cresce; deve-se adicionar `font-optical-sizing: auto` para habilitar o ajuste óptico automático do navegador.

---

## IV. Violações de Material e Hierarquia

### MAT-01 【Médio】Header com dupla sobreposição translúcida, viola Apple §12

**Local:** `src/components/layout/header/DesktopFluidHeader.tsx:184–189`

```tsx
<div className="... bg-background/40 shadow-[...]">
  <div className="... opacity-60 pointer-events-none">
    {/* R3F glass canvas OR radial gradient */}
  </div>
</div>
```

Camada externa `bg-background/40` (40% opacidade) + canvas/gradiente interno (opacity-60): duas superfícies translúcidas empilhadas causam turvação visual. A diretriz Apple afirma categoricamente: "Never stack a light translucent surface on another."

---

### MAT-02 【Leve】Drop shadows decorativos excessivos em estado resting

**Local:**
- `ProjectCard.tsx:136`: `sm:hover:shadow-[0_18px_40px_rgba(0,0,0,0.4)]`
- `AdaptiveMediaLayout.tsx:236`: `shadow-[0_4px_12px_rgba(0,0,0,0.5)]`
- `AntigravityCTA.tsx:96`: `shadow-lg` (padrão Tailwind, valor pesado)

A filosofia Ghost DS é "flutuar sobre o vácuo": cartões não deveriam ter sombra em repouso, apenas surgirá sutilmente no hover. Vários locais aplicam sombra no estado resting.

---

## V. Violações de Preload e Carregamento WebGL

### L-01 【Médio】PPSupplyMono via CDN sem fallback skeleton

**Local:** `src/styles/fonts.css:20–31`

```css
src: url('https://assets.codepen.io/7558/PPSupplyMono-Variable.woff2') format('woff2'),
     local('Space Mono'), local('Courier New'), local('monospace');
font-display: swap;
```

- Fonte principal aponta para CDN de terceiro (CodePen Assets), sem controle do projeto
- Ausência de `<link rel="preload">` (ao contrário de Manrope, que possui)
- Em falha do CDN, o fallback para Space Mono/Courier gera reflow devido a métricas divergentes

---

### L-02 【Positivo】WebGL possui placeholder preto + SSR false + IntersectionObserver pausa loop

**Local:** `src/components/canvas/home/hero/GhostSceneWrapper.tsx:11–13, 29–36`

```tsx
loading: () => (
  <div className="absolute inset-0 w-full h-full bg-background" />
)
```

Este trecho está alinhado ao DS 2.0 — o primeiro frame nunca exibe tela vazia. Única melhoria possível: adicionar fade-in de opacidade no div `bg-background` para suavizar a aparição.

---

### L-03 【Leve】Importação dinâmica do componente R3F sem Suspense fallback

**Local:** `src/components/canvas/home/hero/GhostSceneWrapper.tsx:7–15`

A opção `loading` do `dynamic()` funciona, mas se o lazy load no nível de rota do Next.js App Router falhar, não há proteção. Recomenda-se envolver com `<Suspense fallback={...}>` na camada mais externa.

---

## VI. Governança de Z-Index

### Z-01 【Leve】Três ocorrências de z-[nnn] raw bypassam o sistema de tokens de z-index

**Locais:**
- `src/app/layout.tsx:76` — skip-link `z-[1300]` (ultrapassa z-layer-preloader 1000, intencional, aceitável com anotação)
- `src/components/ui/HTMLVideoBlock.tsx:174` — `z-[9999]` (lightbox fullscreen, razoável mas ignora token)
- `src/components/sobre/origin/OriginComponents.tsx:138` — `z-[9999]` (scanlines overlay)

A norma recomenda centralização em `globals.css @theme` ou `constants/z-indices.ts`. Dois dos três casos utilizam valor extremo 9999, contornando o sistema de governança.

---

## VII. UX Mobile e Layout

### U-01 【Médio】Card de Projeto no mobile remove borda e background, comprometendo identificação visual

**Local:** `src/components/portfolio/ProjectCard.tsx:137`

```tsx
const mobileCardClasses = "max-sm:!w-full max-sm:!h-auto max-sm:!border-none max-sm:!bg-transparent max-sm:!aspect-square ..."
```

Sem borda e fundo transparente, os cards no mobile fundem-se ao fundo da página, dificultando a identificação imediata da área interagível.

---

### U-02 【Leve】Feedback touch depende de CSS :active, não de spring motion

**Local:** `src/app/globals.css:502–511`

```css
.touch-feedback:active { transform: scale(0.97); opacity: 0.9; }
```

A pseudo-classe CSS active tem latência maior que spring (depende da pipeline de renderização do UA) e não permite cancelamento intermediário. Recomendado substituir por `<m.div whileTap={{ scale: 0.97 }}>` para resposta instantânea.

---

### U-03 【Leve】Menu mobile com fundo azul sólido `bg-bluePrimary`, inconsistente com Glass Pill do desktop

**Local:** `src/components/layout/header/mobile/MobileMenuPanel.tsx:43`

```tsx
className="... bg-bluePrimary px-8 backdrop-blur-xl ..."
```

Navegação desktop é pill de vidro fosco; menu mobile é tela cheia azul sólida — ruptura de material. Sugere-se `bg-background/95 backdrop-blur-xl` para manter consistência de material entre breakpoints.

---

## VIII. Resumo Quantificado

| Dimensão | Grave | Médio | Leve | Total |
|---|---|---|---|---|
| Arquitetura de Token | 2 | 2 | 0 | 4 |
| Motion | 2 | 2 | 1 | 5 |
| Tipografia / Fontes | 1 | 1 | 1 | 3 |
| Material / Hierarquia | 0 | 1 | 1 | 2 |
| Preload / WebGL | 0 | 1 | 1 | 2 |
| Z-Index | 0 | 0 | 1 | 1 |
| UX Mobile | 0 | 1 | 1 | 2 |
| **Total** | **5** | **8** | **6** | **19** |

---

*Este relatório contém apenas constatações da auditoria; nenhuma modificação de código foi realizada.*
