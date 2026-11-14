# Ghost Design System — Plano de Refatoração Executável & Robusto

**Baseado em:** `artifacts/ghost_ds_audit.md` e `.context/DESIGN-SYSTEM.md`
**Estado desejado:** Alinhamento completo com Ghost DS 2.0 + Princípios Apple Design
**Governança de Execução:** PREVC (`PLANNING → REVIEW → EXECUTION → VALIDATION → CONFIRMATION`) com **Checkpoints de Rollback por Fase**, **Validação de Bundle Size (QG-15)** e **Testes Automatizados de Reduced Motion (QG-13)**.

---

## Metodologia de Segurança & Rollback
Para cada fase deste plano:
1. **Branch Dedicada:** Cada fase inicia com `git checkout -b codex/ds-refactor-phase-N`.
2. **Rollback Instantâneo:** Em caso de regressão visual ou quebra de build, executar `git reset --hard HEAD~1` ou retornar à branch anterior.
3. **Gate Humano Obrigatório:** Nenhuma fase avança para a próxima sem verificação de evidência de comando e aprovação humana explícita.

---

## Fase 0 — Preparação Preliminar & Baseline (estimativa: 0,5 dia)

### Objetivo
Estabelecer baseline de refatoração, snapshots visuais e isolamento de branch.

| Passo | Conteúdo | Entregável |
|---|---|---|
| 0-1 | Criar branch `codex/ds-refactor-baseline` | Git branch |
| 0-2 | Criar `src/styles/globals-ghost-ds.css` (arquivo de tokens DS 2.0 de referência) | Arquivo novo |
| 0-3 | Produzir `artifacts/token-migration-map.md` mapeando variáveis antigas x novas | `artifacts/token-migration-map.md` |
| 0-4 | Capturar baseline visual via script Playwright em viewports `375px`, `768px`, `1440px` | `.taste-skill/before/` |

**Checklist de Aprovação Humana (Fase 0):**
- [ ] Mapeamento de tokens validado sem duplicidade crítica.
- [ ] Baseline visual capturado com sucesso.

---

## Fase 1 — Unificação de Tokens & Limpeza de CSS (estimativa: 1–1,5 dia)

> Escopo: CSS global e componentes de UI; risco: baixo (renomeação de variáveis).

### 1.1 Rollback Checkpoint
`git checkout -b codex/ds-refactor-phase-1`

### 1.2 Inclusão de Tokens Faltantes
No `@theme` de `src/app/globals.css`, adicionar tokens oficiais do DS 2.0 §2:
- `--color-text-editorial: #E2E6F0`
- `--color-text-muted-aa: #B4B8C5`
- `--color-abyss-end: #040013`
- `--color-glass-surface: rgba(255,255,255,0.05)`
- `--color-glass-border: rgba(255,255,255,0.1)`

### 1.3 Migração Segura de Nomenclaturas & Shadcn
- Manter aliases backward-compat para `--color-bluePrimary` marcados com `@deprecated`.
- **Salvaguarda Shadcn (EX-01):** As variáveis base shadcn (`--card`, `--popover`, `--sidebar`) não serão removidas em massa para evitar quebra de componentes nativos de formulário. Em vez disso, serão isoladas em um bloco dedicado `.shadcn-compat` ou ajustadas pontualmente onde causarem conflito visual.
- Executar `rg --type tsx "bg-\[#"` para inventariar e substituir cores hardcoded pelas variáveis correspondentes em componentes como `ShaderSection.tsx`, `OriginComponents.tsx`, `DesktopFluidHeader.tsx`.

### 1.4 Validação Fase 1
- `pnpm typecheck` (QG-01)
- `pnpm lint` (QG-02)

**Checklist de Aprovação Humana (Fase 1):**
- [ ] Zero erros de tipagem e lint.
- [ ] Verificação visual de que os componentes mantiveram fidelidade cromática sem hex hardcoded.

---

## Fase 2 — Refatoração do Sistema de Motion & Springs (estimativa: 2 dias)

> Escopo: interações de UI com Framer Motion; risco: médio.

### 2.1 Rollback Checkpoint
`git checkout -b codex/ds-refactor-phase-2`

### 2.2 Configuração Padrão de Spring (Apple Design §4)
Em `src/config/motion.ts`, registrar `GHOST_SPRING_DEFAULT` (dampings críticos sem overshoot) e `GHOST_SPRING_MOMENTUM`.

### 2.3 Migração de Tweens & GSAP Mobile Menu
- Substituir tweens lineares em `AntigravityCTA.tsx`, `DesktopFluidHeader.tsx` e botões de contato por `GHOST_SPRING_DEFAULT`.
- Reescrever `useMobileMenuAnimation.ts` de GSAP Timeline puramente imperativo para Framer Motion `AnimatePresence` com suporte a interrupção por gesto.
- Manter GSAP apenas em animações parallax estritas de background (ex: `useOriginAnimations.ts`).

### 2.4 Validação de Performance e Bundle (QG-15)
- Executar `pnpm build --report` antes e depois da Fase 2 para registrar o delta de First Load JS (budget estrito < 180KB).

**Checklist de Aprovação Humana (Fase 2):**
- [ ] Interações de botão e menu mobile respondem com spring fluído e interruptível.
- [ ] Relatório de bundle size aprovado sem estouro de budget.

---

## Fase 3 — Otimização de Fontes & FOUT Prevention (estimativa: 0,5 dia)

### 3.1 Rollback Checkpoint
`git checkout -b codex/ds-refactor-phase-3`

### 3.2 Estratégia FOUT & PPSupplyMono
- Implementar script síncro-gate no `<head>` (`.html.fonts-pending`) com timeout de segurança de 2500ms, eliminando pisucamento de fontes.
- Adicionar `<link rel="preload" as="font" href="https://assets.codepen.io/7558/PPSupplyMono-Variable.woff2" crossorigin>` para acelerar o carregamento da fonte mono técnica.

### 3.3 Token de Tipografia Editorial
- Inserir `.text-body-editorial` em `globals.css` (`line-height: 1.65`, `max-width: 72ch`, cor `--color-text-editorial`).

**Checklist de Aprovação Humana (Fase 3):**
- [ ] Carregamento de página sem reflow visível (FOUT mitigado).

---

## Fase 4 — Correção de Materiais, Z-Index & Hierarquia (estimativa: 1 dia)

### 4.1 Rollback Checkpoint
`git checkout -b codex/ds-refactor-phase-4`

### 4.2 Eliminação de Camadas Translúcidas Duplas (MAT-01)
- Em `DesktopFluidHeader.tsx`, remover o container `bg-background/40` aninhado sobre canvas translúcido, deixando apenas uma única superfície de vidro fosco unificada.
- Retirar sombras decorativas excessivas em estado resting (`ProjectCard.tsx`, `AntigravityCTA.tsx`).

### 4.3 Centralização de Z-Index
- Consolidar ocorrências de `z-[9999]` em `src/constants/z-indices.ts` alinhando com a escala de 19 camadas do DS 2.0.

**Checklist de Aprovação Humana (Fase 4):**
- [ ] Header e cartões apresentam estética limpa e sem sobreposição turva de opacidades.

---

## Fase 5 — Aprimoramento de UX Mobile (estimativa: 0,5 dia)

### 5.1 Rollback Checkpoint
`git checkout -b codex/ds-refactor-phase-5`

### 5.2 Ajustes Mobile
- Restaurar bordas e fundos sutis nos cards de projeto no mobile (`ProjectCard.tsx`) para evitar fusão com o fundo.
- Substituir `.touch-feedback:active` por `whileTap` do Framer Motion, garantindo feedback imediato em toque.
- Unificar menu mobile com `bg-background/95 backdrop-blur-xl` (coerente com a pílula de vidro do desktop).

**Checklist de Aprovação Humana (Fase 5):**
- [ ] Navegação e usabilidade em viewports mobile (< 768px) validadas.

---

## Fase 6 — Validação Completa, Quality Gates & Reduced Motion (estimativa: 1 dia)

### 6.1 Automação de Reduced Motion (QG-13)
- Criar script Playwright `tests/reduced-motion.spec.ts` emulando `reducedMotion: 'reduce'` para verificar desativação de animações contínuas e paralaxes.

### 6.2 Execução Rigorosa de Quality Gates
| Gate ID | Dimensão | Comando de Evidência Obrigatória |
|---|---|---|
| QG-01 | TypeScript | `pnpm typecheck` (0 erros) |
| QG-02 | ESLint & Z-Index | `pnpm lint` (0 erros, zero z-[nnn] raw) |
| QG-07 | Acessibilidade | Lighthouse / Axe-core (WCAG AA ≥ 4.5:1) |
| QG-13 | Reduced Motion | `pnpm test:e2e tests/reduced-motion.spec.ts` |
| QG-15 | Build de Produção | `pnpm build` (sucesso limpo) |

**Checklist Final de Aceite Humano:**
- [ ] Todos os Quality Gates reportados como `PASS` com evidência de comando.
- [ ] Comparação visual antes/depois aprovada sem regressão estética.

