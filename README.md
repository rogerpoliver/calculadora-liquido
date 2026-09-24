# Calculadora de Líquido

Single-page calculator for a Simples Nacional PJ: type the gross amount received in the month and see how much goes to taxes and services and how much is left.

**Live:** https://rogerpoliver.github.io/calculadora-liquido/

## Usage

1. Open the page and type the gross amount (e.g. `28.084,65`).
2. Read the net amount and the breakdown.

Default deductions:

| Item | Default |
| --- | --- |
| Simples Nacional | 6% of gross |
| INSS | R$ 180,00 |
| Contabilidade | R$ 297,00 |

Use **Editar valores** to change them. Edited values stay on this device (browser storage) until **Restaurar padrão**. The gross amount is never stored.

## Development

Plain `index.html`, no build. Open it in a browser, or serve it:

```bash
python3 -m http.server 8765
```

Planning lives in `openspec/`.
