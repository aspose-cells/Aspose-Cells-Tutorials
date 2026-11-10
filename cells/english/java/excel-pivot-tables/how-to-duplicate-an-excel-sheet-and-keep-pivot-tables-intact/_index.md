---
category: general
date: 2026-10-23
description: Learn how to duplicate an Excel sheet in Java while preserving pivot
  tables. This guide also shows how to copy pivot tables, copy Excel ranges, and copy
  a sheet with pivot data.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: en
lastmod: 2026-10-23
og_description: Duplicate an Excel sheet in Java while preserving pivot tables. Follow
  this complete tutorial to copy pivot tables, copy Excel ranges, and copy a sheet
  with pivot data.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Duplicate an Excel sheet with pivot tables in Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: How to duplicate an Excel sheet and keep pivot tables intact in Java
url: /java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to duplicate an Excel sheet and keep pivot tables intact in Java

If you need to **duplicate Excel sheet** while keeping every pivot table alive, this guide shows you exactly how. You’ll see a concise solution that copies a sheet, copies a specific range, and even copies a pivot table to another workbook—all in pure Java using Aspose.Cells.

Duplicating an Excel sheet is a common task when you generate monthly reports from a template or when you need a sandbox copy for testing. The code below works with Aspose.Cells 25.11 or later, which introduced the `setCopyPivotTable(true)` option.

## What you’ll need

Before you start, make sure you have:

- Java 17 (or any recent JDK) installed
- Aspose.Cells for Java 25.11 or newer in your project (Maven coordinate `com.aspose:aspose-cells:25.11`)
- A source workbook (`SourceWithPivot.xlsx`) that already contains a pivot table
- An IDE or build tool of your choice (IntelliJ IDEA, Eclipse, Maven, Gradle, etc.)

## Step 1: Load the source workbook that contains the pivot table

The first operation is to open the workbook that holds the pivot you want to preserve.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Why this step matters:** Loading the source workbook gives you access to the worksheet objects, cells, and the embedded pivot tables. Without this, you cannot reference the pivot data you plan to copy.

## Step 2: Create an empty destination workbook (or load an existing one)

You can either start from a blank workbook or open an existing file that will receive the duplicated sheet.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **Tip:** If you already have a reporting workbook, replace the line above with `new Workbook("ExistingReport.xlsx")` to add the duplicated sheet to it.

## Step 3: Copy the whole worksheet – the pivot table is preserved automatically

Copying the entire worksheet is the simplest way to **copy sheet with pivot**. Aspose.Cells copies the pivot definition and its cache automatically.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Why it works:** `addCopy` clones the sheet structure, cell values, styles, and any embedded pivot tables. The new worksheet in `dstWb` will look identical to the original, including the pivot cache.

## Step 4: (Optional) Copy only a specific range that includes the pivot table

Sometimes you don’t want the whole sheet—maybe you only need a portion that contains the pivot. This is where you **copy Excel range** and explicitly request the pivot to be copied.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **How it helps:** `setCopyPivotTable(true)` forces the engine to duplicate the pivot definition even when you copy a limited range. Without this flag, only the raw data would be copied, and the pivot would be lost.

## Step 5: Save the destination workbook

Finally, write the duplicated content to a new file.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Expected output

Running the program creates `DuplicatedWithPivot.xlsx` in the target directory. Open the file in Excel and you will see:

- A new worksheet named `Sheet1 (Copy)` (or the original name with “Copy” appended)
- The pivot table appears exactly as in the source sheet, fully functional
- If you used the optional range copy, only cells A1:G30 are present, but the pivot still works because its cache was copied

## Common questions and edge cases

### How to copy pivot to another workbook without copying the whole sheet?

If you only need the pivot and its underlying data, copy the range that contains both the source data and the pivot, then use `setCopyPivotTable(true)`. The same code from **Step 4** applies; just ensure the range covers the data source.

### What if the source workbook has multiple worksheets with pivots?

Repeat **Step 3** for each worksheet you want to duplicate:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Does this work with protected worksheets?

Aspose.Cells can copy protected sheets, but you must unprotect them first if you need to modify the pivot after copying:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Can I copy a pivot table to an existing workbook that already contains a sheet with the same name?

Yes. Use `addCopy` with a unique name:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro tip: verify the pivot cache

After copying, you can programmatically confirm that the pivot cache exists:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

If the cache ID prints a non‑negative number, the pivot was successfully duplicated.

## Conclusion

You now know how to **duplicate Excel sheet** in Java while preserving every pivot table, how to **copy pivot** tables directly, how to **copy Excel range** that includes a pivot, and how to **copy sheet with pivot** or **copy pivot to workbook** using Aspose.Cells 25.11+. Apply these patterns to automate report generation, create template clones, or build testing environments that need identical pivot‑driven analytics.

Ready to explore more? Try exporting the duplicated workbook to PDF, or programmatically refresh the pivot cache after copying to ensure the latest data is reflected. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}