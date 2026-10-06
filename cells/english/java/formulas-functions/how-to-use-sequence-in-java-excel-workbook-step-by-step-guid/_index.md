---
category: general
date: 2026-06-18
description: how to use sequence in Java to generate dynamic arrays and save workbook
  as xlsx – a complete, hands‑on tutorial for developers
draft: false
keywords:
- how to use sequence
- save workbook as xlsx
- use sequence function
- create excel workbook java
- set dynamic array formula
language: en
og_description: how to use sequence in Java to build dynamic arrays and save workbook
  as xlsx. Follow this guide for a complete, runnable solution.
og_title: How to Use SEQUENCE in Java Excel Workbook – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  headline: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  type: TechArticle
- description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  name: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  steps:
  - name: Generate a Calendar Header
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)"); ```'
  - name: Create a Multiplication Table
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
      ```'
  - name: Expected Output
    text: '- An `dynamic_sequence_demo.xlsx` file appears in your project directory.
      - Opening the file in Excel shows a 3×2 block of numbers (1‑6) automatically
      filled.'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Dynamic Arrays
title: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
url: /java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide

Ever wondered **how to use sequence** to fill a range of cells without writing a loop? You're not the only one. In modern Excel, the `SEQUENCE` function creates a spill‑range of numbers, and with Java you can push that power straight into a workbook.  

In this tutorial we’ll walk through creating an Excel workbook in Java, **set dynamic array formula** using `SEQUENCE`, recalculate the sheet, and finally **save workbook as xlsx**. By the end you’ll have a runnable program you can drop into any project.

## What You’ll Need

- Java 17 or newer (the code works with Java 8+, but the latest JDK gives you the best performance).  
- Aspose.Cells for Java (or any library that supports dynamic array formulas).  
- An IDE or simple text editor—Visual Studio Code works fine.  

No extra Maven plugins or obscure dependencies are required beyond the library itself.

## Step 1: Create an Excel Workbook with Java

The first thing on the list is to **create excel workbook java** style. This is where we spin up a fresh `Workbook` object that will hold all our sheets.

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();
```

*Why this matters*: The `Workbook` class is the entry point for any Excel manipulation. Think of it as a blank notebook waiting for your data.

## Step 2: Grab the First Worksheet

Next, we need a place to drop our formula. By default a new workbook comes with one sheet, so we simply fetch it.

```java
        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Pro tip*: If you need multiple sheets, just call `workbook.getWorksheets().add("Sheet2")` and repeat the process.

## Step 3: **Set Dynamic Array Formula** Using the SEQUENCE Function

Now we get to the heart of the tutorial—**how to use sequence** inside a cell. The formula `=SEQUENCE(3,2)` creates a 3‑row by 2‑column spill range starting at the cell where you place it.

```java
        // Step 3: Insert a dynamic array formula that spills into B1:C3
        // This will generate numbers 1‑6 arranged in 3 rows and 2 columns.
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");
```

*What’s happening?*  
- `SEQUENCE(rows, columns)` tells Excel to produce a matrix of sequential numbers.  
- Because this is a **dynamic array formula**, Excel automatically expands the result into adjacent cells (B1:C3 in our case).  

If you’re curious about variations, try `=SEQUENCE(5,1,10,2)` to start at 10 and step by 2.

## Step 4: Recalculate So the Spill Range Is Up‑to‑Date

Excel doesn’t evaluate formulas until you ask it to. In Java we trigger a calculation pass:

```java
        // Step 4: Recalculate formulas so the spilled range is up‑to‑date
        workbook.calculateFormula();
```

*Why recalc?* Without this call, the cells would contain the formula text but not the numeric results—making the saved file look empty.

## Step 5: **Save Workbook as XLSX**

Finally, we persist the file to disk. This demonstrates **save workbook as xlsx** using the same library.

```java
        // Step 5: Save the workbook with the dynamic array data
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully!");
    }
}
```

When you open `dynamic_sequence_demo.xlsx` in Excel 365 or later, you’ll see:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |

*Notice*: The numbers spill automatically from A1 into the adjacent cells, exactly as the `SEQUENCE` function dictates.

## Exploring Variations of the SEQUENCE Function

Now that you know **how to use sequence**, let’s quickly explore a couple of common scenarios.

### Generate a Calendar Header

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)");
```

This creates a single row with numbers 1‑12—perfect for month headers.

### Create a Multiplication Table

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
```

Here we multiply two identical spill ranges to get a 5×5 multiplication grid.

## Common Pitfalls and How to Avoid Them

- **Old Excel versions**: Dynamic arrays (including `SEQUENCE`) only work in Excel 365/2021+. Older versions will show `#NAME?`.  
- **Library support**: Not every Java Excel library knows about spill ranges. Aspose.Cells does; Apache POI does not (as of 2024).  
- **Saving format**: Always use `.xlsx` for dynamic arrays; the older `.xls` format will drop the spill behavior.

## Full Working Example (Copy‑Paste Ready)

Below is the complete, ready‑to‑run program. Just drop it into a Maven project with Aspose.Cells as a dependency.

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Set the SEQUENCE formula – this will spill into B1:C3
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");

        // Force calculation so the spilled values are stored
        workbook.calculateFormula();

        // Save the workbook as an XLSX file
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully at dynamic_sequence_demo.xlsx");
    }
}
```

### Expected Output

- An `dynamic_sequence_demo.xlsx` file appears in your project directory.  
- Opening the file in Excel shows a 3×2 block of numbers (1‑6) automatically filled.

## Next Steps: Going Beyond SEQUENCE

Now that you’ve mastered **how to use sequence**, consider blending it with other dynamic functions:

- **FILTER** – extract rows that meet criteria.  
- **SORT** – order a spill range without VBA.  
- **UNIQUE** – pull distinct values from a list.

All of these can be **set dynamic array formula** in the same way we did with `SEQUENCE`. Combining them lets you build powerful data pipelines directly inside Excel, all driven from Java.

## Conclusion

We’ve covered everything you need to know about **how to use sequence** in a Java‑generated Excel file: creating the workbook, **set dynamic array formula**, recalculating, and finally **save workbook as xlsx**. The code is complete, the explanations answer the “why” behind each step, and you’ve seen a few practical variations.

Give the example a spin, tweak the parameters, and watch Excel do the heavy lifting for you. If you run into any quirks—whether it’s a version mismatch or a library limitation—drop a comment below. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Aspose.Cells Java&#58; How to Add XML Maps and Save as XLSX (2023 Guide)](/cells/english/java/import-export/aspose-cells-java-add-xml-map-save-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}