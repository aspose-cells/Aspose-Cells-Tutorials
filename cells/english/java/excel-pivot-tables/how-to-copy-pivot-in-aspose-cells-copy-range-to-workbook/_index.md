---
category: general
date: 2026-08-08
description: How to copy pivot in Aspose.Cells and copy range to workbook using Java.
  Learn the exact steps to duplicate a pivot table with CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: en
lastmod: 2026-08-08
og_description: How to copy pivot in Aspose.Cells and copy range to workbook with
  Java. Follow this complete guide to duplicate a pivot table using CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: How to copy pivot in Aspose.Cells – copy range to workbook
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: How to copy pivot in Aspose.Cells – copy range to workbook
url: /java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot in Aspose.Cells – copy range to workbook

If you need to **how to copy pivot** in an Excel file using Aspose.Cells, this guide shows you the exact process. By the end of the tutorial you will be able to **copy range to workbook** while preserving the pivot table definition.

The example uses Java, but the same concepts apply to any .NET language that works with Aspose.Cells. No external tools are required—just the Aspose.Cells for Java library and a basic development environment.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit (JDK) 8 or later.
* Maven or Gradle to manage dependencies (the example uses Maven).
* Aspose.Cells for Java 23.9 (or the latest version) added to your project.
* An input workbook (`input.xlsx`) that contains at least one pivot table on the first worksheet.

Having these items ready prevents runtime errors when the code accesses the workbook.

## How to copy pivot with Aspose.Cells

This section walks through each step required to **how to copy pivot** from one part of a sheet to another, using the `CopyOptions` class.

### Step 1: Add Aspose.Cells to your project

If you use Maven, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Why this step matters*: The library provides the `Workbook`, `CopyOptions`, and other classes required for **aspose.cells copy range** operations. Without the dependency the compiler cannot resolve those types.

### Step 2: Load the source workbook

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Loading the file creates an in‑memory representation of the spreadsheet. The `Workbook` object gives you access to worksheets, cells, and pivot tables.

### Step 3: Configure copy options to include the pivot table

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` tells Aspose.Cells that the operation should preserve pivot table metadata. If you omit this flag, the pivot table would be reduced to static data, losing its interactivity.

### Step 4: Copy the desired range with the pivot table

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

The `copyRange` method copies cells, formatting, and—because of the options set in the previous step—any pivot tables that intersect the range. This is the core of **copy range to workbook** functionality.

### Step 5: Save the modified workbook

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Saving writes the changes to a new file (`output.xlsx`). You can now open this file in Excel and see that the pivot table has been duplicated exactly where the range was copied.

## Full, runnable example

Putting all pieces together, here is the complete program you can compile and run:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Expected result

* `output.xlsx` contains the same data as `input.xlsx`.
* The pivot table that originally occupied the source range appears in the destination cells, fully functional (filters, refresh capability, etc.).
* All cell formatting, formulas, and column widths are preserved because `copyRange` copies the entire cell block.

## Common questions and edge cases

**What if the destination range overlaps an existing pivot table?**  
Aspose.Cells will overwrite the target cells. To avoid data loss, ensure the destination area is empty or move the existing pivot table first.

**Can I copy a pivot table across worksheets?**  
Yes. Use `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` where `targetSheetIndex` points to the destination sheet.

**Does `setCopyPivotTable(true)` copy the underlying data source?**  
The method copies only the pivot cache reference. If the source data resides in the same workbook, the destination pivot will point to the same cache. To duplicate the cache, you must create a new pivot cache manually.

**How to copy a large range efficiently?**  
When copying very large ranges, consider using `CopyOptions.setCopyFormula(true)` and `setCopyDataValidation(true)` only if needed. Reducing the number of options can improve performance.

## Tips for reliable **aspose.cells copy range** usage

* **Pro tip:** Always call `workbook.calculateFormula()` after copying if the range contains formulas that depend on the pivot cache.
* **Watch out for:** Hidden worksheets. `copyRange` works only on visible worksheets unless you explicitly reference the hidden sheet by index.
* **Version check:** The `setCopyPivotTable` flag is available starting from Aspose.Cells 20.9. Ensure your library version supports it.

## Conclusion

You now know **how to copy pivot** in Aspose.Cells and how to **copy range to workbook** while preserving full pivot functionality. The steps—adding the library, loading the workbook, configuring `CopyOptions`, performing the copy, and saving—form a repeatable pattern you can adapt to other copy‑and‑paste scenarios.

Next, explore related topics such as **aspose.cells copy range** for charts, conditional formatting, and data validation. Experiment with copying between different file formats (XLSX → XLS) to broaden your automation capabilities. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}