---
category: general
date: 2026-10-20
description: Aprenda como usar wrapcols no Aspose.Cells, incorporar fontes em HTML
  e salvar Excel como HTML com um exemplo completo em C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: pt
lastmod: 2026-10-20
og_description: Como usar wrapcols no Aspose.Cells, incorporar fontes em HTML e converter
  a pasta de trabalho para HTML com um tutorial claro em C# para desenvolvedores.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Como usar wrapcols e incorporar fontes ao exportar Excel para HTML
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Como usar wrapcols e incorporar fontes ao salvar Excel para HTML
url: /pt/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar wrapcols e incorporar fontes ao salvar Excel em HTML

Se você precisa de **how to use wrapcols** em uma fórmula Aspose.Cells, este guia mostra os passos exatos. Você também aprenderá como **embed fonts in HTML** e **save Excel as HTML** para que a saída tenha a mesma aparência em todos os navegadores.  

O tutorial cobre três cenários práticos: usar a função `WRAPCOLS`, exportar uma pasta de trabalho com fontes incorporadas e gerar um relatório mestre‑detalhe com Smart Markers. Ao final, você terá um único programa C# executável que demonstra todos esses recursos.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

* .NET 6.0 (ou posterior) instalado.
* Aspose.Cells for .NET adicionado ao seu projeto (`dotnet add package Aspose.Cells`).
* Familiaridade básica com C# e fórmulas do Excel.

Nenhuma biblioteca de terceiros adicional é necessária; Aspose.Cells lida com a conversão para HTML e a incorporação de fontes internamente.

## Etapa 1: Demonstrar a função **how to use wrapcols** em uma fórmula

A função `WRAPCOLS` divide um intervalo unidimensional em uma matriz bidimensional, preenchendo colunas primeiro. Isso é útil quando você precisa remodelar dados para relatórios ou gráficos.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Por que isso funciona:**  
`WRAPCOLS` recebe dois argumentos – o intervalo de origem e o número de colunas. A função preenche a matriz por colunas, descartando quaisquer valores excedentes (o `3` no exemplo). O resultado aparece na célula superior‑esquerda do intervalo de destino (`B1`), e você pode expandir o intervalo manualmente se precisar da matriz completa.

> **Dica profissional:** Após definir a fórmula, chame `workbook.CalculateFormula()` para garantir que o resultado esteja atualizado antes de ler os valores das células.

## Etapa 2: **Convert workbook to HTML** e **embed fonts in html**

Ao exportar um arquivo Excel para HTML, as fontes são frequentemente substituídas pelas fontes padrão do navegador, o que pode quebrar o layout visual. Aspose.Cells permite incorporar as fontes exatas usadas na pasta de trabalho diretamente no arquivo HTML.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Por que a incorporação de fontes importa:**  
Quando `EmbedFonts` está `true`, Aspose.Cells converte cada fonte TrueType/OpenType usada em uma regra `@font-face` codificada em Base64 dentro do HTML gerado. Isso elimina a necessidade de a máquina cliente ter as mesmas fontes instaladas, garantindo renderização pixel‑perfeita.

> **Caso extremo:** Se a pasta de trabalho de origem referenciar uma fonte que não está instalada no servidor, Aspose.Cells retornará a uma fonte padrão e emitirá um aviso. Certifique‑se de que as fontes necessárias estejam disponíveis


## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar WRAPCOLS em C# – Criar pasta de trabalho Excel com funções de wrap](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Como incorporar fontes em HTML – Converter Excel para HTML com C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Como converter arquivos Excel para HTML usando Aspose.Cells para .NET: Ocultando conteúdo sobreposto](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}