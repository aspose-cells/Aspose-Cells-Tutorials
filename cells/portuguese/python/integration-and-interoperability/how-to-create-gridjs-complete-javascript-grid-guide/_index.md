---
category: general
date: 2026-06-30
description: Como criar gridjs facilmente com um exemplo completo em JavaScript, abordando
  a configuração do gridjs, a configuração do contêiner e o processo de renderização.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: pt
og_description: Como criar gridjs facilmente com um exemplo completo em JavaScript,
  abordando a configuração do gridjs, a configuração do contêiner e o processo de
  renderização.
og_title: Como criar Gridjs – Guia completo de grade JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Como criar Gridjs – Guia completo de grid JavaScript
url: /pt/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Criar Gridjs – Guia Completo de Grid em JavaScript

Já se perguntou **como criar gridjs** e ver instantaneamente uma tabela de dados elegante na sua página? Você não está sozinho. Muitos desenvolvedores encontram dificuldades na primeira vez que tentam configurar o Gridjs, especialmente em relação ao objeto de configuração e à chamada de renderização. A boa notícia? É realmente muito fácil uma vez que você conhece os passos corretos.

Neste tutorial vamos percorrer um exemplo do mundo real que mostra **como criar gridjs** do zero, como criar uma **gridjs configuration** adequada, como vincular a grade a um **gridjs container**, e finalmente como acionar o **gridjs render**. Ao final você terá uma grade totalmente funcional que pode ser inserida em qualquer projeto—sem mistério, apenas código claro.

## O que Você Vai Aprender

- Configurar uma página HTML mínima pronta para o Gridjs.  
- Escrever um objeto de **gridjs configuration** que define colunas, dados e opções.  
- Anexar a instância do Gridjs a um elemento **gridjs container**.  
- Chamar **gridjs render** para exibir a tabela.  
- Ajustar configurações comuns (paginação, ordenação, estilo) e evitar armadilhas típicas.  

Nenhuma ferramenta de build externa é necessária; tudo roda no navegador com uma única tag de script. Vamos começar.

## Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

1. Um navegador moderno (Chrome, Edge, Firefox, Safari) – qualquer que suporte ES6.  
2. Conhecimento básico de HTML e JavaScript – você não precisa de um framework.  
3. Acesso à biblioteca Gridjs – vamos carregá‑la de um CDN, portanto não é necessário instalar via npm.  

É isso. Se você já tem uma página que deseja melhorar, pode colar os trechos de código diretamente.

## Etapa 1: Adicionar os Assets do Gridjs à Sua Página

Primeiro, precisamos carregar os arquivos CSS e JavaScript do Gridjs. A versão CDN é leve e perfeita para demonstrações rápidas.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Dica profissional:** O tema Mermaid dá à tabela um visual limpo e moderno sem CSS adicional. Sinta‑se à vontade para trocá‑lo por `classic.min.css` se preferir um estilo diferente.

## Etapa 2: Definir o **gridjs container**

O **gridjs container** é apenas um `<div>` normal que hospedará a tabela renderizada. No markup acima já criamos `<div id="grid"></div>`. O atributo `id` é crucial porque o usaremos para vincular a instância do Gridjs mais tarde.

Se precisar de múltiplas grades na mesma página, dê a cada container um ID único (`grid1`, `grid2`, …) e repita a lógica de vinculação para cada um.

## Etapa 3: Criar um Objeto de **gridjs configuration**  

Agora vem o coração de **como criar gridjs** – a configuração. Esse objeto JavaScript simples informa ao Gridjs quais colunas mostrar, quais dados preencher e quais recursos habilitar.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Por que esta configuração importa

- **Columns** – define o texto do cabeçalho e a largura opcional. Sem isso, o Gridjs inferiria os nomes das colunas a partir da primeira linha de dados, o que costuma ser menos legível.  
- **Data** – um array de linhas, cada linha sendo um array de valores de célula. Você também pode fornecer uma função assíncrona que busca dados de uma API; a biblioteca lidará com promessas automaticamente.  
- **Pagination** – limita o número de linhas por página, evitando que tabelas enormes sobrecarreguem a interface.  
- **Search & Sort** – habilita recursos interativos com um único booleano, poupando a necessidade de escrever manipuladores personalizados.  
- **Language** – personaliza as strings da UI, perfeito para localização ou branding.  

Sinta‑se à vontade para trocar o array de dados estático por uma chamada `fetch` mais tarde; o restante dos passos permanece exatamente o mesmo.

## Etapa 4: Instanciar o Gridjs e Vincular ao **gridjs container**

Com a configuração pronta, criamos um novo `GridJs.Grid` (o nome da classe é `gridjs.Grid` na build UMD) e apontamos para o nosso elemento container.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Observe que usamos `document.getElementById('grid')`—esse é o **gridjs container** que definimos anteriormente. Se você tem múltiplos containers, basta repetir esta linha com o ID apropriado.

## Etapa 5: Acionar a Chamada **gridjs render**

A peça final do quebra‑cabeça é o método **gridjs render**. Ele recebe a configuração que passamos anteriormente e injeta um `<table>` totalmente estilizado no container.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

É isso! Quando você abrir a página em um navegador, verá uma tabela pesquisável e paginada com as quatro linhas que definimos. A caixa de busca aparece automaticamente no topo, e os controles de paginação ficam na parte inferior.

### Saída Esperada

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

A UI se adaptará quando você digitar na caixa de busca ou clicar nos cabeçalhos das colunas para ordenar.

## Variações Comuns & Casos de Borda

### Carregando Dados Assincronamente

Se seus dados estão em um servidor, substitua o array estático `data` por uma função que retorna uma Promise:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

O Gridjs exibirá um spinner de carregamento até que a promessa seja resolvida, então renderizará a tabela automaticamente.

### Renderização Personalizada de Células

Às vezes você precisa de ícones, botões ou datas formatadas dentro das células. Use a propriedade `formatter` em uma coluna:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

O helper `gridjs.h` cria elementos de DOM virtual sem precisar incluir React.

### Múltiplas Grades em Uma Página

Basta repetir as etapas 2‑5 com IDs de container diferentes:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Cada grade opera independentemente, permitindo combinar limites de paginação, conjuntos de colunas e até temas diferentes.

## Dicas Profissionais & Armadilhas a Evitar

- **Don’t forget the CSS** – sem a folha de estilos a tabela aparecerá como uma simples tabela HTML, perdendo toda a estilização agradável e os controles de paginação.  
- **Avoid duplicate IDs** – cada **gridjs container** deve ter um ID único; caso contrário o Gridjs sobrescreverá a primeira instância.  
- **Watch the data shape** – o número de colunas deve corresponder ao número de células em cada linha; arrays incompatíveis causam falhas silenciosas de layout.  
- **Use `gridjs.h` for complex cells** – tentar injetar strings HTML brutas pode quebrar o algoritmo de diff do virtual DOM.  
- **Mind the version** – o link CDN acima aponta para a última versão 5.x (a partir de junho 2026). Se você travar em uma versão mais antiga, algumas opções (como `language`) podem estar ausentes.  

## Exemplo Completo Funcional (Copiar‑Colar)

Abaixo está o arquivo HTML completo que você pode salvar como `gridjs-demo.html` e abrir diretamente no navegador.



## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que expandem as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Aspose.Cells for Java: Como Criar e FormatAR Pastas de Trabalho Excel de Forma Eficiente](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Como Criar e Exportar Excel para HTML Usando Aspose.Cells Java | Guia de Operações de Pastas de Trabalho](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Como Criar e Mesclar Pastas de Trabalho Excel Usando Aspose.Cells for Java | Guia Completo](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}