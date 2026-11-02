---
category: general
date: 2026-06-21
description: Crie uma grade de dados interativa usando o Grid.js e aprenda a exibir
  uma tabela de dados JSON com ordenação, paginação e pesquisa. Perfeito para painéis
  da web.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: pt
og_description: Crie uma grade de dados interativa em minutos. Aprenda a usar o Grid.js
  para exibir uma tabela de dados JSON com paginação, ordenação e pesquisa.
og_title: Crie uma Grade de Dados Interativa com Grid.js – Tutorial Completo
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Crie uma Grade de Dados Interativa com Grid.js – Guia Completo Passo a Passo
url: /pt/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Grade de Dados Interativa com Grid.js – Guia Completo Passo a Passo

Já se perguntou como **criar uma grade de dados interativa** que permite aos usuários ordenar, buscar e paginar linhas sem escrever um backend? Você não está sozinho. Em muitos painéis, o maior ponto doloroso é transformar um dump JSON estático em uma tabela elegante e pesquisável — algo que parece tão suave quanto uma planilha, mas que roda inteiramente no navegador.

Neste tutorial vamos percorrer **como usar o Grid.js** para **exibir uma tabela de dados JSON** em uma página HTML simples. Ao final, você terá um exemplo funcional que pode inserir em qualquer projeto, além de dicas para personalizar a barra de ferramentas, lidar com grandes conjuntos de dados e evitar armadilhas comuns.

## O que você aprenderá

- Como buscar um arquivo JSON que define colunas e linhas.
- Como inicializar o **Grid.js** com paginação, ordenação, busca e uma barra de ferramentas personalizada.
- Como renderizar a grade em um contêiner alvo.
- Ajustes opcionais: formatação personalizada de células, troca de tema e tratamento de erros.
- Um exemplo de código completo, pronto para copiar e colar.

### Pré-requisitos

Antes de mergulharmos, certifique‑se de que você tem:

1. Um navegador moderno (Chrome, Edge ou Firefox) – o Grid.js depende de recursos ES6.  
2. Uma pasta local ou remota contendo um arquivo `grid_data.json` (mostraremos o formato).  
3. Familiaridade básica com HTML e JavaScript – nada sofisticado, apenas a capacidade de abrir um arquivo `.html` em um navegador.

Sem ferramentas de build, sem npm install, sem código server‑side. Essa é a beleza de **criar grade de dados interativa** com Grid.js: funciona direto de um CDN.

---

## Etapa 1: Prepare o JSON que Define sua Tabela

A primeira coisa que você precisa é um payload JSON que informa ao Grid.js quais colunas existem e quais linhas mostrar. Pense nisso como o plano para sua **exibir tabela de dados JSON**. Aqui está um exemplo mínimo que você pode salvar como `grid_data.json` no mesmo diretório do seu arquivo HTML:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Por que esse formato?* O Grid.js espera que `columns` seja um array de strings (ou objetos para configuração avançada) e que `rows` seja um array de arrays onde cada array interno corresponde à ordem das colunas. Você pode, claro, adicionar mais colunas ou objetos aninhados – o Grid.js os renderizará contanto que as estruturas coincidam.

> **Dica de especialista:** Se você estiver obtendo dados de uma API, basta substituir o `fetch('grid_data.json')` estático pela URL do seu endpoint. O resto do código permanece o mesmo.

---

## Etapa 2: Inicializar o Grid.js – O Coração de **how to use gridjs**

Agora que a fonte de dados está pronta, precisamos trazer o Grid.js para a página e dizer a ele como se comportar. É aqui que realmente **criamos grade de dados interativa** com funcionalidades como paginação, ordenação e um prático botão na barra de ferramentas.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

O CDN fornece a versão estável mais recente, e o tema Meri­maid adiciona um visual limpo e moderno pronto para uso. Você pode trocá‑lo por `gridjs.min.css` se preferir o estilo padrão.

Em seguida, dentro de uma tag `<script>`, busque o JSON e inicialize a grade:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Detalhando as Opções

| Opção | O que faz | Por que importa |
|-------|-----------|-----------------|
| `pagination` | Divide as linhas em páginas (padrão 10 por página) | Mantém tabelas grandes utilizáveis sem sobrecarregar a interface. |
| `sort` | Cabeçalhos de coluna clicáveis alternam entre ordem ascendente/descendente | Os usuários podem encontrar rapidamente as linhas com os maiores valores. |
| `search` | Adiciona um campo de texto que filtra as linhas em tempo real | Ótimo para buscas ad‑hoc sem recarregar os dados. |
| `toolbar` | Adiciona botões ou menus suspensos personalizados acima da grade | Perfeito para ações de “Ajuda”, “Exportar” ou “Atualizar”. |
| `formatter` | Permite retornar HTML bruto para uma célula | Aqui transformamos strings de e‑mail em links mailto clicáveis. |

> **Por que essa abordagem?** Ao manter a configuração da grade declarativa, você pode ajustar o comportamento facilmente sem tocar na lógica central de renderização. Essa é a forma recomendada de **how to use Grid.js** para a maioria dos projetos.

---

## Etapa 3: Renderizar a Grade na sua Página

A última linha do script — `grid.render(document.getElementById('grid-container'))` — injeta a tabela totalmente funcional em um `<div>` que você colocou em algum lugar do corpo do HTML:

```html
<div id="grid-container"></div>
```

É isso. Quando a página carrega, o navegador busca o JSON, cria a instância do Grid.js e desenha a tabela interativa na tela. Sem recarregamentos, sem chamadas ao servidor após o carregamento inicial.

---

## Opcional: Ajustes de Estilo e Tema

Se o tema Meri­maid padrão não for do seu agrado, você pode trocá‑lo por qualquer um dos temas embutidos (`gridjs.min.css`) ou escrever seu próprio CSS. Por exemplo, para deixar o fundo do cabeçalho em um cinza suave:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Adicione o trecho dentro de uma tag `<style>` ou em uma folha de estilos externa. O Grid.js respeita seletores CSS padrão, então você tem controle total sobre fontes, cores e espaçamentos.

---

## Armadilhas Comuns & Como Evitá‑las

| Armadilha | Sintoma | Correção |
|-----------|---------|----------|
| **Erros de CORS** ao buscar JSON de outro domínio | O console do navegador mostra “Blocked by CORS policy” | Hospede o JSON na mesma origem ou habilite CORS no servidor. |
| **Conjuntos de dados grandes causam lentidão** | A rolagem fica irregular, a paginação lenta | Use paginação `server` (`pagination: { server: { url: (prev, page, limit) => … } }`) ou carregamento preguiçoso das linhas. |
| **Botão da barra de ferramentas não aparece** | Nenhum botão visível apesar de `toolbar.enabled: true` | Certifique‑se de que está usando o Grid.js versão 2.0+; versões mais antigas tinham uma API de barra de ferramentas diferente. |
| **Links de e‑mail não são clicáveis** | O formatador retorna texto simples | Retorne `gridjs.html(...)` em vez de uma string simples, como mostrado no exemplo. |

Abordar essas questões cedo economiza horas de depuração depois.

---

## Exemplo Completo Funcional (Pronto para Copiar e Colar)

A seguir está o arquivo HTML completo que você pode salvar como `index.html`. Abra-o em um navegador e verá uma demonstração totalmente funcional de **criar grade de dados interativa** que **exibe tabela de dados JSON** com ordenação, busca e um botão de ajuda.



## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Como Criar uma Lista de Validação de Dados no Excel com Aspose.Cells para Java: Um Guia Passo a Passo](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Como Criar Caixas de Seleção no Excel usando Aspose.Cells para .NET | Tutorial de Validação de Dados](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Criar e Importar Dados XML no Excel Usando Aspose.Cells para Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}