---
category: general
date: 2026-09-11
description: Create new worksheet and copy Excel range using Aspose.Cells. Learn how
  to copy range between sheets while preserving pivot tables.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: en
lastmod: 2026-09-11
og_description: Create new worksheet and copy Excel range with Aspose.Cells. This
  tutorial shows the exact steps to copy range between sheets and keep pivot tables
  intact.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Create new worksheet and copy Excel range – Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Create new worksheet and copy Excel range with Aspose.Cells
url: /java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create new worksheet and copy Excel range with Aspose.Cells

If you need to **create new worksheet** and move data around in an Excel file, Aspose.Cells makes it straightforward. This guide shows exactly how to copy an Excel range from one sheet to another while preserving any pivot tables inside the range.

You’ll learn how to **copy excel range**, how to **copy range between sheets**, and why the Aspose.Cells `copy` method keeps pivot table definitions intact. No external tools are required—just a Java project with the Aspose.Cells library.

## Prerequisites

Before you start, make sure you have:

- Java 17 or later installed
- Aspose.Cells for Java (version 23.12 or newer) added to your project’s classpath
- A source workbook (`input.xlsx`) that contains a pivot table in the range you want to copy
- Basic familiarity with Java syntax and Maven/Gradle dependency management

## Step 1: Set up the project and import Aspose.Cells

Create a simple Maven project (or Gradle, if you prefer) and add the Aspose.Cells dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Then import the required classes in your Java source file:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Why this step matters*: Importing the correct classes gives you access to `Workbook`, `Worksheet`, `Range`, and the `copy` method that will handle the range transfer.

## Step 2: Load the source workbook

Open the workbook that contains the data you want to copy. The following code loads `input.xlsx` from a directory you specify:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explanation*: `Workbook` represents the entire Excel file. Loading it once gives you read/write access to every sheet and cell collection.

## Step 3: Identify the source range that includes the pivot table

Select the worksheet that holds the pivot table and define the exact cell block you want to copy. In this example we copy cells A1 through D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Why this matters*: By creating a `Range` object, you tell Aspose.Cells exactly which cells (including any embedded objects like pivot tables) should be duplicated.

## Step 4: **Create new worksheet** that will receive the copied data

Now we add a fresh sheet to the same workbook. This is the point where the primary keyword appears:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explanation*: Adding a new sheet isolates the copied data, making it easy to verify that the **copy excel range** operation succeeded without affecting the original sheet.

## Step 5: Copy the range – the pivot table is preserved automatically

Use the `copy` method to move the range from the source sheet to the destination sheet. Aspose.Cells copies formulas, formatting, and pivot‑table definitions:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Why this works*: The `copy` method performs a deep copy of the source cells. It does not merely copy values; it replicates the entire cell structure, which includes the pivot cache. This is why you can **copy range aspose.cells** and still see a functional pivot table on the new sheet.

## Step 6: Save the workbook with the new worksheet

Finally, write the modified workbook to disk:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Result*: `output.xlsx` now contains the original sheet plus a new sheet called **Copy** that holds the exact same range, pivot table included.

## Full working example

Putting all the pieces together, here is the complete, runnable program:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected output**: Open `output.xlsx` in Excel. You will see a sheet named **Copy** whose cells A1:D20 contain the same data, formatting, and an active pivot table identical to the original.

## Common questions and edge cases

- **What if the source range contains merged cells?**  
  The `copy` method also copies merge information, so merged cells appear unchanged on the destination sheet.

- **Can I copy to a different workbook?**  
  Yes. Load a second `Workbook` instance, create a destination range in that workbook, and call `sourceRange.copy(destinationRange)`. The method handles cross‑workbook copying automatically.

- **What if the destination sheet already has data?**  
  The copy operation overwrites any existing cells that intersect the destination range. To avoid data loss, ensure the destination area is empty or use a different start cell (e.g., `"B2"`).

- **Is the pivot cache duplicated?**  
  Aspose.Cells reuses the original pivot cache, which means the new pivot table remains linked to the same source data. If you need an independent cache, you must recreate the pivot table after copying.

## Tips and best practices

- **Pro tip**: Use `Workbook.setForceFormulaRecalculation(true)` before saving if your range contains formulas that depend on data outside the copied block.
- **Watch out for** large ranges: copying massive sheets can consume significant memory. Consider copying in smaller chunks if you hit `OutOfMemoryError`.
- **Performance tip**: Disable screen updating (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) when working with very large files to speed up the copy process.

## Conclusion

You now know how to **create new worksheet** and **copy excel range** between sheets using Aspose.Cells, preserving pivot tables and all cell attributes. This technique lets you programmatically duplicate data blocks, build report templates, or restructure workbooks without manual copy‑paste.

Next, explore related topics such as **copy range aspose.cells** for cross‑workbook operations, automating pivot‑table refreshes, or exporting the copied sheet to PDF. Experiment with different source ranges and sheet names to fit your specific automation scenario. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}