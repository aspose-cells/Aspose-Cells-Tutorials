---
category: general
date: 2026-06-30
description: Aprenda a obter o endereço da célula selecionada, atualizar o valor da
  célula da grade e ler o valor de entrada com JavaScript usando GridJs. Código passo
  a passo e dicas.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: pt
og_description: Obtenha o endereço da célula selecionada, atualize o valor da célula
  da grade e leia o valor de entrada com JavaScript. Siga este guia completo para
  uma integração suave do GridJs.
og_title: Obtenha o Endereço da Célula Selecionada – Tutorial Completo de GridJs JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Obtenha o Endereço da Célula Selecionada no GridJs – Guia Completo de JavaScript
url: /pt/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obter Endereço da Célula Selecionada – Tutorial Completo de JavaScript com GridJs

Já precisou **obter o endereço da célula selecionada** de uma tabela GridJs, mas não sabia qual chamada de API usar? Você não está sozinho. Em muitos painéis de administração, os usuários clicam em uma célula, editam um valor em um modal e esperam que a grade reflita a alteração instantaneamente. Este tutorial mostra exatamente como recuperar esse endereço, ler o novo preço de um campo de entrada e **atualizar o valor da célula da grade** sem recarregar a página.

Também abordaremos **ler o valor da entrada com JavaScript** da maneira correta, lidar com casos extremos e fechar o modal assim que a atualização terminar. Ao final, você terá um trecho autônomo que pode inserir em qualquer projeto que use GridJs.

## O que Você Vai Construir

- Uma tabela HTML simples alimentada por GridJs.
- Um modal de edição que aparece quando uma célula é clicada.
- JavaScript que **obtém o endereço da célula selecionada**, captura o preço digitado pelo usuário, **atualiza o valor da célula da grade** e, finalmente, oculta o modal.

Nenhuma biblioteca externa além do GridJs é necessária, e o código funciona com navegadores modernos (Chrome 102+, Edge, Firefox). Se você já tem uma instância do GridJs na página, pode copiar‑colar as partes relevantes diretamente.

## Pré‑requisitos

- Conhecimento básico de JavaScript e do DOM.
- Biblioteca GridJs carregada (via CDN ou npm).
- Uma página que já renderiza uma grade GridJs (mostraremos um exemplo mínimo).

Se algum desses itens lhe for desconhecido, não entre em pânico — cada passo inclui um breve resumo.

---

## Etapa 1: Configurar o Esqueleto HTML

Primeiro, disponha o contêiner da tabela, o modal oculto e a entrada de preço. O modal será alternado com classes CSS simples.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Dica profissional:** O `#editModal` usa um truque CSS mínimo — basta adicionar a classe `active` para exibi-lo. Você pode substituir isso por Bootstrap, Tailwind ou qualquer componente de modal que já use.

---

## Etapa 2: Inicializar o GridJs e Capturar Cliques nas Células

Agora criaremos uma grade com dados de exemplo e ouviremos as seleções de células. Quando um usuário clicar em uma célula, **obteremos o endereço da célula selecionada** e abriremos o modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Por que isso funciona:** `GridJs.getSelectedCell()` retorna uma string como `"C2"` (coluna C, linha 2). Armazená‑la em `lastSelectedCell` nos permite referenciar a localização exata quando mais tarde **atualizarmos o valor da célula da grade**.

---

## Etapa 3: Ler o Novo Preço do Campo de Entrada

Quando o usuário clicar em **Salvar**, precisamos **ler o valor da entrada com JavaScript** de forma segura. Esta etapa também valida se o preço inserido é um número positivo.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Nota:** Usar `parseFloat` garante que aceitamos decimais (ex., `1.99`). A verificação `isNaN` impede envios acidentais vazios.

---

## Etapa 4: Atualizar o Valor da Célula Selecionada

Agora finalmente **atualizamos o valor da célula da grade** usando o endereço que capturamos antes. O método `updateCell` do GridJs retorna uma promise, então podemos encadear uma ação de fechamento do modal.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Por que usar uma promise?** O GridJs pode precisar re‑renderizar a tabela ou sincronizar com um backend. Ao aguardar a promise, garantimos que a UI só será ocultada depois que a grade refletir o novo valor.

---

## Etapa 5: Lidar com Cancelar e Casos Limite

Uma solução robusta sempre oferece ao usuário uma saída. O botão **Cancelar** simplesmente oculta o modal e limpa qualquer endereço armazenado.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### E se Nenhuma Célula Estiver Selecionada?

Se um usuário de alguma forma acionar o botão **Salvar** sem clicar em uma célula primeiro (talvez tenha aberto o modal programaticamente), `lastSelectedCell` será `null`. O retorno antecipado em `updateSelectedCell` impede um erro de tempo de execução e registra um aviso útil.

### Lidando com Grades Grandes

Para grades com paginação, `GridJs.getSelectedCell()` ainda retorna o endereço absoluto (ex., `"B12"`), não apenas a linha visível. Isso significa que a atualização funciona mesmo se a linha editada estiver em outra página. Apenas esteja ciente de que a UI não mudará de página automaticamente após uma atualização — se precisar disso, chame `grid.forceUpdate()` ou navegue manualmente para a página apropriada.

---

## Exemplo Completo em Funcionamento

Abaixo está o código completo que você pode copiar‑colar em um único arquivo HTML. Abra‑o em um navegador, clique em qualquer célula, altere o preço e veja a grade atualizar instantaneamente.



## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Obter Endereço, Contagem de Células e Deslocamento para Toda a Faixa do Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Obter Endereço, Contagem de Células e Deslocamento para Toda a Faixa do Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Obter Endereço, Contagem de Células e Deslocamento para Toda a Faixa do Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}