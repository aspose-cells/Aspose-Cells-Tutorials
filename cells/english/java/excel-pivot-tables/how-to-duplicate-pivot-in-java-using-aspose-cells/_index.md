---
category: general
date: 2026-09-18
description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
  between workbooks quickly and reliably.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: en
lastmod: 2026-09-18
og_description: how to duplicate pivot in Java using Aspose.Cells. Follow this complete
  tutorial to copy a pivot table between workbooks with clean Java code.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Duplicate a pivot table in Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to duplicate pivot in Java using Aspose.Cells
url: /java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to duplicate pivot in Java using Aspose.Cells

If you need to **how to duplicate pivot** in a Java application, this guide shows you the exact steps. By loading an Excel workbook, defining the pivot’s cell area, and copying that range to a new workbook, you can move a pivot table without losing its definition or data.

Copying a pivot table is a common requirement when you generate reports, archive analyses, or split a large workbook into modular pieces. In this tutorial you will learn how to **copy range between workbooks**, how to **load Excel workbook Java**, and the nuances of **how to copy pivot** safely.

You’ll finish with a ready‑to‑run Java program that duplicates a pivot table from `Source.xlsx` to `PivotCopied.xlsx` using Aspose.Cells for Java.

## Prerequisites

Before you start, make sure you have:

* JDK 8 or newer installed.
* Maven (or another build tool) to manage dependencies.
* Aspose.Cells for Java version 23.10 or later. Add the following Maven dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* A source workbook (`Source.xlsx`) that contains a pivot table in the range **A1:H30**.

## How to duplicate pivot in Java

The core idea is straightforward:

1. **Load the source workbook** – this gives you access to the worksheet that holds the pivot.
2. **Define the cell area** that encloses the pivot.
3. **Create a destination workbook** – an empty file that will receive the copied range.
4. **Copy the range** – Aspose.Cells automatically duplicates the pivot definition.
5. **Save the destination workbook** – you now have a separate file with the same pivot.

Below is a complete, runnable Java program that follows those steps.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Why this works

* **Aspose.Cells** treats a pivot table as part of the worksheet’s cell collection. When you invoke `copyRange`, the library copies not only cell values but also the underlying pivot cache and definition, so the new workbook contains a fully functional duplicate.
* The `CopyOptions` object defaults to preserving formulas, formats, and embedded objects. You can customize it (e.g., `setCopyColumnWidths(true)`) if you need extra control.

## Copy range between workbooks – deeper look

While the example above copies a single contiguous block, `copyRange` can handle any rectangular area. If your pivot spans non‑adjacent ranges, you can call `copyRange` multiple times or use `Worksheet.copy` to duplicate the entire sheet.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** When copying large workbooks, enable `CopyOptions.setPreserveCellStyle(true)` to avoid unnecessary style duplication, which can improve performance.

## How to copy pivot to workbook – handling multiple pivots

If the source sheet contains more than one pivot, you can iterate over the worksheet’s pivot tables and copy each one individually:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

This approach ensures that every pivot retains its original name and data source.

## Load Excel workbook Java – common pitfalls

* **File path separators:** Use forward slashes (`/`) or `File.separator` to keep the code platform‑independent.
* **Missing license:** Aspose.Cells works in evaluation mode, but the output will contain a watermark. Register a license with `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` before loading the workbook to remove the watermark.
* **Large files:** For workbooks larger than 100 MB, consider using `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` with streaming options to reduce memory consumption.

## Full end‑to‑end example recap

Putting everything together, here’s the final program you can copy‑paste into your IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Expected output:** After execution, `PivotCopied.xlsx` appears in the specified directory. Opening it in Excel shows the same pivot table layout, filters, and data as in `Source.xlsx`. All calculated fields and formatting are preserved.

## Frequently asked questions

* **Does this work with older Excel formats (.xls)?**  
  Yes. Aspose.Cells automatically detects the format. Use `new Workbook("file.xls")` and the same copy logic applies.

* **What if the pivot references external data sources?**  
  The copy retains the original data source reference. If the destination environment cannot reach that source, the pivot will display `#REF!` errors. To avoid this, refresh the pivot after copying or change its data source via `PivotTable.setDataSource(...)`.

* **Can I copy a pivot to a specific sheet name?**  
  Absolutely. After creating the destination worksheet, rename it:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Conclusion

You now know **how to duplicate pivot** tables in Java using Aspose.Cells, how to **copy range between workbooks**, and the best practices for **load Excel workbook Java**. By following the five‑step process—load, define, create destination, copy, and save—you can automate report generation, archive analyses, or split complex workbooks without losing pivot functionality.

Next, explore related topics such as **copy pivot to workbook** with multiple sheets, or integrate the duplicated pivot into a larger data‑processing pipeline using Apache POI for non‑Aspose scenarios. Experiment with different `CopyOptions` settings to fine‑tune performance for massive workbooks.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Group Pivot Fields in Excel Workbooks Using Aspose.Cells for Java - Comprehensive Guide](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}