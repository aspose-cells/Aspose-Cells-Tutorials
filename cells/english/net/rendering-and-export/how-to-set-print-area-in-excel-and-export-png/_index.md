---
category: general
date: 2026-09-27
description: Set print area in Excel and learn how to export PNG images of selected
  cells. This guide also covers saving range as image and adding picture to worksheet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: en
lastmod: 2026-09-27
og_description: Set print area in Excel and export PNG with Aspose.Cells. Follow this
  step‑by‑step guide to save range as image and add picture to worksheet.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Set print area in Excel – export PNG in C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: How to set print area in Excel and export PNG
url: /net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to set print area in Excel and export PNG

If you need to **set print area excel** before creating an image, this guide shows you exactly how to do it. You’ll also learn **how to export png** files from a specific range, **save range as image**, and **add picture to worksheet** in a single, repeatable workflow.

Working with Excel programmatically often means you only want a subset of cells—say a pivot table or a chart—to become an image. By defining a print area first, you guarantee that the exported PNG contains exactly the cells you expect, no more and no less. This tutorial walks you through every step, from loading the workbook to saving the final PNG file, and explains why each setting matters.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* Visual Studio 2022 (or any C# IDE)  
* The **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`)  
* An Excel file (`input.xlsx`) located in a known directory  

These requirements ensure the code runs without additional configuration.

## Step 1: Load the workbook you want to work with

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

The `Workbook` class represents the entire Excel file. Loading it first gives you access to worksheets, cells, and page‑setup options.

## Step 2: **Set print area excel** for the target range

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Setting the **print area** tells Excel (and Aspose.Cells) which cells belong to the printable page. When you later export the sheet as an image, only this area is rendered, which is essential for a clean **export selected cells image**.

## Step 3: Configure image export options – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` controls the output format. By choosing `ImageFormat.Png`, you guarantee a high‑resolution, transparent‑background image that works well in web and desktop contexts.

## Step 4: Create a picture from the defined range and **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

The `Pictures.Add` method inserts a new picture into the worksheet. By passing the range created in Step 2, you **save range as image** directly onto the sheet, which is useful if you later need to reference the picture in other parts of the workbook.

## Step 5: **Save the picture as an image file** – completing the **export selected cells image** workflow

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Calling `Save` writes the picture to the file system using the options defined in Step 3. The resulting `selected_range.png` contains exactly the cells defined by the **set print area excel** command.

## Full, runnable example

Putting all the pieces together gives you a compact program you can drop into any console application:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Expected output

Running the program prints:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

And you’ll find a `selected_range.png` file that shows only the cells A1 through G20 from `input.xlsx`.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| The exported image contains the whole sheet | No print area was defined | Ensure you **set print area excel** before creating the picture |
| PNG is blurry | Default DPI is low | Set `imageOptions.DpiX` and `imageOptions.DpiY` to a higher value (e.g., 300) |
| File not found error | Wrong directory path | Use `Path.Combine` or double‑check the folder exists |
| Picture appears offset | Incorrect row/column indices | The first two parameters of `Pictures.Add` are the top‑left cell where the picture is placed; keep them at `0,0` for a clean export |

## Pro tip: Export multiple ranges in one run

If you need to **export selected cells image** for several areas, repeat Steps 2‑5 inside a loop, changing `printArea` each iteration. Remember to give each picture a unique file name, otherwise the later save will overwrite the previous file.

## Conclusion

You now know how to **set print area excel**, configure **how to export png**, **save range as image**, and **add picture to worksheet** using Aspose.Cells. This end‑to‑end solution lets you turn any cell block into a high‑quality PNG with just a few lines of C# code.

Next, you might explore:

* Adding borders or watermarks to the exported PNG (search for *add picture to worksheet* with styling)
* Exporting directly to PDF for printable reports (*export selected cells image* → PDF workflow)
* Automating the process for multiple workbooks in a batch job

Feel free to experiment with different ranges, DPI settings, or image formats to fit your project's needs. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}