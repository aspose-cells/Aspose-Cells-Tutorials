---
category: general
date: 2026-06-21
description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
  how to copy excel range to another workbook efficiently.
draft: false
keywords:
- programmatically copy worksheet range
- how to copy excel range to another workbook
- Aspose.Cells copy range Java
- copy pivot table between workbooks
- Java Excel automation
language: en
og_description: Programmatically copy worksheet range in Java. This guide shows how
  to copy excel range to another workbook with full code and tips.
og_title: Programmatically Copy Worksheet Range – Java Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  headline: Programmatically Copy Worksheet Range – Complete Java Guide
  type: TechArticle
- description: Programmatically copy worksheet range in Java using Aspose.Cells. Learn
    how to copy excel range to another workbook efficiently.
  name: Programmatically Copy Worksheet Range – Complete Java Guide
  steps:
  - name: 1. Copying Across Different Excel Versions
    text: Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the
      source and destination use different formats, the library automatically converts
      them. Just ensure the file extensions match your desired output.
  - name: 2. Preserving External Data Sources in Pivot Tables
    text: If the pivot table in the source references an external data source (e.g.,
      a database connection), the copied pivot will retain the connection string but
      **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying
      if you need up‑to‑date results.
  - name: 3. Large Ranges and Memory Consumption
    text: Copying massive ranges (hundreds of thousands of rows) can spike memory
      usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before
      loading large files to keep the footprint low.
  - name: 4. Multiple Sheets or Ranges
    text: If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for
      each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook
- Automation
title: Programmatically Copy Worksheet Range – Complete Java Guide
url: /java/range-management/programmatically-copy-worksheet-range-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmatically Copy Worksheet Range – Complete Java Guide

Ever wondered how to **programmatically copy worksheet range** without opening Excel manually? You’re not the only one. Whether you need to duplicate a report, clone a pivot‑driven dashboard, or simply move data between files, doing it in code saves time and eliminates human error.

In this tutorial we’ll walk through a clean, end‑to‑end solution that shows **how to copy excel range to another workbook** using Java and the Aspose.Cells library. By the end you’ll have a ready‑to‑run program, understand the why behind each step, and know the pitfalls to watch out for.

---

## What You’ll Need

- **Java Development Kit (JDK) 11+** – the code compiles with any recent JDK.
- **Aspose.Cells for Java** (free trial or licensed version). Add the Maven dependency or download the JAR.
- Two Excel files: an `input.xlsx` that contains the source range (including a pivot table) and an empty `output.xlsx` where the range will land.
- Any IDE you like – IntelliJ IDEA, Eclipse, or even a simple text editor.

That’s it. No extra services, no COM interop, just pure Java.

---

![Diagram illustrating programmatically copy worksheet range between two workbooks](image.png)

*Image alt text: programmatically copy worksheet range illustration*

---

## Step 1: Set Up the Project and Import Aspose.Cells

First things first, we need the library on the classpath. If you’re using Maven, add:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

If you prefer a manual JAR, drop it into your `libs` folder and add it to the build path.

Why this matters: Aspose.Cells gives us a rich object model (`Workbook`, `Worksheet`, `Range`) that lets us copy data **including pivot tables, formulas, and formatting** in a single call—something the plain Apache POI library can’t do as cleanly.

---

## Step 2: Load the Source Workbook

We’ll open the workbook that holds the data we want to clone. The `Workbook` constructor takes a file path, and Aspose will read the whole file into memory.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Pro tip:* Wrap the loading in a try‑catch block if the file might be missing; otherwise the program will terminate with a clear error.

---

## Step 3: Create an Empty Destination Workbook

A fresh workbook gives us a clean canvas. We don’t need to pre‑populate any sheets; Aspose will add one for us.

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();
```

Why not reuse the source? Keeping them separate prevents accidental overwrites and makes the code reusable for batch operations.

---

## Step 4: Define the Exact Range to Copy

Here’s where the **programmatically copy worksheet range** magic begins. We select cells `A1:D20` from the first worksheet of the source file. The `createRange` method returns a `Range` object that represents exactly those cells, pivot tables included.

```java
        // Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)               // first sheet (index 0)
                                          .getCells()
                                          .createRange("A1:D20");
```

If you need a dynamic range (e.g., “last used row”), you can replace the hard‑coded address with `Cells.maxDisplayRange` or calculate it with `Cells.getMaxDataColumn()` and `Cells.getMaxDataRow()`.

---

## Step 5: Add a Target Worksheet in the Destination Workbook

Aspose creates a default sheet named “Sheet1” when you instantiate `Workbook`. We’ll add a new one to keep things tidy, especially if you plan to copy multiple ranges later.

```java
        // Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
```

You can give the sheet a friendly name:

```java
        targetWorksheet.setName("CopiedData");
```

---

## Step 6: Perform the Copy – Including Pivot Tables

Now the core operation: `copyRange`. This method copies **values, formulas, formatting, and embedded objects** (like pivot tables) from the source range to a destination cell (`A1` in our new sheet). It’s the simplest way to achieve **how to copy excel range to another workbook** without fiddling with low‑level cell loops.

```java
        // Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)               // source sheet index
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");
```

Behind the scenes Aspose serializes the source range into an intermediate format, then deserializes it into the target sheet—so everything stays intact.

---

## Step 7: Save the Destination Workbook and Verify

Finally, we write the destination workbook to disk. Open `output.xlsx` in Excel to see the copied range, pivot table, and all styling preserved.

```java
        // (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Range copied successfully!");
    }
}
```

When you open `output.xlsx`, you should see a sheet named “CopiedData” with the same layout as `A1:D20` from the source, including the pivot table that now points to the copied data.

---

## Handling Common Edge Cases

### 1. Copying Across Different Excel Versions
Aspose.Cells works with `.xls`, `.xlsx`, `.xlsb`, and even `.csv`. If the source and destination use different formats, the library automatically converts them. Just ensure the file extensions match your desired output.

### 2. Preserving External Data Sources in Pivot Tables
If the pivot table in the source references an external data source (e.g., a database connection), the copied pivot will retain the connection string but **won’t automatically refresh**. Call `pivotTable.refreshData()` after copying if you need up‑to‑date results.

```java
        PivotTable pt = targetWorksheet.getPivotTables().get(0);
        pt.refreshData();
        pt.calculateData();
```

### 3. Large Ranges and Memory Consumption
Copying massive ranges (hundreds of thousands of rows) can spike memory usage. Use `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before loading large files to keep the footprint low.

### 4. Multiple Sheets or Ranges
If you need to copy several non‑contiguous ranges, repeat steps 4‑6 for each range, or use `copyRange` with a union range (`Cells.createRange("A1:B10,C1:D10")`).

---

## Pro Tips for Robust Automation

- **Validate the source range** before copying. Use `sourceRange.isValid()` to avoid runtime errors.
- **Lock the destination file** with `FileInfo.setReadOnly(false)` if you’re overwriting an existing workbook.
- **Log actions** with a lightweight logger (SLF4J) – especially useful when processing batches.
- **Dispose of workbooks** (`sourceWorkbook.dispose(); destinationWorkbook.dispose();`) in long‑running services to free native resources.

---

## Full Working Example Recap

Below is the complete, self‑contained Java class you can paste into your IDE and run. Remember to replace `YOUR_DIRECTORY` with the actual folder path on your machine.

```java
import com.aspose.cells.*;

public class CopyWorksheetRange {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook containing the data and pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2️⃣ Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 3️⃣ Define the range to copy (A1:D20) from the first worksheet of the source
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:D20");

        // 4️⃣ Add a new worksheet to the destination workbook where the range will be placed
        Worksheet targetWorksheet = destinationWorkbook.getWorksheets().add();
        targetWorksheet.setName("CopiedData");

        // 5️⃣ Copy the defined range (including the pivot table) to cell A1 of the new worksheet
        sourceWorkbook.getWorksheets()
                      .get(0)
                      .getCells()
                      .copyRange(sourceRange, targetWorksheet, "A1");

        // 6️⃣ (Optional) Save the destination workbook to verify the result
        destinationWorkbook.save("YOUR_DIRECTORY/output.xlsx");

        System.out.println("Programmatically copy worksheet range completed successfully.");
    }
}
```

**Expected output:** An `output.xlsx` file with a sheet named “CopiedData”. Cells `A1:D20` will mirror the source, and any pivot table inside that block will be fully functional, pointing to the copied data.

---

## Conclusion

We’ve just demonstrated a clean, **programmatically copy worksheet range** solution in Java, answering the common question **how to copy excel range to another workbook**. By leveraging Aspose.Cells’ high‑level API we avoided low‑level cell loops, preserved pivot tables, and kept the code readable.

What’s next? Try extending this pattern to:

- Copy entire worksheets instead of a single range.
- Batch‑process dozens of workbooks in a folder.
- Export the copied range to CSV or PDF for reporting pipelines.

Feel free to experiment, and when you hit a snag, drop a comment. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java&#58; A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Excel Columns Efficiently Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/range-management/copy-excel-columns-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}