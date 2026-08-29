---
category: general
date: 2026-07-23
description: Create new workbook in Java and learn how to copy pivot table, copy excel
  range, and export pivot table with Aspose.Cells in minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: en
lastmod: 2026-07-23
og_description: Create new workbook in Java and instantly copy pivot table, copy excel
  range, then export pivot table using Aspose.Cells. Follow this complete tutorial.
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: Create New Workbook in Java – Copy Pivot Table Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Create New Workbook in Java – Full Guide to Copy Pivot Table
url: /java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Workbook in Java – Full Guide to Copy Pivot Table

Ever wondered how to **create new workbook** in Java while preserving a complex pivot table? You're not the only one scratching your head over this. In many reporting apps you need to move a pivot from a source file to a fresh workbook, maybe to ship it to a client or to run further calculations. The good news? With a handful of lines you can do exactly that—no manual copy‑pasting required.

In this tutorial we’ll walk through the entire process: loading the source file, defining the range that holds the pivot, **copying the Excel range**, creating a **new workbook**, and finally **exporting the pivot table** to a new file. By the end you’ll have a self‑contained, runnable Java program that answers the question “**how to copy pivot**” without any guesswork.

## Prerequisites

Before we dive in, make sure you have:

- Java 17 or later (the code works with any recent JDK)
- Aspose.Cells for Java library (free trial or licensed version)
- A sample `source.xlsx` that contains a pivot table in the range `A1:G20`
- An IDE or build tool (Maven/Gradle) to manage the Aspose.Cells JAR

Got those? Great—let’s get started.

## Step 1: Set Up the Project and Import Aspose.Cells

First things first, you need to add Aspose.Cells to your project. If you’re using Maven, drop this dependency into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

If you prefer Gradle, the equivalent is:

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

Once the library is on the classpath, import the classes you’ll need:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Aspose.Cells is a commercial library, but it offers a fully functional 30‑day evaluation that stamps a watermark on the output—perfect for trying this out.

## Step 2: Load the Source Workbook

Now we’ll **create new workbook** objects, but first we need the source that holds the pivot. This step is the foundation for any **copy excel range** operation because the range object knows exactly which cells (including the pivot cache) to transfer.

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Why not just read the range directly? Because the pivot table’s metadata lives in the worksheet’s pivot cache, and Aspose.Cells automatically bundles that when you copy the range.

## Step 3: Define the Range That Holds the Pivot Table

In many real‑world files the pivot occupies a rectangular block. For this example we’ll assume it lives in `A1:G20`. You can, of course, adjust the address to match your actual layout.

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

If you’re unsure about the exact address, you can use `sourceSheet.getCells().getMaxDataRow()` and `getMaxDataColumn()` to calculate the bounds dynamically. That’s a handy trick when the pivot size changes over time.

## Step 4: **Create New Workbook** and Destination Worksheet

Here’s the moment we actually **create new workbook** that will receive the copied content. Think of this as the blank canvas you’ll paste the pivot onto.

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Why start with an empty workbook? It guarantees that no hidden styles or previous pivots interfere with the copy, giving you a clean result ready for **export pivot table**.

## Step 5: Copy the Pivot Table (and Its Underlying Range)

Now the core of the tutorial: **copy pivot table**. Aspose.Cells treats a range copy as a deep copy, meaning the pivot cache travels with the cells. That’s why this single line does the heavy lifting.

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

If you ever wondered **how to copy pivot** without losing its functionality, this is the answer. The destination sheet now contains a fully working pivot that you can refresh, modify, or simply export.

### Edge Case: Preserving Refresh Settings

Sometimes the source pivot is set to refresh on opening. To keep that behavior, you can copy the pivot’s options explicitly:

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

That snippet ensures the copied pivot behaves exactly like the original.

## Step 6: Save the Destination Workbook – **Export Pivot Table**

Finally, we **export pivot table** by saving the new workbook to disk. You can choose any format Aspose supports: XLSX, XLS, CSV, PDF, etc. For this guide we’ll stick with XLSX.

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

If you need to send the file over a web service, you can write it to a `ByteArrayOutputStream` instead of a file path—Aspose makes that trivial.

## Full Working Example

Putting it all together, here’s a complete, ready‑to‑run program. Feel free to copy, paste, and execute it in your IDE.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### Expected Output

When you run the program, the console prints:

```
Pivot table copied successfully!
```

And the file `copied_with_pivot.xlsx` appears in `YOUR_DIRECTORY`. Open it in Excel, and you’ll see the pivot table intact, ready to be refreshed or edited.

## Common Questions & Troubleshooting

- **What if the source pivot spans more than one worksheet?**  
  You’ll need to copy each relevant range separately, then recreate the pivot on the destination sheet using `PivotTable` APIs.

- **Can I copy only the pivot layout without the data?**  
  Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose to keep the cache but not the underlying source data.

- **Is there a way to copy the pivot to a CSV file?**  
  CSV doesn’t support pivots, but you can export the pivot’s *result* by calling `pivotTable.calculate()` and then saving the sheet as CSV.

- **Why does the copied pivot lose its formatting?**  
  Formatting lives in the style collection. After copying, you can call `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` to transfer styles.

## Conclusion

We’ve just shown you how to **create new workbook** in Java, **copy pivot table**, and **export pivot table**—all with a clean, reproducible code sample. By defining the exact **copy excel range**, leveraging Aspose.Cells’s deep‑copy semantics, and preserving optional settings, you can automate virtually any pivot‑migration task.

Ready for the next step? Try swapping the output format to PDF, or loop through multiple source files to batch‑process dozens of pivots. The same pattern applies—just adjust the file paths and range addresses.

If you hit a snag, drop a comment below or check the Aspose.Cells documentation for advanced pivot manipulation. Happy coding, and enjoy the time you saved by automating those tedious copy‑paste chores!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}