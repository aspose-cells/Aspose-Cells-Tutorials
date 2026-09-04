---
category: general
date: 2026-02-09
description: Create PowerPoint from Excel in minutes – learn how to convert Excel
  to PowerPoint and export Excel to PPT with a simple C# code example.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: en
og_description: Create PowerPoint from Excel quickly. This guide shows how to convert
  Excel to PowerPoint, export Excel to PPT, and generate PPT from Excel using C#.
og_title: Create PowerPoint from Excel – Complete Programming Guide
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: Create PowerPoint from Excel – Step‑by‑Step Guide
url: /net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PowerPoint from Excel – Complete Programming Guide

Ever needed to **create PowerPoint from Excel** but weren’t sure which API to call? You’re not alone. Many developers hit a wall when they want to turn spreadsheets into slide decks without manual copy‑pasting.  

Good news: with a few lines of C# you can **convert Excel to PowerPoint**, export the sheet’s shapes, and end up with a ready‑to‑present PPTX file. In this tutorial we’ll walk through the entire process, explain why each step matters, and show you how to handle the most common pitfalls.

## What You’ll Learn

- How to load an Excel workbook that contains charts, images, or SmartArt.
- The exact call that **export Excel to PPT** using the Aspose.Cells library.
- How to save the generated presentation and verify the result.
- Tips for handling workbooks without shapes, adjusting slide size, and troubleshooting version mismatches.

No external tools, no COM interop, just pure .NET code that runs anywhere .NET Core or .NET 5+ is supported.

---

## Prerequisites

Before we dive in, make sure you have:

1. **Aspose.Cells for .NET** (the library that provides `SaveToPresentation`). You can grab it from NuGet:  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. A recent .NET SDK (6.0 or later is recommended).  
3. An Excel file (`shapes.xlsx`) that contains at least one shape, chart, or image you want to appear on a slide.

That’s it—no Office installation, no licensing headaches for the purpose of this demo (the free evaluation works fine).

---

## Step 1: Load the Excel Workbook (Create PowerPoint from Excel)

The first thing we need is a `Workbook` object that points at the source file. This object represents the entire Excel document, including all worksheets, charts, and embedded objects.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Pro tip:** If you’re unsure whether the file exists, wrap the constructor in a `try/catch` and provide a helpful error message. It saves you from a cryptic `FileNotFoundException` later on.

---

## Step 2: Convert the Workbook to a PowerPoint Presentation (Export Excel to PPT)

Aspose.Cells ships with a built‑in exporter that turns the whole workbook—or just selected sheets—into a PowerPoint presentation. The `SaveToPresentation` method does the heavy lifting.

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

If you only need **generate ppt from excel** for a subset of sheets, you can use the overload that accepts a `SheetOptions` collection. For most scenarios the default conversion is sufficient.

---

## Step 3: Save the Generated Presentation (How to Convert Excel to PPTX)

Now that we have a `Presentation` instance, persisting it to disk is straightforward. The output will be a standard `.pptx` file that any modern version of PowerPoint can open.

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **What if the workbook has no shapes?**  
> The exporter will still create slides, but they’ll be empty. You can check `workbook.Worksheets[i].Shapes.Count` before conversion and decide whether to skip that sheet.

---

## Optional: Fine‑Tuning the Output (Advanced Export Excel to PPT)

Sometimes the default slide size (standard 4:3) isn’t ideal for widescreen presentations. You can adjust the slide dimensions before saving:

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

These tweaks demonstrate **how to convert Excel to PowerPoint** with a professional look, not just a raw dump of data.

---

## Full Working Example (All Steps Combined)

Below is the complete, ready‑to‑run program. Copy‑paste it into a console app, adjust the file paths, and hit **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Expected outcome:** Open `shapes.pptx` in PowerPoint. You’ll see one slide per worksheet, each preserving the original charts, images, and other shapes. The optional title slide appears at the very beginning, giving the deck a polished introduction.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if I need only a single sheet?* | Use `Workbook.Worksheets[0]` and call `SaveToPresentation` on that sheet via `SheetOptions`. |
| *Can I preserve Excel formulas?* | No—formulas are rendered as static values in the slide. If you need live data, consider linking the PPTX to the Excel file later. |
| *Does this work on Linux/macOS?* | Yes. Aspose.Cells is platform‑agnostic; just install the .NET runtime and you’re good. |
| *What about password‑protected workbooks?* | Load with `LoadOptions` that include the password before calling `SaveToPresentation`. |
| *Why am I getting blank slides?* | Check that the workbook actually contains shapes (`Shapes.Count > 0`). Blank slides are created for empty sheets. |

---

## Conclusion

You now have a clear, end‑to‑end solution for **create PowerPoint from Excel** using C#. By loading the workbook, invoking `SaveToPresentation`, and saving the result, you can **convert Excel to PowerPoint**, **export Excel to PPT**, and **generate PPT from Excel** with just a handful of lines.  

From here you might explore:

- Adding animations to the generated slides with Aspose.Slides.  
- Automating the whole pipeline (e.g., read files from a folder, batch‑convert them).  
- Integrating the code into an ASP.NET Core API so users can upload an Excel file and receive a PPTX instantly.

Give it a spin, tweak the slide size, throw in a custom title—there’s plenty of room to make the output truly yours. Got questions or run into a hiccup? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}