---
category: general
date: 2026-09-21
description: Learn how to copy range in Java while preserving the pivot table. This
  step‑by‑step guide shows you how to export a pivot table safely.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: en
lastmod: 2026-09-21
og_description: How to copy range in Java while preserving the pivot table. Follow
  this complete guide to export pivot tables safely.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: How to copy range and preserve a pivot table in Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: How to copy range and preserve a pivot table in Java
url: /java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy range and preserve a pivot table in Java

If you need to **how to copy range** that contains a pivot table, this guide shows you a reliable way to keep the pivot intact. Many developers struggle with losing the pivot when they export data, but the approach below lets you **copy pivot table** data without breaking its functionality. By the end of this tutorial you’ll be able to **preserve pivot table** structure, **export pivot table** files, and understand **how to preserve pivot** in different scenarios.

The example uses Aspose.Cells for Java, a popular library for Excel automation. No additional tooling is required beyond a standard Java development environment.

## Prerequisites

Before you start, make sure you have:

* Java 17 (or later) installed.
* Maven or Gradle to manage dependencies.
* Aspose.Cells for Java (version 23.9 or newer). Add the following Maven dependency:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* A source workbook (`Source.xlsx`) that contains the pivot table you want to copy.

## How to copy range and keep the pivot table intact

The core idea is to copy the **range** that encloses the entire pivot—including its data source—using `copyRange`. This method copies both the raw data and the pivot definition, ensuring the destination workbook receives a fully functional pivot.

### Step 1: Load the source workbook

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Why this step?*  
Loading the workbook gives you access to the worksheet that hosts the pivot. The `Workbook` class abstracts the entire Excel file, while `Worksheet` provides cell‑level operations.

### Step 2: Define the range that covers the pivot table

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Why this step?*  
A pivot table is not a single cell; it spans a block that includes headers, data rows, and the pivot cache. By specifying a range that fully contains the pivot, you guarantee that `copyRange` will also copy the underlying cache, which is essential for **preserve pivot table** behavior.

### Step 3: Create an empty destination workbook

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Why this step?*  
Starting with a clean workbook prevents accidental conflicts with existing sheets or named ranges. The destination workbook will receive the copied range, effectively **export pivot table** content.

### Step 4: Copy the range – the pivot table is preserved

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Why this step?*  
`copyRange` performs a deep copy: cell values, formatting, and pivot metadata are transferred. This is the critical operation that enables **copy pivot table** without losing its functionality. The `CellArea` object defines where the range lands in the destination sheet.

### Step 5: Save the destination workbook

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Why this step?*  
Saving finalizes the **export pivot table** process. The resulting file (`DestWithPivot.xlsx`) contains a fully operational pivot that you can open in Excel, Google Sheets, or any other spreadsheet viewer.

## Verifying that the pivot table was preserved

Open `DestWithPivot.xlsx` in Excel and check the following:

1. The pivot table appears in the same location (A1:G20) as in the source.
2. Refreshing the pivot updates the data correctly, proving the cache was copied.
3. All formatting (column widths, number formats) matches the original.

If any of these checks fail, verify that the source range fully encloses the pivot and its data source. A common mistake is to select a range that stops short of the data cache, which leads to a broken pivot.

## Additional considerations

### Copy pivot table across different workbook versions

Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format. The same code works regardless of the file extension, making it a universal solution for **how to preserve pivot** across versions.

### Preserving pivot table when using a filtered source

If the source pivot is filtered, the filter state is also copied. Should you need to reset filters in the destination, call `PivotTable.refreshData()` after copying:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Export pivot table as a static snapshot

Sometimes you may want a static copy (values only) rather than a live pivot. Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)` to disable further calculations.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Handling large workbooks

For workbooks with many worksheets, limit the copy operation to the specific sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` to fine‑tune performance.

## Complete runnable example

Below is the full program you can copy, paste, and run. Adjust the file paths to match your environment.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Expected output**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

When you open `DestWithPivot.xlsx`, you should see the original pivot table fully functional, confirming that you have successfully **how to copy range** while **preserve pivot table**.

## Common pitfalls and pro tips

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Pivot appears but shows `#REF!` errors | The copied range omitted the hidden cache sheet | Extend the source range to include the entire cache (usually the rows beneath the pivot) |
| Destination workbook is larger than expected | `copyRange` also copies formatting | Use `CopyOptions` to exclude formatting if size is a concern |
| Refresh fails with “Data source not found” | Source workbook used external data connections | Replicate the connection in the destination or copy the data source sheet first |

**Pro tip:** Always run a quick `destWs.getPivotTables().size()` check after copying. If the count is zero, the range didn’t include the pivot definition and you need to expand it.

## Conclusion

In this tutorial we demonstrated **how to copy range** that contains a pivot table and guarantee that the **preserve pivot table** behavior remains intact. By loading the source workbook, defining a comprehensive range, using `copyRange`, and saving the destination file, you can reliably **export pivot table** data and answer the question **how to preserve pivot** in Java projects.

Next steps you might explore include:

* Automating the copy for multiple sheets (use the secondary keyword **copy pivot table** in a loop).
* Converting the exported workbook to CSV while keeping raw data (still **preserve pivot table** logic for the source).


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}