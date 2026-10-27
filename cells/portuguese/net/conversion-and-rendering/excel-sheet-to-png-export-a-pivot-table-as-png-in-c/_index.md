---
category: general
date: 2026-03-18
description: Tutorial de planilha Excel para PNG mostrando como exportar a tabela
  dinâmica, definir a área de impressão da tabela dinâmica e exportar a imagem de
  um intervalo do Excel usando Aspose.Cells.
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: pt
og_description: Tutorial de planilha Excel para PNG que orienta passo a passo como
  exportar tabelas dinâmicas, definir a área de impressão da tabela dinâmica e exportar
  a imagem de um intervalo do Excel com C#.
og_title: planilha Excel para PNG – Guia completo para exportar tabelas dinâmicas
tags:
- Aspose.Cells
- C#
- Excel automation
title: Planilha do Excel para PNG – Exportar uma Tabela Dinâmica como PNG em C#
url: /pt/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel sheet to png – Exportar uma Tabela Dinâmica como PNG em C#

Já precisou transformar uma **excel sheet to png** mas não sabia como capturar apenas a tabela dinâmica? Você não está sozinho. Em muitos pipelines de relatório, a visualização de uma pivot é a estrela, e exportá‑la como PNG permite incorporá‑la em e‑mails, dashboards ou documentação sem precisar incluir a planilha inteira.

Neste guia vamos mostrar **como exportar pivot** data, **set print area pivot**, e finalmente **export excel range image** para que você obtenha um arquivo **export worksheet to image** limpo. Sem links misteriosos para documentos externos — apenas um snippet completo e executável e o raciocínio por trás de cada linha.

## What You’ll Need

- **Aspose.Cells for .NET** (o pacote NuGet `Aspose.Cells` – versão 23.12 ou mais recente).  
- Um ambiente de desenvolvimento .NET (Visual Studio, Rider ou a CLI `dotnet`).  
- Um arquivo Excel (`input.xlsx`) que contenha ao menos uma tabela dinâmica.

É só isso. Se você tem esses itens, vamos começar.

## Step 1 – Load the Workbook and Grab the First Worksheet

Antes de tocar na pivot, precisamos carregar a workbook na memória.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Why this matters:* Carregar o arquivo nos dá acesso a todos os objetos (tables, charts, pivots). Usar a primeira worksheet é um padrão simples; você pode substituir `0` pelo índice ou nome da planilha real, se necessário.

## Step 2 – Retrieve the Pivot Table Range

Uma tabela dinâmica vive dentro de um bloco de células. Precisamos desse bloco para dizer ao Excel o que imprimir.

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Why we do this:* O `PivotTableRange` nos informa a linha/coluna inicial e final exatas. Sem ele, a exportação incluiria a planilha inteira, o que anula o objetivo de **set print area pivot**.

## Step 3 – Define the Print Area So Only the Pivot Is Rendered

O motor de impressão do Excel respeita a propriedade `PrintArea`. Ao restringi‑la à pivot, evitamos dados estranhos ou células vazias.

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Pro tip:* Se você tem múltiplas pivots na mesma planilha, pode combinar seus intervalos usando uma lista separada por vírgulas (`"0,0:10,5,12,0:22,5"`). Essa é a técnica de **export excel range image** para vários blocos.

## Step 4 – Set Up Image Export Options (PNG Format)

Aspose.Cells permite ajustar finamente a saída. PNG é sem perdas, perfeito para visualizações nítidas de pivots.

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Why PNG?* Diferente do JPEG, o PNG preserva a nitidez do texto e fundos transparentes, tornando‑se a escolha ideal para cenários de **excel sheet to png**.

## Step 5 – Export the Worksheet (Pivot Area) to a PNG File

Agora a mágica acontece — renderizamos a área de impressão definida para uma imagem.

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*What you’ll see:* Um arquivo `pivot.png` que contém apenas a tabela dinâmica, sem linhas ou colunas extras. Abra‑o em qualquer visualizador de imagens e você terá um visual pronto para ser compartilhado.

---

## Frequently Asked Questions & Edge Cases

### What if the workbook has **multiple pivot tables**?

Recupere o `PivotTableRange` de cada pivot, mescle os intervalos e atribua a string combinada à `PrintArea`. Exemplo:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### Can I export to **other image formats**?

Com certeza. Altere `imgOptions.ImageFormat = ImageFormat.Jpeg;` (ou `Bmp`, `Gif`, `Tiff`). Apenas lembre‑se de que JPEG introduz artefatos de compressão — geralmente não ideal para pivots com muito texto.

### How do I handle **large pivots** that span many pages?

Defina `imgOptions.OnePagePerSheet = false;` para permitir renderização em múltiplas páginas, e então itere pelas páginas:

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### What about **hidden rows/columns**?

Aspose respeita as configurações de visibilidade da worksheet. Se precisar ignorar elementos ocultos, desoculte‑os temporariamente antes da exportação ou ajuste a `PrintArea` manualmente.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

Execute o programa e você encontrará `pivot.png` exatamente onde apontou. Abra o arquivo — você deverá ver a renderização nítida apenas da tabela dinâmica, nada mais.

---

## Conclusion

Agora você tem uma **solução completa, ponta a ponta** para transformar uma **excel sheet to png** focando exclusivamente em uma tabela dinâmica. Ao **setting the print area pivot**, configurar **image export options** e usar o método `ToImage` do Aspose.Cells, você pode automatizar a geração de relatórios, incorporar visuais em páginas web ou simplesmente arquivar instantâneos analíticos.

Qual o próximo passo? Experimente trocar o PNG por um PDF de alta resolução (`ImageFormat.Pdf`), teste múltiplas pivots em uma única planilha ou combine essa abordagem com exportação de gráficos para criar um pipeline de exportação de dashboard completo.

Tem alguma variação que gostaria de compartilhar? Deixe um comentário, ou acompanhe o próximo tutorial onde exploraremos **export worksheet to image** para capturas de tela de planilhas inteiras, incluindo gráficos e formatação condicional. Happy coding!  

<img src="pivot.png" alt="excel sheet to png example of pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}