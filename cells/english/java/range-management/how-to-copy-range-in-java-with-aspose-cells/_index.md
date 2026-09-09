---
category: general
date: 2026-09-08
description: How to copy range in Java using Aspose.Cells – learn to copy pivot table,
  duplicate pivot table, and export pivot table while preserving formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: en
lastmod: 2026-09-08
og_description: How to copy range in Java with Aspose.Cells. This tutorial shows you
  how to copy pivot table, duplicate pivot table, and export pivot table while preserving
  formatting.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: How to copy range in Java – complete Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to copy range in Java with Aspose.Cells
url: /java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy range in Java with Aspose.Cells

If you need to **how to copy range** in Java, Aspose.Cells makes the task straightforward. Whether you’re moving a regular cell block or a full‑featured pivot table, the library handles the copy operation while keeping formulas, styles, and pivot cache intact. In this guide you’ll learn to **copy pivot table**, **duplicate pivot table**, and even **export pivot table** to a new workbook with full formatting.

The tutorial covers everything from project setup to the final verification step, so you can run the code immediately after reading. No external tools are required beyond the Aspose.Cells for Java JAR.

## Prerequisites

Before you start, make sure you have:

- Java 17 (or any supported JDK) installed and configured in your IDE.
- Maven or Gradle for dependency management (the examples use Maven).
- A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:H20`.
- Basic familiarity with Java programming.

## Step 1: Add Aspose.Cells to your project

Aspose.Cells is a commercial library, but a free evaluation version is available. Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** If you prefer Gradle, the equivalent entry is:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Adding the JAR gives you access to the `Workbook`, `Worksheet`, `Range`, and `CopyOptions` classes used throughout this guide.

## Step 2: Load the source workbook and select the first worksheet

The first part of **how to copy range** is to open the workbook that contains the data you want to move.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Why this matters:** Opening the workbook creates an in‑memory representation that the API can manipulate without touching the original file on disk.

## Step 3: Define the range that contains the pivot table

A pivot table lives inside a rectangular block. You must specify that block so Aspose.Cells knows what to copy.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Note:** The `createRange` method does **not** copy anything yet; it only creates a `Range` object that points to the cells you intend to duplicate.

## Step 4: Create a new workbook and get its first worksheet

Now create the destination workbook where the copied range will reside.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Why a new workbook?** Using a fresh file guarantees that no hidden styles or named ranges interfere with the copy operation, which is especially important when you **export pivot table** to a separate file.

## Step 5: Copy the range (including the pivot table) to the destination sheet

This is the core of **how to copy range with formatting**. The `CopyOptions` object tells Aspose.Cells to preserve everything: values, formulas, styles, and pivot cache.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Copy pivot table:** Because the source range includes the pivot table, the API automatically duplicates the pivot cache, so the new worksheet contains a fully functional pivot table that behaves exactly like the original.

## Step 6: Save the destination workbook

Finally, write the result to disk.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

When you open `dest.xlsx`, you’ll see an exact replica of the original pivot table, complete with its formatting, slicers, and calculated fields.

## Expected output

- `dest.xlsx` contains a worksheet named **Sheet1**.
- Cells `A1:H20` hold the same data and pivot table as the source.
- All cell styles (fonts, colors, borders) are preserved.
- The pivot table is fully interactive; refreshing it reflects the underlying data in the copied range.

## How to copy range with formatting – deeper dive

The previous example shows the simplest scenario, but you may encounter variations that require a slightly different approach.

### Copy pivot table to an existing workbook

If you need to **duplicate pivot table** inside a workbook that already has data, use the same `copyRange` call but point to a different destination address:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Export pivot table only (without surrounding data)

Sometimes you want just the pivot table, not the source data. Identify the pivot table’s display range via its `getPivotTable` method:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Preserve conditional formatting

Conditional formatting rules are part of the style collection. The `PasteType.ALL` flag already copies them, but you can be explicit:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Edge cases and troubleshooting

| Situation | What to watch for | Recommended fix |
|-----------|-------------------|-----------------|
| Source and destination workbooks use different Excel versions | Some newer pivot features (e.g., data model) may not render correctly | Use the latest Aspose.Cells version and set `Workbook.setFileFormatType(FileFormatType.XLSX)` for both workbooks |
| Very large pivot tables ( > 10 000 rows) cause memory pressure | Out‑of‑memory errors during copy | Enable `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` before loading |
| Destination sheet already contains a named range with the same name as the source | Name collision leads to `CopyOptions` failure | Call `copyOptions.setIgnoreNameConflicts(true)` |

## Full, runnable example

Below is the complete program you can copy‑paste into a Java class. It includes all imports, error handling, and comments.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Run the program, then open `dest.xlsx` to verify that the pivot table works exactly like the original.

## Conclusion

You now know **how to copy range** in Java using Aspose.Cells, including how to **copy pivot table**, **duplicate pivot table**, and **export pivot table** while preserving all formatting. The library abstracts away the low‑level details of Excel’s XML structure, letting you focus on business logic.

### Next steps

- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
- Automate batch processing: loop over multiple source files and consolidate their pivot tables into a summary workbook.
- Combine this technique with Aspose.Slides to generate PowerPoint reports that embed the copied pivot


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimize Pivot Table Loading in Java using Aspose.Cells – A Comprehensive Guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}