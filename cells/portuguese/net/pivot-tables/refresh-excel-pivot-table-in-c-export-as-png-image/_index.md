---
category: general
date: 2026-02-23
description: Atualize a tabela dinâmica do Excel em C# e exporte-a como imagem PNG.
  Aprenda a carregar a pasta de trabalho do Excel em C#, atualizar a tabela dinâmica
  e salvar o resultado.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: pt
og_description: Atualize a tabela dinâmica do Excel em C# e exporte-a como imagem
  PNG. Guia passo a passo com código completo e dicas práticas.
og_title: Atualizar Tabela Dinâmica do Excel em C# – Exportar como Imagem PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Atualizar Tabela Dinâmica do Excel em C# – Exportar como Imagem PNG
url: /pt/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atualizar Tabela Dinâmica do Excel em C# – Exportar como Imagem PNG

Já precisou **refresh an Excel pivot table** a partir de uma aplicação C# e depois transformá‑la em uma imagem? Você não é o único a ficar coçando a cabeça com isso. Neste tutorial vamos percorrer passo a passo como **refresh Excel pivot table**, **load Excel workbook C#**, e finalmente **export pivot as image** — tudo em um trecho de código limpo e executável.

O que você terá ao final é um arquivo PNG que se parece exatamente com a tabela dinâmica que você veria no Excel, pronto para ser incorporado em relatórios, e‑mails ou dashboards. Sem copiar‑colar manual, sem interop COM complicado, apenas código .NET direto ao ponto.

## Prerequisites

- .NET 6+ (ou .NET Framework 4.7+)
- Aspose.Cells for .NET (versão de avaliação ou licenciada) – você pode obtê‑lo via NuGet com `Install-Package Aspose.Cells`.
- Um `input.xlsx` existente que contenha ao menos uma tabela dinâmica.
- Uma pasta onde você tenha permissão de gravação para a imagem de saída.

> **Pro tip:** Se você estiver usando o Visual Studio, habilite **nullable reference types** (`<Nullable>enable</Nullable>`) para capturar bugs relacionados a nulls mais cedo.

---

## Step 1: Load Excel Workbook in C#

The first thing we need is a `Workbook` object that points to our source file. Think of this as opening the Excel file programmatically.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Why this matters:** Loading the workbook gives us access to the worksheets, cells, and—most importantly—the pivot tables you’ve built. If the file isn’t found, Aspose throws a clear `FileNotFoundException`, which you can catch for a graceful fallback.

---

## Step 2: Configure Image Export Options (Export Pivot as Image)

Aspose.Cells lets you define how the pivot should be rendered. Here we ask for a PNG because it’s lossless and widely supported.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Why PNG?** Unlike JPEG, PNG preserves the crisp grid lines and text shading that pivot tables rely on. If you need a smaller file, you could switch to `ImageFormat.Jpeg` and adjust the quality, but you’ll lose a bit of clarity.

---

## Step 3: Refresh the Pivot Table

Before we capture the visual, we must make sure the pivot reflects the latest data. This is the core of **refresh excel pivot table**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**What’s happening under the hood?** `Refresh()` re‑calculates the pivot based on the source range. If you’ve added rows to the source data after the workbook was saved, this call pulls them in. Skipping this step results in a stale image that doesn’t match the current data.

---

## Step 4: Render the Pivot Table to PNG (Export Excel Pivot Image)

Now that everything is up‑to‑date, we can render the pivot directly to an image file.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Result:** Open `pivot.png` and you’ll see a pixel‑perfect snapshot of the refreshed pivot. This file can be attached to an email, embedded in a web page, or fed into a reporting engine.

### Expected Output

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

If you browse to the folder, the PNG should display the same rows, columns, and filters you’d see in Excel.

---

## Handling Common Edge Cases

| Situation | What to Do |
|-----------|------------|
| **Multiple pivot tables** | Loop through `worksheet.PivotTables` and call `Refresh()` / `RenderToImage()` for each. |
| **Dynamic sheet names** | Use `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` or search by `worksheet.Name`. |
| **Large datasets** | Increase `imgOptions.OnePagePerSheet = false` and set `imgOptions.PageWidth`/`PageHeight` to control paging. |
| **Missing Aspose.Cells license** | The free trial adds a watermark. Acquire a license and call `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` before loading the workbook. |
| **File‑path issues** | Use `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` to avoid hard‑coded separators. |

---

## Pro Tips & Best Practices

- **Dispose properly** – Wrap the `Workbook` in a `using` block or call `wb.Dispose()` when done to free native resources.
- **Cache rendered images** – If you need the same pivot image repeatedly, cache the PNG on disk and reuse it instead of re‑rendering each time.
- **Thread safety** – Each thread should work with its own `Workbook` instance; Aspose.Cells objects are not thread‑safe.
- **Performance** – Rendering large pivots can be memory intensive. Adjust `imgOptions.ImageFormat` to `Bmp` for faster but larger files, or lower the DPI for quicker renders.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Run the program, open `pivot.png`, and you’ll see the refreshed pivot table exactly as it appears in Excel.

---

## Frequently Asked Questions

**Q: Does this work with .xlsx files created by LibreOffice?**  
A: Yes. Aspose.Cells reads the Open XML format regardless of the originating application, so you can **load excel workbook c#** from LibreOffice, Google Sheets export, or any other source.

**Q: Can I export multiple worksheets at once?**  
A: Absolutely. Loop over `wb.Worksheets` and apply the same `RenderToImage` logic per sheet. Just remember to give each output a unique filename.

**Q: What if the pivot uses an external data source?**  
A: Aspose.Cells can refresh external connections if they’re embedded in the file, but you’ll need to supply the connection string and credentials programmatically. See the Aspose documentation for `DataSourceOptions`.

---

## Conclusion

You now have a solid, end‑to‑end solution to **refresh excel pivot table** from C# and **export excel pivot image** as a PNG. The code shows how to **load excel workbook c#**, configure image settings, ensure the pivot reflects the latest data, and finally render it to a file. 

Next, you might explore **export pivot as image** in other formats (PDF, SVG) or automate the process for multiple workbooks in a batch job. Want to embed the PNG in a Word report? The same `ImageOrPrintOptions` class works with Aspose.Words.

Feel free to experiment, break things, and ask questions in the comments—happy coding! 

![Refresh Excel pivot table screenshot](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}