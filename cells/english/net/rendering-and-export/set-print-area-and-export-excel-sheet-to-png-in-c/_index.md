---
category: general
date: 2026-10-26
description: Set print area and export an Excel sheet to PNG in C#. Learn image export
  options, how to export PNG, and get a printable image from a workbook.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: en
lastmod: 2026-10-26
og_description: Set print area and export an Excel sheet to PNG in C#. This step‑by‑step
  tutorial covers image export options and how to export PNG from a workbook.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Set print area and export Excel sheet to PNG – C# guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Set print area and export Excel sheet to PNG in C#
url: /net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set print area and export Excel sheet to PNG in C#

If you need to **set print area** before exporting an Excel sheet to PNG, this guide shows you how. You’ll see a complete C# example that configures image export options, adjusts the worksheet’s print area, and saves the result as an image.

Exporting an Excel sheet to PNG is a common requirement when you want to embed a worksheet snapshot in a report, email, or web page. The code below works with any workbook that contains a pivot table, but the technique applies to regular data ranges as well. No external tools are required—just the Aspose.Cells for .NET library.

## Prerequisites

- .NET 6.0 or later (the sample targets .NET 6, but any recent .NET version works)
- Aspose.Cells for .NET (install via NuGet: `Install-Package Aspose.Cells`)
- Basic familiarity with C# and Excel concepts such as worksheets and print areas

## Step 1: Configure image export options

The first thing you do is create an `ImageOrPrintOptions` instance. This object tells Aspose.Cells how to render the sheet as an image.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Why this matters:** `ImageOrPrintOptions` controls the output format, resolution, and other rendering details. Using PNG ensures lossless quality, which is ideal for reports that require crisp text and graphics.

## Step 2: Load the workbook and access the target worksheet

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Why this matters:** You must work with a specific `Worksheet` object because the print area is a worksheet‑level setting.

## Step 3: Identify the range you want to print

In many scenarios the data you care about lives inside a pivot table. The following code extracts the data range of the first pivot table on the sheet.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

If your worksheet does not contain a pivot table, you can replace `pivotDataRange` with any `CellArea` you create manually, e.g.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Step 4: **Set print area** to match the selected range

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Why this matters:** The print area tells Excel (and Aspose.Cells) which cells to include when rendering the sheet to an image. By aligning the print area with the pivot data range, you avoid blank margins and ensure the exported PNG contains only the relevant data.

## Step 5: Export the worksheet to a PNG image

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Why this matters:** `worksheet.ToImage` respects the previously set print area, so the PNG file contains exactly the cells you defined. Assigning the image to a picture shape allows you to embed it back into the workbook if needed, while saving it to disk gives you a standalone file.

## Full working example

Putting all steps together yields a self‑contained program you can run immediately.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Expected output

Running the program creates `C:\Temp\WorksheetExport.png`. Opening the file shows a crisp PNG image that contains only the cells defined by the **set print area** (the pivot table data in this example). The image can be inserted into Word documents, PowerPoint slides, or web pages without additional conversion steps.

## Handling multiple worksheets or pivot tables

- **Multiple worksheets:** Loop through `wb.Worksheets` and repeat steps 3‑5 for each sheet you need to export.
- **Multiple pivot tables:** Choose the appropriate `PivotTables[index]` or iterate over `worksheet.PivotTables` to export each table individually.
- **No pivot table:** Create a `CellArea` manually (see the comment in Step 3) and assign it to `PrintArea`.

## Practical tips (E‑E‑A‑T)

- **Pro tip:** Set `HorizontalResolution` and `VerticalResolution` to 300 DPI for print‑ready PNGs; lower values reduce file size for web use.
- **Watch out for empty picture shapes:** If the worksheet has no picture shapes, add one before assigning the image:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance:** Reusing a single `ImageOrPrintOptions` instance for multiple worksheets avoids unnecessary allocations.
- **Compatibility:** Aspose.Cells 23.9+ fully supports .NET 6 and later; earlier versions may require adjustments to the API names.

## Conclusion

You now know how to **set print area** and export an Excel


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}