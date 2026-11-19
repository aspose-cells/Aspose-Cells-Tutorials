---
category: general
date: 2026-11-19
description: Learn how to copy pivot table in Java while preserving its data and layout.
  This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: en
lastmod: 2026-11-19
og_description: Copy pivot table in Java with Aspose.Cells. Follow this guide to learn
  how to preserve pivot tables and copy excel pivot data accurately.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Copy pivot table in Java – complete Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: How to copy pivot table in Java with Aspose.Cells
url: /java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot table in Java with Aspose.Cells

If you need to **copy pivot table** from one workbook to another, this guide shows you exactly how to do it in Java. Whether you’re building a reporting engine or migrating data, you’ll see a reliable way to preserve the pivot’s cache, fields, and formatting.

Copying a pivot table can be tricky because a simple range copy often loses the underlying data source. In this tutorial we’ll use Aspose.Cells to **how to copy pivot** while keeping every calculation intact, and we’ll also cover **how to preserve pivot** tables when the destination workbook is empty.

## Prerequisites

Before you start, make sure you have:

* Java 17 or newer installed.
* Aspose.Cells for Java (version 23.9 or later) added to your project’s classpath.
* Two Excel files: a source workbook that contains the pivot table and an empty destination workbook (or a workbook you want to merge into).

You don’t need any special licensing for the code sample, but a valid Aspose.Cells license removes evaluation watermarks.

## Step 1: Load the source workbook that contains the pivot table

The first step is to open the workbook that holds the original pivot. Loading the file gives you access to the worksheet, cells, and the pivot cache.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Why this matters*: Aspose.Cells reads the entire workbook, including hidden cache data that powers the pivot. Without loading the full file, the copy operation would lose the pivot’s definition.

## Step 2: Prepare the destination workbook

Create a fresh workbook (or open an existing one) and grab its first worksheet. This is where the pivot will be placed.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*Tip*: If you already have a target workbook, replace the `new Workbook()` call with `new Workbook("target.xlsx")`. This lets you **copy excel pivot** into a pre‑populated workbook.

## Step 3: Define the cell area that encloses the pivot table

You must specify the exact range that covers the pivot. The range includes the pivot’s table, field list, and any surrounding data you want to keep.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Why this matters*: The `CellArea` tells Aspose.Cells what to copy. If the area is too small, the pivot will be truncated; if it’s too large, you’ll copy unnecessary data. Adjust the coordinates based on your actual pivot size.

## Step 4: Perform the copy operation with CopyOptions

Use the `copy` method on the source worksheet’s cells collection. Passing a new `CopyOptions()` object ensures that all formatting, formulas, and pivot cache are transferred.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Why `CopyOptions` preserves the pivot

`CopyOptions` tells Aspose.Cells to treat the range as a *whole* object rather than a flat set of values. This is the key to **how to preserve pivot** tables: the underlying pivot cache is duplicated, so the destination workbook can recalculate the pivot without manual intervention.

## Step 5: Save the destination workbook

Finally, write the destination file to disk. The saved file will contain a fully functional copy of the original pivot.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Expected result*: Opening `copied_with_pivot.xlsx` in Excel shows the identical pivot table, complete with slicers, filters, and calculated fields. You can refresh it, and the data source will point to the copied range inside the same workbook.

---

![Diagram showing copy pivot table process](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Diagram illustrating the copy pivot table workflow from source to destination workbook"}

## How to copy pivot tables across multiple worksheets

If you need to **copy excel pivot** tables from several sheets, repeat Steps 3‑4 for each source worksheet. You can also loop through `srcWb.getWorksheets()` and copy each pivot into a corresponding sheet in `destWb`. Here’s a concise loop example:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro tip*: Use `srcWs.getPivotTables().getCount()` to detect whether a sheet actually contains a pivot before copying. This avoids copying irrelevant data.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot loses its cache** | Using `Worksheet.copy()` without `CopyOptions` copies only cell values. | Always use `srcWs.getCells().copy(..., new CopyOptions())`. |
| **Destination shows #REF! errors** | The copied pivot still references the original workbook’s external data source. | After copying, call `destWs.getPivotTables().get(0).refresh();` to rebind the cache to the new range. |
| **Slicers disappear** | Slicers are stored outside the main cell area. | Expand `CellArea` to include slicer ranges, or copy the entire worksheet (`srcWs.copy(destWs, new CopyOptions())`). |
| **Performance slowdown on large pivots** | Copying huge ranges with formatting can be slow. | Use `CopyOptions.setOnlyData(true)` if you don’t need formatting, then reapply styles manually. |

## How to preserve pivot table formatting while updating data

Sometimes you need to **how to preserve pivot** layout after the source data changes. After copying, you can lock the pivot’s style:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

Setting `PreserveFormatting` ensures that any custom styles you applied in the source survive the copy.

## Verifying the copy

A quick way to confirm the copy succeeded is to compare the pivot definitions:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

If the counts match and the destination opens without errors, you’ve successfully **copy pivot table**.

## Conclusion

You now know how to **copy pivot table** from one Excel workbook to another using Aspose.Cells for Java, and you’ve seen the exact steps to **how to copy pivot** while ensuring the pivot’s cache, formatting, and slicers stay intact. The same pattern works for **copy excel pivot** scenarios across multiple sheets, and you can adapt the code to meet edge cases like preserving pivot formatting or handling large data sets.

### Next steps

* Explore **preserve pivot table** options such as `setPreserveFormatting` and `refresh` for dynamic data sources.  
* Try copying pivot tables between workbooks with different column orders—adjust the `CellArea` accordingly.  
* Combine this technique with Aspose.Slides to embed pivot snapshots into PowerPoint presentations.

Happy coding, and feel free to experiment with variations to fit your specific automation pipeline!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [How to copy a pivot table between worksheets in Java](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [How to copy pivot table to a new workbook in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}