---
category: general
date: 2026-08-04
description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
  range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: en
lastmod: 2026-08-04
og_description: Copy pivot table using Aspose.Cells for Java. This tutorial walks
  you through copying an Excel range, duplicating a pivot table, and preserving all
  data in a new worksheet.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Copy pivot table in Java – full Aspose.Cells tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
url: /java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table in Java – step‑by‑step guide using Aspose.Cells

If you need to **copy a pivot table** from one worksheet to another in Java, this guide shows you exactly how to do it with Aspose.Cells. Whether you’re generating reports programmatically or building a data‑migration tool, you’ll see a complete, runnable example that preserves the pivot table’s definition and data.

Copying a pivot table is more than just copying a cell range; the underlying cache and data source must stay intact. In this tutorial we also cover how to **copy excel range**, how to **duplicate pivot table** across worksheets, and how to **copy worksheet with pivot** using the same API.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit (JDK) 8 or newer.
* Maven or Gradle to manage dependencies.
* Aspose.Cells for Java (the latest version, e.g., 23.12). Add the following Maven coordinate to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* A source workbook (`Source.xlsx`) that contains a pivot table on the first worksheet.

## How to copy pivot table in Java with Aspose.Cells

The core idea is to copy the *source range* that encloses the pivot table and then paste it into a new worksheet. Aspose.Cells automatically copies the pivot cache, so the resulting sheet contains a fully functional **duplicate pivot table**.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Why this works

* **Range copy includes the pivot cache** – Aspose.Cells treats a pivot table as a special object embedded in the cell range. When you call `Range.copy`, the library copies both the visible cells and the hidden cache that powers the pivot.
* **No manual recreation needed** – You don’t have to rebuild the pivot fields or data source; the duplicate is ready to refresh instantly.
* **Works with any Excel version** – The generated file follows the Office Open XML (XLSX) standard, so Excel 2007+ can open it without warnings.

## Copy excel range – reusing the same code for non‑pivot data

If you only need to **copy excel range** without a pivot table, the same pattern applies. Just adjust the range address to the region you want to duplicate.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

The method `copy` preserves formulas, formatting, and comments, making it a universal solution for any block of Excel data.

## Duplicate pivot table across multiple worksheets

Sometimes you need to **duplicate pivot table** several times—e.g., one per department. Loop over the destination worksheets and reuse the same `sourceRange.copy` call:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Each new sheet contains an independent pivot that can be refreshed separately. The cache is duplicated, so changes in one sheet won’t affect the others.

## Copy worksheet with pivot – preserving sheet‑level settings

If you want to **copy worksheet with pivot** while also keeping page setup, column widths, and named ranges, use `Worksheet.copy` instead of copying a range manually. This method clones the entire sheet, including the pivot table.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy` is handy when the worksheet contains charts, images, or custom styles that must travel together with the pivot.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot cache lost after copy** | Using `Cell.copy` on individual cells (instead of a range) discards the hidden cache. | Always copy the *entire* range that encloses the pivot table, as shown in Step 2. |
| **Source range too small** | The range doesn’t include the pivot’s data area, so the new sheet shows only static values. | Expand the address (e.g., `A1:G20`) to cover the full pivot table plus any slicers or filters. |
| **Destination workbook version mismatch** | Saving as XLS (legacy) drops modern pivot features. | Save as XLSX (default) or explicitly set `SaveFormat.XLSX`. |
| **External data source broken** | Pivot points to a data source outside the workbook; copying doesn’t embed it. | Use `PivotTable.refreshData()` after copy, or embed the source data in the same workbook. |

## Expected output

After running the program:

1. `CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.
2. Opening the file in Excel shows a new sheet named **CopySheet**.
3. **CopySheet** contains a fully functional pivot table identical to the original, ready to refresh.
4. All formatting, filters, and calculated fields are preserved.

If you open `FullCopy.xlsx`, you’ll see a complete replica of the original worksheet, including any charts or images that were on the source sheet.

## Recap

* You learned how to **copy pivot table** in Java using Aspose.Cells.
* The same approach works for a plain **copy excel range** or **copy range java** scenarios.
* For bulk operations, you can **duplicate pivot table** across many sheets.
* When you need the whole sheet, **copy worksheet with pivot** using `addCopy`.

## Next steps

* Explore **PivotTable.refreshData()** to programmatically update the cache after copying.
* Combine the copy logic with **Excel file streaming** to handle large workbooks without loading everything into memory.
* Check out Aspose.Cells’ support for **pivot slicers** if your reports rely on interactive filters.

Feel free to adapt the code to your own project structure, experiment with different range sizes, or integrate it into a larger data‑processing pipeline. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}