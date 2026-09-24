# Proposal

## Why

Every month the owner receives a gross PJ payment and needs to know, in seconds, how much goes to taxes and services and how much is left. Today this is done by hand (6% Simples Nacional + fixed INSS + fixed accounting fee), which is repetitive and error-prone.

## What Changes

- New static web page, published on GitHub Pages, that takes the gross amount received and shows the breakdown: Simples Nacional, INSS, accounting fee, total deductions, net amount, and deductions as a percentage of gross.
- Deduction values come pre-filled with defaults (Simples 6%, INSS R$ 180,00, accounting R$ 297,00), so the normal monthly flow is: open page → type gross → read result.
- An "Editar valores" control reveals the three deduction inputs so a month can be calculated with different values; a "Restaurar padrão" control returns to the defaults.
- New repository `calculadora-liquido` under `~/www`, with a public GitHub remote serving the page.

## Capabilities

### New Capabilities
- `net-income-calculator`: gross-to-net calculation for a Simples Nacional PJ, with default deductions, editable overrides and a pt-BR (BRL) presentation.

### Modified Capabilities
<!-- none -->

## Impact

- New repo, no existing code affected.
- No backend, no dependencies, no data leaves the browser. Edited deduction values are kept only in the visitor's own browser storage.
- Publishing requires creating a GitHub repository and enabling Pages — an outward-facing step done only with the owner's explicit go-ahead.
