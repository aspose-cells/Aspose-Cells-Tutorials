---
category: general
date: 2026-05-30
description: Aprenda como criar uma instância de GridJsOptions e configurar as opções
  de grade em JavaScript para tabelas dinâmicas. Guia passo a passo com código completo.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: pt
og_description: Crie uma instância de GridJsOptions e configure as opções de grade
  JavaScript em minutos. Exemplo completo, explicações e dicas de boas práticas.
og_title: Criar Instância GridJsOptions – Configurar Opções da Grade JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Criar Instância GridJsOptions – Configurar Opções da Grade em JavaScript
url: /pt/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Instância GridJsOptions – Configurar Grid Options JavaScript

Já se perguntou como **create GridJsOptions instance** sem vasculhar documentos espalhados? Você não é o único. Quando você precisa de uma tabela elegante e ordenável em uma página web, dominar como **configure grid options JavaScript** é o primeiro passo para uma UI polida.

Neste tutorial, vamos percorrer o código exato que você precisa, explicar por que cada configuração importa e mostrar um exemplo completo e executável. Ao final, você estará confortável em create GridJsOptions instance, ajustando alinhamento, paginação e até renderizadores de célula personalizados — tudo com JavaScript puro.

## O que você aprenderá

- Como **create GridJsOptions instance** do zero.
- As propriedades principais que permitem **configure grid options JavaScript** (ordenamento, paginação, formatação de números, etc.).
- Armadilhas comuns (por exemplo, misturar tipos string e numéricos) e como evitá‑las.
- Uma página HTML completa que você pode copiar‑colar em qualquer projeto e ver os resultados instantaneamente.

### Pré-requisitos

- Um navegador moderno (Chrome, Edge, Firefox) – sem necessidade de ferramentas de build.
- Familiaridade básica com JavaScript (variáveis, objetos, DOM).
- A biblioteca Grid.js (iremos obtê‑la de um CDN).

Se algum desses parecer desconhecido, não entre em pânico — cada passo inclui um rápido reforço.

---

## Etapa 1: Carregar Grid.js e Preparar o Esqueleto HTML

Antes de podermos **create GridJsOptions instance**, precisamos da própria biblioteca. A maneira mais fácil é usar o CDN oficial. Abaixo está um esqueleto HTML mínimo que também reserva um `<div>` onde a grade será renderizada.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Pro tip:** Mantenha o link CSS antes dos seus próprios estilos para que o tema padrão da grade seja carregado corretamente.

### Por que isso importa

Carregar a biblioteca de um CDN garante que você sempre obtenha a versão estável mais recente sem uma instalação local. O `<div id="grid-wrapper">` é o espaço reservado que o construtor Grid.js irá direcionar assim que **configure grid options JavaScript**.

## Etapa 2: Criar uma Nova Instância GridJsOptions

Agora vem o coração do tutorial: a linha que realmente **creates GridJsOptions instance**. Em um arquivo separado chamado `grid-config.js` (referenciado no HTML acima) escreveremos:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Essa única linha fornece um objeto limpo que você pode começar a preencher com configurações. Pense em `gridOptions` como o painel de controle para cada recurso que você habilitará posteriormente.

### O que você está configurando

- **NumberFormatAlignment** – alinha strings numéricas automaticamente.
- **Pagination** – controla o tamanho da página e a navegação.
- **Sorting** – alterna a ordenação das colunas.
- **Columns** – define cabeçalhos, tipos de dados e renderizadores personalizados.

Você pode adicionar qualquer uma dessas propriedades antes de finalmente instanciar a Grid.

## Etapa 3: Habilitar Alinhamento Numérico (Um Requisito Comum)

A maioria das tabelas contém uma mistura de texto e números. Por padrão, o Grid.js alinha tudo à esquerda, o que parece estranho para valores monetários. Para **configure grid options JavaScript** com alinhamento adequado, defina a flag `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Por que habilitar isso? Quando a flag está verdadeira, o Grid.js inspeciona cada célula; se ela parecer um número (ex.: “1234”, “12.34%”), ele alinha à direita automaticamente. Esse pequeno ajuste torna os relatórios muito mais legíveis.

## Etapa 4: Adicionar Paginação e Ordenação

Uma grade do mundo real raramente cabe em uma única tela. Vamos ativar a paginação (10 linhas por página) e permitir que os usuários ordenem qualquer coluna.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Observação de caso extremo

Se mais tarde você fornecer uma fonte de dados personalizada que já retorna resultados paginados, você desejará desativar a paginação interna do Grid.js para evitar paginação dupla. Basta definir `gridOptions.Pagination.enabled = false;`.

## Etapa 5: Definir Colunas e Dados de Exemplo

Agora vamos alimentar a grade com alguns dados simulados e dizer a ela o que cada coluna representa. É aqui que o padrão **create gridjsoptions instance** realmente brilha — tudo vive em um único objeto organizado.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Observe que mantemos os valores `id` das colunas idênticos às chaves em cada objeto de dados. Essa convenção permite que o Grid.js mapeie os valores automaticamente, economizando a necessidade de escrever um formatador personalizado para cada coluna.

## Etapa 6: Instanciar a Grid com Nossas Opções

Finalmente **configure grid options javascript** passando o objeto `gridOptions` para o construtor Grid. A grade será renderizada dentro do `<div id="grid-wrapper">` que preparamos anteriormente.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

É isso. Todo o processo — de **create gridjsoptions instance** à renderização — leva menos de um minuto de codificação.

### Saída Esperada

Quando você abrir o arquivo HTML em um navegador você deve ver:

- Uma linha de cabeçalho com “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Números de salário alinhados à direita (graças ao `NumberFormatAlignment`).
- Controles de paginação na parte inferior (se você adicionou mais de dez linhas).
- Cabeçalhos de coluna clicáveis que ordenam ascendente/descendente.

Se algo parecer errado, abra o console do navegador (F12) e procure mensagens de erro — a maioria dos bugs provém de IDs de coluna incompatíveis ou scripts de biblioteca ausentes.

## Etapa 7: Ajustes Avançados (Opcional)

Abaixo estão algumas ideias rápidas que você pode experimentar assim que a grade básica funcionar.

| Recurso | Como habilitar | Por que ajuda |
|---------|----------------|---------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Realça os salários em negrito. |
| **Search bar** | `gridOptions.Search = true;` | Permite que os usuários filtrem linhas instantaneamente. |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Escala para milhares de linhas. |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Combina com designs em modo escuro. |

Sinta-se à vontade para combinar — o Grid.js é deliberadamente flexível. Apenas lembre‑se de manter a linha original **create gridjsoptions instance** no topo; todos os ajustes posteriores dependem desse único objeto.

## Conclusão

Acabamos de percorrer um fluxo de trabalho completo para **create GridJsOptions instance** e **configure grid options JavaScript** para uma tabela de dados funcional, ordenável e paginada. Começando com uma página HTML simples, carregamos a biblioteca, construímos um objeto de opções, habilitamos o alinhamento numérico, adicionamos paginação, definimos colunas e, finalmente, renderizamos a grade.

A partir daqui você pode:

- Substituir o `sampleData` estático por uma chamada AJAX.
- Adicionar formatadores personalizados para datas, moedas ou ícones.
- Integrar a grade a um framework como React ou Vue (o mesmo objeto `gridOptions` funciona lá também).

As possibilidades são praticamente infinitas, e o padrão que usamos — centralizar todas as configurações em uma única instância `GridJsOptions` — mantém seu código limpo e sustentável.

Tem um caso de uso sobre o qual você tem dúvidas? Deixe um comentário, e exploraremos juntos. Boa codificação e aproveite a criação de tabelas dinâmicas com o Grid.js!

## O que Você Deve Aprender a Seguir?

- [Como Criar e Configurar Pastas de Trabalho Excel com Aspose.Cells .NET: Um Guia Passo a Passo](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Como Criar e Estilizar Tabelas Excel Usando Aspose.Cells para .NET | Guia Passo a Passo](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Como Criar e FormatAR Células Excel Usando Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}