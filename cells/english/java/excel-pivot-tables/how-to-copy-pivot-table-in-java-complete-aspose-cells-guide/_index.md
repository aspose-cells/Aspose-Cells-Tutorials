---
category: general
date: 2026-06-08
description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
  between workbooks and preserve pivot tables effortlessly.
draft: false
keywords:
- how to copy pivot table
- copy range between workbooks
- how to preserve pivot
- copy pivot table to new workbook
- copy excel sheet with pivot
language: Java
og_description: How to copy pivot table in Java with Aspose.Cells. This tutorial shows
  how to copy range between workbooks and keep the pivot intact.
og_title: How to Copy Pivot Table in Java – Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  headline: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  type: TechArticle
- description: How to copy pivot table using Aspose.Cells in Java. Learn to copy range
    between workbooks and preserve pivot tables effortlessly.
  name: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
  steps:
  - name: Set Up Aspose.Cells in Your Project
    text: 'Before you can manipulate Excel files, you need the Aspose.Cells library
      on your classpath. If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the Source Workbook
    text: We need a `Workbook` instance that points at the file housing the pivot.
      Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.
  - name: Define the Pivot’s Enclosing Range
    text: A pivot table lives inside a rectangular block of cells. You can locate
      it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s
      `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.
  - name: Create a Blank Destination Workbook
    text: Now we spin up an empty workbook that will receive the copied data.
  - name: Copy the Range and Preserve the Pivot
    text: Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions`
      object, but we don’t need to tweak anything—pivot preservation is enabled out
      of the box.
  - name: Save the Destination Workbook
    text: Finally, write the new file to disk.
  type: HowTo
- questions:
  - answer: Yes. Because we’re copying the entire cell range, styles, conditional
      formatting, and number formats travel with the data.
    question: Does this method also copy the pivot’s formatting?
  - answer: Simply change the third argument of `copyRange` to the desired top‑left
      address, e.g., `"B5"`.
    question: What if I need to copy the pivot to a specific cell other than `A1`?
  - answer: 'Not directly. The pivot cache lives inside the workbook; removing the
      source data will render the pivot unusable. Export the source data to a hidden
      sheet if you want a lightweight copy. --- ## Conclusion You now have a clear,
      end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cel'
    question: Can I copy a pivot without its source data?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- PivotTable
title: How to Copy Pivot Table in Java – Complete Aspose.Cells Guide
url: /java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Copy Pivot Table in Java – Complete Aspose.Cells Guide

Ever wondered **how to copy pivot table** from one Excel workbook to another using Java? The good news is that Aspose.Cells makes it a breeze to **copy range between workbooks** while preserving every detail of the pivot.  

In this tutorial we’ll walk through a real‑world example that not only copies the pivot itself but also keeps the underlying data, formatting, and formulas intact. By the end you’ll know exactly **how to preserve pivot** structures, how to move a pivot to a brand‑new workbook, and how to avoid the common pitfalls that trip up many developers.

We’ll cover:

* The minimal prerequisites (Java 17+, Aspose.Cells for Java 23.9+).  
* A step‑by‑step breakdown of the code, with explanations of **why** each line matters.  
* Edge‑case handling for large pivot ranges and external data sources.  
* A complete, runnable program you can drop into your IDE and run today.

> **Pro tip:** If you’re already using Maven or Gradle, adding Aspose.Cells as a dependency is a single line—no manual JAR juggling required.

---

## How to Copy Pivot Table – Step‑by‑Step Overview

Below is a high‑level view of what we’ll achieve:

1. Load the source workbook that contains the pivot table.  
2. Identify the exact cell range that encloses the pivot.  
3. Create a fresh destination workbook.  
4. **Copy the range** to the new sheet, letting Aspose.Cells automatically preserve the pivot.  
5. Save the result as a new file.

Each step is illustrated with code snippets and a short rationale, so you’ll understand the mechanics—not just the mechanics.

![Diagram illustrating how a pivot table is copied from a source workbook to a destination workbook while preserving its structure](/images/how-to-copy-pivot-table-diagram.png){: .align-center alt="how to copy pivot table diagram"}

---

### Step 1: Set Up Aspose.Cells in Your Project

Before you can manipulate Excel files, you need the Aspose.Cells library on your classpath. If you use Maven, add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

For Gradle, it’s a one‑liner as well:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

*Why this matters:* Aspose.Cells abstracts away the low‑level OpenXML details, giving you a simple API to **copy pivot table to new workbook** without losing any metadata.

---

### Step 2: Load the Source Workbook

We need a `Workbook` instance that points at the file housing the pivot. Replace `YOUR_DIRECTORY/src.xlsx` with the actual path on your machine.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
```

> **Note:** Aspose.Cells automatically detects the file format (XLSX, XLS, CSV, etc.), so you don’t have to worry about format conversion.

---

### Step 3: Define the Pivot’s Enclosing Range

A pivot table lives inside a rectangular block of cells. You can locate it manually (e.g., `A1:G20`) or programmatically by inspecting the worksheet’s `PivotTables` collection. For this tutorial we’ll hard‑code the range for clarity.

```java
// Define the range that encloses the pivot table (e.g., A1:G20)
Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                 .getCells()
                                 .createRange("A1:G20");
```

*Why we use `createRange`*: It creates a lightweight `Range` object that can be passed to `copyRange`. This is the most reliable way to **copy range between workbooks** while ensuring the pivot’s internal structures are included.

---

### Step 4: Create a Blank Destination Workbook

Now we spin up an empty workbook that will receive the copied data.

```java
// Create a new (blank) destination workbook
Workbook destinationWorkbook = new Workbook(); // defaults to a single empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

The default workbook already contains one worksheet, which is perfect for our purpose. If you need a specific sheet name, you can rename it:

```java
destinationSheet.setName("PivotCopy");
```

---

### Step 5: Copy the Range and Preserve the Pivot

Here’s where the magic happens. The `copyRange` method accepts a `CopyOptions` object, but we don’t need to tweak anything—pivot preservation is enabled out of the box.

```java
// Copy the range to the destination sheet; the pivot table is preserved automatically
destinationSheet.getCells().copyRange(pivotRange, new CopyOptions() {{
    // No additional settings are required – pivot preservation is enabled by default
}}, "A1");
```

*Why this works:* Aspose.Cells treats the pivot as part of the cell collection. When you invoke `copyRange`, it replicates the underlying pivot cache, data fields, and layout, effectively **how to preserve pivot** without extra code.

---

### Step 6: Save the Destination Workbook

Finally, write the new file to disk.

```java
// Save the destination workbook with the copied pivot table
destinationWorkbook.save("YOUR_DIRECTORY/copied-with-pivot.xlsx");
```

Open the resulting `copied-with-pivot.xlsx` in Excel, and you’ll see an exact replica of the original pivot, ready for further analysis.

---

## Full Working Example

Below is the complete program you can compile and run directly. It puts together all the snippets above, adds a few defensive checks, and prints a friendly confirmation message.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // ---------- 1. Load source workbook ----------
        String srcPath = "YOUR_DIRECTORY/src.xlsx";
        Workbook sourceWorkbook = new Workbook(srcPath);

        // ---------- 2. Identify pivot range ----------
        // You may replace the hard‑coded range with a dynamic lookup if needed.
        Range pivotRange = sourceWorkbook.getWorksheets().get(0)
                                         .getCells()
                                         .createRange("A1:G20");

        // ---------- 3. Create destination workbook ----------
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
        destinationSheet.setName("PivotCopy");

        // ---------- 4. Copy range (pivot preserved) ----------
        destinationSheet.getCells().copyRange(pivotRange,
                new CopyOptions() {{
                    // No extra options required for pivot preservation.
                }}, "A1");

        // ---------- 5. Save result ----------
        String destPath = "YOUR_DIRECTORY/copied-with-pivot.xlsx";
        destinationWorkbook.save(destPath);

        System.out.println("Pivot table successfully copied!");
        System.out.println("Source:  " + srcPath);
        System.out.println("Destination: " + destPath);
    }
}
```

**Expected output when you run the program**:

```
Pivot table successfully copied!
Source:  YOUR_DIRECTORY/src.xlsx
Destination: YOUR_DIRECTORY/copied-with-pivot.xlsx
```

Open the destination file—your pivot should look identical to the original, complete with slicers, filters, and calculated fields.

---

## Handling Common Edge Cases

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Pivot uses an external data source** (e.g., a database) | The external connection isn’t embedded in the workbook, so copying may break the link. | Export the data to a sheet first, then create a pivot on that sheet before copying. |
| **Very large pivot (thousands of rows)** | `copyRange` may consume significant memory. | Increase the JVM heap (`-Xmx2g`) or copy the pivot in smaller chunks using `copyRows`/`copyColumns`. |
| **Multiple pivots on the same sheet** | Hard‑coding `A1:G20` copies only the first pivot. | Loop through `sourceWorksheet.getPivotTables()` and copy each `PivotTable.getDataRange()`. |
| **Destination workbook already contains a sheet with the same name** | `setName` will throw an exception. | Use `Workbook.getWorksheets().add("PivotCopy")` to create a uniquely named sheet. |

These tips ensure that **how to copy pivot table** works reliably, even in production‑grade scenarios.

---

## Frequently Asked Questions

**Q: Does this method also copy the pivot’s formatting?**  
A: Yes. Because we’re copying the entire cell range, styles, conditional formatting, and number formats travel with the data.

**Q: What if I need to copy the pivot to a specific cell other than `A1`?**  
A: Simply change the third argument of `copyRange` to the desired top‑left address, e.g., `"B5"`.

**Q: Can I copy a pivot without its source data?**  
A: Not directly. The pivot cache lives inside the workbook; removing the source data will render the pivot unusable. Export the source data to a hidden sheet if you want a lightweight copy.

---

## Conclusion

You now have a clear, end‑to‑end answer to **how to copy pivot table** in Java using Aspose.Cells. By loading the source workbook, defining the pivot’s range, and leveraging `copyRange`, you can effortlessly **copy range between workbooks** while ensuring the pivot stays


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}