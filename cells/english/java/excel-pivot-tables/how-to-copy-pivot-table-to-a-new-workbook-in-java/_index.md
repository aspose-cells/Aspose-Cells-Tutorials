---
category: general
date: 2026-10-26
description: Learn how to copy pivot table to a new workbook using Java, preserving
  formatting and the pivot definition while you copy excel range with formatting via
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: en
lastmod: 2026-10-26
og_description: Copy pivot table to a new workbook in Java with Aspose.Cells. This
  guide shows how to copy excel range, preserve formatting, and create empty workbook
  efficiently.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Copy pivot table to a new workbook in Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to copy pivot table to a new workbook in Java
url: /java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot table to a new workbook in Java

If you need to **copy pivot table** from one Excel file to another, this guide shows you a complete, runnable solution. You’ll see how to preserve the pivot definition, keep all formatting, and avoid common pitfalls when copying an Excel range.

Copying a pivot table often raises questions like *how to copy pivot* without breaking the data source or losing styles. By the end of this tutorial you will have a self‑contained Java program that creates an empty workbook, copies the desired range, and saves the result with the pivot intact.

## What you’ll achieve

* Load a source workbook that contains a pivot table.  
* **Create empty workbook** that will receive the copied data.  
* **Copy excel range** that includes the pivot, using options that keep the pivot and formatting.  
* Save the destination file and verify that the pivot works exactly like the original.

### Prerequisites

* Java 17 or later.  
* Aspose.Cells for Java (version 23.10 or newer).  
* Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).  

> **Pro tip:** Use the free Aspose.Cells evaluation license for quick testing; replace it with a full license before production use.

## Copy pivot table to a new workbook

The first step is to set up the source and destination workbooks. The destination starts as a **create empty workbook** call, which gives you a clean file with a single worksheet.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Why this works

* `new Workbook()` **creates empty workbook** with a default sheet, avoiding the need to delete existing data.  
* `CopyOptions` tells Aspose.Cells to copy **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries cell styles, number formats, and conditional formatting—fulfilling the **copy range with formatting** requirement.  
* `copyRange` performs a **copy excel range** operation that respects the source’s internal structures, so the pivot remains functional after the copy.

## How to copy pivot without losing formatting

If you only use the default `CopyOptions`, some style information may be omitted on older Aspose.Cells versions. Explicitly setting the paste type guarantees that **copy range with formatting** is respected.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Adding `setPasteSpecialType` ensures that column widths, row heights, and even data validation rules travel with the range. This is especially useful when the pivot table spans multiple columns with custom widths.

## Create empty workbook before copying

Sometimes developers attempt to copy into an existing workbook that already contains data. That can cause overlapping ranges or unexpected overwrites. Starting with a **create empty workbook** call isolates the operation:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

If you need more than one sheet in the destination, you can add them after the copy:

```java
destWb.getWorksheets().add("Summary");
```

## Copy excel range with formatting using CopyOptions

Beyond pivot tables, the same pattern works for any **copy excel range** that requires formatting preservation—charts, tables, or conditional formats.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

The `CopyOptions` instance remains the same, so you get consistent behavior across different ranges.

### Edge cases to consider

| Situation                              | Recommended handling |
|----------------------------------------|----------------------|
| Source workbook has multiple pivots   | Copy each pivot’s range separately or copy the whole sheet. |
| Destination already contains data      | Choose a non‑conflicting start cell (e.g., "H1") when calling `copyRange`. |
| Pivot data source is external (e.g., DB) | Ensure the destination workbook points to the same external data source, or refresh the pivot after copy. |
| Large workbook ( > 10 MB )             | Increase Java heap size (`-Xmx2g`) to avoid `OutOfMemoryError`. |

## Verify the result

After running the program, open `destination.xlsx`. You should see:

* The same pivot table layout as in `source.xlsx`.  
* All cell colors, number formats, and column widths preserved.  
* The pivot’s data source still points to the original data range inside the new file, so refreshing the pivot updates the values correctly.

If the pivot appears as a static table, double‑check that `CopyOptions.setPasteType(PasteType.PASTE_ALL)` is set. Without this option Aspose.Cells treats the pivot as plain data.

## Conclusion

You now know how to **copy pivot table** to a new workbook in Java while preserving formatting, data connections, and sheet layout. The complete solution demonstrates loading a source file, **create empty workbook**, configuring **copy excel range** options, and saving the result.  

From here you can explore related topics such as **how to copy pivot** across different worksheets, embed charts alongside pivots, or automate batch processing of multiple workbooks. Experiment with the `CopyOptions` settings to fit your specific automation needs, and you’ll have a robust Excel manipulation toolkit at your fingertips.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}