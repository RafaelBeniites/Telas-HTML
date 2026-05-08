# HABIT — Projeto Interface (HTML + CSS)

Reconstrução fiel em HTML5 + CSS3 puros dos mockups do exercício acadêmico (Mackenzie). Sem frameworks, sem JavaScript, mobile-first com 5 breakpoints, acessível conforme WCAG AA.

## Repositório

- **URL pública**: https://github.com/RafaelBeniites/Telas-HTML
- **Branch principal**: `main`
- **Branch de desenvolvimento**: `bruno-oliveira`

## Como visualizar

Abra `index.html` em qualquer navegador moderno. Não há build, dependências ou servidor — basta clonar o repositório e abrir o arquivo.

```bash
git clone <url-do-repositorio>
cd Telas-HTML
# abrir index.html no navegador
```

## Telas implementadas

| # | Arquivo | Descrição |
|---|---------|-----------|
| 1 | `index.html` | Home — navegue por tópicos, categorias populares, todas as categorias, postagens em destaque, escolhas do editor |
| 2 | `html/categoria-techno.html` | Listagem da categoria Techno com filtros e grid 3×3 |
| 3 | `html/destaques.html` | Grid 3×3 de destaques |
| 4 | `html/newsletter.html` | Assinatura da newsletter |
| 5 | `html/busca.html` | Resultados de busca |
| 6 | `html/entrar.html` | Login (e-mail/senha + Google) |
| 7 | `html/cadastro.html` | Criar conta |
| 8 | `html/perfil.html` | Perfil + Suas Postagens |
| 9 | `html/admin-categorias.html` | Admin — CRUD de categorias |
| 10 | `html/admin-criar-post.html` | Admin — editor de post |
| 11 | `html/admin-escolhas-editor.html` | Admin — escolhas do editor |
| 12 | `html/admin-usuarios.html` | Admin — gestão de usuários |
| 13 | `html/admin-fila-revisao.html` | Admin — fila de revisão |
| 14 | `html/admin-fila-comentarios.html` | Admin — fila de comentários |

## Estrutura de pastas

```
/
  index.html                    Home (raiz, conforme rubrica)
  /html/                        13 páginas internas
  /css/
    tokens.css                  :root com cores, tipografia, espaçamento
    reset.css                   normalização mínima
    base.css                    tipografia base, foco visível, skip-link
    layout.css                  container e page-shell
    /components/                header, footer, button, form, card, table,
                                sidebar, pill, placeholder
    /pages/                     home, categoria, destaques, auth, perfil,
                                busca, admin
  /assets/
    placeholder.svg             placeholder cinza reutilizado
    favicon.svg
  /docs/                        PDF do enunciado
  README.md
```

## Decisões de layout

- **Mobile-first**: o CSS base é escrito para telas ≤ 420px; o layout cresce via `@media (min-width: ...)`. Nenhuma regra usa `max-width` para layout principal.
- **CSS Grid** para layouts macro (admin shell, home-bottom, perfil, grids de cards). **Flexbox** para componentes (header, pills, ações, cards).
- **Sem `<table>` para layout** — `<table>` é usada apenas para dados tabulares (Usuários, Fila de revisão, Fila de comentários) e é transformada em cards verticais no mobile via CSS, preservando a semântica.
- **Header com hambúrguer CSS-only** abaixo de 768px, usando `<input type="checkbox" hidden>` + `<label>`. Em ≥768px o menu volta a layout horizontal.
- **Sidebar admin** vira `<details>` colapsável em mobile e ganha posição fixa de 260px à esquerda em ≥768px (grid `260px 1fr`).
- **Reuso de componentes**: header, footer e shell admin têm o mesmo HTML em todas as páginas. As classes CSS são compartilhadas, garantindo consistência visual.
- **Acessibilidade integrada ao layout**: skip-link em todas as páginas, `aria-current="page"` no item ativo do menu, `aria-label` em ícones, `aria-labelledby` em sections.

## Breakpoints utilizados

| Largura | Dispositivo | Mudanças principais |
|---------|-------------|---------------------|
| ≤ 420 px | Mobile pequeno (base) | Layout em coluna única, hambúrguer ativo, tabelas em cards verticais |
| ≥ 480 px | Mobile grande | Cards 2 colunas, footer 2 colunas |
| ≥ 640 px | Mobile XL | Grid de posts 2 colunas, resultados de busca com mídia maior |
| ≥ 768 px | Tablet | Header em linha, sidebar admin fixa, tabelas voltam ao formato linha, footer 3 colunas |
| ≥ 1024 px | Desktop | Layout final do mockup, grids 3 colunas, perfil 2 colunas, footer 5 colunas |
| ≥ 1440 px | Monitor grande | Container limitado a 1200px centralizado, ajustes finos de tipografia |

Atende ao mínimo da rubrica (≥3 breakpoints) e cobre 320–1440px conforme exigido.

## Observações de acessibilidade

- **Tags semânticas** em todas as páginas: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`.
- **Hierarquia de títulos** respeitada: 1 `<h1>` por página (título da tela), `<h2>` para seções, `<h3>` para cards e sub-blocos. Nenhum nível pulado.
- **Formulários acessíveis**:
  - Todo `<input>` tem `<label for="id">` visível associado.
  - `type` correto em cada campo (`email`, `password`, `search`, `checkbox`, `submit`, `button`).
  - Atributos `required` e `autocomplete` quando aplicável.
- **Imagens e ícones**:
  - `alt` descritivo em imagens não-decorativas; placeholders puramente visuais marcados com `aria-hidden="true"`.
  - `aria-label` em todos os links/botões que não têm texto visível (footer, brand).
- **Foco visível**: regra global `:focus-visible` aplica `outline: 3px solid #0F766E` com `outline-offset: 2px` em todos os elementos focáveis.
- **Skip link**: "Pular para o conteúdo" presente em todas as páginas, visível apenas no foco.
- **Contraste WCAG AA validado** (calculado sobre fundo branco):
  - `--color-text` (#111827): **16.9:1** ✓
  - `--color-text-muted` (#4B5563): **7.6:1** ✓
  - `--color-text-subtle` (#6B7280): **4.8:1** ✓
  - `--color-primary` (#0F766E): **5.5:1** ✓
  - Texto branco sobre `--color-primary`: **5.5:1** ✓
- **Estados de interação visíveis**: `:hover`, `:focus`, `:focus-visible`, `:active` e `:disabled` definidos para todos os botões e links.
- **Navegação por teclado**: ordem lógica de tab, sem armadilhas de foco, sem elementos focáveis fora do fluxo visual.

## Restrições técnicas atendidas

- ❌ Sem frameworks CSS (sem Bootstrap, Tailwind, etc.)
- ❌ Sem `<table>` para layout
- ❌ Sem imagens contendo títulos/labels
- ✅ CSS Grid e Flexbox apenas
- ✅ Mobile-first com base ≤ 420px
- ✅ 5 breakpoints (excede o mínimo de 3 da rubrica)
- ✅ Variáveis CSS centralizadas em `:root`
- ✅ Escala tipográfica em rem (h1 2.5, h2 2, h3 1.5, body 1, small 0.875)
- ✅ Tokens de espaçamento consistentes (xs/sm/md/lg/xl/2xl)
- ✅ Imagens fluidas (`max-width: 100%; height: auto` no reset)
- ✅ Contraste mínimo WCAG AA (4.5:1 para texto, 3:1 para grandes/ícones)
- ✅ Estados `:hover`, `:focus`, `:active`, `:disabled` visíveis

## Autores

- **Bruno Oliveira**
- **Caue Kenzo**
- **Rafael Benites**
