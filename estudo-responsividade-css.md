# Estudo: Responsividade no CSS

Este material e um guia rapido para aprender e praticar responsividade em CSS.

## 1) O que e responsividade

Responsividade e a capacidade de um layout se adaptar a diferentes tamanhos de tela:

- celular
- tablet
- notebook
- monitor grande

Objetivo: manter boa leitura, espacamento e usabilidade em qualquer dispositivo.

## 2) Base obrigatoria no HTML

Sempre inclua no `head`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

Sem isso, o navegador mobile pode renderizar a pagina como se fosse desktop reduzido.

## 3) Unidades mais usadas

Prefira unidades flexiveis:

- `%` para larguras relativas ao elemento pai
- `vw` e `vh` para tamanho relativo a viewport
- `rem` para tipografia e espacamentos consistentes
- `fr` no CSS Grid para dividir espaco

Evite travar layout com muitos valores fixos em `px`.

## 4) Mobile First

Abordagem recomendada:

1. Comece o CSS para telas pequenas (mobile)
2. Depois adicione `@media (min-width: ...)` para telas maiores

Exemplo:

```css
.card {
  padding: 1rem;
  font-size: 1rem;
}

@media (min-width: 768px) {
  .card {
    padding: 1.5rem;
    font-size: 1.125rem;
  }
}
```

## 5) Media Queries essenciais

### Breakpoints comuns (nao sao regras fixas)

- 480px (celulares maiores)
- 768px (tablet)
- 1024px (desktop pequeno)
- 1280px+ (desktop grande)

Exemplo:

```css
.container {
  width: min(100% - 2rem, 1100px);
  margin-inline: auto;
}

@media (min-width: 768px) {
  .grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }
}

@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

## 6) Flexbox para responsividade

Bom para alinhamento em uma dimensao (linha OU coluna).

```css
.menu {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

.menu a {
  flex: 1 1 140px;
}
```

`flex-wrap: wrap` evita que itens estourem em telas pequenas.

## 7) Grid para layouts mais complexos

Bom para duas dimensoes (linhas E colunas).

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}
```

`auto-fit + minmax` cria colunas adaptaveis sem varios media queries.

## 8) Imagens responsivas

```css
img {
  max-width: 100%;
  height: auto;
  display: block;
}
```

Se necessario, use `object-fit`:

```css
.thumb {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;
}
```

## 9) Tipografia fluida

Use `clamp()` para texto escalar sem exagero:

```css
h1 {
  font-size: clamp(1.5rem, 2.5vw, 2.5rem);
}
```

Formato: `clamp(minimo, ideal, maximo)`.

## 10) Padrao util para container

```css
:root {
  --max-width: 1100px;
  --space: 1rem;
}

.container {
  width: min(100% - (var(--space) * 2), var(--max-width));
  margin-inline: auto;
}
```

## 11) Erros comuns

- Esquecer meta viewport
- Usar largura fixa em todos os blocos
- Nao testar em tela pequena real
- Muito breakpoint sem necessidade
- Nao considerar espacamento e toque em botoes mobile

## 12) Checklist rapido

- [ ] A pagina funciona em 320px de largura?
- [ ] O texto continua legivel sem zoom?
- [ ] Botoes tem area boa para toque?
- [ ] Imagens nao estouram o layout?
- [ ] Layout usa Flexbox/Grid com adaptacao?
- [ ] Existe estrategia mobile first?

## 13) Exercicio pratico (20 min)

Crie um layout com:

- cabecalho
- secao principal com cards
- rodape

Regras:

1. Mobile: 1 coluna
2. Tablet (>= 768px): 2 colunas
3. Desktop (>= 1024px): 3 colunas
4. Imagens ajustadas com `max-width: 100%`
5. Titulo principal com `clamp()`

## 14) Mini template para iniciar projetos

```css
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family:
    system-ui,
    -apple-system,
    Segoe UI,
    Roboto,
    sans-serif;
  line-height: 1.5;
}

img {
  max-width: 100%;
  height: auto;
  display: block;
}

.container {
  width: min(100% - 2rem, 1100px);
  margin-inline: auto;
}

.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

@media (min-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

---

Se quiser, no proximo passo eu posso transformar este estudo em uma pagina HTML de resumo visual com exemplos funcionando lado a lado.
