---
category: general
date: 2026-10-10
description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
  – learn how to export Excel, set print area, and generate a PPTX file.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: en
lastmod: 2026-10-10
og_description: Convert Excel to PowerPoint with Aspose.Cells. This tutorial shows
  how to set the print area, export Excel, and create a PPTX file in C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Convert Excel to PowerPoint – full guide for C# developers
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Convert Excel to PowerPoint and set print area
url: /net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Excel to PowerPoint and set print area

If you need to **convert Excel to PowerPoint**, this guide shows you exactly how to do it in C#. By defining a print area first, you control which cells appear on each slide, and the final PPTX file matches your layout expectations. The solution also answers “how to export Excel” and “how to set print area” using the same code base.

In this tutorial you will:

* Load an existing workbook.
* Set the print area for a worksheet (the **set print area excel** step).
* Configure conversion options for PowerPoint output.
* Generate a **convert excel to pptx** file in a single method call.

All required code is included, so you can copy, paste, and run it immediately.

## Prerequisites

Before you begin, make sure you have:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | The sample targets .NET 6+, but any .NET version that supports C# 10 works. |
| **Aspose.Cells for .NET** | This library provides `Workbook`, `ImageOrPrintOptions`, and the `ConvertToPdf` (used for PPTX) method. Install it via NuGet: `dotnet add package Aspose.Cells` |
| **An input Excel file** | The tutorial uses `input.xlsx`. Place it in a folder you can reference from code. |
| **Write permission to the output folder** | The program writes `output.pptx`. Ensure the directory exists and is writable. |

> **Pro tip:** If you work with multiple worksheets, repeat the print‑area step for each sheet before conversion.

## Step 1: Create a new C# console project

Open a terminal or PowerShell window and run:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

This creates a fresh project named **ExcelToPowerPointDemo** and adds the Aspose.Cells package, which is the core dependency for **how to export Excel** to other formats.

## Step 2: Write the conversion code

Replace the content of `Program.cs` with the complete example below. The code demonstrates **convert excel to powerpoint**, shows **how to set print area**, and produces a **convert excel to pptx** file.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Why each part matters

* **Loading the workbook** – This is the first step in any **how to export Excel** scenario. `Workbook` reads the file into memory, giving you full access to sheets, cells, and formatting.
* **Setting the print area** – By assigning `PageSetup.PrintArea`, you tell Aspose.Cells which cells to render. This is the core of **set print area excel**; without it, the entire sheet would be exported, potentially creating huge, unreadable slides.
* **Choosing `SaveFormat.Pptx`** – The `ImageOrPrintOptions` object lets you switch output formats. Setting `SaveFormat` to `Pptx` triggers the **convert excel to pptx** pipeline.
* **Calling `ConvertToPdf`** – Despite the method name, when `SaveFormat` is `Pptx` the library outputs a PowerPoint file. This is the recommended way to **convert excel to powerpoint** in a single call.

## Step 3: Run the program

From the project folder, execute:

```bash
dotnet run
```

If everything is configured correctly, you should see console output similar to:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Open `output.pptx` in Microsoft PowerPoint or any compatible viewer. Each slide corresponds to the printed page of the worksheet, limited to the range you defined.

## Handling multiple worksheets

If your workbook contains more than one sheet and you want each sheet on its own slide deck, loop through the collection:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

This pattern shows **how to export Excel** data sheet‑by‑sheet while still **setting print area** individually.

## Edge cases and best‑practice tips

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | Reduce the print area or increase `HorizontalResolution`/`VerticalResolution` to keep the PPTX size manageable. |
| **Different page orientations** | Set `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` before conversion. |
| **Custom slide size** | Use `conversionOptions.OnePagePerSheet = false;` and adjust `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Wrap the loading code in a `try { … } catch (FileNotFoundException)` block to provide a clear error message. |
| **Non‑ASCII characters** | Ensure the workbook is saved with UTF‑8 encoding; Aspose.Cells handles Unicode automatically. |

## Full source code for reference

Below is the entire program, including `using` directives and comments. Save it as `Program.cs` inside the project created in **Step 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Expected output

Running the program produces a PowerPoint file (`output.pptx`) that contains:

* One slide per printed page of the worksheet.
* Only the cells inside **A1:G30** visible on each slide.
* Preserved formatting (fonts, colors, borders) as they appear in Excel.

Open the file in PowerPoint to verify that the layout matches the defined print area.

## Conclusion

You now know how to **convert Excel to PowerPoint** while precisely **set print area excel** using Aspose.Cells in C#. The tutorial covered **how to export Excel**, demonstrated **how to set print area**, and showed the full **convert excel to pptx**


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}