---
category: general
date: 2026-11-22
description: preencher modelo Excel usando Aspose.Cells para gerar várias planilhas,
  salvar a pasta de trabalho Aspose e criar um relatório mestre‑detalhe em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: pt
lastmod: 2026-11-22
og_description: preencher modelo Excel com Aspose.Cells, gerar várias planilhas, salvar
  a pasta de trabalho Aspose e criar um relatório mestre‑detalhe em um único programa
  C#.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Preencha o modelo Excel e gere várias planilhas com Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Como preencher um modelo Excel e gerar várias planilhas com Aspose.Cells
url: /pt/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como preencher um modelo Excel e gerar várias planilhas com Aspose.Cells

Se você precisa **preencher um modelo Excel** com dados dinâmicos, este guia mostra uma solução completa, pronta‑para‑executar. Usando o mecanismo Smart Marker do Aspose.Cells você pode **gerar várias planilhas**, salvar a **pasta de trabalho Aspose** e produzir um **relatório mestre‑detalhe** completo sem cópias manuais ou macros VBA.

O tutorial percorre cada passo — desde a preparação das coleções mestre‑detalhe até a gravação do arquivo final — para que você possa copiar o código para seu próprio projeto e ver resultados imediatos.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+)
* Aspose.Cells for .NET instalado (`dotnet add package Aspose.Cells`)
* Um ambiente básico de desenvolvimento C# (Visual Studio, VS Code, Rider, etc.)
* Um modelo Excel (`MasterDetailTemplate.xlsx`) que contém tags Smart Marker como `&=Orders.OrderId` e uma tabela de detalhe marcada com `&=OrderLines`.

> **Dica profissional:** Mantenha o modelo na mesma pasta do projeto ou use um caminho absoluto para evitar `FileNotFoundException`.

## Visão geral da solução

1. **Preparar coleções de dados mestre‑detalhe** – os objetos fonte que alimentam o relatório.  
2. **Carregar o modelo Excel** que já contém os marcadores Smart Marker.  
3. **Criar um `SmartMarkerProcessor`** para interpretar os marcadores.  
4. **Aplicar os dados** e deixar o Aspose.Cells **gerar várias planilhas** automaticamente.  
5. **Salvar a pasta de trabalho Aspose** no disco.

Cada passo é explicado abaixo, com código completo e saída esperada.

![exemplo de preenchimento de modelo excel](https://example.com/images/populate-excel-template.png "exemplo de preenchimento de modelo excel")

## Etapa 1: Preparar coleções de dados mestre‑detalhe

Relatórios mestre‑detalhe dependem de duas coleções relacionadas: uma lista de pedidos (mestre) e uma lista de linhas de pedido (detalhe). O motor Smart Marker combina linhas pelo campo `OrderId`.

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**Por que isso importa:**  
O `SmartMarkerProcessor` varre o modelo em busca de marcadores como `&=Orders.OrderId` e `&=OrderLines.Item`. Ao fornecer duas coleções separadas, o Aspose.Cells cria automaticamente uma nova planilha para cada registro mestre e preenche as linhas de detalhe de acordo.

## Etapa 2: Carregar o modelo Excel que contém Smart Markers

O modelo contém o layout, a formatação e as tags de espaço reservado. Mantenha o nome do arquivo e o caminho corretos.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Por que isso importa:**  
Carregar o modelo fornece ao processador um objeto workbook que já sabe onde inserir os dados. Toda a formatação (fontes, bordas, fórmulas) permanece intacta, de modo que o relatório gerado tem aparência profissional sem código extra de estilo.

## Etapa 3: Criar um SmartMarkerProcessor

O processador é o mecanismo que substitui os marcadores pelos valores reais.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Por que isso importa:**  
`SmartMarkerProcessor` isola a lógica de Smart Marker do restante da pasta de trabalho, permitindo reutilizar o mesmo workbook para outras operações (por exemplo, gráficos) após a aplicação dos dados.

## Etapa 4: Aplicar os dados mestre‑detalhe e gerar várias planilhas

Aqui vinculamos as duas coleções ao processador e informamos ao Aspose.Cells como nomear cada planilha gerada.

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**Por que isso importa:**  
O padrão `DetailSheetNewName` cria planilhas nomeadas `Details_1`, `Details_2`, etc., correspondendo a cada pedido na coleção mestre. Essa geração automática de planilhas é o núcleo da **geração de várias planilhas** sem percorrer a pasta de trabalho manualmente.

### Como a pasta de trabalho resultante se parece

| Nome da planilha | Conteúdo |
|------------------|----------|
| **Master** | Linha de cabeçalho com resumo do pedido (OrderId, Customer) |
| **Details_1** | Todas as `OrderLines` onde `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Todas as `OrderLines` onde `OrderId = 2` (Pencil) |

A planilha mestre também pode ser preenchida adicionando uma tabela Smart Marker que itera sobre `Orders`. As planilhas de detalhe são criadas automaticamente pelo processador.

## Etapa 5: Salvar a pasta de trabalho Aspose

Por fim, grave a pasta de trabalho preenchida em um novo arquivo.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Por que isso importa:**  
Chamar `Save` grava a pasta de trabalho em memória em um arquivo físico `.xlsx`, concluindo a etapa **salvar pasta de trabalho Aspose**. O arquivo pode ser aberto no Excel, Google Sheets ou qualquer visualizador que suporte o formato OpenXML.

### Saída esperada

Abra `MasterDetailResult.xlsx` e você verá:

* **Planilha “Master”** – uma tabela listando Order 1 (Alice) e Order 2 (Bob).  
* **Planilha “Details_1”** – duas linhas: Pen (10) e Notebook (5).  
* **Planilha “Details_2”** – uma linha: Pencil (20).

Toda a formatação do modelo original (cores de cabeçalho, larguras de coluna, formatos numéricos) é preservada.

## Tratamento de casos comuns

| Situação | Abordagem recomendada |
|----------|-----------------------|
| **Modelo não encontrado** | Envolva a chamada `new Workbook(...)` em um `try/catch` e registre `FileNotFoundException`. |
| **Conjuntos de dados grandes (10 000+ linhas)** | Aumente `SmartMarkerOptions.MaxRowsPerSheet` se precisar de mais linhas por planilha, ou pagine manualmente. |
| **Nomeação personalizada de planilhas** | Use uma string de formato como `DetailSheetNewName = "Order_{0}_{1}"` onde `{1}` pode ser uma propriedade do registro mestre (ex.: `Customer`). |
| **Formatação condicional por pedido** | Adicione uma regra de formatação condicional ao modelo que referencia um marcador (ex.: `&=Orders.Status`) e deixe o processador avaliá‑la. |

## Programa completo executável

A seguir está o aplicativo console C# completo que reúne todas as peças. Substitua `YOUR_DIRECTORY` por um caminho de pasta real na sua máquina.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

Execute o programa (`dotnet run` ou `Ctrl+F5` no Visual Studio). Quando terminar, abra `MasterDetailResult.xlsx` para verificar se **preencher modelo Excel** produziu o relatório mestre‑detalhe esperado com **várias planilhas**.

## Conclusão

Agora você sabe como **preencher um modelo Excel** com Aspose.Cells, **gerar várias planilhas**, **salvar a pasta de trabalho Aspose** e construir um robusto **relatório mestre‑detalhe** em apenas algumas linhas de C#. O motor Smart Marker elimina a necessidade de loops manuais, mantém sua formatação intacta e escala facilmente para conjuntos de dados maiores.

### Próximos passos

* Explore **SmartMarkerOptions** como `EnableFormulaCalculation` para avaliar fórmulas após a inserção dos dados.  
* Adicione gráficos à planilha mestre e deixe o processador atualizar os intervalos de série automaticamente.  
* Combine esta abordagem com **Aspose.Slides** para exportar os mesmos dados para apresentações PowerPoint.

Sinta‑se à vontade para experimentar diferentes layouts de modelo, padrões de nomeação de planilhas personalizados ou coleções de detalhe adicionais. Boa codificação!


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Create master detail report in C# – Populate Excel template with SmartMarker](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [How to generate Excel from template with C# and Aspose.Cells](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Populate Excel Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}