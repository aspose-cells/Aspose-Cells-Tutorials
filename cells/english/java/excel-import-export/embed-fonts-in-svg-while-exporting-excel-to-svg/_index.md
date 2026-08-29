---
category: general
date: 2026-08-14
description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells. Learn
  how to set print area, set print options, and use WRAPCOLS function.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: en
lastmod: 2026-08-14
og_description: Embed fonts in SVG while exporting Excel to SVG with Aspose.Cells.
  This guide shows you how to set print area, configure print options, and apply the
  WRAPCOLS function.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Embed fonts in SVG while exporting Excel to SVG – step‑by‑step
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Embed fonts in SVG while exporting Excel to SVG
url: /java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Embed fonts in SVG while exporting Excel to SVG

If you need to **embed fonts in SVG while exporting Excel to SVG**, this tutorial shows you exactly how to do it with Aspose.Cells for Java. We'll also cover how to **set print area**, **set print options**, and **use WRAPCOLS function** to format data without losing layout.

You’ll walk through a complete, runnable example that loads an existing workbook, applies the `WRAPCOLS` formula, configures SVG‑specific image options, defines the print region, and finally saves the file as an SVG with embedded fonts. No external documentation is required—just copy the code, run it, and inspect the resulting SVG.

## Embed fonts in SVG – configuring ImageOrPrintOptions

Embedding fonts ensures that the SVG renders exactly as it appears in Excel, even on machines that don’t have the original typefaces installed.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Why this matters*: When `setEmbedFonts(true)` is enabled, Aspose.Cells writes the font data directly into the `<defs>` section of the SVG. The result is a self‑contained file that looks identical across browsers and platforms.

## Export Excel to SVG – full workflow

The following steps illustrate the end‑to‑end process, from loading the workbook to saving the SVG file.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Expected output**: `output.svg` appears in `YOUR_DIRECTORY`. Opening it in a browser shows the worksheet with all fonts embedded, the data wrapped into three columns (thanks to `WRAPCOLS`), and only the cells inside `A1:H30` rendered.

## Set print area for the worksheet

Defining a print area limits the exported SVG to a specific range, which reduces file size and focuses the viewer on the relevant data.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tip*: The range follows Excel’s A1 notation. If you need a dynamic range, you can compute it programmatically with `ws.getCells().getMaxDisplayRange()`.

## Set print options for SVG output

Print options control how Aspose.Cells translates the worksheet into an image. In addition to embedding fonts, you can adjust resolution, scaling, and page layout.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Why you should set print options*: Without explicit options, Aspose.Cells uses defaults that may omit font embedding or apply an unwanted scaling factor, leading to blurry or incorrectly styled SVGs.

## Use WRAPCOLS function to wrap column data

`WRAPCOLS` is an Excel formula that distributes a vertical range into a specified number of columns. It’s handy when you want to display a long list in a compact grid.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

When the workbook is saved, Aspose.Cells evaluates the formula, producing a three‑column layout inside the defined print area. This technique works for any size range—just adjust the second argument to the desired column count.

## Complete runnable example

Below is the full Java program that you can paste into any IDE. Make sure you have the Aspose.Cells for Java library on your classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Verification steps**

1. Run the program.  
2. Open `output.svg` in a web browser.  
3. Confirm that the text uses the same typeface as the original Excel file (fonts are embedded).  
4. Verify that only the cells within `A1:H30` appear and that the data from `A2:A10` is displayed in three columns.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Fonts are missing in the SVG | `setEmbedFonts(false)` or the font file is not accessible | Ensure `setEmbedFonts(true)` and that the font is installed on the machine running the code |
| WRAPCOLS does not evaluate | Calculation engine disabled | Call `workbook.calculateFormula()` before exporting, or let Aspose.Cells evaluate during save |
| Exported SVG is blank | Print area does not include any data | Double‑check the range passed to `setPrintArea` |
| SVG file is huge | No scaling applied, large image resolution | Adjust `imgOptions.setResolution(96)` or similar to control DPI |

## Pro tip: reuse ImageOrPrintOptions for multiple worksheets

If your workbook contains several sheets that need identical SVG settings, create a single `ImageOrPrintOptions` instance and assign it to each worksheet’s `PageSetup`. This reduces memory consumption and guarantees consistent font embedding across all exported files.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Next steps

* **Export to other vector formats** – Change `ImageFormat.SVG` to `ImageFormat.PDF` for high‑quality PDFs.  
* **Batch processing** – Loop through a folder of `.xlsx` files and generate SVGs automatically.  
* **Custom font handling** – Use `FontSettings` to load fonts from a specific directory when the system fonts are insufficient.  

By mastering **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options**, and **use WRAPCOLS function**, you can automate high‑fidelity SVG generation for reports, dashboards, and web visualizations directly from Excel data. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}