# Tasks

## 1. Page

- [x] 1.1 Create `index.html` with gross input (autofocus, `inputmode="decimal"`), hero net amount and itemized breakdown; verify it opens from disk with no console errors
- [x] 1.2 Implement pt-BR parsing and integer-cents calculation; verify `28.084,65` → Simples `R$ 1.685,08`, total `R$ 2.162,08`, net `R$ 25.922,57`, share `7,7%`, and `300,00` → net `-R$ 195,00` in warning style
- [x] 1.3 Add "Editar valores" disclosure with Simples %, INSS and Contabilidade inputs, live recalculation, localStorage persistence, "Valores personalizados" badge and "Restaurar padrão"; verify edit → reload keeps values, restore returns defaults, gross is not remembered
- [x] 1.4 Apply styling (system font, tokens, dark mode, phone width, `:active` feedback, reduced-motion fallback); verify at 375px and desktop, light and dark

## 2. Repository

- [x] 2.1 Add `README.md` (what it is, how to use, Pages URL) and `.gitignore`; verify `git status` shows only intended files
- [x] 2.2 Commit locally with a Conventional Commit message; verify `git log` shows it

## 3. Publish (only after the owner's explicit go-ahead)

- [ ] 3.1 Create public GitHub repo `rogerpoliver/calculadora-liquido` and push `main`; verify the repo page lists `index.html`
- [ ] 3.2 Enable GitHub Pages on `main` / root; verify `https://rogerpoliver.github.io/calculadora-liquido/` renders the reference month correctly
