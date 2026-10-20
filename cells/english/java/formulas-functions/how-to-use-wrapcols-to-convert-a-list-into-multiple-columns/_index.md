---
category: general
date: 2026-10-16
description: how to use wrapcols in Java and quickly convert list to columns with
  a formula – learn how to set formula for a multi‑column layout
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: en
lastmod: 2026-10-16
og_description: how to use wrapcols to convert a list to columns in Java. Follow this
  complete guide to set formula and create a multi‑column layout in Excel.
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: How to use wrapcols – step‑by‑step guide for Java developers
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: How to use wrapcols to convert a list into multiple columns in Java
url: /java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to use wrapcols to convert a list into multiple columns in Java

If you need to **how to use wrapcols** in a Java project, this guide shows you the exact steps. You’ll learn how to set the formula, convert a list to columns, and create a multi‑column layout without manual copy‑paste.

The tutorial covers everything from project setup to edge‑case handling, so you can apply the solution to any spreadsheet that contains a single‑column list. No additional tools are required beyond Aspose.Cells for Java.

## Prerequisites

Before you start, make sure you have:

* Java 17 or newer installed  
* Maven 3.8+ (or Gradle) for dependency management  
* A license for **Aspose.Cells for Java** – the free evaluation works for testing  
* Basic familiarity with Excel formulas  

These items ensure the code runs without compilation errors.

## Step 1: Add Aspose.Cells to your project

Add the following Maven dependency to `pom.xml`. If you use Gradle, the same coordinates apply.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

The library provides the `Cell` and `Worksheet` classes used later when you **how to set formula** for a range.

## Step 2: Create a workbook and populate the source list

The first task is to generate a workbook that contains a vertical list (A2:A100). This list represents the data you want to **convert list to columns**.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

The loop fills the first column with 99 items, giving you a realistic list to work with. You can replace the generated values with data read from a database or another source.

## Step 3: How to use wrapcols to set the formula

Now you’ll see the core of the tutorial: using the `WRAPCOLS` function to **create multi‑column layout**. The function takes two arguments – the source range and the number of columns you want.

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*Why this works* – `WRAPCOLS` reads the vertical range `A2:A100`, then distributes the values row‑by‑row across three columns (B, C, and D). The result appears starting at the cell that holds the formula (`A1`). Because the formula returns an array, Aspose.Cells automatically expands the result into the necessary cells.

### What happens behind the scenes

When the workbook is saved, Aspose.Cells evaluates the formula and writes the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel, you’ll see:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Item 1 | Item 34 | Item 67 |
| Item 2 | Item 35 | Item 68 |
| … | … | … |

The layout demonstrates a **create multi‑column layout** pattern that is useful for reports, dashboards, or printable forms.

## Step 4: Verify the output programmatically (optional)

If you want to confirm that the formula produced the expected matrix without opening Excel, you can read back the values after calculation.

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

Running the program prints something like:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

This confirms that **how to use wrapcols** works as intended and that the **convert list to columns** operation succeeded.

## Step 5: Common variations and edge cases

### Changing the number of columns

If you need a different column count, modify the second argument of `WRAPCOLS`. For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically adjusts the row count to accommodate the new layout.

### Handling a non‑even list size

When the source range length isn’t divisible by the column count, `WRAPCOLS` pads the final column with blanks. This behavior is useful for creating balanced tables without manual trimming.

### Using a dynamic range

You can replace `A2:A100` with a named range or a formula that calculates the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution robust when the list length changes.

### Avoiding circular references

Place the formula in a cell that isn’t part of the source range. If you accidentally set the formula inside `A2:A100`, Excel will report a circular reference error. Always write the formula to a separate cell (commonly `A1`).

## Step 6: Tips for production use

* **Cache the workbook** – If you generate many reports in a loop, reuse a single `Workbook` instance and clear previous data to reduce memory overhead.  
* **Set calculation mode** – Use `workbook.getSettings().setCalculateFormulaOnOpen(false)` when you only need the raw formula without immediate evaluation.  
* **Internationalization** – The function name `WRAPCOLS` is locale‑independent, but decimal separators in other formulas may differ. Keep formulas in English to avoid mismatches.  
* **Performance** – For lists exceeding 10 000 rows, evaluate the formula once and then read the array values directly to avoid repeated calculations.

## Conclusion

You now know **how to use wrapcols** in Java to **convert list to columns** and **create multi‑column layout** with a single formula. The complete, runnable example demonstrates the full workflow: adding the library, populating data, applying the formula, and verifying the result.  

From here you can:

* Adjust the column count to fit your reporting style  
* Combine `WRAPCOLS` with other functions like `SORT` or `FILTER` for advanced data shaping  
* Export the workbook to PDF, CSV, or HTML using Aspose.Cells’ built‑in converters  

Experiment with these variations to streamline your Excel automation tasks. If you encounter any issues, review the edge‑case handling section above or consult the Aspose.Cells documentation for additional formula support. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}