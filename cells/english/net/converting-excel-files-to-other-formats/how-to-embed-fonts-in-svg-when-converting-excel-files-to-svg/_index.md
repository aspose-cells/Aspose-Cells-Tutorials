---
category: general
date: 2026-09-15
description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
  covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: en
lastmod: 2026-09-15
og_description: Embed fonts in SVG and export Excel chart to PowerPoint with step‑by‑step
  C# code. Convert XLSX to SVG and XLSX to PPTX quickly and reliably.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Embed fonts in SVG and export Excel chart to PowerPoint – complete guide
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
url: /net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to embed fonts in SVG when converting Excel files to SVG and PowerPoint  

If you need to **embed fonts in SVG** while converting an Excel workbook, this guide shows you exactly how to do it. You’ll also learn how to **export Excel chart to PowerPoint**, and how to **convert XLSX to SVG** and **convert XLSX to PPTX** with editable charts.  

Working with Excel data programmatically often means you have to move the same visual content between different file formats. Manually recreating a chart in PowerPoint or re‑applying fonts in an SVG is error‑prone and time‑consuming. By the end of this tutorial you will have a single, reusable C# snippet that:

* Saves a workbook as an SVG file with embedded fonts and font‑variation selectors.  
* Exports the same workbook to a PPTX file where the chart remains editable.  

The only prerequisite is a recent version of **Aspose.Cells for .NET** (2024‑x or later) and a .NET development environment such as Visual Studio 2022.

---

## What you will need  

* .NET 6.0 or later (the code also works on .NET Framework 4.8).  
* Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`).  
* An Excel file (`input.xlsx`) that contains at least one chart.  
* Write permission to the output directory.  

---

## Embed fonts in SVG while converting XLSX to SVG  

Embedding fonts ensures that the SVG renders correctly on any device, even if the target system lacks the original typefaces. The `SvgSaveOptions` class provides two flags that make this possible: `EmbedFonts` and `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Why this works:**  
* `EmbedFonts = true` copies the font files into the SVG’s `<defs>` section, eliminating external dependencies.  
* `FontVariationSelectors = true` adds the necessary selectors for fonts that support OpenType features, preserving glyph variations such as ligatures.  

**Expected result:** Open `WithFonts.svg` in any modern browser; the text inside the chart or cells appears with the exact typeface used in Excel, even on machines that don’t have that font installed.

---

## Export Excel chart to PowerPoint with editable charts  

When you need to embed a chart into a PowerPoint slide but still allow the recipient to edit the chart data, Aspose.Cells’ `PptxSaveOptions` offers the `ExportEditableChart` flag.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Why this matters:**  
Setting `ExportEditableChart` to `true` stores the chart as an Office Open XML chart object rather than a static image. When you open `EditableChart.pptx` in PowerPoint, you can right‑click the chart → **Edit Data** and modify the series just like a native PowerPoint chart.

**Verification steps:**  

1. Open `EditableChart.pptx` in PowerPoint.  
2. Locate the slide containing the chart.  
3. Choose **Chart Tools → Design → Edit Data**.  
4. Confirm that the Excel‑style data grid appears and that you can change values.

---

## Convert XLSX to SVG – full workflow recap  

Below is a compact version that combines loading, optional data manipulation, and saving as SVG. Use this when you only need the SVG output.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Call the method like so:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Edge case tip:** If your workbook contains custom fonts that are not installed on the server, embed them manually before calling `Save`. Use `FontInfoCollection` to add the font files to the `SvgSaveOptions` via `CustomFonts` property (available in newer Aspose.Cells releases).

---

## Convert XLSX to PPTX – preserving chart editability  

The following helper method demonstrates the **convert XLSX to PPTX** path while ensuring the chart remains editable.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Usage:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Common question:** *What if my workbook has multiple worksheets with charts?*  
**Answer:** Aspose.Cells exports the first worksheet by default. To include additional sheets, iterate over `workbook.Worksheets`, copy each chart to a new slide, and save each slide individually using `Presentation` objects from Aspose.Slides. This advanced scenario is beyond the basic “save workbook as SVG” and “export Excel chart to PowerPoint” flow, but the core flags remain the same.

---

## Practical tips and pitfalls  

* **Performance:** Embedding fonts increases the SVG file size. If size is a concern, set `EmbedFonts = false` and rely on web‑safe fonts.  
* **Font licensing:** Ensure you have the right to embed the fonts you use; some commercial fonts restrict embedding.  
* **Chart compatibility:** Editable charts are saved as `chart.xml` parts inside the PPTX. Very complex charts (e.g., 3‑D or combo charts) may lose some styling when edited in PowerPoint. Test the most common chart types you need.  
* **Version mismatches:** The `ExportEditableChart` flag requires Aspose.Cells 20.10 or later. Using an older version will silently fallback to a raster image.  
* **Thread safety:** Workbook objects are not thread‑safe. Create a new `Workbook` instance per request in a web service scenario.  

---

## Full end‑to‑end example  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Running this program produces two files:

* **WithFonts.svg** – an SVG that renders exactly like the Excel view, fonts included.  
* **EditableChart.pptx** – a PowerPoint presentation where the chart can be edited directly.

---

## Conclusion  

You now know how to **embed fonts in SVG** when you **convert XLSX to SVG**, and how to **export Excel chart to PowerPoint** while keeping the chart editable. The same code also demonstrates a clean way to **save workbook as SVG** and **convert XLSX to PPTX** with minimal effort.  

From here you can explore further topics such as:

* Adding custom fonts programmatically (`svgOptions.CustomFonts`).  
* Batch‑processing multiple workbooks in a background service.  
* Using Aspose.Slides to create multi‑slide PPTX files that combine several Excel charts.  

Experiment with the options, adapt the snippets to your project, and enjoy reliable Excel‑to‑SVG/PPTX conversions without manual post‑processing. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}