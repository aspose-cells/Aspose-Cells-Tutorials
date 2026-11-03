---
category: general
date: 2026-10-16
description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
  to another sheet and copy range between worksheets efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: en
lastmod: 2026-10-16
og_description: How to copy pivot table in Java using Aspose.Cells. This tutorial
  shows you how to copy range to another sheet and copy range between worksheets with
  full code.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: How to copy a pivot table between worksheets in Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: How to copy a pivot table between worksheets in Java
url: /java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy a pivot table between worksheets in Java

If you need to **how to copy pivot table** from one sheet to another in the same workbook, this guide provides a complete, ready‑to‑run solution. You’ll see how to copy the source range that contains the pivot table, preserve its functionality, and verify the result—all using Aspose.Cells for Java.

Copying a pivot table is a common task when you generate reports programmatically, and doing it correctly avoids losing the pivot cache or breaking formulas. By the end of this tutorial you’ll be able to **copy range to another sheet** and **copy range between worksheets** without any manual steps.

## What you’ll learn

* Load an existing Excel file with a pivot table.
* Define the source range that holds the pivot table.
* Define a destination range on a different worksheet.
* Use `CopyOptions` to keep the pivot table intact.
* Verify that the copied pivot table works as expected.

**Prerequisites**

* Java 17 or later.
* Aspose.Cells for Java (version 23.12 or newer).  
* An Excel file (`input.xlsx`) that contains a pivot table on the first sheet.

---

## How to copy pivot table with Aspose.Cells

The core of the operation is a four‑step process: load the workbook, locate the source range, set the destination range, and perform the copy. Below each step is explained in detail.

### Step 1: Load the workbook

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Why this step?*  
Loading the workbook brings the entire file into memory, giving you access to worksheets, cells, and the pivot cache. Aspose.Cells reads the file format automatically, so you don’t need to worry about `.xls` vs `.xlsx`.

### Step 2: Locate the source range that contains the pivot table

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Why this step?*  
A pivot table is stored in a cell block that also references a hidden cache. By selecting the exact range (`A1:G20` in this example), you ensure the cache stays linked when the range is copied.

### Step 3: Define the destination range on another sheet

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Why this step?*  
Choosing a destination on a different worksheet lets you **copy range to another sheet**. The top‑left cell (`A1`) is a common starting point, but you can place it anywhere by changing the address.

### Step 4: Copy the source range while preserving the pivot table

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Why this step?*  
`CopyOptions` controls what gets transferred. Using `PasteType.PASTE_ALL` guarantees that the pivot table, its formatting, and underlying formulas are duplicated. Without these options, only raw values might be copied, breaking the pivot functionality.

### Step 5: Save the workbook and verify the result

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Open `output.xlsx` in Excel and confirm that:

* The second sheet contains a fully functional pivot table identical to the original.
* Refreshing the pivot table updates the data, proving the cache is intact.

---

## Copy range to another sheet using Java

If your goal is simply **copy range to another sheet** without a pivot table, the same code works with a regular cell range. The only change is the source address. The `CopyOptions` configuration stays the same, ensuring formulas and formatting are preserved.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

This snippet demonstrates the flexibility of the API for both pivot and non‑pivot scenarios.

---

## Copy range between worksheets without losing formulas

When you **copy range between worksheets**, formulas that reference other sheets can become broken if the relative references change. To avoid this:

1. Use `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` if you only need formulas.
2. Keep the destination sheet in the same workbook so internal references stay valid.
3. After copying, call `workbook.calculateFormula();` to force a recalculation.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

These extra steps ensure that a copied range behaves exactly like the original, even when it spans multiple worksheets.

---

## Pro tips and common pitfalls

| Situation | Tip |
|-----------|-----|
| **Pivot cache not updating** | After copying, call `destSheet.getPivotTables().get(0).refresh();` to refresh the cache. |
| **Copying to a different workbook** | Use `Workbook destWorkbook = new Workbook();` and then `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Remember to copy the pivot cache separately if needed. |
| **Large pivot tables** | Increase the Java heap size (`-Xmx2g`) to avoid `OutOfMemoryError` during the copy. |
| **Preserving styles** | Set `copyOptions.setPasteType(PasteType.PASTE_ALL)`; otherwise, only values are copied. |

---

## Expected output

Running the full program produces `output.xlsx`. When opened in Excel:

* **Sheet2!A1:G20** displays the same pivot table as **Sheet1!A1:G20**.
* The pivot field list, row/column labels, and data values match the source.
* Refreshing the pivot updates the numbers, confirming the cache is functional.

The console will print:

```
Pivot table copied successfully.
```

---

## Conclusion

In this tutorial you learned **how to copy pivot table** from one worksheet to another using Aspose.Cells for Java. By loading the workbook, selecting the correct source range, defining a destination, and configuring `CopyOptions`, you can reliably **copy range to another sheet** and **copy range between worksheets** while preserving all pivot functionality.  

Next, you might explore:

* Exporting the copied pivot table to PDF or HTML.
* Automating pivot table refreshes across multiple workbooks.
* Using `CopyOptions` to copy only specific elements (e.g., values, formats).

Feel free to experiment with different range addresses, workbook structures, or even cross‑workbook copies. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Copy Pivot Table Excel – Step‑by‑Step Guide Using Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}