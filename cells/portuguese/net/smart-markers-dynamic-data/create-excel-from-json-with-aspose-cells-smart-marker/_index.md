---
category: general
date: 2026-08-07
description: Crie Excel a partir de JSON usando Aspose.Cells Smart Marker – aprenda
  como preencher um modelo Excel, aplicar nomes de planilhas dinâmicos e gerar várias
  planilhas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: pt
lastmod: 2026-08-07
og_description: Crie Excel a partir de JSON com o Smart Marker do Aspose.Cells para
  preencher rapidamente modelos, usar nomes de planilhas dinâmicos e gerar várias
  planilhas.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Criar Excel a partir de JSON – Guia do Marcador Inteligente do Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Criar Excel a partir de JSON com Aspose.Cells Smart Marker
url: /pt/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Excel a partir de JSON com Aspose.Cells Smart Marker

Se você precisa **criar Excel a partir de JSON**, este tutorial mostra uma solução completa e pronta para produção. Você verá como **preencher um modelo Excel**, configurar **nomeação dinâmica de planilhas** e **gerar várias planilhas** automaticamente com o motor **Aspose.Cells Smart Marker**.

O guia conduz você por cada passo necessário, desde a definição do objeto fonte semelhante a JSON até a gravação da pasta de trabalho final. Nenhum script externo é necessário, e o código roda em .NET 6 ou superior.

## O que você vai alcançar

* Carregar um objeto de dados no estilo JSON na memória.  
* Inserir um placeholder Smart Marker em um modelo de pasta de trabalho.  
* Aplicar um padrão de nomeação para que cada planilha de detalhe duplicada receba um nome exclusivo.  
* Processar o modelo para criar uma planilha separada para cada pedido na coleção.  
* Salvar o resultado como um arquivo `.xlsx` pronto para consumo posterior.

Pré-requisitos: Visual Studio 2022 (ou qualquer IDE C#), .NET 6+ e o pacote NuGet **Aspose.Cells**. O exemplo usa C#; os mesmos conceitos se aplicam a VB.NET ou outras linguagens .NET.

## Criar Excel a partir de JSON – fluxo de trabalho geral

As seções a seguir dividem o fluxo de trabalho em cinco etapas lógicas. Cada etapa inclui o código exato que você precisa, uma explicação do porquê é importante e dicas para escalar a solução.

### Etapa 1: Definir os dados de origem compatíveis com JSON

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Por que isso importa** – O objeto `ordersData` reflete a estrutura que você receberia de uma API JSON real. Aspose.Cells Smart Marker lê propriedades públicas, portanto um tipo anônimo funciona enquanto os nomes das propriedades coincidirem com as tags do marcador (`{{Orders}}`). Quando você substituir posteriormente o tipo anônimo por um objeto JSON desserializado, nenhuma alteração de código será necessária.

### Etapa 2: Preparar o modelo de pasta de trabalho e inserir um Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Por que isso importa** – O marcador `{{Orders}}` indica ao processador que ele deve iterar sobre a coleção `Orders`. Colocar o marcador na célula `A1` da primeira planilha torna essa planilha a planilha *mestre*. O processador clonará essa planilha para cada pedido, preservando qualquer formatação que você adicionar posteriormente.

> **Dica:** Se você tem um modelo pré‑designado (por exemplo, com cabeçalhos, fórmulas ou estilos), carregue‑o com `new Workbook("Template.xlsx")` em vez de criar uma pasta de trabalho em branco.

### Etapa 3: Configurar nomeação dinâmica de planilhas

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Por que isso importa** – Por padrão, o Aspose.Cells nomeia planilhas duplicadas como `Sheet1`, `Sheet2`, etc. O padrão `DetailSheetNewName` insere um índice incremental (`{0}`) para que cada planilha receba um nome significativo. Você pode incorporar placeholders adicionais (por exemplo, `{Id}`) para incluir dados do registro atual.

> **Pro dica:** Use `DetailSheetNewName = "Order_{Id}"` para nomear as planilhas com base no identificador do pedido, o que facilita a navegação em pastas de trabalho grandes.

### Etapa 4: Processar o modelo com os dados e opções de nomeação

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Por que isso importa** – O `SmartMarkerProcessor` mescla o `ordersData` na pasta de trabalho, cria uma nova planilha para cada elemento em `Orders` e aplica o padrão de nomeação definido anteriormente. O processador também expande quaisquer coleções aninhadas (por exemplo, `Items`) se você adicionar marcadores adicionais dentro da planilha de detalhe.

### Etapa 5: Salvar a pasta de trabalho resultante

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Por que isso importa** – O método `Save` grava a pasta de trabalho totalmente preenchida no disco. O arquivo agora contém uma planilha mestre (que pode ser ocultada ou excluída) e uma série de planilhas de detalhe nomeadas `DetailSheet_1`, `DetailSheet_2`, …, cada uma contendo os dados de um único pedido.

#### Saída esperada

| Nome da planilha  | Conteúdo (simplificado)                 |
|-------------------|------------------------------------------|
| DetailSheet_1     | Pedido Id = 1, Itens: Apple, Banana       |
| DetailSheet_2     | Pedido Id = 2, Itens: Orange              |

Todas as planilhas mantêm qualquer formatação que você aplicou à planilha mestre antes do processamento.

## Variações avançadas

### Preencher o modelo Excel com campos adicionais

Se o seu JSON inclui mais propriedades (por exemplo, `CustomerName`, `TotalAmount`), adicione marcadores correspondentes ao modelo:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

O processador substituirá cada marcador pelo valor da propriedade correspondente.

### Gerar várias planilhas a partir de coleções aninhadas

Você pode criar um segundo nível de duplicação colocando um marcador dentro da planilha de detalhe que referencia uma coleção aninhada, como `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Durante o processamento, o Aspose.Cells cria uma linha para cada item no array `Items`, permitindo gerar listas detalhadas por pedido.

### Nomeação personalizada com dados do registro

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Agora as planilhas são nomeadas `Order_1`, `Order_2`, o que alinha o nome da planilha com o identificador de negócio.

## Armadilhas comuns e como evitá‑las

| Armadilha                                                          | Solução                                                                                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| O texto do marcador não corresponde ao nome da propriedade (sensível a maiúsculas/minúsculas) | Certifique‑se de que o marcador (`{{Orders}}`) corresponde exatamente à propriedade, incluindo maiúsculas/minúsculas.               |
| O modelo contém células mescladas que abrangem a região do marcador | Desmescle as células ou coloque o marcador em uma única célula não mesclada para evitar alterações inesperadas no layout.        |
| Coleções JSON grandes causam pressão de memória                    | Processar os dados em lotes ou transmitir o JSON para um `DataTable` e usar `SmartMarkerProcessor` com `DataSource`.                |
| O caminho do arquivo salvo é inválido                               | Use `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` ou verifique as permissões de gravação.                           |

## Exemplo completo em funcionamento

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

Executar o programa gera um arquivo Excel na área de trabalho contendo duas planilhas de detalhe (`DetailSheet_1` e `DetailSheet_2`). Cada planilha reflete o registro de pedido correspondente.

## Conclusão

Agora você sabe como **criar Excel a partir de JSON** usando **Aspose.Cells Smart Marker**, como **preencher um modelo Excel**, aplicar **nomeação dinâmica de planilhas** e **gerar várias planilhas** automaticamente. O mesmo padrão escala para dezenas ou milhares de registros, suporta coleções aninhadas e integra‑se perfeitamente com qualquer biblioteca de desserialização JSON .NET.

### Próximos passos

* Explore **formatação condicional** dentro da planilha de detalhe para destacar pedidos de alto valor.  
* Substitua o objeto anônimo por um modelo fortemente tipado desserializado via `System.Text.Json`.  
* Combine Smart Markers com a geração de **PivotTable** para relatórios avançados.  

Experimente o padrão de nomeação, adicione mais marcadores e integre este fluxo de trabalho aos seus pipelines de exportação de dados existentes. Boa codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Gerar Relatórios Excel Dinâmicos Usando Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Preencher Excel com Dados Usando Aspose.Cells e Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Como Criar e Mesclar Pastas de Trabalho Excel Usando Aspose.Cells para Java | Guia Completo](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}