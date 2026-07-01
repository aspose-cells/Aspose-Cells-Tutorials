---
category: general
date: 2026-06-30
description: Set font bold while importing a DataTable to Excel using Java. Learn
  conditional formatting code, import datatable excel and style tables effortlessly.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: en
og_description: Set font bold in Java when exporting a DataTable to Excel. This guide
  covers conditional formatting code, import datatable excel, and styling the table.
og_title: Set Font Bold in Java Excel Export – Step‑by‑Step Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Set Font Bold in Java Excel Export – Complete Guide
url: /java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Font Bold in Java Excel Export – Complete Guide

Ever wondered **how to set font bold** for specific columns while you **import datatable excel** files? You’re not the only one. Many developers hit a wall when they need a nicely‑styled spreadsheet without manually tweaking each cell. The good news? With a few lines of Java you can import a `DataTable`, apply bold fonts, and even sprinkle in some **conditional formatting code**—all programmatically.

In this tutorial we’ll walk through a full, runnable example that shows **how to import datatable** into an Excel workbook, apply **set font bold** on every even‑indexed column, and optionally add a simple conditional format. By the end you’ll have a ready‑to‑run snippet and a clear understanding of **import table with styles** for any project.

## Prerequisites

- Java 8 or newer (the code works on Java 17 as well)  
- Aspose.Cells for Java (free trial version is fine) – add the Maven dependency or the JAR to your classpath.  
- Basic familiarity with `java.sql` `ResultSet` → `DataTable` conversion (we’ll mock a table for simplicity).  
- An IDE or a build tool like Maven/Gradle.

> **Pro tip:** If you’re using Maven, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Overview of the Solution

1. **Create a mock `DataTable`** that mimics data you’d normally pull from a database.  
2. **Generate a `CellStyle` array** where every even column gets a bold font – that’s the core of **set font bold**.  
3. **Grab the first worksheet** from the workbook.  
4. **Import the `DataTable`** with column headers, starting at cell `A1`, and apply the prepared styles.  
5. (Optional) **Add a conditional formatting rule** to illustrate the **conditional formatting code** keyword.

Each step is explained in plain English, and the code blocks are fully self‑contained so you can copy‑paste and run instantly.

---

## Step 1: Retrieve or Build the DataTable to Import

In real‑world apps you’d probably call `ResultSet` → `DataTable` conversion utilities. For this guide we’ll construct a simple `DataTable` manually so you can focus on the Excel part.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Why this matters:** Having a `DataTable` ready lets us focus on the **import datatable excel** API and the style logic. The method above is reusable—just replace the hard‑coded rows with a database query when you go to production.

---

## Step 2: Prepare Styles – This Is Where We **Set Font Bold**

Now we’ll build an array of `CellStyle` objects, one per column. The rule is simple: **set font bold** for every even‑indexed column (0, 2, 4,…). The odd columns stay normal.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Why Use an Array of Styles?

- **Performance:** Applying a style per column is faster than styling each cell individually.  
- **Consistency:** Every cell in a column inherits the same formatting, guaranteeing a uniform look.  
- **Scalability:** Adding more columns later only requires extending the array—no code rewrite.

---

## Step 3: Access the First Worksheet in the Workbook

Aspose.Cells creates a default worksheet for us, but it’s good practice to fetch it explicitly. This also demonstrates **how to import datatable** into a specific sheet.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## Step 4: Import the DataTable with Styles – The Core **Import Table With Styles** Operation

The `importDataTable` method does the heavy lifting. It copies the data, adds column headers, and applies the style array we built earlier.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

When you run the example, you’ll see **set font bold** applied to columns `ID` and `Score`, while `Name` stays regular.

---

## Step 5 (Optional): Add Conditional Formatting – A Quick **Conditional Formatting Code** Example

If you want to highlight rows where the score exceeds 90, a few extra lines will do the trick. This showcases the **conditional formatting code** keyword without derailing the main flow.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Note:** The above snippet is optional but demonstrates how you can layer **conditional formatting code** on top of the already‑styled table.

---

## Putting It All Together – Full, Runnable Example

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Implement Custom Font Settings in Aspose.Cells Java for Excel Formatting](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Set Font Size in Excel Using Aspose.Cells Java - Comprehensive Guide](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}