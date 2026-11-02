---
category: general
date: 2026-06-27
description: Copy pivot table excel with Java in minutes – learn how to copy range
  to another workbook and discover how to copy pivot table efficiently.
draft: false
keywords:
- copy pivot table excel
- copy range to another workbook
- how to copy pivot table
language: en
og_description: Copy pivot table excel using Java. This guide shows how to copy range
  to another workbook and answers how to copy pivot table with a complete example.
og_title: Copy Pivot Table Excel – Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  headline: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  type: TechArticle
- description: Copy pivot table excel with Java in minutes – learn how to copy range
    to another workbook and discover how to copy pivot table efficiently.
  name: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
  steps:
  - name: Expected Result
    text: '- Opening `destination.xlsx` shows a sheet named **CopiedPivot**. - The
      sheet contains a pivot table that can be refreshed, filtered, and rearranged
      just like the original. - No error messages appear in the console, confirming
      that **copy pivot table excel** succeeded.'
  - name: What if the source workbook has multiple pivot tables?
    text: 'You can repeat the range‑selection logic for each pivot table, or you can
      copy the entire worksheet:'
  - name: How to handle external data connections?
    text: 'If your pivot table pulls data from an external database, the destination
      workbook will retain the connection string. To avoid broken links, update the
      connection after copying:'
  - name: Does this work with .xls files?
    text: Yes. Aspose.Cells abstracts the file format, so the same code works for
      `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in
      the `Workbook` constructors.
  type: HowTo
tags:
- pivot-table
- excel
- java
- aspose-cells
title: Copy Pivot Table Excel – Step‑by‑Step Guide Using Java
url: /java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy Pivot Table Excel – Java Tutorial

Ever wondered how to **copy pivot table excel** files without losing the underlying data connections? You’re not the only one. Many developers hit a wall when they try to move a pivot table from one workbook to another, only to end up with a static range or a broken reference.  

The good news? With a few lines of Java and the right library, you can **copy pivot table excel** workbooks cleanly, preserving every field, filter, and layout. In this guide we’ll also show you **how to copy pivot table** using the Aspose.Cells for Java API, and we’ll sprinkle in tips on **copy range to another workbook** for those edge‑case scenarios.

> **What you’ll walk away with:** a fully runnable program that loads a source workbook, copies the pivot‑table‑containing range, and saves a new workbook that looks exactly like the original.

## Prerequisites

Before we dive in, make sure you have:

- Java 17 or newer (the code compiles with any recent JDK).
- Aspose.Cells for Java 23.10 or later – the free trial works fine for testing.
- A source Excel file (`source.xlsx`) that already contains a pivot table on the first worksheet.
- An IDE or a simple command‑line build setup (Maven/Gradle).

No other external dependencies are required.

## Step 1: Set Up the Project and Import Classes

First, create a Maven project (or Gradle, if you prefer) and add the Aspose.Cells dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Now import the classes we’ll need:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **Pro tip:** Keep your `src/main/resources` folder tidy; place `source.xlsx` there and reference it with a relative path to avoid hard‑coding absolute directories.

## Step 2: Load the Source Workbook that Contains the Pivot Table

The first line of any **copy pivot table excel** operation is to load the workbook that holds the pivot table you want to duplicate.

```java
// Step 2: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
```

Why do we load the whole workbook instead of just the sheet? Because the pivot cache lives at the workbook level; copying only the sheet would break the cache and your pivot table would turn into a plain range.

## Step 3: Grab the Worksheet and Define the Pivot‑Table Range

Next, we locate the worksheet and the exact cell block that encloses the pivot table. In most cases the pivot table starts at `A1`, but you should adjust the range to match your file.

```java
// Step 3: Access the worksheet where the pivot table resides
Worksheet srcWs = srcWb.getWorksheets().get(0);

// Define the range that includes the pivot table (e.g., A1:E20)
Range srcRange = srcWs.getCells().createRange("A1:E20");
```

If you’re unsure about the range, you can let Aspose.Cells calculate the used cells:

```java
int maxRow = srcWs.getCells().getMaxDataRow();
int maxCol = srcWs.getCells().getMaxDataColumn();
String autoRange = String.format("A1:%s%d",
        CellsHelper.columnIndexToName(maxCol), maxRow + 1);
Range srcRange = srcWs.getCells().createRange(autoRange);
```

That little snippet is handy when you need to **copy range to another workbook** without hard‑coding the address.

## Step 4: Create the Destination Workbook

Now we spin up a fresh workbook that will receive the copied pivot table. This is the heart of **how to copy pivot table**—you create a clean slate and then paste the range.

```java
// Step 4: Create a new destination workbook (or load an existing one)
Workbook dstWb = new Workbook(); // empty workbook by default
```

If you already have a template file you want to enrich, just replace the constructor with `new Workbook("template.xlsx")`.

## Step 5: Add a Worksheet to the Destination Workbook

Even though a new `Workbook` already contains one default sheet, we’ll add a second sheet to demonstrate the process of copying to a specific location.

```java
// Step 5: Add a new worksheet to the destination workbook
Worksheet dstWs = dstWb.getWorksheets().add();
```

You can rename the sheet for clarity:

```java
dstWs.setName("CopiedPivot");
```

## Step 6: Copy the Range – Pivot Table Is Preserved

Here’s the magic line that actually **copy range to another workbook** while keeping the pivot table intact. The `CopyOptions` object tells Aspose.Cells to preserve everything, including the pivot cache.

```java
// Step 6: Copy the range—pivot table is preserved—to the new worksheet at A1
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);
dstWs.getCells().copyRange(srcRange, "A1", copyOptions);
```

Why do we set `PasteType.PASTE_ALL`? Because the default paste operation only copies values and formatting, discarding the pivot cache. By explicitly requesting `PASTE_ALL`, we ensure the destination workbook receives a fully functional pivot table.

## Step 7: Save the Destination Workbook

Finally, write the new file to disk. After this step you can open `destination.xlsx` in Excel and see the pivot table exactly as it appeared in the source file.

```java
// Step 7: Save the destination workbook with the copied pivot table
dstWb.save("src/main/resources/destination.xlsx");
```

### Expected Result

- Opening `destination.xlsx` shows a sheet named **CopiedPivot**.
- The sheet contains a pivot table that can be refreshed, filtered, and rearranged just like the original.
- No error messages appear in the console, confirming that **copy pivot table excel** succeeded.

## Common Questions & Edge Cases

### What if the source workbook has multiple pivot tables?

You can repeat the range‑selection logic for each pivot table, or you can copy the entire worksheet:

```java
srcWs.getCells().copy(dstWs.getCells());
```

Copying the whole sheet also moves all pivot caches, making it a quick way to **copy range to another workbook** when you have many tables.

### How to handle external data connections?

If your pivot table pulls data from an external database, the destination workbook will retain the connection string. To avoid broken links, update the connection after copying:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
pt.getPivotCache().setExternalDataSource("newConnectionString");
```

### Does this work with .xls files?

Yes. Aspose.Cells abstracts the file format, so the same code works for `.xls`, `.xlsx`, `.xlsb`, and even `.ods`. Just change the file extension in the `Workbook` constructors.

## Full Working Example

Putting it all together, here’s a ready‑to‑run Java class that demonstrates **how to copy pivot table** from one workbook to another:

```java
import com.aspose.cells.*;

public class CopyPivotTableExcel {
    public static void main(String[] args) throws Exception {
        // Load source workbook containing the pivot table
        Workbook srcWb = new Workbook("src/main/resources/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Determine the used range automatically (covers the pivot table)
        int maxRow = srcWs.getCells().getMaxDataRow();
        int maxCol = srcWs.getCells().getMaxDataColumn();
        String rangeAddress = String.format("A1:%s%d",
                CellsHelper.columnIndexToName(maxCol), maxRow + 1);
        Range srcRange = srcWs.getCells().createRange(rangeAddress);

        // Create destination workbook and add a sheet
        Workbook dstWb = new Workbook();
        Worksheet dstWs = dstWb.getWorksheets().add();
        dstWs.setName("CopiedPivot");

        // Copy the range with all pivot information preserved
        CopyOptions opts = new CopyOptions();
        opts.setPasteType(PasteType.PASTE_ALL);
        dstWs.getCells().copyRange(srcRange, "A1", opts);

        // Save the result
        dstWb.save("src/main/resources/destination.xlsx");
        System.out.println("Pivot table copied successfully!");
    }
}
```

Run the class, open `destination.xlsx`, and you’ll see the exact replica of the original pivot table. 🎉

## Conclusion

We’ve just walked through a complete **copy pivot table excel** workflow using Java. By loading the source workbook, pinpointing the pivot‑table range, and employing `CopyOptions` with `PASTE_ALL`, you can reliably **copy range to another workbook** while preserving every pivot feature.  

If you’re curious about **how to copy pivot table** in other languages, the same concepts apply—just swap the Aspose.Cells SDK for the appropriate platform. Next, you might explore programmatically refreshing the copied pivot table, or exporting it to PDF for reporting purposes.  

Got a twist on this scenario? Maybe you need to copy a chart that’s linked to a pivot table, or you want to batch‑process dozens of files. Those topics are natural extensions of what we covered today.  

Give the code a spin, tweak the range, and let your Excel automation adventures begin. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}