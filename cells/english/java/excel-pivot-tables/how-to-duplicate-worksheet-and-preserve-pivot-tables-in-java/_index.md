---
category: general
date: 2026-08-17
description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
  pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: en
lastmod: 2026-08-17
og_description: How to duplicate worksheet in Java using Aspose.Cells, preserving
  the pivot table, copying pivot to a new workbook, and creating a workbook from a
  sheet—all steps explained.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: How to duplicate worksheet and keep pivot tables – Java guide
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: How to duplicate worksheet and preserve pivot tables in Java
url: /java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to duplicate worksheet and preserve pivot tables in Java

How to duplicate worksheet while keeping its pivot table intact is a frequent need when you automate Excel reporting. This guide shows you how to copy pivot to a new workbook using Aspose.Cells for Java, and also covers how to preserve pivot when you create a workbook from a sheet.

You’ll learn how to load an existing workbook, duplicate the worksheet that contains a pivot table, and save the result as a fresh file. The tutorial assumes you have a basic Java development environment and a valid Aspose.Cells license (the free evaluation works for testing). No external tools are required beyond the Aspose.Cells JAR.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit (JDK) 8 or newer.
* Maven or Gradle to manage the Aspose.Cells dependency.
* An Excel file (`source.xlsx`) that contains at least one pivot table on the first worksheet.
* A directory where you can read the source file and write the duplicated workbook.

Add the Aspose.Cells dependency to your `pom.xml` (Maven) or `build.gradle` (Gradle). For Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## How to duplicate worksheet with a pivot table

The core operation is a three‑step process: load, copy, and save. Each step is explained below.

### Step 1 – Load the workbook that contains the pivot table

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Why this step matters*: The `Workbook` object represents the entire Excel file. By retrieving the first worksheet (`get(0)`), you target the sheet that holds the pivot table you intend to duplicate.

### Step 2 – Create a new workbook and duplicate the entire worksheet

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` clones the worksheet **including** all embedded objects, formulas, and pivot caches. This is the recommended way to **how to copy pivot** because the pivot definition and its data source are transferred together.

### Step 3 – Save the new workbook

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

After execution, `copy_with_pivot.xlsx` contains an exact copy of the original sheet, and the pivot table works without additional configuration.

**Expected result**: Opening `copy_with_pivot.xlsx` in Excel shows the duplicated worksheet with the same pivot layout, filters, and calculated fields as the source file.

## How to copy pivot to another workbook

If you need to move a pivot table without copying the whole sheet, you can extract the pivot cache and attach it to a new worksheet. The following snippet demonstrates that approach:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

This code answers **how to copy pivot** by copying only the pivot object, not the entire worksheet. The method `addCopy` on the `PivotTables` collection ensures the pivot cache is duplicated, satisfying **how to preserve pivot** requirements.

## How to preserve pivot when creating workbook from a sheet

Sometimes you start with a sheet that does not belong to a workbook (for example, you generate a sheet in memory). To **create workbook from sheet** while keeping the pivot, follow these steps:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

By adding the worksheet to a fresh `Workbook` after the pivot is fully defined, you guarantee that **how to preserve pivot** works even when the worksheet originated outside an existing file.

## Practical tips and common pitfalls

| Tip | Why it matters |
|-----|----------------|
| Use `addCopy` instead of `copy` | `addCopy` clones the underlying pivot cache; a plain `copy` may lose the connection to the data source. |
| Keep source and destination files on the same file system | Relative paths in the pivot’s data source resolve correctly, reducing “source not found” errors. |
| Verify the pivot’s cache after copying | Call `pivot.refresh()` if the source data changed between the copy and the save operation. |
| Dispose of workbooks when done | `sourceWorkbook.dispose();` frees native resources, which is important for large files. |

## Edge cases you might encounter

* **Multiple worksheets with inter‑dependent pivots** – Copy each worksheet individually; shared caches are duplicated automatically, but you may need to re‑assign external data connections.
* **Pivot tables based on external SQL queries** – Ensure the destination environment can reach the same database; otherwise the pivot will show “#REF!” errors.
* **Large workbooks (>100 MB)** – Use `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` to reduce memory pressure during the copy operation.

## Complete, runnable example

Below is the full program that incorporates all the steps discussed. Save it as `CopyPivotTable.java`, adjust the file paths, and run it with your preferred IDE or via `javac`/`java`.

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);

        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving the pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);

        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");

        // Optional: copy only the pivot table to a separate workbook
        PivotTable pivot = sourceWorksheet.getPivotTables().get(0);
        Workbook pivotOnlyWorkbook = new Workbook();
        Worksheet pivotSheet = pivotOnlyWorkbook.getWorksheets().add("PivotOnly");
        pivotSheet.getPivotTables().addCopy(pivot);
        pivotOnlyWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");

        // Optional: create a new workbook from a freshly built sheet with a pivot
        Worksheet tempSheet = new Worksheet();
        PivotTable newPivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");
        // Configure newPivot (data source, rows, columns, etc.) here...

        Workbook createdFromSheet =


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Implement Slicers in Pivot Tables Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}