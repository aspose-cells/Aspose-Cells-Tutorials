---
category: general
date: 2026-07-06
description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  to duplicate Excel pivot tables programmatically.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: en
lastmod: 2026-07-06
og_description: How to copy pivot table in Java using Aspose.Cells lets you duplicate
  Excel pivot tables quickly and reliably.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: How to copy pivot table in Java – Complete Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: How to copy pivot table in Java using Aspose.Cells
url: /java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot table in Java using Aspose.Cells

Ever wondered **how to copy pivot** tables inside an Excel file without opening the workbook manually? You're not the only one. In many reporting pipelines you need to **duplicate Excel pivot** tables on the fly—maybe to create a snapshot, to move it to a new sheet, or to generate a template for downstream users.

In this tutorial we’ll walk through a complete, runnable example that shows exactly that. Using the Aspose.Cells for Java library we’ll load a workbook, locate the source pivot range, copy it to a new location, and save the result. No vague references, just a concrete solution you can drop into your project today.

---

## Prerequisites

Before we dive in, make sure you have:

* **Java Development Kit (JDK) 8+** – the code compiles with any recent JDK.
* **Aspose.Cells for Java** version 25.11 or newer – the `Range.copy` method that supports pivot tables was introduced in this release.
* An **input.xlsx** file that already contains a pivot table (you can create one in Excel for testing).
* A build tool of your choice (Maven, Gradle, or plain `javac`). We'll show the Maven dependency for quick start.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Step 1: Load the source workbook

The first thing we do is open the Excel file that holds the original pivot table. Aspose.Cells treats the workbook as an in‑memory object, so you can manipulate it without launching Excel.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Why this matters:** Loading the workbook gives us access to worksheets, cells, and, crucially, the pivot cache that backs the pivot table. Without this step the library has nothing to copy.

---

## Step 2: Get the worksheet containing the pivot

If your workbook has multiple sheets, you need to point to the right one. Here we simply grab the first sheet, but you can also use `get("SheetName")` for a named lookup.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** When dealing with many sheets, cache the index or name in a config file to avoid hard‑coding numbers.

---

## Step 3: Define the source range that includes the pivot table

Starting with version 25.11 Aspose.Cells lets you treat a pivot table as a regular cell range. Specify the top‑left and bottom‑right cells that enclose the entire pivot.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Edge case:** If your pivot expands dynamically (e.g., rows are added later), consider using `worksheet.getPivotTables().get(0).getDataRange()` to fetch the exact range programmatically.

---

## Step 4: Define the destination range where the pivot will be copied

Pick any empty cell where you want the duplicated pivot to appear. In this demo we start at **F1**, leaving a gap between the original and the copy.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Why not a new sheet?** You can also create a fresh worksheet (`workbook.getWorksheets().add("Copy")`) and use its cells as the destination. The same `copy` method works across sheets.

---

## Step 5: Copy the pivot table to the new location

Now the magic happens. The `copy` method clones the pivot, its cache, formatting, and even any associated slicers (as of the latest version).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Important:** The copy operation is *deep*; it does **not** create a reference back to the original pivot. You can modify the new pivot independently without affecting the source.

---

## Step 6: Save the workbook with the duplicated pivot

Finally, write the modified workbook back to disk. You can overwrite the original or create a new file; here we choose the latter to keep the source untouched.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

When you open **output.xlsx** in Excel, you’ll see the original pivot in columns A‑D and a perfect copy beginning at column F. Both pivots can be refreshed separately.

---

## Full Working Example

Putting everything together, here’s the complete Java class you can compile and run directly:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected result:** Opening `output.xlsx` shows the original pivot (A1:D20) and an identical pivot beginning at F1. Both tables retain their filters, styles, and calculated fields.

---

## Handling Common Variations

| Situation | What to adjust |
|-----------|----------------|
| **Multiple pivots** on the same sheet | Loop through `worksheet.getPivotTables()` and copy each with its own destination range. |
| **Dynamic data range** | Use `worksheet.getPivotTables().get(0).getDataRange()` to auto‑detect the source area. |
| **Copy to another workbook** | Load a second `Workbook` instance, create a destination worksheet, then call `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`. |
| **Preserve slicers** | As of 25.12, slicers are copied automatically when the range includes them. Verify in Excel after saving. |

---

## Pro Tips & Pitfalls

* **Version check:** The `copy` method that supports pivots was added in **Aspose.Cells 25.11**. If you’re on an older version you’ll get an exception. Always verify `aspose-cells` version in your `pom.xml`.
* **Performance:** Copying large pivots can be memory‑intensive. If you only need the data, consider exporting the pivot to a flat table instead of cloning the whole object.
* **Refresh behavior:** The duplicated pivot retains its own cache. If you modify the underlying data, call `pivotTable.refresh()` on the new pivot to recalculate.
* **Formatting quirks:** Some custom number formats may not survive the copy on very old Excel versions (<2007). Test with your target audience’s Excel version.

---

## Conclusion

You now have a solid, end‑to‑end answer to **how to copy pivot** tables using Aspose.Cells for Java, and you’ve seen how to **duplicate Excel pivot** tables in a few lines of code. The approach works for single or multiple pivots, across worksheets, and even between workbooks.

Next steps could include:

* Automating the copy for every pivot in a batch job.
* Adding code to rename the duplicated pivot (e.g., `pivotTable.setName("Copy_of_Sales")`).
* Integrating the routine into a larger reporting service that generates PDFs or CSV exports.

Give it a try, tweak the ranges to match your real data, and let the library handle the heavy lifting. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}