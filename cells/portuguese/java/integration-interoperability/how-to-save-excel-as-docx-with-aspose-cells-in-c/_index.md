---
category: general
date: 2026-08-17
description: salvar Excel como DOCX usando Aspose.Cells – converta rapidamente uma
  planilha ou gráfico do Excel em um documento Word editável (DOCX) com algumas linhas
  de código C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as docx
- convert excel to word
- convert spreadsheet to word document
- export chart from excel to word
- save excel file as word document
language: pt
lastmod: 2026-08-17
og_description: salvar excel como docx com Aspose.Cells em C#. Este tutorial mostra
  passo a passo como converter uma pasta de trabalho do Excel, incluindo gráficos
  incorporados, em um documento do Word editável.
og_image_alt: Screenshot of C# code converting an Excel file with a chart into a Word
  DOCX file
og_title: Salvar Excel como DOCX – guia completo de C# usando Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: save excel as docx using Aspose.Cells – quickly convert an Excel workbook
    or chart to an editable Word document (DOCX) with a few lines of C# code.
  headline: How to save Excel as DOCX with Aspose.Cells in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to Word
- DOCX conversion
title: Como salvar Excel como DOCX com Aspose.Cells em C#
url: /pt/java/integration-interoperability/how-to-save-excel-as-docx-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como salvar Excel como DOCX com Aspose.Cells em C#

Se você precisa **salvar Excel como DOCX**, este guia mostra passo a passo o que é necessário em C#. Seja para **converter Excel para Word** para edição posterior ou incorporar um gráfico do Excel em um relatório Word, a solução abaixo lida com ambos os cenários com código mínimo.

Neste tutorial você aprenderá a:

* Carregar uma pasta de trabalho `.xlsx` existente que contém dados e gráficos.  
* Exportar a pasta de trabalho (ou apenas um gráfico) para um arquivo Word `.docx` editável.  
* Tratar casos comuns, como múltiplas planilhas e dimensionamento de gráficos.

O único pré-requisito é a biblioteca Aspose.Cells for .NET, que fornece a sobrecarga `Workbook.save` que grava diretamente no formato Word.

## Pré-requisitos

| Requisito | Por que é importante |
|-------------|----------------|
| .NET 6.0 or later | Fornece recursos modernos da linguagem e suporte de longo prazo. |
| Visual Studio 2022 (or any C# IDE) | Facilita a depuração e o gerenciamento de projetos. |
| **Aspose.Cells for .NET** NuGet package | Fornece o método `Workbook.save(..., SaveFormat.DOCX)` usado para **salvar arquivo Excel como documento Word**. |

Instale o pacote usando a CLI do .NET:

```bash
dotnet add package Aspose.Cells
```

## Etapa 1: Criar um projeto console C#

Abra um terminal e execute:

```bash
dotnet new console -n ExcelToWordDemo
cd ExcelToWordDemo
```

Isso cria um projeto mínimo onde você pode colar o código de conversão.

## Etapa 2: Carregar a pasta de trabalho Excel que contém o gráfico

A primeira operação é ler o arquivo `.xlsx` de origem. Aspose.Cells suporta tanto caminhos locais quanto streams, permitindo carregar pastas de trabalho do disco, armazenamento em nuvem ou um array de bytes.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source Excel file that contains data and optionally a chart.
        const string sourcePath = @"YOUR_DIRECTORY\chart.xlsx";

        // Load the workbook. The constructor automatically detects the format.
        Workbook workbook = new Workbook(sourcePath);

        Console.WriteLine($"Workbook loaded. Worksheets count: {workbook.Worksheets.Count}");
```

**Por que esta etapa é importante:** Carregar a pasta de trabalho valida que o arquivo existe e que o Aspose.Cells pode analisar as estruturas internas (células, tabelas, gráficos). Se o arquivo estiver corrompido, uma exceção é lançada aqui, permitindo tratar o erro antes de tentar a conversão.

## Etapa 3: (Opcional) Exportar um único gráfico em vez de toda a pasta de trabalho

Se o seu objetivo é **exportar gráfico do Excel para Word** em vez de toda a planilha, você pode extrair o gráfico como imagem e inseri-lo manualmente em um novo documento Word. O trecho a seguir demonstra ambas as abordagens.

```csharp
        // ------------------------------------------------------------
        // Option A: Convert the entire workbook (including all charts)
        // ------------------------------------------------------------
        // The SaveFormat.DOCX overload writes the full workbook to a
        // Word document where each worksheet becomes a separate table.
        // This is the simplest way to **convert spreadsheet to Word document**.
        const string docxPathFull = @"YOUR_DIRECTORY\chart_editable.docx";
        workbook.Save(docxPathFull, SaveFormat.DOCX);
        Console.WriteLine($"Full workbook saved as DOCX at: {docxPathFull}");

        // ------------------------------------------------------------
        // Option B: Export only the first chart as a picture
        // ------------------------------------------------------------
        // Some scenarios require only the visual chart without the data grid.
        // The code below extracts the first chart from the first worksheet.
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Charts.Count > 0)
        {
            // Render the chart to an image (PNG by default).
            var chart = sheet.Charts[0];
            using var chartImage = chart.ToImage();

            // Save the image temporarily.
            string tempImagePath = @"YOUR_DIRECTORY\temp_chart.png";
            chartImage.Save(tempImagePath, System.Drawing.Imaging.ImageFormat.Png);
            Console.WriteLine($"Chart extracted to image: {tempImagePath}");

            // Create a new empty workbook that will be saved as DOCX.
            Workbook chartOnlyWorkbook = new Workbook();
            Worksheet chartSheet = chartOnlyWorkbook.Worksheets[0];
            // Insert the picture into the worksheet; when saved as DOCX,
            // the picture appears in the Word document.
            int pictureIndex = chartSheet.Pictures.Add(0, 0, tempImagePath);
            chartSheet.Pictures[pictureIndex].Placement = PlacementType.FreeFloating;
            const string docxPathChartOnly = @"YOUR_DIRECTORY\chart_only.docx";
            chartOnlyWorkbook.Save(docxPathChartOnly, SaveFormat.DOCX);
            Console.WriteLine($"Chart-only DOCX created at: {docxPathChartOnly}");
        }
        else
        {
            Console.WriteLine("No charts found in the workbook – only the full conversion was performed.");
        }
    }
}
```

### Explicação do código

* **Opção A** usa `Workbook.Save(..., SaveFormat.DOCX)` que salva diretamente **excel como docx**. Cada planilha é transformada em uma tabela Word, e quaisquer gráficos incorporados tornam‑se objetos Word editáveis.
* **Opção B** demonstra uma abordagem mais granular para o requisito de **exportar gráfico do excel para word**. Ela:
  1. Recupera o primeiro gráfico via `sheet.Charts[0]`.
  2. Renderiza o gráfico para uma imagem PNG (`chart.ToImage()`).
  3. Insere a imagem em uma nova pasta de trabalho.
  4. Salva essa pasta de trabalho como DOCX, resultando em um arquivo Word que contém apenas a imagem do gráfico.

Ambos os caminhos garantem que o arquivo `.docx` resultante seja totalmente editável no Microsoft Word.

## Etapa 4: Verificar a saída

Abra os arquivos gerados (`chart_editable.docx` e/ou `chart_only.docx`) no Microsoft Word:

* **Conversão completa** – você deve ver cada planilha Excel como uma tabela separada. Os gráficos aparecem como objetos de gráfico Word editáveis que podem ser redimensionados ou formatados.
* **Conversão apenas do gráfico** – você verá uma única imagem representando o gráfico original do Excel.

Se o documento Word não abrir, verifique se o arquivo Excel de origem não está protegido por senha e se a licença do Aspose.Cells (se houver) foi aplicada corretamente.

## Armadilhas comuns e como evitá‑las

| Problema | Causa | Correção |
|-------|-------|-----|
| Arquivo Word está corrompido | Versão do Aspose.Cells ausente ou incompatível | Use a mesma versão do Aspose.Cells tanto no desenvolvimento quanto na produção. |
| Gráfico aparece borrado | PNG salvo com DPI baixo | Chame `chart.ToImage(300, 300)` para aumentar a resolução antes de salvar. |
| Apenas a primeira planilha é salva | `Workbook.Save` chamado em uma pasta de trabalho que contém planilhas ocultas | Defina `workbook.Worksheets[i].IsVisible = true` para cada planilha que você deseja incluir. |
| Aviso de licença no console | Versão de avaliação do Aspose.Cells | Aplique uma licença válida via `License license = new License(); license.SetLicense("Aspose.Cells.lic");` antes de carregar a pasta de trabalho. |

## Exemplo completo executável

Abaixo está o programa completo e autocontido que você pode copiar para `Program.cs`. Substitua `YOUR_DIRECTORY` pelo caminho absoluto ou relativo onde seu arquivo Excel está localizado.

```csharp
using System;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1. Load the Excel workbook containing data and charts
        // ------------------------------------------------------------
        const string sourcePath = @"YOUR_DIRECTORY\chart.xlsx";
        Workbook workbook = new Workbook(sourcePath);
        Console.WriteLine($"Workbook loaded. Worksheets: {workbook.Worksheets.Count}");

        // ------------------------------------------------------------
        // 2. Convert the entire workbook to an editable Word document
        // ------------------------------------------------------------
        const string docxPathFull = @"YOUR_DIRECTORY\chart_editable.docx";
        workbook.Save(docxPathFull, SaveFormat.DOCX);
        Console.WriteLine($"Full workbook saved as DOCX: {docxPathFull}");

        // ------------------------------------------------------------
        // 3. (Optional) Export only the first chart as a picture in Word
        // ------------------------------------------------------------
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Charts.Count > 0)
        {
            // Render chart to high‑resolution PNG (300 DPI)
            var chart = sheet.Charts[0];
            using var chartImage = chart.ToImage(300, 300);
            string tempImagePath = @"YOUR_DIRECTORY\temp_chart.png";
            chartImage.Save(tempImagePath, ImageFormat.Png);
            Console.WriteLine($"Chart image saved: {tempImagePath}");

            // Create a new workbook that will become the chart‑only DOCX
            Workbook chartOnlyWb = new Workbook();
            Worksheet chartSheet = chartOnlyWb.Worksheets[0];
            int picIdx = chartSheet.Pictures.Add(0, 0, tempImagePath);
            chartSheet.Pictures[picIdx].Placement = PlacementType.FreeFloating;

            const string docxPathChartOnly = @"YOUR_DIRECTORY\chart_only.docx";
            chartOnlyWb.Save(docxPathChartOnly, SaveFormat.DOCX);
            Console.WriteLine($"Chart‑only DOCX created: {docxPathChartOnly}");
        }
        else
        {
            Console.WriteLine("No charts detected – only full workbook conversion performed.");
        }
    }
}
```

### Saída esperada no console



## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como converter arquivos Excel para DOCX usando Aspose.Cells for .NET em C#](/cells/english/net/workbook-operations/convert-excel-to-docx-aspose-csharp/)
- [Criar e salvar pasta de trabalho Excel como PDF em ASP.NET usando Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Como criar e salvar uma pasta de trabalho Excel como ODS usando Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}