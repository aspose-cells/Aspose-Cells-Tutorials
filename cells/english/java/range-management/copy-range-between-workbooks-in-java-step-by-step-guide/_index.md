---
category: general
date: 2026-08-14
description: Copy range between workbooks with Java using Aspose.Cells. Learn to copy
  pivot table workbook, export picture to PowerPoint and remove AutoFilter from Excel
  table.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: en
lastmod: 2026-08-14
og_description: Copy range between workbooks in Java. This guide shows how to copy
  pivot table workbook, export picture to PowerPoint and remove AutoFilter from Excel
  table.
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Copy range between workbooks in Java – complete Aspose.Cells tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Copy range between workbooks in Java – step‑by‑step guide
url: /java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy range between workbooks in Java – step‑by‑step guide

If you need to **copy range between workbooks** in Java, Aspose.Cells provides a clean API that handles complex objects such as pivot tables and pictures. This tutorial shows how to **copy pivot table workbook**, **export picture to PowerPoint**, and **remove AutoFilter from Excel table** while keeping the code easy to read and maintain.

You will learn how to:

* Load a source workbook and define the source range.  
* Create a destination workbook and copy the range so that the pivot table stays intact.  
* Export the first picture on the sheet as an editable PowerPoint object.  
* Remove an AutoFilter from the first Excel table.  
* Load a workbook with `SmartMarkerOptions` to treat JSON arrays as a single cell value.

The example uses Aspose.Cells 23.10 for Java, but the concepts apply to earlier versions as well.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 or newer | Required by the latest Aspose.Cells runtime. |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | Provides the `Workbook`, `Worksheet`, `Range`, and related classes used in the code. |
| A source Excel file (`src.xlsx`) that contains a pivot table, a picture, and a table with an AutoFilter. | The tutorial manipulates these objects to demonstrate each feature. |

Add the Maven dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copy range between workbooks – load source and destination

The first step is to open the source workbook, pick the range that contains the data you want to copy, and create an empty destination workbook.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Why this matters:** By using `Range.copy`, Aspose.Cells copies not only raw cell values but also the underlying pivot cache, keeping the pivot table functional in the destination workbook.

---

## Copy pivot table workbook while copying the range

Now copy the defined range from the source workbook to the destination workbook. The pivot table is preserved automatically because the range includes the pivot cache.

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Result:** Opening `destination.xlsx` shows the same pivot table layout as `src.xlsx`. No additional code is required to rebuild the pivot cache.

---

## Export picture to PowerPoint

Aspose.Cells can mark a picture for export to an editable PowerPoint object. The following code selects the first picture on the destination sheet and sets the export flag.

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **What you see:** Opening `destination.pptx` in PowerPoint shows the picture as a native shape that you can edit, resize, or animate.

---

## Remove AutoFilter from Excel table

If the source sheet contains a table with an AutoFilter, you may want to clear it after copying. The code below accesses the first table and removes its filter.

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effect:** The table remains in the workbook, but the drop‑down filter arrows disappear, giving you a clean data view.

---

## Load workbook with SmartMarker options – treat JSON arrays as a single cell

When you generate a report from JSON, Aspose.Cells can treat an entire array as a single cell value. This is useful for embedding JSON strings into a template without expanding them into multiple cells.

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Why you might use this:** If your JSON payload contains an array that should appear as a JSON string in a single cell, `setArrayAsSingle(true)` prevents Aspose.Cells from expanding the array into separate rows or columns.

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*Image alt text:* **Copy range between workbooks in Java – Aspose.Cells code example** (matches the primary keyword).

---

## Expected output

| File name                | Contains |
|--------------------------|----------|
| `destination.xlsx`       | Copied range with functional pivot table. |
| `destination.pptx`       | Exported picture as an editable PowerPoint shape. |
| `final_output.xlsx`      | Table without AutoFilter arrows. |
| `template_filled.xlsx`   | JSON array stored as a single cell value. |

Open each file in the appropriate application (Excel or PowerPoint) to verify that the operations succeeded.

---

## Conclusion

You now know how to **copy range between workbooks** in Java using Aspose.Cells, while preserving a pivot table, exporting a picture to PowerPoint, and removing an AutoFilter from an Excel table. The same pattern can be extended to copy any Excel range to a new workbook, handle SmartMarker JSON arrays, or chain additional transformations.

Next steps you might explore:

* **Copy Excel range to new workbook** with multiple worksheets.  
* Use **export picture to PowerPoint** for batch image extraction.  
* Apply **remove autofilter from excel table** in larger reporting pipelines.  
* Combine these techniques with Aspose.Slides for full Excel‑to‑PowerPoint automation.

Feel free to experiment with different range addresses, multiple pivot tables, or custom picture formats. The Aspose.Cells API is designed for programmatic flexibility, so you can adapt the patterns shown here to fit any enterprise Excel automation scenario.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}