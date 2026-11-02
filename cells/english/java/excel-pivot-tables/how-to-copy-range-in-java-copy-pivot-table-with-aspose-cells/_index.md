---
category: general
date: 2026-06-30
description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
  copy pivot table, and load Excel workbook efficiently.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: en
og_description: How to copy range in Java with Aspose.Cells. Learn to duplicate Excel
  range, copy pivot table, and load Excel workbook in minutes.
og_title: How to copy range in Java – Step-by-Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: How to copy range in Java – Copy Pivot Table with Aspose.Cells
url: /java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy range in Java – Copy Pivot Table with Aspose.Cells

Ever wondered **how to copy range** from one Excel workbook to another without losing the pivot table integrity? You're not the only one. In many reporting pipelines the need to *duplicate Excel range* while preserving pivot logic is a daily headache. Luckily, Aspose.Cells for Java makes this a breeze, and in this tutorial we’ll walk through a complete, runnable example that also shows you how to **load Excel workbook**, copy a pivot table, and save the result.

By the end of this guide you’ll have a self‑contained Java program that:

* Loads an existing workbook (`load excel workbook`);
* Defines the exact cells that contain a pivot table;
* Copies that **pivot table to sheet** in a brand‑new workbook;
* Saves the new file, ready for downstream processing.

No external scripts, no manual steps—just pure code.

## What You’ll Need

Before we dive in, make sure you have:

* Java 8 or newer (the code works with Java 11+ as well);
* Aspose.Cells for Java library (you can grab it from Maven Central);
* Two sample Excel files – one source with a pivot table (`source.xlsx`) and a destination folder where you’ll write `copy-pivot.xlsx`.

That’s it. No fancy IDE tricks required; any text editor plus `javac` will do.

## Step 1: Set Up the Project and Import Aspose.Cells

First things first—let’s get the library on board. If you use Maven, add this dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

If you’re not on Maven, download the JAR from the Aspose website and drop it on your classpath. Once that’s sorted, create a new Java class called `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Keep your `src/main/java` folder clean and give the class a meaningful name; it makes future maintenance easier.

## Step 2: Load the Source Workbook (`load excel workbook`)

Now we actually **load excel workbook** that contains the pivot table we want to copy. The `Workbook` constructor takes a file path, so make sure the path is correct.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Why do we pick the first worksheet? In most simple cases the pivot lives on the first sheet, but you can change the index or use the sheet name if needed. This flexibility is one of the reasons Aspose.Cells shines.

## Step 3: Define the Range that Holds the Pivot Table

A pivot table usually spans a block of cells. Let’s assume it occupies `A1:G20`. You can adjust the address to match your real data.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

If you’re unsure about the exact address, open the workbook in Excel, select the whole pivot, and look at the name box. Remember, **duplicate excel range** works best when you target the exact area—no extra rows, no missing columns.

## Step 4: Create a New Workbook for the Destination

We need a fresh workbook that will receive the copied range. This is where we’ll **copy pivot table** to a new sheet.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

At this point the destination workbook is empty, but Aspose.Cells automatically adds a default sheet, which we’ll use as the target.

## Step 5: Copy the Range – Pivot Table Stays Intact

Here’s the magic line that **copy pivot table** while keeping all its internal connections alive.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

The `copy` method takes two arguments: the source `Range` and the destination `Range`. By starting the destination at `A1`, we place the pivot exactly where it was in the source. Aspose.Cells copies the underlying pivot cache, so the new workbook still knows how to refresh the pivot.

## Step 6: Save the Resulting Workbook

Finally, write the new file to disk. You can choose any format Aspose supports (`.xlsx`, `.xls`, `.csv`, etc.). We’ll stick with `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Run the program, and you should see a fresh workbook with the same pivot layout. Open it in Excel—if everything went well, you’ll be able to refresh the pivot without errors.

### Expected Output

When you execute `CopyPivotDemo`, the console prints:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Opening `copy-pivot.xlsx` reveals a sheet that looks identical to the source’s pivot area, and the **pivot table to sheet** works just like the original.

## Full Working Example

Below is the complete, ready‑to‑run Java class that ties all the steps together. Copy‑paste it into your IDE, adjust the file paths, and hit run.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Note:** If your pivot table spans more than one worksheet, repeat the copy step for each relevant sheet, or use `Workbook.copy` to clone entire worksheets.

## Common Questions & Edge Cases

### What if the source workbook has multiple worksheets?

You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant range. Just be careful to maintain the same sheet names in the destination if you need to preserve references.

### Does the copied pivot retain its data source?

Yes. Aspose.Cells copies the pivot cache along with the range, so the destination workbook still points to the original data source within the same file. If you later move the data to a different sheet, you may need to refresh the pivot manually.

### How to copy a pivot that uses an external data source?

When the pivot’s data source is an external file, you’ll have to embed that data into the destination workbook first (e.g., copy the source data range) before copying the pivot. Otherwise the pivot will show “#REF!” errors.

### Can I copy the pivot without the surrounding data?

Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()` to retrieve the exact range programmatically.

## Tips for Real‑World Projects

* **Batch processing:** If you need to duplicate dozens of workbooks, wrap the code above in a method and call it inside a loop that iterates over a directory.
* **Performance:** For large files, reuse a single `Workbook` instance and call `Workbook.calculateFormula()` only after all copies are done.
* **Error handling:** Surround the copy logic with try‑catch blocks and log `Exception.getMessage()`; Aspose throws `CellsException` for invalid ranges.

## Conclusion

We’ve just covered **how to copy range** in Java using Aspose.Cells, showing you how to **duplicate excel range**, **copy pivot table**, and **load excel workbook** all in one tidy program. The steps are straightforward, the code is fully runnable, and the approach scales from a single‑sheet demo to enterprise‑level batch jobs.

Ready for the next challenge? Try exporting the copied pivot to PDF, or programmatically refresh it after adding new data. Both tasks build on the same foundation we laid out here, so you’ll be well‑equipped to tackle them.

Got questions or want to share your own tweaks? Drop a comment below—happy coding! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}