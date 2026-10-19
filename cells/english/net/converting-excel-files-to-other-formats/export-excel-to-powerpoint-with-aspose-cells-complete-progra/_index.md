---
category: general
date: 2026-08-14
description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
  Excel formulas in code. Step‑by‑step C# example with full source.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: en
lastmod: 2026-08-14
og_description: Export Excel to PowerPoint with Aspose.Cells and calculate Excel formulas
  in code. Follow this complete guide to generate editable PPTX files from workbooks.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Export Excel to PowerPoint with Aspose.Cells – full C# tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
url: /net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel to PowerPoint with Aspose.Cells – complete programming guide

If you need to **export Excel to PowerPoint** programmatically, this guide shows you exactly how to do it with Aspose.Cells for .NET. You’ll also learn how to **calculate Excel formulas in code**, copy pivot tables without losing definitions, and use the new Office‑365 EXPAND function for dynamic arrays.

In the following sections we’ll walk through a real‑world C# example, explain why each line matters, and cover common pitfalls so you can adapt the solution to your own projects.

## What this tutorial covers

* Loading an existing workbook (`input.xlsx`)  
* Copying a range that contains a pivot table while preserving its definition  
* Exporting the workbook to a PowerPoint (`.pptx`) file with editable textboxes and shapes  
* Exporting a cell range as strings using custom logic  
* Calculating Excel formulas in code, including the Office‑365 EXPAND function  
* Saving the final workbook with all changes applied  

**Prerequisites**  
* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+)  
* Aspose.Cells for .NET v25.11 or newer (the `CopyPivotTable` option was introduced in v25.11)  
* A basic understanding of C# and Excel concepts such as ranges, pivot tables, and formulas  

> **Pro tip:** Install Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) to keep your project up‑to‑date with the latest features.

## Export Excel to PowerPoint with Aspose.Cells

The first major task is converting the workbook into a PowerPoint presentation while keeping all visual elements editable. This is essential when you want to generate slide decks from financial reports or dashboards automatically.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Why this works

* **`Workbook`** loads the entire Excel file into memory, giving you full API access.  
* **`CopyRange`** with `CopyPivotTable = true` ensures the pivot table’s data source, cache, and layout are duplicated exactly—something older versions of Aspose.Cells could not do.  
* Adding a new worksheet (`Copy`) lets you keep the original sheet untouched, which is useful for audit trails.

## Export the workbook to PowerPoint with editable objects

Now we turn the workbook into a PowerPoint file. By enabling `ExportEditableObjects`, every chart, shape, or textbox becomes a native PowerPoint object that users can edit directly after the export.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Explanation

* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook for export, handling Smart Markers, named ranges, and layout adjustments.  
* Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel drawings into PowerPoint shapes rather than flattening them into images. This yields a **fully editable** slide deck.

> **Edge case:** If your workbook contains complex charts built from external data connections, make sure those connections are resolved before calling `ExportToPptx`, otherwise the chart may appear blank.

## Export a range as strings using custom logic

Sometimes you need raw string values for downstream processing (e.g., feeding a CSV parser). The `ExportTableOptions` class lets you control how each cell is converted.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Why you might use this

* **Uniform data type:** Exporting as strings avoids type‑mismatch errors when the consumer expects text.  
* **Custom formatting:** Replace `value.ToString()` with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).  

## Calculate Excel formulas in code

A frequent requirement is to **calculate Excel formulas in code** without opening Excel. Aspose.Cells provides a built‑in calculation engine that works offline and supports the latest Office‑365 functions, including `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### How the calculation engine works

* The `Formula` property stores the expression exactly as you would type it in Excel.  
* `CalculateFormula()` triggers a full workbook recalculation, respecting dependencies between cells.  
* The `EXPAND` function (available in Excel 365) returns a spill range based on the source cell (`B1`) and the specified rows (`5`) and columns (`3`).  

> **Tip:** If you need to calculate only a subset of the workbook, use `Worksheet.CalculateFormula()` to limit the scope and improve performance.

## Save the workbook with all changes applied

Finally, write the modified workbook back to disk. You can save in any of the supported formats (`.xlsx`, `.xls`, `.csv`, etc.) by changing the file extension.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### What to verify

* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND` formula result, and any custom‑exported strings.  
* Open `output.pptx` in PowerPoint; you should see a slide that mirrors the Excel layout, and all charts/textboxes should be editable.

## Common questions and troubleshooting

| Question | Answer |
|----------|--------|
| **Do I need a license to use Aspose.Cells?** | Yes. A trial works for evaluation, but a full license removes evaluation watermarks and unlocks the `CopyPivotTable` feature. |
| **What if the exported PPTX shows blank shapes?** | Verify that the workbook’s drawing objects are not hidden (`Visible = true`) and that any external image links are embedded before export. |
| **Can I export multiple worksheets to separate PPTX slides?** | Use `WorkbookDesigner.ExportToPptx` in a loop, specifying a different `ExportOptions` for each worksheet, or combine them into a single presentation by adding slides manually via Aspose.Slides. |
| **Is `CalculateFormula` thread‑safe?** | No. Perform calculations on a single thread or clone the workbook per thread to avoid race conditions. |

## Conclusion

You now have a **complete, end‑to‑end solution for export Excel to PowerPoint** using Aspose.Cells, and you understand how to **calculate Excel formulas in code**—including the modern `EXPAND` function. The tutorial covered loading a workbook, copying pivot tables, exporting to editable PowerPoint, custom string export, formula calculation, and final saving.

From here you can:

* Extend the export to include multiple slides per worksheet (secondary keyword: *calculate Excel formulas in code* can be reused when generating chart data).  
* Integrate Aspose.Slides to add animations or master slide layouts.  
* Replace the simple `CustomExport` delegate with locale‑aware formatting for international projects.  

Feel free to experiment with different ranges, explore other Office‑365 functions (e.g., `FILTER`, `SORT`), and combine this workflow with automated email delivery for fully hands‑off reporting pipelines.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Automate Excel Data Export Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}