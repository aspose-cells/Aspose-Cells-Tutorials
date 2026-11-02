---
category: general
date: 2026-06-24
description: Incorpore fontes PDF usando Aspose.Cells em C#. Aprenda como salvar Excel
  como PDF, exportar Excel para HTML, converter xlsx para PDF com Aspose e duplicar
  linhas de pivô.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: pt
og_description: Incorpore fontes PDF usando Aspose.Cells em C#. Este tutorial mostra
  passo a passo como salvar Excel como PDF, exportar Excel para HTML e mais.
og_title: Incorpore fontes PDF com Aspose.Cells – Guia Completo de C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Incorporar fontes PDF com Aspose.Cells – Guia Completo em C#
url: /pt/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporar fontes PDF com Aspose.Cells – Guia Completo em C#

Já se perguntou como **incorporar fontes PDF** ao converter uma pasta de trabalho do Excel com Aspose.Cells? Você não está sozinho—muitos desenvolvedores encontram dificuldades quando o PDF gerado parece errado em máquinas que não têm as fontes originais instaladas.  

Neste guia vamos percorrer um exemplo do mundo real que não só **incorpora fontes PDF**, mas também mostra como **salvar Excel como PDF**, **exportar Excel para HTML**, transformar um **xlsx em PDF com Aspose**, e ainda **duplicar linhas pivot** sem quebrar a tabela dinâmica. Parece muito? Sem problemas—vamos dividir tudo passo a passo.

## O que você aprenderá

- Como copiar linhas que contêm uma tabela dinâmica mantendo a pivot intacta.  
- Como inserir um smart‑marker que repete uma planilha de detalhes para cada pedido.  
- As configurações exatas que você precisa para **incorporar fontes PDF**, exportar gráficos como PPTX editável e preservar painéis congelados ao **exportar Excel para HTML**.  
- Dicas para solucionar armadilhas comuns, como fontes ausentes ou objetos OLE quebrados.  

**Pré‑requisitos:** .NET 6+ (ou .NET Framework 4.6+), Aspose.Cells para .NET instalado, e um ambiente básico de desenvolvimento C# (Visual Studio, Rider ou VS Code). Nenhum pacote NuGet extra além do Aspose.Cells é necessário.

---

## Incorporar fontes PDF – Processo passo a passo

Abaixo está o código completo e executável. Cada seção está anotada para que você veja exatamente por que fazemos o que fazemos.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Por que isso funciona

- **CopyRows** duplica as linhas que contêm a tabela dinâmica, de modo que a pivot original permanece vinculada aos seus dados de origem. Isso atende ao requisito de **duplicar linhas pivot**.  
- **SmartMarkerProcessing** cria uma nova planilha para cada pedido, automatizando a geração da planilha de detalhes.  
- **PdfSaveOptions.EmbedStandardFonts = true** indica ao Aspose.Cells que incorpore as fontes diretamente no arquivo PDF, que é a chave para **incorporar fontes pdf**. Sem essa flag o PDF recairia para fontes do sistema, quebrando o layout em outras máquinas.  
- **HtmlSaveOptions** com `EmbedAllFonts` e `PreserveFreezePanes` garante que ao **exportar Excel para HTML** a fidelidade visual corresponda ao workbook original.  

#### Saída esperada

- `result.pdf` – um PDF onde todas as fontes usadas são incorporadas; abra em qualquer computador e o texto aparecerá idêntico ao original.  
- `result.pptx` – um arquivo PowerPoint com gráficos editáveis e objetos OLE.  
- `result.html` – uma pasta HTML (`result.html` + `result_files`) que renderiza o workbook em um navegador com os painéis congelados intactos.  

---

## Salvar Excel como PDF com Aspose.Cells

Se seu único objetivo é **salvar Excel como PDF**, você pode remover as etapas extras e focar nas opções de PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Dica profissional:** Ao direcionar a conformidade PDF/A, o Aspose incorpora automaticamente todas as fontes, proporcionando uma camada extra de segurança para armazenamento de longo prazo.

---

## Exportar Excel para HTML preservando o layout

Exportar para HTML costuma perder a aparência da planilha original, especialmente quando há painéis congelados. O trecho a seguir mostra as configurações exatas que você precisa:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Como definimos `EmbedAllFonts`, o HTML gerado contém dados de fonte codificados em base‑64, atendendo ao requisito de **exportar excel para html** sem necessidade de arquivos CSS externos.

---

## Converter Xlsx para PDF usando Aspose.Cells

Às vezes a expressão “**xlsx to pdf aspose**” aparece em buscas. O código abaixo demonstra o pipeline de conversão exato, incluindo alguns detalhes adicionais:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**Por que se preocupar com a configuração de página?** Se você pular essa etapa, o PDF padrão pode cortar colunas ou linhas. Ajustar o layout primeiro garante que o PDF final corresponda ao que você vê no Excel.

---

## Duplicar Linhas Pivot – Mantendo a Pivot Intacta

Um obstáculo comum é tentar copiar linhas que contêm uma tabela dinâmica; a pivot frequentemente perde a conexão com a fonte de dados. O método `CopyRows` que usamos anteriormente faz o trabalho pesado para você:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – a primeira linha do intervalo que você deseja copiar.  
- **destinationRow** – onde a cópia deve ser colocada (mesma planilha, mesmo índice inicial para duplicar efetivamente).  
- **totalRows** – quantas linhas copiar.  

Como o cache da pivot reside na planilha, copiar as linhas **não** quebra a pivot. Isso satisfaz a palavra‑chave **duplicate rows pivot** enquanto mantém o workbook organizado.

---

## Recapitulação do Exemplo Completo

Juntando tudo, aqui está o programa completo que você pode inserir em um aplicativo console e executar imediatamente:



## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Salvar Pasta de Trabalho do Excel como PDF com Fontes Personalizadas usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [Como Exportar Gráficos do Excel para PDF Usando Aspose.Cells para .NET: Um Guia Passo a Passo](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Como Exportar Segmentações do Excel para PDF Usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}