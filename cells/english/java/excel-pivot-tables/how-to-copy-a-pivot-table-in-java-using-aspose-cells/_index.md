---
category: general
date: 2026-09-27
description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
  shows how to copy range and preserve pivot definitions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot table
- copy range aspose cells
language: en
lastmod: 2026-09-27
og_description: Copy pivot table in Java using Aspose.Cells. Follow this complete
  tutorial to copy range aspose cells and keep pivot definitions intact.
og_image_alt: Screenshot of copy pivot table operation in Aspose.Cells Java
og_title: Copy a pivot table in Java – Aspose.Cells quick guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Copy pivot table in Java with Aspose.Cells – a step‑by‑step guide that
    shows how to copy range and preserve pivot definitions.
  headline: How to copy a pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to copy a pivot table in Java using Aspose.Cells
url: /java/excel-pivot-tables/how-to-copy-a-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy a pivot table in Java using Aspose.Cells

If you need to **copy pivot table** from one workbook to another, this guide shows you exactly how to do it with Aspose.Cells for Java. The solution works for any pivot you have built, and it preserves the pivot definition without manual recreation.

You’ll learn how to load the source file, define the range that holds the pivot, copy that range to a new workbook, and finally save the result. The tutorial also covers common pitfalls, such as preserving data sources and handling large workbooks.

## What you’ll need

Before you start, make sure you have:

* Java 17 or later (the code compiles with JDK 8+ as well)
* Aspose.Cells for Java 23.9 or newer – the latest version offers the most reliable **copy range aspose cells** support
* A source Excel file that contains a pivot table (e.g., `SourceWithPivot.xlsx`)
* An IDE or build tool (Maven/Gradle) that can reference the Aspose.Cells JAR

## Step 1: Load the source workbook that contains the pivot table

The first action is to open the workbook that holds the pivot you want to duplicate. Loading the file creates an in‑memory representation of all worksheets, cells, and pivot caches.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Access the first worksheet (adjust the index if needed)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Why this matters:**  
Aspose.Cells reads the entire workbook, including hidden pivot cache sheets. If you skip this step, the subsequent **copy pivot table** operation would lose the underlying data source.

## Step 2: Create an empty destination workbook

Next, instantiate a new workbook that will receive the copied pivot. Starting with a clean workbook avoids accidental overwrites.

```java
        // Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Tip:** The default workbook contains one empty sheet, which is perfect for a simple copy. If you need to copy into a specific sheet name, rename `destWs` with `destWs.setName("TargetSheet")`.

## Step 3: Define the source range that includes the pivot table

A pivot table occupies a rectangular block of cells. You must specify the exact range; otherwise only raw data will be copied. In this example we assume the pivot occupies **A1:G20**, but you can adjust the address to match your file.

```java
        // Define the range that includes the pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Why this works:**  
When you call `createRange` on the worksheet’s `Cells` collection, Aspose.Cells includes the pivot definition, its cache, and any formatting. This is the core of **how to copy pivot table** correctly.

## Step 4: Copy the defined range to the destination sheet

Now use the `copy` method to duplicate the range. The method copies everything inside the range, including the pivot definition, formulas, and styles.

```java
        // Copy the range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));
```

**Important note:**  
If you only need the data without the pivot, you could use `srcRange.copyData`. However, for a true **copy pivot table** you must copy the whole range as shown above.

## Step 5: Save the destination workbook

Finally, write the new workbook to disk. The resulting file will contain a fully functional pivot table identical to the source.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Running the program produces `CopyPivotResult.xlsx` with the same pivot layout, filters, and calculations as the original file.

## Expected output

When you open `CopyPivotResult.xlsx` in Excel:

* The pivot table appears at **A1:G20** on the first sheet.
* All row/column fields, filters, and value fields are intact.
* Refreshing the pivot updates the same data source as the source workbook (if the source data is embedded).

## Edge cases and practical tips

| Situation | How to handle it |
|-----------|------------------|
| **Pivot spans more columns than anticipated** | Use `srcWs.getPivotTables().get(0).getPivotTableArea()` to get the exact address programmatically. |
| **Source workbook contains multiple pivots** | Loop through `srcWs.getPivotTables()` and copy each range individually, adjusting destination addresses. |
| **Large workbooks cause memory pressure** | Enable `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before loading the source. |
| **You need to copy only the pivot definition, not the data** | After copying, delete the source data rows in the destination with `destWs.getCells().deleteRows(startRow, count)`. |
| **Destination file must keep original formatting** | Set `CopyOptions` with `options.setPasteType(PasteType.ALL)` for a full fidelity copy. |

**Pro tip:** Always verify the copied pivot by calling `destWs.getPivotTables().get(0).refresh()` programmatically. This ensures the cache is up‑to‑date, especially when the source data resides in an external connection.

## Complete runnable example

Below is the entire program you can copy‑paste into your IDE. Replace `YOUR_DIRECTORY` with the actual path on your machine.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Create an empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 3: Define the range that includes the pivot table in the source sheet
        // Adjust the address if your pivot occupies a different area
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 4: Copy the defined range (pivot table definition is included) to the destination sheet
        srcRange.copy(destWs.getCells().createRange("A1"));

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

Running this code will **copy pivot table** exactly as described, and it demonstrates the most straightforward way to **copy range aspose cells** while preserving pivot functionality.

## Conclusion

You now know how to **copy pivot table** in Java using Aspose.Cells, from loading the source workbook to saving the destination file. The guide covered the essential steps, explained why each step matters, and addressed common edge cases.  

Next, you might explore:

* **how to copy pivot table** across different worksheets within the same workbook
* Using **copy range aspose cells** to duplicate charts or conditional formatting
* Automating pivot refresh after copying to keep data current

Feel free to experiment with larger ranges, multiple pivots, or integrating this logic into a larger Excel‑processing pipeline. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}