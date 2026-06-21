---
category: general
date: 2026-06-21
description: Export XLSX as CSV in Java quickly. Learn to convert Excel to CSV, save
  workbook as CSV, and how to set CSV delimiter with a custom separator.
draft: false
keywords:
- export xlsx as csv
- convert excel to csv
- save workbook as csv
- convert spreadsheet to csv
- how to set csv delimiter
language: en
og_description: Export XLSX as CSV in Java. This guide shows how to convert Excel
  to CSV, set a custom delimiter, and save workbook as CSV with Aspose.Cells.
og_title: Export XLSX as CSV – Full Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Export XLSX as CSV in Java quickly. Learn to convert Excel to CSV,
    save workbook as CSV, and how to set CSV delimiter with a custom separator.
  headline: Export XLSX as CSV – Complete Java Guide
  type: TechArticle
tags:
- Java
- Excel
- CSV
- Aspose.Cells
title: Export XLSX as CSV – Complete Java Guide
url: /java/excel-import-export/export-xlsx-as-csv-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export XLSX as CSV – Complete Java Guide

Ever wondered how to **export XLSX as CSV** without fiddling with manual copy‑pastes? You're not the only one. Whether you need to feed data into a legacy system, feed a data‑warehouse pipeline, or just give a non‑technical colleague a simple text file, converting Excel to CSV is a daily chore for many developers.

In this tutorial we’ll walk through a clean, production‑ready way to **export XLSX as CSV** using Java. You’ll see exactly how to **save workbook as CSV**, how to **convert spreadsheet to CSV** with a custom column separator, and we’ll answer the burning question **how to set CSV delimiter** so your downstream parser never complains again.

---

## What You’ll Learn

* Load an `.xlsx` workbook from disk (or a stream)  
* Configure export options – including **how to set CSV delimiter**  
* Write the file out as **CSV** with a single method call  
* Common pitfalls when you **convert Excel to CSV** and how to avoid them  

No external CLI tools, no Excel installation required – just pure Java code.

---

## Prerequisites

| Requirement | Reason |
|-------------|--------|
| Java 8 or newer | The Aspose.Cells API we’ll use targets Java 8+. |
| Aspose.Cells for Java (free trial or licensed) | Handles the heavy lifting of reading XLSX and writing CSV. |
| An `.xlsx` file to test with (e.g., `data.xlsx`) | Gives us something concrete to export. |
| A build tool (Maven/Gradle) or plain `javac` | To compile and run the example. |

If you haven’t added Aspose.Cells to your project yet, drop this snippet into your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Or, for Gradle:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

---

## Step 1: Load the Workbook (Export XLSX as CSV – Start)

The first thing you need to do is bring the Excel file into memory. Aspose.Cells represents every spreadsheet as a `Workbook` object.

```java
import com.aspose.cells.*;

public class ExcelToCsvDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from an Excel file
        Workbook workbook = new Workbook("YOUR_DIRECTORY/data.xlsx");
        // Continue with export options...
```

> **Why this matters:** Loading the workbook validates that the file is a proper XLSX and gives you access to all worksheets, styles, and formulas. Skipping this step would make it impossible to **convert spreadsheet to CSV** reliably.

---

## Step 2: Configure Export Options – How to Set CSV Delimiter

By default Aspose.Cells writes CSV files using a comma (`,`). If your downstream system expects a pipe (`|`) or a semicolon (`;`), you must tell the library **how to set CSV delimiter**. The `ExportTableOptions` class is where the magic happens.

```java
        // Create export options for CSV conversion
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // Export all cell values as strings
        exportOptions.setCustomSeparator("|");          // Use a custom column separator (pipe)
```

A few notes on the flags:

* `setExportAsString(true)` forces numeric cells to be rendered exactly as they appear in Excel, preventing rounding surprises.
* `setCustomSeparator("|")` is the answer to **how to set CSV delimiter**; replace `"|"` with any character you need.

> **Pro tip:** If you need to preserve line breaks inside a cell, also call `exportOptions.setQuoteAllFields(true)` – it wraps every field in double quotes, keeping CSV parsers happy.

---

## Step 3: Save the Workbook as CSV – The Core “Export XLSX as CSV” Action

Now that we have a workbook and a fully‑configured options object, writing the CSV is a one‑liner.

```java
        // Save the workbook as a CSV file using the configured options
        workbook.save("YOUR_DIRECTORY/data.csv", SaveFormat.CSV, exportOptions);
        System.out.println("Export completed: data.csv");
    }
}
```

When you run the program, you’ll end up with `data.csv` that looks something like this (assuming a pipe delimiter):

```
Name|Age|Country
Alice|30|USA
Bob|25|Canada
```

> **Why this works:** `workbook.save` respects the `ExportTableOptions` we passed, so the output file follows the exact delimiter we specified. This is the cleanest way to **save workbook as CSV** without manually looping over rows and columns.

---

## Advanced: Converting Multiple Worksheets

Sometimes an XLSX contains several sheets, and you need each as a separate CSV. Here’s a quick pattern:

```java
        for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
            Worksheet sheet = workbook.getWorksheets().get(i);
            // Set the sheet you want to export
            exportOptions.setExportSheetIndex(i);
            String csvPath = String.format("YOUR_DIRECTORY/%s.csv", sheet.getName());
            workbook.save(csvPath, SaveFormat.CSV, exportOptions);
            System.out.println("Exported sheet '" + sheet.getName() + "' to " + csvPath);
        }
```

Notice we reuse the same `ExportTableOptions` object, only swapping the `ExportSheetIndex`. This keeps the code DRY and demonstrates another way to **convert spreadsheet to CSV** efficiently.

---

## Common Pitfalls When You Convert Excel to CSV

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| **Locale‑dependent decimal separator** | Numbers appear as `1,23` instead of `1.23` | Force `exportOptions.setExportAsString(true)` or set `WorkbookSettings.setCultureInfo(CultureInfo.InvariantCulture)`. |
| **Hidden columns/rows still appear** | CSV contains data you thought was hidden | Use `exportOptions.setExportHiddenColumns(false)` and `setExportHiddenRows(false)`. |
| **Formulas instead of values** | CSV shows `=SUM(A1:A5)` | Ensure `exportOptions.setExportFormulaValue(true)`. |
| **Incorrect delimiter** | Target system rejects the file | Double‑check `setCustomSeparator` matches the receiving parser; remember to escape special characters if needed. |

Addressing these issues early saves you from frustrating downstream bugs when you **convert Excel to CSV**.

---

## Full Source Code – Ready to Copy & Paste

Below is the complete, self‑contained program that you can drop into any Java project.

```java
import com.aspose.cells.*;

public class ExcelToCsvDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the workbook (export xlsx as csv start)
        // -------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/data.xlsx");

        // -------------------------------------------------
        // 2️⃣ Configure export options – how to set csv delimiter
        // -------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);          // Keep cell formatting as text
        exportOptions.setCustomSeparator("|");          // Custom delimiter (pipe)
        exportOptions.setQuoteAllFields(true);          // Optional: quote every field
        exportOptions.setExportHiddenColumns(false);    // Skip hidden columns
        exportOptions.setExportHiddenRows(false);       // Skip hidden rows
        exportOptions.setExportFormulaValue(true);      // Export calculated values

        // -------------------------------------------------
        // 3️⃣ Save the workbook as CSV (save workbook as csv)
        // -------------------------------------------------
        workbook.save("YOUR_DIRECTORY/data.csv", SaveFormat.CSV, exportOptions);
        System.out.println("✅ Export completed: data.csv");
    }
}
```

Compile and run:

```bash
javac -cp "path/to/aspose-cells-24.10.jar" ExcelToCsvDemo.java
java -cp ".:path/to/aspose-cells-24.10.jar" ExcelToCsvDemo
```

You should see the confirmation message and find `data.csv` beside your source file.

---

## Visual Overview

![Diagram showing export xlsx as csv process](image.png "Export XLSX as CSV workflow diagram")

*Alt text:* Diagram showing **export xlsx as csv** process – load workbook, set custom separator, save as CSV.

---

## Next Steps & Related Topics

* **Stream‑based conversion** – If you’re dealing with large files, use `Workbook.load(InputStream)` and `workbook.save(OutputStream, ...)` to avoid hitting the file system.
* **Encoding control** – Call `exportOptions.setEncoding(Encoding.getUTF8())` when you need UTF‑8 output for multilingual data.
* **Batch processing** – Combine the multi‑sheet loop with a directory scan to **convert Excel to CSV** en‑masse.
* **Other formats** – Aspose.Cells also supports **convert spreadsheet to TSV**, **HTML**, or even **JSON** with similar one‑liner calls.

---

## Conclusion

You now have a solid, end‑to‑end solution to **export XLSX as CSV** in Java. By loading the workbook, tweaking `ExportTableOptions` (the answer to **how to set CSV delimiter**), and calling `save`, you can reliably **convert Excel to CSV**, **save workbook as CSV**, and even **convert spreadsheet to CSV** for every sheet in a file.  

Give it a spin, tweak the delimiter to suit your downstream parser, and you’ll see how painless data interchange can be. Got questions, edge‑case scenarios, or want to share a clever tweak? Drop a comment below—happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Load and Save Excel as CSV Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Trim & Save Excel Files as CSV Using Aspose.Cells in Java](/cells/english/java/workbook-operations/excel-aspose-cells-java-trim-save-csv/)
- [Convert Excel to CSV using Aspose.Cells .NET: A Complete Guide](/cells/english/net/workbook-operations/load-save-excel-csv-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}