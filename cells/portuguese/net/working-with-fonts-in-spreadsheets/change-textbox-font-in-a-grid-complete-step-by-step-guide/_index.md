---
category: general
date: 2026-06-21
description: Aprenda como alterar a fonte de uma caixa de texto, definir a cor da
  fonte programaticamente e ajustar o tamanho da fonte da célula em uma grade. Siga
  este tutorial prático para estilizar caixas de texto.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: pt
og_description: Altere a fonte da caixa de texto em uma grade rapidamente. Este guia
  mostra como estilizar a caixa de texto, definir a cor da fonte programaticamente
  e ajustar o tamanho da célula com código claro.
og_title: Alterar a Fonte da Caixa de Texto em uma Grade – Tutorial Completo de Programação
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Alterar a Fonte da Caixa de Texto em uma Grade – Guia Completo Passo a Passo
url: /pt/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alterar a Fonte da Caixa de Texto em uma Grade – Guia Completo Passo a Passo

Já precisou **alterar a fonte da caixa de texto** dentro de uma grade de dados, mas não sabia qual propriedade ajustar? Você não está sozinho—a maioria dos desenvolvedores encontra esse obstáculo ao criar tabelas editáveis ou dashboards. Neste tutorial vamos percorrer exatamente como mudar a fonte da caixa de texto, definir sua cor programaticamente e ainda ajustar o tamanho da fonte célula por célula.

Também vamos incluir dicas sobre **como estilizar caixas de texto**, abordar cenários de **alterar tamanho da fonte da célula** e mostrar como **definir a cor da fonte programaticamente** sem perder a cabeça. Ao final, você terá um trecho reutilizável que funciona com qualquer componente de grade que exponha a API `getCell`.

## Pré‑requisitos

- Um navegador moderno com suporte a ES6 (Chrome, Edge, Firefox, Safari)
- Uma biblioteca de grade que ofereça `grid.getCell(row, col)` e retorne um objeto de célula contendo uma referência `textbox`
- Conhecimento básico de objetos JavaScript e propriedades CSS

Nenhum pacote adicional é necessário—apenas JavaScript puro e a própria API da grade.

## Visão Geral da Solução

A ideia central é simples: obter a célula alvo, capturar sua caixa de texto incorporada e, em seguida, atribuir um novo objeto de fonte que define família, tamanho e cor. Pense nisso como dar um novo visual à caixa de texto. A seguir, o fluxo de alto nível:

1. **Acessar a célula alvo** – localizar a linha/coluna desejada.
2. **Recuperar a caixa de texto** – o elemento UI que contém o texto.
3. **Criar um objeto de estilo de fonte** – especificar família, tamanho e cor.
4. **Aplicar o estilo** – atribuir o objeto à propriedade `font` da caixa de texto.

É isso. Vamos mergulhar em cada passo, explicar por que ele importa e ver o código em ação.

![Captura de tela de uma célula de grade com uma caixa de texto estilizada – alterar fonte da caixa de texto](/images/change-textbox-font-example.png)

## Passo 1: Acessar a Célula Alvo na Grade

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Por que isso importa:**  
> Grades geralmente armazenam linhas e colunas como índices baseados em zero. Ao chamar `grid.getCell(2, 3)` obtemos a célula na **linha 2, coluna 3**. Se precisar **alterar tamanho da fonte da célula** em outra posição, basta ajustar os índices.

**Dica profissional:** Se sua grade suportar colunas nomeadas, você pode substituir a coluna numérica por uma chave, por exemplo, `grid.getCell(2, "price")`.

## Passo 2: Capturar a Caixa de Texto Dentro Dessa Célula

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **O que está acontecendo:**  
> A maioria das implementações de grade envolve o conteúdo editável dentro de um elemento `<input>` ou `<textarea>` e o expõe como `cell.textbox`. Obter a referência nos permite manipular seu estilo visual diretamente.

Se a grade usar um nome de propriedade diferente (como `cell.editor`), ajuste o código de acordo—esta é uma variação comum ao **como estilizar caixas de texto** para um componente personalizado.

## Passo 3: Definir as Propriedades de Fonte Desejadas

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Detalhando o Objeto

| Propriedade | Finalidade | Valores de Exemplo |
|-------------|------------|--------------------|
| `family`    | Família da fonte – controla o tipo de letra. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`      | Tamanho da fonte em pixels (ou pontos, dependendo da grade). | `12`, `14`, `16` |
| `color`     | Cor do texto em qualquer formato compatível com CSS. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Por que usamos um objeto:**  
> Agrupar os três atributos torna o código mais organizado e reflete como muitas bibliotecas UI esperam informações de estilo. Também permite **alterar família de fonte da grade** ou **definir cor da fonte programaticamente** com uma única atribuição.

## Passo 4: Aplicar o Estilo de Fonte à Caixa de Texto

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Nos bastidores:**  
> O componente de caixa de texto da grade interpreta a propriedade `font` e atualiza seu CSS de acordo. Essa única linha substitui a família, o tamanho e a cor da fonte anteriores de uma só vez—exatamente o que você precisa ao **alterar fonte da caixa de texto** em várias células.

Se o componente usar uma API diferente (por exemplo, `textbox.style.fontFamily = ...`), adapte a atribuição mantendo o mesmo princípio.

## Exemplo Completo Funcional

Abaixo está um trecho autônomo que você pode colar em um arquivo HTML que inclui um objeto de grade simulado. Ele demonstra todo o fluxo do passo 1 ao passo 4, além de uma rápida verificação de que o estilo foi alterado.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Saída Esperada

- A caixa de texto localizada na **linha 2, coluna 3** agora exibe texto em **Arial**, **14 px**, e um tom azul **#0066CC**.
- Abrindo o console do navegador será impresso algo como:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Se você abrir a página, confirmará visualmente a mudança—não há mais fonte padrão do sistema.

## Perguntas Frequentes (FAQ)

### Posso mudar apenas o tamanho da fonte sem afetar a família ou a cor?
Com certeza. Basta omitir as propriedades que você não deseja modificar:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### E se minha grade usar um nome de propriedade diferente para a caixa de texto?
Inspecione o objeto da célula no console (`console.log(cell)`). Você provavelmente verá algo como `cell.editor` ou `cell.input`. Substitua `cell.textbox` pela referência correta.

### Como aplicar o mesmo estilo a uma coluna inteira?
Percorra as linhas e defina a fonte para cada célula daquela coluna:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Existe uma forma de reverter para a fonte original?
Armazene o estilo original antes de sobrescrevê‑lo:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Dicas & Boas Práticas

- **Atualizações em lote:** Se precisar estilizar muitas células, envolva as mudanças em `requestAnimationFrame` ou em um método de lote específico da grade para evitar “layout thrashing”.
- **Fontes responsivas:** Use unidades relativas (`em`, `rem`) em vez de pixels fixos se sua UI precisar escalar.
- **Acessibilidade:** Garanta contraste suficiente ao **definir cor da fonte programaticamente**—o mínimo WCAG AA é uma proporção de 4,5:1 para texto normal.
- **Quirks entre navegadores:** Algumas grades mais antigas podem exigir a definição direta de `style.fontFamily` no elemento `<input>` em vez de usar um objeto `font`.

## Conclusão

Acabamos de cobrir **como alterar a fonte da caixa de texto** dentro de uma grade, desde capturar a célula correta até definir um objeto reutilizável `fontStyle` e aplicá‑lo em uma única linha. No caminho, aprendemos a **alterar tamanho da fonte da célula**, **definir cor da fonte programaticamente** e até ajustar a **alterar família de fonte da grade** para uma coluna específica.

Agora você pode levar esse padrão e adaptá‑lo a qualquer biblioteca UI—seja construindo um dashboard administrativo, um editor estilo planilha ou uma ferramenta de relatórios personalizada. Experimente diferentes famílias, tamanhos e cores; talvez adicione efeitos de hover ou estilização condicional baseada em valores de dados.

Tem outro desafio de estilo? Deixe um comentário e vamos enfrentá‑lo juntos. Feliz codificação!

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Alterar a Cor da Fonte no Excel Usando Aspose.Cells para Java: Um Guia Completo](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Alterar Cor da Fonte Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Alterar Cor da Fonte Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}