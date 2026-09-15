---
category: general
date: 2026-09-15
description: Create Excel workbook in C# and learn how to save workbook as PDF while
  spilling dynamic arrays using the EXPAND function.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: en
lastmod: 2026-09-15
og_description: Create Excel workbook in C# and quickly save workbook as PDF while
  using the EXPAND function to spill a dynamic array.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Create Excel workbook and save as PDF with dynamic arrays
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Create Excel workbook and save as PDF with dynamic arrays
url: /net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook and save as PDF with dynamic arrays

If you need to **create Excel workbook** programmatically and then **save workbook as PDF**, this guide shows you a complete, end‑to‑end solution in C#. You’ll also see how to **spill dynamic array** results by using the **EXPAND function**, which is the modern way to generate arrays without VBA.  

Whether you are building a reporting service, an export feature for an ERP system, or a data‑driven dashboard, the steps below let you generate a workbook, populate it with smart‑marker data, and produce a PDF that preserves advanced font features.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works with .NET Framework 4.8)
* A recent version of **Aspose.Cells for .NET** (v25.8 or newer) – it provides `Workbook`, `PdfSaveOptions`, and `SmartMarkerProcessor`.
* An IDE such as Visual Studio 2022 (any editor that can compile C# works).

Add the NuGet package to your project:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Step 1: Create Excel workbook and set up the first worksheet

The first task is to **create Excel workbook** and obtain a reference to the default worksheet. This worksheet will host the dynamic array and the Smart Marker template.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Why this matters*: Instantiating `Workbook` allocates the internal workbook structure, while accessing `Worksheets[0]` gives you a ready‑to‑use sheet without having to add one manually.

## Step 2: Spill dynamic array using the EXPAND function

Excel’s **EXPAND function** can turn a static array literal into a spill range of any size. Here we ask Excel to expand `{1,2,3}` into a 5‑row × 1‑column range starting at `A1`.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Why this matters*: Using `EXPAND` avoids manual loops in C#. The engine calculates the spill range and stores the values directly in the worksheet, which later appear in the PDF.

## Step 3: Save workbook as PDF while preserving font variation selectors

When you need to **save workbook as PDF**, you can also enable advanced typographic features such as font variation selectors (available from Aspose.Cells v25.8). This ensures that PDFs render complex scripts correctly.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Why this matters*: Setting `FontVariationSelectors` to `true` is essential for languages that rely on glyph variation (e.g., Chinese, Japanese, emoji). The PDF produced mirrors the on‑screen Excel view.

## Step 4: Insert a Smart Marker template that references a nested data source

Smart Markers let you embed placeholders directly in the worksheet. The template below will generate a list of orders and their items.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Why this matters*: By placing the template in `A1`, you tell Aspose.Cells where to start expanding the data. The `:` syntax (`Items:ItemName`) tells the processor to iterate over a nested collection.

## Step 5: Define the nested data source (orders containing items)

We create an anonymous array of orders, each containing its own collection of item objects. This mirrors a typical master‑detail scenario.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Why this matters*: The nested structure demonstrates **how to create dynamic array in Excel** through Smart Markers, without writing any VBA or manual cell loops.

## Step 6: Process the Smart Markers and save the final Excel file

Now we hand the workbook and the data source to `SmartMarkerProcessor`. After processing, the placeholders are replaced with actual rows, and we save the result as a regular `.xlsx` file.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Why this matters*: `SmartMarkerProcessor` automatically expands the template, creates the necessary rows, and fills them with data. The final workbook can be opened in Excel to verify that each order and its items appear correctly.

## Expected output

* **VarSelector.pdf** – a PDF file that shows the numbers 1‑3 spilling down five rows, rendered with any OpenType font variations you enabled.
* **NestedSmartMarker.xlsx** – an Excel file with the following rows (starting at `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

The PDF version retains the same numeric spill because the worksheet state was saved before Smart Marker processing; you can repeat the PDF save after processing if you need the final data in PDF as well.

## Pro tips and common pitfalls

| Tip | Explanation |
|-----|-------------|
| **Reuse the same `PdfSaveOptions`** | Creating the options object once and reusing it avoids subtle differences in rendering (e.g., missing variation selectors). |
| **Call `ws.Calculate()` after setting formulas** | Without an explicit calculation, the spill range may stay empty when you inspect the workbook programmatically. |
| **Place Smart Marker templates on a clean sheet** | Mixing templates with existing data can cause unexpected row insertion. Use a dedicated sheet if possible. |
| **Mind the file paths** | Use `Path.Combine(Environment.CurrentDirectory, "output.pdf")` to avoid hard‑coded directories on different machines. |
| **Version check** | `FontVariationSelectors` is only available from version 25.8; older versions will ignore the property without throwing. |

## Next steps

Now that you know how to **create Excel workbook**, **spill dynamic array**, and **save workbook as PDF**, you can explore:

* Adding charts or images before the PDF conversion.
* Exporting the same workbook to other formats (e.g., HTML, CSV) using `Save` overloads.
* Using **Smart Marker expressions** (`${Orders.Total:SUM(Items.Price)}`) to calculate aggregates on the fly.
* Integrating this code into an ASP.NET Core API so users can download the generated PDF directly from a web endpoint.

---

**Summary** – This tutorial showed you how to **create Excel workbook**, use the **EXPAND function** to **spill dynamic array**, embed a **Smart Marker** that works with a nested data source, and finally **save workbook as PDF** while preserving advanced font features. The complete, runnable example can be copied into any C# project and adapted to your own data structures. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}