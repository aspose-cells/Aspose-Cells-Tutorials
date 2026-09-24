---
category: general
date: 2026-03-30
description: Create PowerPoint from Excel quickly using Aspose.Cells and Aspose.Slides.
  Learn how to export worksheet as image and save presentation as PPTX in C#.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: en
og_description: Create PowerPoint from Excel in C# with Aspose. Export worksheet as
  image, keep shapes editable, and save the result as PPTX.
og_title: Create PowerPoint from Excel – Complete C# Tutorial
tags:
- Aspose
- C#
- Office Automation
title: Create PowerPoint from Excel – Step‑by‑Step C# Guide
url: /net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PowerPoint from Excel – Complete C# Tutorial

Ever needed to **create PowerPoint from Excel** but weren’t sure which library could keep your charts editable? You’re not alone. In many reporting scenarios you’ll want to turn a spreadsheet into a slide deck without losing the ability to tweak text boxes later. This guide shows you exactly how to **convert Excel to PowerPoint** using Aspose.Cells and Aspose.Slides, while also covering how to **export worksheet as image** and finally **save presentation as PPTX**.

We’ll walk through every line of code, explain *why* each setting matters, and even discuss what to do if your workbook contains complex charts that you’d rather export as a picture. By the end you’ll have a ready‑to‑run C# console app that takes `ShapesDemo.xlsx` and spits out `Result.pptx` – all with editable text boxes and crisp images.

## What You’ll Need

- .NET 6.0 or later (the API works with .NET Framework too, but .NET 6 is the sweet spot).  
- **Aspose.Cells** and **Aspose.Slides** NuGet packages (free trial licenses work for testing).  
- A basic familiarity with C# syntax – if you can write a `Console.WriteLine`, you’re good to go.  

No additional COM interop, no Office installed on the server, and no manual copy‑paste of images. Everything is handled programmatically.

---

## Create PowerPoint from Excel – Load Workbook and Set Export Options

The first thing we do is open the Excel file and tell Aspose.Cells how we want the sheet rendered. The `ImageOrPrintOptions` object is where the magic happens: we enable `ExportShapes` and `ExportEditableTextBoxes` so that any shapes (including charts) become part of the slide **and** stay editable after the conversion.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Why these flags?**  
- `OnePagePerSheet` prevents the sheet from being split across multiple slides – you get a single, full‑size picture.  
- `ExportShapes` tells Aspose.Cells to rasterize charts *and* vector shapes, preserving their look.  
- `ExportEditableTextBoxes` is the secret sauce that lets you double‑click a textbox in PowerPoint and edit the text without opening Excel again.

> **Pro tip:** If you only need a static picture of a chart, set `ExportShapes = false` and use the `ExportExcelChartAsPicture` method later (see the final section).

---

## Convert Excel to PowerPoint – Generate Image from Worksheet

With the options ready, we now turn the worksheet into a `System.Drawing.Image`. The `WorksheetToImageConverter` does the heavy lifting, applying the settings we just defined.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

The `0` argument indicates the first page (we only have one because of `OnePagePerSheet`). The resulting `sheetImage` retains the original DPI, so your slide won’t look pixelated even on high‑resolution displays.

---

## Save Presentation as PPTX – Insert Image into a Slide

Now we create a fresh PowerPoint file, add a slide, and drop the bitmap onto it. Aspose.Slides treats the picture as a *picture frame* shape, which you can later resize or move just like any native PowerPoint object.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **What if the image is larger than the slide size?**  
> PowerPoint will automatically clip anything that exceeds the slide dimensions. A quick fix is to scale the image before inserting it:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

You can then pass `newWidth` and `newHeight` to `AddPictureFrame`.

---

## Export Worksheet as Image – Save the PPTX File

Finally we persist the presentation to disk. The `SaveFormat.Pptx` flag guarantees the modern OpenXML format, which works across all recent versions of PowerPoint.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

When you open `Result.pptx` you’ll see a single slide that looks exactly like your Excel sheet, but you can still click on any textbox and edit its content directly in PowerPoint.

---

## Export Excel Chart as Picture – When Raster Images Are Preferred

Sometimes you don’t need editable shapes; a high‑quality PNG of a chart is enough. Aspose.Cells can export a specific chart to an image without converting the whole sheet:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

You can then embed `chart.png` into a slide the same way we added `sheetImage`. This approach reduces the PPTX file size and is useful when the surrounding data isn’t needed on the slide.

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Text looks blurry** | Exported at low DPI (default 96). | Set `imageOptions.Dpi = 300;` before conversion. |
| **Shapes disappear** | `ExportShapes` left `false`. | Ensure `ExportShapes = true` when you need editable graphics. |
| **Slide size mismatch** | Image larger than slide dimensions. | Scale the image (see code snippet) or change slide size via `presentation.SlideSize`. |
| **License exception** | Using trial version without proper activation. | Call `License license = new License(); license.SetLicense("Aspose.Total.lic");` early in `Main`. |

---

## Full Working Example (Copy‑Paste Ready)

Below is the entire program, ready to drop into a new console project. Replace `YOUR_DIRECTORY` with the folder that holds your Excel file.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Expected output:**  
Running the program prints `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`. Opening the PPTX shows a single slide mirroring the original Excel sheet, with editable text boxes.

---

## Recap & Next Steps

You now know how to **create PowerPoint from Excel** using Aspose’s powerful APIs, how to **export worksheet as image**, and how to **save presentation as PPTX** while preserving editability. The same pattern works for multi‑sheet workbooks—just loop through `workbook.Worksheets` and add a new slide for each.

**What to explore next?**  

- **Batch conversion:** Loop over a folder of Excel files and generate a slide deck per file.  
- **Dynamic layouts:** Use `slide.LayoutSlide` to apply pre‑designed PowerPoint templates.  
- **Chart‑only export:** Combine the “Export Excel chart as picture” snippet with slide placeholders for a leaner deck.  
- **Advanced styling:** Apply custom slide backgrounds, transitions, or animation via Aspose.Slides.

Feel free to experiment—change the DPI, swap `ShapeType.Ellipse` for a circular picture frame, or even embed multiple images per slide. The sky’s the limit when you have programmatic control over

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}