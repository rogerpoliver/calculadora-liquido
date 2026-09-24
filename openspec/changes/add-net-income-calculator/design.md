# Design

## Context

Greenfield repo. See proposal.md - Why. Monthly, single-user, personal tool; GitHub account `rogerpoliver` is authenticated on this machine.

## Goals / Non-Goals

**Goals:**
- Open → type → read in under 5 seconds, on phone or desktop.
- Apple-style craft: system font, clear hierarchy, net amount as the hero number.

**Non-Goals:**
- History of past months, charts, export.
- Other tax regimes (Fator R, Anexo changes, IRPF, pró-labore split).
- Build tooling, frameworks, tests runner.

## Decisions

- **Single `index.html` with inline CSS/JS, no build.** GitHub Pages serves it as-is from `main` root. Alternative (Vite/React) rejected: zero benefit for one screen, adds maintenance.
- **Integer-cents math.** Parse inputs into cents, compute `simples = round(grossCents × rate / 100)`, sum in cents. Avoids float drift (`0.1 + 0.2`). Rate kept as a number with up to 2 decimals.
- **Formatting via `Intl.NumberFormat('pt-BR', { style: 'currency', currency: 'BRL' })`.** Parsing: strip `R$`/spaces, remove `.`, swap `,` → `.`.
- **Input: `inputmode="decimal"`** so phones open the numeric keypad; formatting applied on blur, not while typing (live reformat fights the caret).
- **Live recalculation on `input`**, no submit button (§1 Response: feedback is continuous).
- **Deduction editor = disclosure panel** under an "Editar valores" button (common path first, advanced one level deeper). Open/close is a height+opacity transition with critically damped feel (~300ms ease-out); cross-fade only under `prefers-reduced-motion`.
- **Persistence: `localStorage` key `calculadora-liquido:deductions`**, wrapped in try/catch; only deductions stored, never gross. A "Valores personalizados" badge appears when they differ from defaults.
- **Layout:** card with gross input on top; hero "Sobra pra você" number; itemized list (Simples, INSS, Contabilidade, Total) with deduction share; colors as CSS tokens with dark-mode overrides; buttons react on `:active` (scale 0.97).

## Risks / Trade-offs

- [Public repo exposes default INSS/fee values] → Low sensitivity; no gross amount or personal data is committed. Private repo + Pages needs a paid plan.
- [Simples rate changes with revenue bracket] → Rate is editable and persisted.
- [localStorage unavailable (private mode)] → Falls back to defaults silently.

## Migration Plan

1. Commit locally.
2. With the owner's explicit go: `gh repo create rogerpoliver/calculadora-liquido --public --source . --push`, then enable Pages on `main` / root via `gh api`.
3. Rollback: disable Pages or delete the repo from GitHub.
