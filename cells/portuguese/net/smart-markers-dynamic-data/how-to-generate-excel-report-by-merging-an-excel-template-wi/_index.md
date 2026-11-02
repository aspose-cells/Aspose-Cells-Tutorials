---
category: general
date: 2026-10-10
description: Gerar relatório em Excel ao mesclar um modelo de Excel usando Smart Markers
  — substituir tags inteligentes e manipular a tag da planilha de detalhes de forma
  eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- generate Excel report
- merge Excel template
- detail sheet tag
- use smart markers
- replace smart tags
language: pt
lastmod: 2026-10-10
og_description: Gere relatório Excel usando Smart Markers. Aprenda como mesclar o
  modelo Excel, substituir tags inteligentes e trabalhar com uma tag de planilha de
  detalhes em um exemplo completo em C#.
og_image_alt: Generated Excel report after merging template with Smart Markers
og_title: Gerar relatório Excel mesclando um modelo Excel com Smart Markers
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  headline: How to generate Excel report by merging an Excel template with Smart Markers
  type: TechArticle
- description: Generate Excel report by merging an Excel template using Smart Markers—replace
    smart tags and handle detail sheet tag efficiently.
  name: How to generate Excel report by merging an Excel template with Smart Markers
  steps:
  - name: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
    text: '**Load the Excel template** – The template holds the layout, formulas,
      and styling. Smart Markers are placeholders like `${MasterSheet:Orders}` that
      the processor will replace.'
  - name: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
    text: '**Prepare the data source** – `SmartMarkerProcessor` works with any enumerable
      collection. Here we use a list of `Order` objects that contain a nested list
      of `OrderDetail` objects, which is exactly what a master‑detail report needs.'
  - name: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
    text: '**Create the processor** – Instantiating `SmartMarkerProcessor` is cheap;
      you can reuse it for multiple worksheets if you need to generate several reports
      in one run.'
  - name: '**Process the worksheet** – This single call does three things:'
    text: '**Process the worksheet** – This single call does three things:'
  - name: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
    text: '**Save the result** – The output file (`GeneratedReport.xlsx`) is a fully‑populated
      Excel report ready for distribution.'
  - name: Creates a new worksheet for every master row.
    text: Creates a new worksheet for every master row.
  - name: Copies the formatting from the template’s detail area.
    text: Copies the formatting from the template’s detail area.
  - name: Inserts each item from the enumerable into consecutive rows.
    text: Inserts each item from the enumerable into consecutive rows.
  - name: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
    text: A **master sheet** named *Sheet1* with two rows—one for each order. Columns
      display Order ID, Customer, Order Date, and Total.
  - name: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
    text: Two **detail sheets** named `OrderDetails_1001` and `OrderDetails_1002`.
      Each sheet lists the products, quantities, and unit prices for the corresponding
      order.
  type: HowTo
tags:
- Excel
- C#
- SmartMarkers
title: Como gerar um relatório Excel mesclando um modelo Excel com Smart Markers
url: /pt/net/smart-markers-dynamic-data/how-to-generate-excel-report-by-merging-an-excel-template-wi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como gerar relatório Excel mesclando um modelo Excel com Smart Markers

Se você precisa **gerar relatório Excel** a partir de uma planilha reutilizável, os Smart Markers permitem mesclar dados de forma rápida e confiável. Ao usar a abordagem de **mesclar modelo Excel**, você mantém o layout separado da lógica de negócios, e o mesmo modelo pode servir a dezenas de relatórios.

Este tutorial mostra como definir uma **tag de planilha de detalhe**, **usar smart markers** para preencher dados mestre‑detalhe e **substituir smart tags** no arquivo final. Você receberá um programa C# completo e executável que produz um relatório Excel com aparência profissional em segundos.

## O que você precisará

- .NET 6.0 ou superior (o código também funciona com .NET Framework 4.7+)
- Visual Studio 2022 ou qualquer IDE C#
- O pacote NuGet `GroupDocs.Viewer` / `Aspose.Cells` (ou qualquer biblioteca que forneça `SmartMarkerProcessor`)
- Um arquivo de modelo Excel (`ReportTemplate.xlsx`) que contém as tags Smart Marker descritas abaixo

> **Dica profissional:** Mantenha o modelo na pasta `Resources` do projeto e defina a propriedade *Copy to Output Directory* como *Copy if newer* para que o código possa localizá‑lo em tempo de execução.

## Gerar relatório Excel: passo a passo com Smart Markers

A seguir está o arquivo fonte completo `Program.cs`. Cada região é explicada nas seções subsequentes.

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.Cells;               // SmartMarkerProcessor lives in this namespace
using Aspose.Cells.Tables;        // For master‑detail handling

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the Excel template that contains Smart Marker tags
            string templatePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "ReportTemplate.xlsx");
            Workbook workbook = new Workbook(templatePath);
            Worksheet ws = workbook.Worksheets[0];   // assume the first sheet is the master sheet

            // 2️⃣ Prepare the data source – a list of orders, each with order lines
            List<Order> ordersData = GetSampleOrders();

            // 3️⃣ Create a SmartMarkerProcessor instance
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 4️⃣ Process the worksheet, merging the template with the data source
            // This replaces all ${...} tags with real values and expands the detail sheet tag.
            processor.Process(ws, ordersData);

            // 5️⃣ Save the merged workbook as the final report
            string outputPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "GeneratedReport.xlsx");
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Report generated successfully: {outputPath}");
        }

        // Sample data generator – in a real project you would pull from a database or service
        private static List<Order> GetSampleOrders()
        {
            return new List<Order>
            {
                new Order
                {
                    OrderId = 1001,
                    Customer = "Acme Corp",
                    OrderDate = new DateTime(2024, 9, 15),
                    Total = 1250.75,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Widget A", Quantity = 10, UnitPrice = 25.00 },
                        new OrderDetail { Product = "Widget B", Quantity = 5,  UnitPrice = 75.00 }
                    }
                },
                new Order
                {
                    OrderId = 1002,
                    Customer = "Beta Ltd.",
                    OrderDate = new DateTime(2024, 9, 16),
                    Total = 980.00,
                    Details = new List<OrderDetail>
                    {
                        new OrderDetail { Product = "Gadget X", Quantity = 8, UnitPrice = 80.00 },
                        new OrderDetail { Product = "Gadget Y", Quantity = 4, UnitPrice = 50.00 }
                    }
                }
            };
        }
    }

    // Simple POCO classes that represent master‑detail data
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime OrderDate { get; set; }
        public double Total { get; set; }
        public List<OrderDetail> Details { get; set; }
    }

    public class OrderDetail
    {
        public string Product { get; set; }
        public int Quantity { get; set; }
        public double UnitPrice { get; set; }
    }
}
```

### Por que cada parte importa

1. **Carregar o modelo Excel** – O modelo contém o layout, fórmulas e estilos. Smart Markers são marcadores como `${MasterSheet:Orders}` que o processador substituirá.

2. **Preparar a fonte de dados** – `SmartMarkerProcessor` funciona com qualquer coleção enumerável. Aqui usamos uma lista de objetos `Order` que contém uma lista aninhada de objetos `OrderDetail`, exatamente o que um relatório mestre‑detalhe necessita.

3. **Criar o processador** – Instanciar `SmartMarkerProcessor` é barato; você pode reutilizá‑lo para várias planilhas se precisar gerar vários relatórios em uma única execução.

4. **Processar a planilha** – Esta chamada única faz três coisas:
   - **Substituir smart tags** como `${MasterSheet:Orders}` pelos valores reais dos campos.
   - **Expandir a tag de planilha de detalhe** (`${DetailSheetNewName:OrderDetails}`) em uma nova planilha para cada linha mestre.
   - **Copiar formatação** do modelo para as linhas geradas, preservando seu design.

5. **Salvar o resultado** – O arquivo de saída (`GeneratedReport.xlsx`) é um relatório Excel totalmente preenchido, pronto para distribuição.

## Mesclar modelo Excel com a fonte de dados

O núcleo da técnica de **mesclar modelo Excel** é a sintaxe do Smart Marker. No `ReportTemplate.xlsx` você colocaria tags como:

| Célula | Valor |
|--------|-------|
| A1     | `${MasterSheet:Orders.OrderId}` |
| B1     | `${MasterSheet:Orders.Customer}` |
| C1     | `${MasterSheet:Orders.OrderDate:MM/dd/yyyy}` |
| D1     | `${MasterSheet:Orders.Total}` |
| A5     | `${DetailSheetNewName:OrderDetails}` |
| A6     | `${DetailSheet:OrderDetails.Product}` |
| B6     | `${DetailSheet:OrderDetails.Quantity}` |
| C6     | `${DetailSheet:OrderDetails.UnitPrice}` |

- `${MasterSheet:Orders}` indica ao processador que ele deve ler a coleção `Orders` da fonte de dados.
- `${DetailSheetNewName:OrderDetails}` cria uma **tag de planilha de detalhe** que gera uma nova planilha nomeada a partir da linha mestre (ex.: `OrderDetails_1001`).
- `${DetailSheet:OrderDetails.*}` preenche cada linha de detalhe.

Quando `processor.Process(ws, ordersData)` é executado, a biblioteca substitui automaticamente **smart tags** pelos valores de `ordersData` e duplica a planilha de detalhe para cada pedido.

## Sintaxe da tag de planilha de detalhe

Uma **tag de planilha de detalhe** segue o padrão `${DetailSheetNewName:TagName}`. O `TagName` deve corresponder a uma propriedade que retorne um `IEnumerable` (no nosso caso `Order.Details`). O processador:

1. Cria uma nova planilha para cada linha mestre.
2. Copia a formatação da área de detalhe do modelo.
3. Insere cada item da coleção em linhas consecutivas.

Se precisar que a planilha de detalhe mantenha o mesmo nome para todas as linhas mestre (ex.: uma única planilha com todos os detalhes), substitua `${DetailSheetNewName:OrderDetails}` por `${DetailSheet:OrderDetails}`. O primeiro é útil em cenários de **gerar relatório Excel** onde cada pedido recebe sua própria aba.

## Usar smart markers para substituir smart tags

Smart Markers são mais que simples marcadores. Eles suportam:

- **Strings de formatação** (`:MM/dd/yyyy` no exemplo) para controlar a exibição de datas ou números.
- **Seções condicionais** (`${if:Orders.Total > 1000}`) para ocultar linhas com base nos dados.
- **Looping** sobre coleções sem escrever código além da tag.

Como o processador lida com esses recursos internamente, você **substitui smart tags** no modelo sem escrever loops personalizados ou atribuições célula a célula. Isso reduz bugs e mantém o modelo fácil de manter.

## Saída esperada

Após executar o programa, abra `GeneratedReport.xlsx`. Você deverá ver:

1. Uma **planilha mestre** chamada *Sheet1* com duas linhas — uma para cada pedido. As colunas exibem Order ID, Customer, Order Date e Total.
2. Duas **planilhas de detalhe** chamadas `OrderDetails_1001` e `OrderDetails_1002`. Cada planilha lista os produtos, quantidades e preços unitários do pedido correspondente.
3. Toda a formatação original (fontes, cores, bordas) preservada a partir de `ReportTemplate.xlsx`.

![Generated Excel report after merging template with Smart Markers](generated-report.png "Generated Excel report after merging template


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Aspose Cells Smart Markers: Load Excel Template & Generate Excel from Template](/cells/english/java/templates-reporting/aspose-cells-smart-markers-load-excel-template-generate-exce/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose Cells Smart Markers: Generate Excel from Model in C#](/cells/english/net/smart-markers-dynamic-data/aspose-cells-smart-markers-generate-excel-from-model-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}