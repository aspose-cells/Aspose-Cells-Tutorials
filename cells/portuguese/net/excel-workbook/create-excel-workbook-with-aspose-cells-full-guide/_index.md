---
category: general
date: 2026-06-30
description: Criar pasta de trabalho Excel usando Aspose.Cells, aplicar estilo de
  tabela, salvar como xlsx, exportar Excel para PDF e incorporar fontes ao PDF para
  uma saída impecável.
draft: false
keywords:
- create excel workbook
- apply table style
- save as xlsx
- export excel to pdf
- embed fonts pdf
language: pt
og_description: Crie uma pasta de trabalho Excel com Aspose.Cells, aplique estilo
  de tabela, salve como xlsx, exporte o Excel para PDF e incorpore fontes no PDF em
  um tutorial contínuo.
og_title: Criar Pasta de Trabalho do Excel – Aspose.Cells Passo a Passo
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create excel workbook using Aspose.Cells, apply table style, save as
    xlsx, export excel to pdf and embed fonts pdf for flawless output.
  headline: Create Excel Workbook with Aspose.Cells – Full Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PDF export
title: Criar Pasta de Trabalho do Excel com Aspose.Cells – Guia Completo
url: /pt/net/excel-workbook/create-excel-workbook-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar Excel Workbook – Tutorial Completo do Aspose.Cells

Já tentou **create excel workbook** programaticamente e encontrou um obstáculo quando o resultado parecia simples ou o PDF perdeu suas fontes? Você não é o único. Em muitos projetos do mundo real — pense em relatórios mensais de vendas ou painéis financeiros automatizados — você precisa de uma planilha bem elaborada **e** um PDF que respeite a identidade corporativa.  

Neste guia vamos percorrer tudo o que você precisa saber: desde criar uma nova workbook, estilizar os dados como uma tabela adequada, salvar o arquivo como **xlsx**, e finalmente **export excel to pdf** com **embed fonts pdf** para qualidade de arquivamento perfeita. Sem enrolação, apenas uma solução executável que você pode inserir em um aplicativo console .NET hoje.

## Prerequisites

Antes de começarmos, certifique‑se de que você tem:

- .NET 6‑or‑later SDK (o código funciona tanto em .NET Core quanto em .NET Framework)  
- Aspose.Cells for .NET instalado (`dotnet add package Aspose.Cells`)  
- Uma pasta onde você possa gravar (substitua `YOUR_DIRECTORY` no exemplo)  
- Familiaridade básica com C# — nada sofisticado, apenas as declarações `using` habituais

Tem tudo? Ótimo, vamos começar.

## Step 1: Create Excel Workbook and Open the First Worksheet

A primeira coisa a fazer é **create excel workbook**. O Aspose.Cells fornece a classe `Workbook` que inicia a vida com uma única planilha vazia.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateWorkbook()
{
    // Step 1: Instantiate a new workbook (contains one empty worksheet)
    var workbook = new Workbook();

    // Grab the first worksheet so we can start populating it
    var worksheet = workbook.Worksheets[0];
    worksheet.Name = "SalesData";
```

Por que nomeamos a planilha imediatamente? Um nome significativo torna as referências posteriores (como quando você abre o arquivo manualmente) muito mais claras, especialmente se a workbook crescer além de uma planilha.

## Step 2: Fill the Sheet with Sample Data

Em seguida, adicionamos nomes de meses e valores de receita. Isso imita um típico relatório de vendas‑por‑mês.

```csharp
    // Header row
    worksheet.Cells["A1"].PutValue("Month");
    worksheet.Cells["B1"].PutValue("Revenue");

    // Sample data arrays
    string[] months   = { "Jan", "Feb", "Mar", "Apr", "May", "Jun" };
    double[] revenue  = { 12500, 15800, 14200, 16700, 19000, 21000 };

    // Populate rows
    for (int i = 0; i < months.Length; i++)
    {
        worksheet.Cells[i + 1, 0].PutValue(months[i]);   // Column A
        worksheet.Cells[i + 1, 1].PutValue(revenue[i]); // Column B
    }
```

Observe o uso de `PutValue` — ele infere automaticamente o tipo da célula, então números permanecem numéricos e strings permanecem texto. Isso importa mais tarde quando somamos a coluna de receita.

## Step 3: Convert the Range into a Table and **Apply Table Style**

Um intervalo simples parece sem graça. Transformá‑lo em uma tabela do Excel fornece filtragem incorporada, auto‑formatação e uma linha de total com uma única linha de código.

```csharp
    // Determine the used range (including header)
    int totalRows = months.Length + 1; // +1 for header

    // Add a ListObject (Excel table) that covers A1:B{totalRows}
    var tableIndex = worksheet.ListObjects.Add(0, 0, totalRows - 1, 1, true);
    var salesTable = worksheet.ListObjects[tableIndex];

    // Apply a built‑in style – this is where we **apply table style**
    salesTable.TableStyleType = TableStyleType.TableStyleMedium9;
```

`TableStyleMedium9` é um estilo limpo, com listras cinzas, que funciona bem tanto na tela quanto no PDF impresso. Você pode trocá‑lo por qualquer um dos mais de 70 estilos incorporados; basta alterar o valor do enum.

## Step 4: Show a Totals Row That Sums the Revenue Column

Ter uma soma na parte inferior é quase sempre necessário para relatórios financeiros.

```csharp
    // Enable the totals row
    salesTable.ShowTotals = true;

    // Set the second column (Revenue) to calculate a SUM
    salesTable.Columns[1].TotalsCalculation = TotalsCalculationType.Sum;
```

O Aspose.Cells faz o trabalho pesado — não é preciso escrever uma fórmula separada. A linha de totais será atualizada automaticamente se você modificar os dados posteriormente.

## Step 5: **Save as XLSX** – The Native Excel Format

Agora que a planilha está apresentável, persistimos ela como um arquivo Excel adequado.

```csharp
    // Step 5: Save the workbook as an XLSX file
    workbook.Save("YOUR_DIRECTORY/SalesReport.xlsx", SaveFormat.Xlsx);
```

Por que o `SaveFormat.Xlsx` explícito? Ele garante que o arquivo esteja em conformidade com o padrão Office Open XML, essencial se ferramentas posteriores esperarem um `.xlsx` moderno.

## Step 6: **Export Excel to PDF** with **Embed Fonts PDF**

Gerar um PDF é simples, mas garantir que o PDF esteja pronto para arquivamento (PDF/A‑1b) e que todas as fontes estejam incorporadas requer algumas opções.

```csharp
    // Step 6: Export to PDF with PDF/A‑1b compliance and embed Windows fonts
    var pdfOptions = new PdfSaveOptions
    {
        Compliance = PdfCompliance.PdfA1b,          // PDF/A‑1b for long‑term preservation
        EmbedStandardWindowsFonts = true           // This **embed fonts pdf** flag
    };

    workbook.Save("YOUR_DIRECTORY/SalesReport.pdf", pdfOptions);
}
```

A configuração `PdfCompliance.PdfA1b` força a saída a atender à especificação PDF/A‑1b — perfeito para arquivos legais ou regulatórios. Enquanto isso, `EmbedStandardWindowsFonts = true` garante que Calibri, Arial e outras fontes padrão viajem dentro do PDF, de modo que o documento tenha a mesma aparência em qualquer máquina.

### Full Source Code (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateWorkbook()
{
    // Step 1: Create a new workbook (contains one empty worksheet)
    var workbook = new Workbook();

    // Step 2: Get the first worksheet and give it a meaningful name
    var worksheet = workbook.Worksheets[0];
    worksheet.Name = "SalesData";

    // Step 3: Populate the worksheet with sample month and revenue data
    worksheet.Cells["A1"].PutValue("Month");
    worksheet.Cells["B1"].PutValue("Revenue");
    string[] months = { "Jan", "Feb", "Mar", "Apr", "May", "Jun" };
    double[] revenue = { 12500, 15800, 14200, 16700, 19000, 21000 };

    for (int i = 0; i < months.Length; i++)
    {
        worksheet.Cells[i + 1, 0].PutValue(months[i]);   // Column A
        worksheet.Cells[i + 1, 1].PutValue(revenue[i]); // Column B
    }

    // Step 4: Convert the data range into an Excel table and **apply table style**
    int totalRows = months.Length + 1;
    var tableIdx = worksheet.ListObjects.Add(0, 0, totalRows - 1, 1, true);
    var salesTable = worksheet.ListObjects[tableIdx];
    salesTable.TableStyleType = TableStyleType.TableStyleMedium9;

    // Step 5: Show a total row that sums the Revenue column
    salesTable.ShowTotals = true;
    salesTable.Columns[1].TotalsCalculation = TotalsCalculationType.Sum;

    // Step 6: **Save as xlsx** – the native Excel format
    workbook.Save("YOUR_DIRECTORY/SalesReport.xlsx", SaveFormat.Xlsx);

    // Step 7: **Export excel to pdf** with **embed fonts pdf**
    var pdfOptions = new PdfSaveOptions
    {
        Compliance = PdfCompliance.PdfA1b,
        EmbedStandardWindowsFonts = true
    };
    workbook.Save("YOUR_DIRECTORY/SalesReport.pdf", pdfOptions);
}
```

## Expected Output

- **SalesReport.xlsx** – Abra no Excel e você verá uma tabela bem estilizada (listras cinzas, setas de filtro e uma linha de totais mostrando a soma da coluna Revenue).  
- **SalesReport.pdf** – Ao abrir o PDF, o layout da tabela espelha exatamente a visualização do Excel. As fontes estão incorporadas, então mesmo em uma máquina sem Calibri o texto permanece nítido. O PDF está marcado como PDF/A‑1b, o que pode ser verificado no Adobe Acrobat em *File → Properties → Description*.

## Frequently Asked Questions (and Quick Answers)

**What if I need a different table style?**  
Just change `TableStyleMedium9` to any other `TableStyleType` enum value, e.g., `TableStyleLight1` for a cleaner look.

**Can I add more worksheets before saving?**  
Absolutely. Call `workbook.Worksheets.Add("AnotherSheet")` and repeat the data‑population steps.

**Do I have to embed fonts for PDF/A compliance?**  
The PDF/A‑1b spec requires all fonts to be embedded. Setting `EmbedStandardWindowsFonts = true` satisfies that requirement for the default system fonts. For custom fonts, load them into the document’s font collection first.

**Is the code compatible with .NET Framework 4.5?**  
Yes—Aspose.Cells supports .NET Framework 4.0 and newer, so the same snippet runs without changes.

## Conclusion

You now know how to **create excel workbook** with Aspose.Cells, **apply table style**, **save as xlsx**, and **export excel to pdf** while **embed fonts pdf** for reliable, standards‑compliant output. This end‑to‑end flow covers the most

## What Should You Learn Next?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [Criar e Salvar Pasta de Trabalho Excel como PDF em ASP.NET Usando Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/german/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/french/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}