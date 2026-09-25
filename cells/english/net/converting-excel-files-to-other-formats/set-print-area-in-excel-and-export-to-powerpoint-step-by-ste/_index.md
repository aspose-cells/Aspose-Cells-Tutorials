---
category: general
date: 2026-03-22
description: Set print area in Excel and convert excel to powerpoint with editable
  shapes. Learn how to repeat title row, create powerpoint from excel and export excel
  to pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: en
og_description: Set print area in Excel and convert it to a PowerPoint slide with
  editable shapes. Follow this complete guide to repeat title row and export excel
  to pptx.
og_title: Set Print Area in Excel – Export to PowerPoint Tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide
url: /net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Print Area in Excel and Export to PowerPoint – Complete Programming Tutorial

Ever needed to **set print area** in an Excel worksheet and then turn that slice into a PowerPoint slide? You're not the only one. In many reporting pipelines the same data that prints nicely also needs to appear in a presentation, often with the first row repeated as a title. The good news? With a few lines of C# you can **convert excel to powerpoint**, keep all text boxes editable, and even **repeat title row** automatically.

In this guide we’ll walk through everything you need to know: from configuring the print area to creating a PPTX file that you can edit right in PowerPoint. By the end you’ll be able to **create powerpoint from excel**, export the result as **export excel to pptx**, and reuse the same code in any .NET project. No magic, just clear steps and a full, runnable example.

## What You’ll Need

Before we dive in, make sure you have:

- **.NET 6.0** or later (the API works with .NET Framework as well)
- **Aspose.Cells for .NET** (the library that provides `Workbook`, `ImageOrPrintOptions`, etc.)
- A basic C# IDE (Visual Studio, Rider, or VS Code with the C# extension)
- An Excel file (`input.xlsx`) that contains the data you want to export

That’s it—no extra NuGet packages beyond Aspose.Cells. If you haven’t added the library yet, run:

```bash
dotnet add package Aspose.Cells
```

Now we’re ready to roll.

## Step 1: Load the Workbook – the Starting Point for Export

The first thing you have to do is load the workbook that holds the sheet you want to turn into a slide. Think of the workbook as the source document; without it nothing else matters.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Why this matters:** Loading the workbook gives you access to the worksheet collection, page‑setup options, and the export engine. If you skip this step you won’t be able to set the **print area** or repeat any rows.

> **Pro tip:** Use an absolute path while testing, then switch to a relative one or configuration‑based path for production.

## Step 2: Configure Export Options – Keep Text Boxes and Shapes Editable

When you export to PowerPoint you probably want the resulting slide to be editable. Aspose.Cells lets you control that with `ImageOrPrintOptions`. Setting `ExportTextBoxes` and `ExportShapeObjects` to `true` tells the library to preserve those objects as native PowerPoint elements instead of flattening them into an image.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Why this matters:** If you ever needed to **convert excel to powerpoint** and then tweak the slide manually, this setting saves you from re‑creating text boxes from scratch. It also ensures that any shapes (like arrows or charts) stay as vector objects you can resize.

## Step 3: Set Print Area and Repeat the Title Row

Now we get to the heart of the tutorial: **set print area** and make the first row repeat on every printed page (or, in our case, on the exported slide). The print area tells Excel which cells to consider for printing—or exporting in our scenario.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Why this matters:** By limiting the export to `A1:G20` you avoid pulling in massive empty ranges, which speeds up the conversion and keeps the slide tidy. The `PrintTitleRows` line makes the first row act like a header—exactly what you want when you **repeat title row** in a presentation.

> **Edge case:** If your data starts on row 2, adjust the range accordingly (e.g., `PrintTitleRows = "$2:$2"`).

## Step 4: Save the Worksheet as a PowerPoint File

Finally, we write the slide to disk. The `Save` method takes the target filename and the options we configured earlier. The result is a PPTX file with editable text boxes and shapes, ready to be opened in PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**What you’ll see:** Open `SheetWithEditableShapes.pptx` in PowerPoint. The first row appears as a title, all cells from `A1:G20` are rendered, and any shapes you added in Excel are still movable and editable. No rasterized images—just native PowerPoint objects.

## Full Working Example – All Steps Combined

Below is the complete, copy‑paste‑ready program. Run it as a console app or embed it in any larger solution.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Expected output:** After running the program, the console prints the success message, and the PPTX file appears at the specified location. Opening the file shows a single slide with the selected range, editable text boxes, and any original shapes.

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **Does this work with multiple worksheets?** | Yes. Loop through `workbook.Worksheets` and repeat the same steps for each sheet, changing the output filename each time. |
| **What if I need to export more than one slide?** | Call `workbook.Save` multiple times with different `ImageOrPrintOptions` objects, each configured with a different `PageSetup` if needed. |
| **Can I change the slide size?** | Use `exportOptions.ImageFormat` to set DPI, or adjust `sheet.PageSetup.PaperSize` before saving. |
| **Is Aspose.Cells free?** | It offers a free evaluation with watermarks. For production, a license is required. |
| **What about Excel formulas?** | The exported values are the **calculated results** at the time of export. If you need live formulas in PowerPoint, you’ll need a different approach. |

## Tips for a Smooth Workflow

- **Pro tip:** Set `Workbook.Settings.CalcMode = CalculationModeType.Automatic` before export to guarantee all formulas are up‑to‑date.
- **Watch out for:** Very large ranges can cause memory pressure. Trim the print area to the smallest necessary range.
- **Performance tip:** Reuse a single `ImageOrPrintOptions` instance if you’re exporting many sheets; creating a new one each time adds overhead.
- **Version note:** The code above targets Aspose.Cells 23.10 (released November 2023). Later versions keep the same API, but always double‑check the release notes for breaking changes.

## Conclusion

We’ve covered how to **set print area** in an Excel worksheet, repeat the first row as a title, and then **export excel to pptx** while preserving editable text boxes and shapes. In short, you now know a reliable way to **convert excel to powerpoint**, **repeat title row**, and **create powerpoint from excel** with just a few lines of C#.

Ready for the next step? Try automating a batch conversion of dozens of reports, or add custom slide layouts using the PowerPoint SDK after the export. The sky’s the limit—experiment, break things, and enjoy the power of programmatic document generation.

If you found this tutorial useful, give it a share, drop a comment with your own tweaks, or explore our other guides on **export excel to pptx** and related automation topics. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}