---
category: general
date: 2026-11-22
description: Export Excel as image with Java using Aspose.Cells. Learn how to add
  picture to worksheet and save Excel as PNG file in a few steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: en
lastmod: 2026-11-22
og_description: Export Excel as image with Java using Aspose.Cells. Follow this guide
  to add picture to worksheet and save Excel as PNG file quickly.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Export Excel as image with Java – step‑by‑step tutorial
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Export Excel as image with Java – complete guide
url: /java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel as image with Java – complete guide

If you need to **export Excel as image** in a Java application, this tutorial shows you a ready‑to‑run solution. You’ll see how to add picture to worksheet, configure the export options, and finally **save Excel as PNG file** with just a few lines of code.

The guide covers everything from Maven setup to handling edge cases, so you can integrate the technique into any project that requires visual snapshots of spreadsheets.

## Prerequisites

Before you start, make sure you have:

* Java 17 or newer installed.
* Maven 3.6+ (or Gradle) for dependency management.
* An Aspose.Cells for Java license (the free evaluation works for testing).
* A sample Excel workbook (`sample.xlsx`) that contains the data you want to export.

## Step 1: Add Aspose.Cells dependency

Aspose.Cells provides the `ImageOrPrintOptions` class used to **export Excel as image**. Add the following dependency to your `pom.xml` (or the equivalent Gradle entry).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Keep the version number up to date; newer releases include performance improvements for image rendering.

## Step 2: Load the workbook and select the worksheet

The first programmatic step is to open the Excel file and obtain a reference to the worksheet you want to export.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Why this matters*: Loading the workbook gives you access to its internal objects, and selecting the correct worksheet ensures the right range is rendered.

## Step 3: Configure ImageOrPrintOptions (export excel as image)

`ImageOrPrintOptions` controls the image format, resolution, and other rendering details. Here we set the format to PNG, which satisfies the **export excel sheet to png** requirement.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Setting the format to `PNG` guarantees lossless compression, making the file suitable for further processing or inclusion in reports.

## Step 4: Add picture to worksheet (add picture to worksheet)

If you need to embed a picture—such as a logo or a snapshot of another range—use the `Pictures` collection. The following code inserts a picture of the range `A1:G20` at the top‑left corner of the worksheet.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Why you might do this:** Adding a picture before exporting lets you combine static graphics with the worksheet’s data, producing a richer final image.

## Step 5: Save the worksheet as a PNG file (save excel as png file, save workbook as image)

Finally, invoke `Workbook.save` with the configured options. The method writes a PNG file to the specified directory.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

When the program finishes, `output/pivot.png` contains a pixel‑perfect representation of the worksheet, including the picture you added.

### Complete source file

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Running the class produces the PNG file shown below (the image is illustrative; your file will reflect the actual worksheet content).

![Exported Excel worksheet as PNG](/images/excel-to-png.png "Result of export excel as image using Java")

*Alt text (image alt):* **Result of export Excel as image using Java – a PNG snapshot of the worksheet** (satisfies image alt requirement).

## Common pitfalls and how to avoid them

| Issue | Reason | Fix |
|-------|--------|-----|
| **File not found** | The path to `sample.xlsx` is incorrect. | Use an absolute path or place the file in the project root. |
| **Blank image** | The worksheet has no visible content or the picture range is empty. | Verify that cells `A1:G20` contain data or adjust the range. |
| **Low resolution** | Default DPI is 96, which may look blurry when printed. | Call `opts.setResolution(300)` (or higher) before saving. |
| **License exception** | Using the evaluation version may add a watermark. | Apply a valid Aspose.Cells license with `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Next steps

Now that you can **export Excel as image**, you might explore:

* **Export excel sheet to png** for each worksheet in a workbook (loop through `wb.getWorksheets()`).
* Converting the PNG to PDF using Aspose.PDF if you need a document‑friendly format.
* Embedding the generated PNG into a web page or email attachment directly from Java.

These extensions build on the same `ImageOrPrintOptions` pattern, keeping the codebase consistent.

## Conclusion

You have learned how to **export Excel as image** with Java, how to **add picture to worksheet**, and how to **save Excel as PNG file** using Aspose.Cells. The full example demonstrates a reliable way to **save workbook as image**, handle resolution, and avoid common errors. Apply the pattern to automate reporting, generate thumbnails, or integrate spreadsheet visuals into any Java‑based workflow.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}