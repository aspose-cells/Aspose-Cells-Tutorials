---
category: general
date: 2026-10-07
description: Learn how to create PNG from range and export data as PNG in Java. This
  guide shows you how to save Excel range image using Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: en
lastmod: 2026-10-07
og_description: Create PNG from range in Java and export data as PNG with Aspose.Cells.
  Follow this complete tutorial to save Excel range image instantly.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Create PNG from range in Java – step‑by‑step Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to create PNG from range in Java with Aspose.Cells
url: /java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create PNG from range in Java with Aspose.Cells

If you need to **create PNG from range** in an Excel workbook, this tutorial shows you exactly how to do it. By the end of the guide you’ll be able to **export data as PNG**, save an Excel range image, and reuse the file in reports or web pages.

You’ll see a full, runnable Java program that loads a workbook, selects the desired cells, renders them as a PNG, and saves the result to disk. No external tools are required—Aspose.Cells handles everything internally.

## What this tutorial covers

* Prerequisites and Maven setup for Aspose.Cells
* Loading a workbook that contains a pivot table or any data range
* Defining the exact cell range you want to convert
* Configuring image options for PNG output
* Rendering the range and saving the PNG file
* Common pitfalls and tips for high‑quality images

After completing these steps you’ll be able to **convert worksheet to PNG** for any range, whether it’s a simple table or a complex pivot chart.

## Prerequisites

* Java 17 or later (the code compiles with JDK 11+)
* Maven 3.6+ (or Gradle if you prefer)
* Aspose.Cells for Java 23.12 or newer – add the dependency shown below
* An existing Excel file (`PivotWithStyle.xlsx`) that contains the range you want to capture

> **Pro tip:** If you don’t have a license, you can request a temporary evaluation key from Aspose. The library works in evaluation mode without additional configuration.

### Maven dependency

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Step 1: Load the workbook that holds the target range

The first operation is to open the Excel file. Aspose.Cells reads the file into memory without requiring Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Why this matters*: Loading the workbook gives you access to worksheets, cells, and page‑setup properties needed for rendering.

## Step 2: Access the worksheet that contains the range

Most workbooks have a default sheet at index 0, but you can also use the sheet name.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

If your data lives on a different sheet, replace `0` with the appropriate index or use `workbook.getWorksheets().get("SheetName")`.

## Step 3: Define the cell range you want to convert

You can specify any rectangular area using A1 notation. In this example we capture `A1:D15`, which might be a pivot table or a regular data block.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Edge case*: When the range includes merged cells, Aspose.Cells automatically expands the image to include the merged area.

## Step 4: Prepare PNG image options

`ImageOrPrintOptions` lets you control format, resolution, and other rendering details. Setting the save format to PNG ensures lossless quality.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Increasing the DPI is useful when the source cells contain small fonts or detailed charts.

## Step 5: Limit the render area to the selected range

By assigning the range as the print area, Aspose.Cells renders only those cells and ignores the rest of the sheet.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

If you skip this step, the entire worksheet will be rasterized, which can waste memory and produce a larger image.

## Step 6: Render the range and add the picture to the worksheet (optional)

If you want to embed the generated PNG back into the workbook (for preview purposes), you can add it as a picture. This step is optional for pure export scenarios.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Why you might do this*: Some workflows require the image to be part of the workbook before distribution, such as creating a printable report that mixes native cells and images.

## Step 7: Save the PNG file to disk

Finally, write the image to a file. The `save` method respects the format specified in `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

When the program finishes, `PivotImage.png` will contain a pixel‑perfect snapshot of cells `A1:D15`.

### Expected output

* A file named `PivotImage.png` located in `YOUR_DIRECTORY`.
* The image shows the exact layout, fonts, colors, and borders from the selected range.
* If the source range contains a pivot table, the rendered image includes the same styling and calculated values as displayed in Excel.

## Handling common scenarios

### Exporting a non‑contiguous range

Aspose.Cells does not render disjoint ranges in a single image. To export multiple areas, create separate images for each range and combine them later with an image‑processing library (e.g., ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Saving a large worksheet as PNG

Rendering an entire sheet that spans thousands of rows can consume significant memory. Mitigate this by:

* Reducing the DPI (`imageOptions.setResolution(72)`) for a smaller file.
* Using `setPageCount` to limit the number of pages rendered.
* Exporting one printable page at a time via `worksheet.getPageSetup().setPrintArea(...)`.

### Preserving cell formulas

A PNG image is a raster format; formulas are not retained. If downstream consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.

## Full, runnable example

Below is the complete Java class you can copy‑paste into your IDE. Replace `YOUR_DIRECTORY` with an absolute or relative path on your machine.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Run the program with `mvn compile exec:java` (or your preferred build tool). After execution, open `PivotImage.png` to verify the result.

## Conclusion

You now know how to **create PNG from range** in Java using Aspose.Cells, effectively **export data as PNG** and **save excel range image** for any reporting or sharing scenario. The steps—loading the workbook, defining the range, configuring image options, setting the print area, and saving the file—cover the entire workflow for **convert worksheet to PNG** and **save cells as PNG**.

### Next steps

* Experiment with different `Resolution` values to balance quality and file size.
* Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG with a transparent background.
* Combine multiple range images into a single PDF using `PdfSaveOptions` for multi‑page reports.
* Explore exporting to other raster formats (JPEG, BMP) by changing `setSaveFormat`.

Feel free to adapt this pattern to charts, tables, or even entire worksheets. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}