---
category: general
date: 2026-10-20
description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and save
  Excel as HTML with a complete C# example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: en
lastmod: 2026-10-20
og_description: How to use wrapcols in Aspose.Cells, embed fonts in HTML, and convert
  workbook to HTML with a clear C# walkthrough for developers.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: How to use wrapcols and embed fonts exporting Excel to HTML
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
title: How to use wrapcols and embed fonts saving Excel to HTML
url: /net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to use wrapcols and embed fonts saving Excel to HTML

If you need to **how to use wrapcols** in an Aspose.Cells formula, this guide shows you the exact steps. You’ll also learn how to **embed fonts in HTML** and **save Excel as HTML** so the output looks identical across browsers.  

The tutorial covers three practical scenarios: using the `WRAPCOLS` function, exporting a workbook with embedded fonts, and generating a master‑detail report with Smart Markers. By the end you’ll have a single, runnable C# program that demonstrates all of these features.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 (or later) installed.
* Aspose.Cells for .NET added to your project (`dotnet add package Aspose.Cells`).
* Basic familiarity with C# and Excel formulas.

No additional third‑party libraries are required; Aspose.Cells handles HTML conversion and font embedding internally.

## Step 1: Demonstrate the **how to use wrapcols** function in a formula

The `WRAPCOLS` function splits a one‑dimensional range into a two‑dimensional array, filling columns first. This is useful when you need to reshape data for reporting or charting.

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

**Why this works:**  
`WRAPCOLS` takes two arguments – the source range and the number of columns. The function fills the array column‑wise, discarding any excess values (the `3` in the example). The result appears in the top‑left cell of the target range (`B1`), and you can expand the range manually if you need the full array.

> **Pro tip:** After setting the formula, call `workbook.CalculateFormula()` to ensure the result is up‑to‑date before reading cell values.

## Step 2: **Convert workbook to HTML** and **embed fonts in html**

When you export an Excel file to HTML, fonts are often substituted by the browser’s defaults, which can break the visual layout. Aspose.Cells lets you embed the exact fonts used in the workbook directly into the HTML file.

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

**Why embedding fonts matters:**  
When `EmbedFonts` is `true`, Aspose.Cells converts each used TrueType/OpenType font into a Base64‑encoded `@font-face` rule inside the generated HTML. This eliminates the need for the client machine to have the same fonts installed, guaranteeing pixel‑perfect rendering.

> **Edge case:** If the source workbook references a font that is not installed on the server, Aspose.Cells will fall back to a default font and issue a warning. Ensure the required fonts are available


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Embed Fonts in HTML – Convert Excel to HTML with C#](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [How to Convert Excel Files to HTML Using Aspose.Cells for .NET: Hiding Overlaid Content](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}