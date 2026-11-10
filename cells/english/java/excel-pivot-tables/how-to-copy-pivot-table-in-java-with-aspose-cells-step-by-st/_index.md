---
category: general
date: 2026-10-20
description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
  shows how to copy range to new sheet and duplicate pivot table sheet safely.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: en
lastmod: 2026-10-20
og_description: How to copy pivot table with Aspose.Cells in Java. Follow this guide
  to copy range to new sheet and duplicate pivot table sheet without losing data.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: How to copy pivot table in Java – complete Aspose.Cells tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
url: /java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide

If you need to **how to copy pivot table** in a Java application, this guide walks you through the exact steps. Whether you are building a reporting engine or automating data migration, you’ll see how to copy range to new sheet while preserving the pivot table’s definition and data.

Copying a pivot table can feel risky because the underlying cache and field settings often get lost. This tutorial demonstrates a reliable approach using Aspose.Cells, shows the complete runnable code, and explains why each line matters. By the end, you’ll be able to duplicate pivot table sheet in seconds.

## Prerequisites

Before you start, make sure you have:

* Java 8 or newer installed.
* Aspose.Cells for Java (version 23.10 or later) added to your project’s classpath.
* A source workbook (`source.xlsx`) that contains a pivot table in the range `A1:G20`.
* Basic familiarity with Java and Excel concepts.

No additional libraries are required; Aspose.Cells handles all Excel operations internally.

## How to copy pivot table – overall strategy

The core idea is simple:

1. Load the workbook that holds the original pivot table.
2. Identify the exact range that includes the pivot table.
3. Create a new worksheet that will receive the copied data.
4. Use the `Range.copy` method to transfer the range to the new sheet.  
   This method automatically copies the pivot cache, so the pivot table remains functional.
5. Save the workbook to a new file.

Because the copy operation works at the range level, the **duplicate pivot table sheet** retains all field configurations, filters, and calculated items.

## Step 1: Load the source workbook

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Why this matters*: Loading the workbook gives you access to its worksheets, cells, and the pivot cache. Aspose.Cells reads the entire file into memory, so subsequent operations are fast and thread‑safe.

## Step 2: Define the source range that contains the pivot table

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Why this matters*: The `createRange` call tells Aspose.Cells exactly which cells to copy. Including the entire pivot table area ensures that the hidden cache rows are also transferred. If you omit any part of the cache, the copied pivot table would appear empty.

## Step 3: Add a destination worksheet for the copied data

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Why this matters*: Adding a dedicated sheet isolates the copied pivot table from the original, making it easy to compare results or use the sheet as a template for further processing.

## Step 4: Copy the range to the destination worksheet (pivot table is preserved)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Why this matters*: The `copy` method not only copies cell values and formatting but also replicates the pivot cache. This is the key step that enables you to **duplicate pivot table sheet** without losing any functionality.

## Step 5: Save the workbook with the copied range

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Why this matters*: Saving creates a new Excel file (`result.xlsx`) that contains both the original and the duplicated pivot table sheet. You can now open the file in Excel to verify that the pivot table works exactly as before.

## Full, runnable example

Putting everything together, here’s the complete program you can copy‑paste into your IDE:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Expected output

* Opening `result.xlsx` shows two worksheets:
  * **Sheet1** – the original data and pivot table.
  * **CopyResult** – an exact duplicate of the pivot table, fully functional.
* All pivot fields, filters, and calculated items behave identically to the source.

If you modify the source pivot table after the copy, the duplicated sheet will **not** reflect those changes because the cache was duplicated at copy time. This isolation is often desirable when you need a snapshot of the report.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Pivot table appears blank** | The copied range omitted the hidden cache rows. | Ensure the range includes the entire cache (usually a few rows below the visible table). |
| **Destination sheet name already exists** | `add("CopyResult")` throws an exception if the name is taken. | Use `workbook.getWorksheets().addUniqueName("CopyResult")` or check `contains` before adding. |
| **File path errors** | Incorrect `YOUR_DIRECTORY` leads to `FileNotFoundException`. | Use absolute paths or Java’s `Paths.get(...).toAbsolutePath()` to resolve locations. |
| **Performance slowdown on large workbooks** | Copying massive ranges copies unnecessary cells. | Limit the range to the exact pivot area, or use `Range.copy` with `CopyOptions` to skip formatting if not needed. |

## Pro tip: Using `CopyOptions` for finer control

If you only need the pivot table data and want to skip cell formatting, you can pass a `CopyOptions` object:

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

This reduces the file size of the duplicated sheet and speeds up the copy operation, especially for large workbooks.

## How to copy range to new sheet without losing formulas

The example above already copies formulas because `Range.copy` preserves them by default. If you want values only (e.g., to freeze the current state), set `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

Now the destination sheet contains static values, but the pivot table will still function because its cache is part of the range.

## Recap of the solution

* **How to copy pivot table** – load the workbook, define the exact range, add a new worksheet, copy the range, and save.
* The process also demonstrates **copy range to new sheet** and how to **duplicate pivot table sheet** safely.
* You can fine‑tune the copy with `CopyOptions` for performance or value‑only scenarios.

## Next steps and related topics

* **Refresh pivot cache programmatically** – use `PivotTable.refreshData()` after updating source data.
* **Export pivot table to PDF** – combine this copy technique with `PdfSaveOptions` to create snapshot reports.
* **Automate multi‑sheet duplication** – loop through all worksheets and apply the same copy logic.

Experiment with these variations to adapt the pattern to your specific reporting pipeline. If you encounter edge cases, such as external data sources or VBA‑driven pivots, the same range‑copy approach works, but you may need to copy the underlying connection objects as well.

---

*Happy coding! If this tutorial helped you learn **how to copy pivot table**, feel free to share it with teammates or contribute improvements.*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}