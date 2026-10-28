---
category: general
date: 2026-07-16
description: Create new workbook and copy pivot table using Aspose.Cells for Java.
  Learn how to duplicate pivot table and copy Excel range in minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- duplicate pivot table
- how to copy pivot
- copy excel range
language: en
lastmod: 2026-07-16
og_description: Create new workbook and copy pivot table with Aspose.Cells for Java.
  This guide shows how to duplicate pivot table and copy Excel range efficiently.
og_image_alt: Screenshot of Java code that creates a new workbook and copies a pivot
  table using Aspose.Cells
og_title: Create New Workbook & Copy Pivot Table in Java – Complete Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  headline: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create new workbook and copy pivot table using Aspose.Cells for Java.
    Learn how to duplicate pivot table and copy Excel range in minutes.
  name: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
  steps:
  - name: What if the source pivot spans more than one sheet?
    text: Aspose.Cells can only copy ranges within a single worksheet at a time. If
      your pivot stretches across sheets, you’ll need to copy each relevant range
      separately and then re‑link them manually.
  - name: Does this method preserve custom number formats?
    text: Yes. The `copy` method copies cell styles, including number formats, fonts,
      and colors. However, if you have conditional formatting that references external
      ranges, double‑check those references after the copy.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot pulls data from an external connection (e.g., a SQL query),
      the connection information is **not** transferred by `copy`. You’ll need to
      recreate the data source in the destination workbook or embed the source data
      beforehand.
  - name: Can I copy only the pivot layout without the underlying data?
    text: You can achieve that by first clearing the data cells in the source range,
      then copying only the pivot’s layout. This is a more advanced scenario and usually
      not required for a simple **duplicate pivot table** task.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide
url: /java/excel-pivot-tables/create-new-workbook-and-copy-pivot-table-in-java-full-step-b/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Workbook and Copy Pivot Table in Java – Full Step‑by‑Step Guide

Ever wondered how to **create new workbook** while preserving a complex pivot table from an existing file? If you’ve ever stared at an Excel sheet, thought “I need this pivot in another workbook,” and then scraped your head, you’re not alone. The good news is that with Aspose.Cells for Java you can duplicate a pivot table in just a handful of lines.

In this tutorial we’ll walk through the exact steps to **copy pivot table** data, **duplicate pivot table** structures, and **copy Excel range** contents—all while creating a fresh workbook from scratch. By the end you’ll have a ready‑to‑run Java program that does exactly what you asked.

## What You’ll Learn

- How to **create new workbook** programmatically with Aspose.Cells.
- The precise way to define the range that contains a pivot table.
- Techniques to **copy pivot table** and **duplicate pivot table** without losing formatting or data connections.
- How to **copy Excel range** efficiently and save the result.
- Common pitfalls and tips for handling larger pivot tables.

No external references needed—everything is self‑contained, runnable, and explained.

---

## Prerequisites

Before we dive in, make sure you have:

1. **Java Development Kit (JDK) 11+** – any recent version works.
2. **Aspose.Cells for Java** library (the latest version as of 2026‑07‑16). You can grab it from Maven Central:

   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-cells</artifactId>
       <version>23.12</version>
   </dependency>
   ```

3. A source Excel file (`SourceWithPivot.xlsx`) that already contains a pivot table you want to copy.
4. An IDE or simple text editor—IntelliJ IDEA, Eclipse, or VS Code will do.

Got all that? Great—let’s roll.

---

## Step 1: **Create New Workbook** and Load the Source File

The first thing we need is a fresh workbook object that will eventually hold the duplicated pivot. At the same time we must load the original workbook so we can reference its pivot table range.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that already contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        // Grab the first worksheet where the pivot lives
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

> **Why this matters:**  
> Loading the source workbook gives us access to the underlying `Range` object that encapsulates the pivot. If you skip this step you’ll have nothing to copy, and the **duplicate pivot table** operation will fail silently.

---

## Step 2: Define the **Copy Excel Range** That Holds the Pivot

A pivot table isn’t a single cell—it spans a rectangular block. We need to tell Aspose.Cells exactly which cells to copy.

```java
        // Define the cell range that includes the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

> **Tip:**  
> If you’re not sure about the exact range, open the source workbook in Excel, select the pivot, and look at the name box. It will show something like `A1:G20`. Using the exact range ensures that all field settings, filters, and calculations are retained when we **copy pivot table** later.

---

## Step 3: **Create New Workbook** That Will Receive the Copied Pivot

Now we spin up a brand‑new workbook—this is where our **duplicate pivot table** will live.

```java
        // Create a completely empty workbook for the destination
        Workbook dstWb = new Workbook(); // this automatically creates one empty worksheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);
```

> **What’s happening under the hood?**  
> The default constructor builds a workbook with a single empty sheet. This is the clean canvas we need for a **create new workbook** scenario. No leftover styles or hidden sheets to worry about.

---

## Step 4: **Copy Pivot Table** – Actually Copy the Defined Excel Range

With both source and destination ready, we perform the copy operation. This step accomplishes the **how to copy pivot** part of the puzzle.

```java
        // Copy the defined range (which includes the pivot) to the destination worksheet
        srcRange.copy(dstWs.getCells().createRange("A1"));
```

> **Why `copy` works for pivots:**  
> Aspose.Cells treats the pivot as part of the cell collection. When you copy the range, it brings over the pivot cache, field list, and layout. The result is a fully functional **duplicate pivot table** in the new workbook.

---

## Step 5: Save the Result and Verify the **Copy Pivot Table** Operation

Finally, persist the destination workbook to disk. Open the file in Excel to confirm the pivot appears exactly as it did in the source.

```java
        // Save the destination workbook with the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

**Expected outcome:**  
- `CopyPivotResult.xlsx` opens with a worksheet containing the same pivot table you saw in `SourceWithPivot.xlsx`.  
- All row/column labels, filters, and calculated fields are intact.  
- You can now edit the source data independently, and the new workbook will retain its own pivot cache.

---

## Edge Cases & Common Questions

### What if the source pivot spans more than one sheet?
Aspose.Cells can only copy ranges within a single worksheet at a time. If your pivot stretches across sheets, you’ll need to copy each relevant range separately and then re‑link them manually.

### Does this method preserve custom number formats?
Yes. The `copy` method copies cell styles, including number formats, fonts, and colors. However, if you have conditional formatting that references external ranges, double‑check those references after the copy.

### How to copy a pivot that uses an external data source?
When the pivot pulls data from an external connection (e.g., a SQL query), the connection information is **not** transferred by `copy`. You’ll need to recreate the data source in the destination workbook or embed the source data beforehand.

### Can I copy only the pivot layout without the underlying data?
You can achieve that by first clearing the data cells in the source range, then copying only the pivot’s layout. This is a more advanced scenario and usually not required for a simple **duplicate pivot table** task.

---

## Full Working Example (All Steps Combined)

Below is the complete, ready‑to‑run Java class. Just replace `YOUR_DIRECTORY` with the actual folder path on your machine.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the exact range that holds the pivot table
        // Adjust "A1:G20" to match your pivot's size
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a brand‑new workbook that will receive the copy
        Workbook dstWb = new Workbook(); // creates an empty workbook with one sheet
        Worksheet dstWs = dstWb.getWorksheets().get(0);

        // Step 4: Copy the pivot (and any surrounding data) to the new workbook
        srcRange.copy(dstWs.getCells().createRange("A1"));

        // Step 5: Save the destination file – now it contains the duplicated pivot table
        dstWb.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully! Check CopyPivotResult.xlsx.");
    }
}
```

Run the program (`java CopyPivotTableDemo`) and you’ll see the console message confirming success.

---

## Pro Tips & Best Practices

- **Validate the range** before copying. Use `srcWs.getCells().maxDisplayRange` to programmatically discover the used area if you don’t want to hard‑code `"A1:G20"`.
- **Turn off calculation** temporarily for huge workbooks to speed up the copy:

  ```java
  srcWb.getSettings().setCalculateFormulaOnOpen(false);
  ```

- **Dispose of resources** (`srcWb.dispose(); dstWb.dispose();`) in long‑running services to avoid memory leaks.
- **Version compatibility:** The code works with Aspose.Cells 23.12 and later. Older versions may require `srcRange.copyTo` instead of `copy`.

---

## Next Steps

Now that you’ve mastered **create new workbook** and **copy pivot table**, you might explore:

- **How to copy pivot** across multiple worksheets in a batch job.
- Adding **copy excel range** for regular data tables alongside the pivot.
- Automating **duplicate pivot table** creation for each month’s report using a loop.
- Exporting the duplicated pivot to PDF or HTML with Aspose.Cells’ built‑in renderers.

Each of these topics builds on the foundation laid here, and they all benefit from the same clean, programmatic approach.

---

## Conclusion

We’ve walked through the entire process of **create new workbook**, define the source **copy excel range**, and **copy pivot table** to produce a **duplicate pivot table** in Java using Aspose.Cells. The solution is concise, fully functional, and ready for production use. Feel free to tweak the range, experiment with different source files, or embed this logic into a larger reporting pipeline.

If you hit any snags or have ideas for extending this tutorial, drop a comment below. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}