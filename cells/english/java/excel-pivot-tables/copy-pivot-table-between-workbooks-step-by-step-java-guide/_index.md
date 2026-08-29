---
category: general
date: 2026-07-14
description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
  copy Excel range, and export pivot table in minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- copy range between workbooks
- export pivot table
language: en
lastmod: 2026-07-14
og_description: Copy pivot table in Java quickly. This guide shows how to copy pivot,
  copy Excel range, and export pivot table with Aspose.Cells.
og_image_alt: Diagram illustrating copy pivot table process between two Excel workbooks
og_title: Copy Pivot Table Between Workbooks – Java Automation Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Copy pivot table between workbooks using Java. Learn how to copy pivot,
    copy Excel range, and export pivot table in minutes.
  headline: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide
url: /java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy Pivot Table Between Workbooks – Complete Java Tutorial

Ever needed to **copy pivot table** from one workbook to another and wondered why the usual copy‑paste tricks keep breaking the layout? You're not alone. In many reporting pipelines the pivot lives in a master file, but downstream processes demand a lightweight copy.  

In this guide we’ll walk through a clean, programmatic way to duplicate a pivot—no manual fiddling required. By the end you’ll know **how to copy pivot**, how to **copy Excel range** safely, and even how to **export pivot table** to a new file, all with Aspose.Cells for Java.

## What You'll Build

- Load a source workbook that already contains a pivot table.  
- Create (or open) a destination workbook.  
- Define the exact range that houses the pivot.  
- Copy that range—including the pivot definition—into the new workbook.  
- Save the result so other apps can open it without losing any calculations.

No external tools, no VBA, just pure Java code that you can drop into any Maven or Gradle project.

## Prerequisites

- Java 17 or later (the code works on Java 8+, but newer JDKs give you better performance).  
- Aspose.Cells for Java 23.9 or newer – add the dependency from Maven Central.  
- Two Excel files: `SourceWithPivot.xlsx` (contains the pivot) and an empty placeholder for the copy.  

If you’re new to Aspose.Cells, the library abstracts the low‑level OOXML details, letting you treat worksheets like regular Java objects.

## Step 1: Set Up Your Project

First, add the Aspose.Cells Maven artifact to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust if you use a different JDK -->
</dependency>
```

Or, for Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.9:jdk17'
```

> **Pro tip:** If you’re using an IDE like IntelliJ, let it auto‑import the library; it saves a lot of typing.

## Step 2: Load the Source Workbook

We need a `Workbook` instance that points to the file holding the pivot. The constructor reads the entire file into memory, so you can work with it offline.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {

        // Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Why load it first? Because the pivot’s cache, field list, and layout are all stored inside the sheet. Pulling the workbook into memory guarantees we copy the *definition* and not just the rendered values.

## Step 3: Create or Open the Destination Workbook

You have two choices: start with a brand‑new workbook, or open an existing template. Here we’ll create a blank one, which is the most common scenario when you need a clean copy.

```java
        // Create an empty destination workbook (or open an existing one)
        Workbook destinationWorkbook = new Workbook(); // blank workbook with a default sheet
```

If you later decide to copy into a specific sheet, just replace `getWorksheets().get(0)` with the appropriate index or name.

## Step 4: Define the Exact Range That Holds the Pivot

A pivot table usually occupies a rectangular block. The safest approach is to specify the top‑left and bottom‑right cells explicitly. In our example the pivot lives from **A1** to **H30**.

```java
        // Define the range in the source sheet that includes the pivot table
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                     // first worksheet
                                          .getCells()
                                          .createRange("A1:H30");
```

> **Why not use `copyRows`?**  
> `copyRows` copies raw cell values but discards the underlying pivot cache. By copying the whole range, Aspose.Cells preserves the pivot’s metadata, allowing the destination to retain full interactivity.

## Step 5: Copy the Range (Including the Pivot) to the Destination

Now the magic happens. The `copy` method clones everything—values, formulas, formats, and the pivot object itself—into the target location.

```java
        // Copy the defined range (with the pivot table) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)               // destination sheet
                                            .getCells()
                                            .createRange("A1"));
```

If you need to paste into a different cell, just change `"A1"` to `"C5"` or any address you like. The method automatically adjusts internal references so the pivot continues to work.

## Step 6: Save the Destination Workbook

Finally, write the new workbook to disk. The resulting file can be opened in Excel, LibreOffice, or any other spreadsheet viewer, and the pivot will behave exactly as it did in the source.

```java
        // Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");
    }
}
```

### Expected Result

- `CopyPivotResult.xlsx` opens with a fully functional pivot table identical to the original.  
- All slicers, filters, and calculated fields remain intact.  
- No data loss—values are calculated on‑the‑fly when you refresh the pivot.

## Common Variations & Edge Cases

| Situation | What to Adjust |
|-----------|----------------|
| **Copy into an existing workbook** | Load the target workbook instead of creating a new one: `new Workbook("ExistingFile.xlsx")`. |
| **Pivot spans an unknown size** | Use `Worksheet.getPivotTables().get(0).getPivotTableRange()` to retrieve the exact address programmatically. |
| **Preserve data connections** | After copying, call `destinationWorkbook.getWorksheets().get(0).getPivotTables().get(0).setRefreshOnLoad(true);` to keep external data links alive. |
| **Export pivot table as CSV** | Once copied, you can call `destinationWorkbook.save("PivotExport.csv", SaveFormat.CSV);` – this flattens the pivot values only. |

> **Watch out for:** When the source and destination workbooks use different locale settings, number formats may shift. Explicitly set the workbook’s `setLocale` if you need consistency.

## Full Working Example (All Imports Included)

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load source workbook containing the pivot
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Create (or open) destination workbook
        Workbook destinationWorkbook = new Workbook(); // blank workbook

        // 3️⃣ Identify the range that encloses the pivot table
        //    If you don't know the range, you can retrieve it via:
        //    PivotTable pt = sourceWorkbook.getWorksheets().get(0).getPivotTables().get(0);
        //    String address = pt.getPivotTableRange().getRefersTo();
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:H30");

        // 4️⃣ Copy the range (pivot included) to the destination sheet
        sourceRange.copy(destinationWorkbook.getWorksheets()
                                            .get(0)
                                            .getCells()
                                            .createRange("A1"));

        // 5️⃣ Persist the result
        destinationWorkbook.save("YOUR_DIRECTORY/CopyPivotResult.xlsx");

        System.out.println("Pivot table copied successfully!");
    }
}
```

Run the program, open `CopyPivotResult.xlsx`, and you’ll see the exact same pivot you started with—ready for further analysis or distribution.

## Recap

We just demonstrated **how to copy pivot** from one workbook to another using Aspose.Cells for Java. The steps covered loading the source, defining the exact **copy Excel range**, performing the copy, and finally **export pivot table** to a new file. By handling the range rather than individual cells, we guarantee the pivot’s internal cache travels with it, keeping the report dynamic.

## What to Explore Next

- **Automate refresh**: Schedule the copy operation with a Quartz job so your downstream files stay up‑to‑date.  
- **Copy multiple pivots**: Loop through `sourceWorkbook.getWorksheets().get(0).getPivotTables()` and copy each one to separate sheets.  
- **Apply styling**: Use `Style` objects to harmonize fonts and colors across the destination workbook.  

If you’ve got questions about handling large workbooks or preserving external data sources, drop a comment below. Happy coding, and enjoy the freedom of programmatic Excel automation!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Automate Excel Pivot Table Styling and Saving with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}