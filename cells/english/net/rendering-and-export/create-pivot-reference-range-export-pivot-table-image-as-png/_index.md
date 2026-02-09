---
category: general
date: 2026-02-09
description: Create pivot reference range in C# and export pivot table image. Learn
  how to save Excel range as png using Aspose.Cells – quick, complete guide.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: en
og_description: Create pivot reference range in C# and export the pivot table image
  to PNG. Complete step‑by‑step guide for saving an Excel range as png.
og_title: Create Pivot Reference Range – Export Pivot Table Image as PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Create Pivot Reference Range – Export Pivot Table Image as PNG
url: /net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Pivot Reference Range – Export Pivot Table Image as PNG

Need to **create pivot reference range** in an Excel workbook using C#? You can also **export pivot table image** and **save Excel range as png** with just a few lines of code. In my experience, turning a live pivot into a static image is a handy way to embed analytics into reports, emails, or dashboards without pulling the whole workbook along.

In this tutorial we’ll walk through everything you need to know: the required libraries, the exact code, why each call matters, and a few gotchas you might run into. By the end you’ll be able to generate a PNG file of any pivot table with confidence, and you’ll understand how to adapt the pattern for multiple worksheets or custom image formats.

## Prerequisites

Before we dive in, make sure you have:

- **Aspose.Cells for .NET** (the free trial works fine for testing).  
- **.NET 6.0** or later – the API we use is fully compatible with .NET Standard 2.0+, so older frameworks will also compile.  
- A basic C# project (Console App, WinForms, or ASP.NET – anything that can reference a NuGet package).  

If you haven’t installed Aspose.Cells yet, run:

```bash
dotnet add package Aspose.Cells
```

That’s it – no COM interop, no Excel installed on the server.

## Step 1: Open the Workbook and Access the First Worksheet

The first thing you do is load the workbook file and grab the worksheet that holds the pivot table. We deliberately pick the **first worksheet** (`Worksheets[0]`) because most demo files place the pivot there, but you can replace the index with a name if you prefer.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Why this matters:* `Worksheet` is the entry point for any range‑based operation. If you point at the wrong sheet, the subsequent `PivotTables[0]` call will throw an `IndexOutOfRangeException`.

## Step 2: Create Pivot Reference Range

Now we ask the pivot table itself to give us a **reference range**. This range represents the exact cells that make up the pivot – headers, data rows, and totals. The method `CreateReferenceRange()` does the heavy lifting internally, handling merged cells and hidden rows for you.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** If your workbook contains multiple pivots, iterate `worksheet.PivotTables` and pick the one you need by its `Name` property.

## Step 3: Render the Reference Range as an Image

Aspose.Cells can render any `Range` to an image. The returned object implements both raster (PNG, JPEG) and vector (SVG) formats. Here we ask for the default raster image, which is a `System.Drawing.Image`‑compatible object.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*What’s happening under the hood?* The API snapshots the visual layout of the range, respecting cell styles, fonts, and conditional formatting. It’s essentially the same as taking a screenshot, but programmatically and without a UI.

## Step 4: Save the Generated Image to a File

Finally, we persist the image. The `Save` method automatically chooses PNG when you give it a “.png” extension. You can also pass a `SaveOptions` object if you need DPI control or a different format.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

After this line runs, open `pivot.png` and you’ll see a pixel‑perfect snapshot of the pivot table, ready to be embedded anywhere.

## Full Working Example

Putting it all together, here’s a self‑contained console program you can copy‑paste and run:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Expected output:** a file named `pivot.png` located in `YOUR_DIRECTORY`. Open it with any image viewer – you should see the exact layout of the original pivot, including column headings, data rows, and grand totals.

## Export Pivot Table Image – Customizing Size and DPI

Sometimes the default image is too small for a presentation slide. You can control the resolution by passing a `ImageOrVectorSaveOptions` object:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Why adjust DPI?* Higher DPI yields sharper edges, especially when the PNG is scaled up in PowerPoint or a PDF.

## Save Excel Range as PNG – Handling Multiple Worksheets

If you need to export pivots from several sheets, loop through `Workbook.Worksheets` and repeat the steps. Here’s a concise snippet:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

This pattern **export pivot table image** for every pivot across the workbook, and each file is named after its sheet and pivot – perfect for batch processing.

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | Worksheet has no pivot tables. | Check `worksheet.PivotTables.Count` before accessing. |
| Blank image output | Pivot is filtered to hide all rows. | Ensure the pivot has visible data, or call `pivot.RefreshData();` before creating the range. |
| Low‑resolution PNG | Default DPI is 96. | Use `ImageOrVectorSaveOptions.Resolution` as shown above. |
| File‑path errors | Invalid characters in `YOUR_DIRECTORY`. | Use `Path.Combine` and `Path.GetInvalidPathChars()` to sanitize. |

## Verification – Quick Test

After running the full example:

1. Open `pivot.png` in Windows Photo Viewer.  
2. Verify that column headers, data rows, and total rows match the Excel view.  
3. If you notice missing rows, double‑check that the pivot’s **RefreshData** method was called before `CreateReferenceRange()`.

## Bonus: Embedding the PNG into a Word Document

Because the image is already a PNG, you can feed it straight into Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Now you have a Word report that contains the exact snapshot of your pivot – no manual copy‑paste required.

## Conclusion

You’ve just learned how to **create pivot reference range**, **export pivot table image**, and **save Excel range as png** using Aspose.Cells in C#. The key takeaways are:

- Use `PivotTable.CreateReferenceRange()` to isolate the visual area of a pivot.  
- Convert that range to an image with `Range.ToImage()`.  
- Persist the image as PNG, optionally tweaking DPI for print quality.  

From here you can explore batch exporting, different image formats (SVG, JPEG), or even embedding the PNG into PDFs or Word docs. The sky’s the limit once you have the pivot captured as a static graphic.

Got questions or a tricky scenario? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}