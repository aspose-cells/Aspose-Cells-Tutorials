---
category: general
date: 2026-07-16
description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
  Learn how to export Excel formulas to text and save worksheet as txt file.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: en
lastmod: 2026-07-16
og_description: Set custom cell separator in Aspose.Cells lets you export Excel table
  to TXT with exact formatting. Export Excel formulas to text and save worksheet as
  txt file easily.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Set Custom Cell Separator – Export Excel Table to TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Set Custom Cell Separator – Export Excel Table to TXT
url: /java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Custom Cell Separator – Export Excel Table to TXT

Set custom cell separator is the secret sauce you need when you want a tidy text dump from an Excel sheet. Ever wondered how to **export excel table to txt** without ending up with a jumbled mess of commas and line‑breaks? In this tutorial we’ll walk through the whole process using Aspose.Cells for Java, from loading a workbook to **save worksheet as txt file** with a delimiter you choose.

## What You’ll Learn

- How to **set custom cell separator** for text exports.
- The exact steps to **export excel formulas to text** so the evaluated values travel with you.
- Ways to **export excel data as plain text** while preserving layout.
- A complete, ready‑to‑run code sample that you can copy‑paste into your project.

By the end of this guide you’ll be able to take any Excel workbook, pick a pipe (`|`), a tab (`\t`), or any character you like, and produce a clean, delimited text file that downstream systems love.

### Prerequisites

- Java 8 or newer installed.
- Maven (or any build tool) to pull in the Aspose.Cells for Java library.
- A sample workbook (`TableDemo.xlsx`) that contains a table with formulas.

If you’ve got those, let’s dive in—no extra fluff, just practical steps.

## Step 1: Add Aspose.Cells to Your Project

Before you can **set custom cell separator**, you need the Aspose.Cells JAR on the classpath. The easiest way is via Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

If you prefer Gradle, swap the XML for the equivalent `implementation 'com.aspose:aspose-cells:24.10'`. Once the dependency is resolved, you’re ready to write Java code that talks to Excel files.

## Step 2: Load the Workbook – Preparing to Export Excel Table to TXT

The first real code line is always the same: open the workbook that holds the table you want to export.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Here we grab the first worksheet (`get(0)`). If your data lives on a different sheet, just change the index or use `get("SheetName")`. This part is essential for **export excel table to txt** because the exporter works at the worksheet level.

## Step 3: Set Custom Cell Separator – The Core of Exporting

Now comes the star of the show: configuring `ExportTableOptions`. This object lets you decide exactly how each cell appears in the final text file.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Why do we **set custom cell separator**? Because the default separator is a tab, which may clash with data that already contains tabs. By picking a pipe (`|`) or a semicolon, you guarantee that each column stays distinct when a downstream parser reads the file.

### Export Excel Formulas to Text

The line `setFormulaValueInCell(true)` tells Aspose.Cells to write the **export excel formulas to text** as the *result* of the formula, not the formula string itself. If you omitted this, a cell containing `=SUM(A1:A5)` would appear as `=SUM(A1:A5)` in the TXT, which is rarely what you want.

## Step 4: Attach Export Options to TXT Save Options

Now we bind those table options to the overall TXT export configuration.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` is the umbrella object that controls how the entire worksheet is written out. By plugging `exportTableOptions` into it, you ensure every table on the sheet respects the **set custom cell separator** rule.

## Step 5: Save the Worksheet as TXT File – Finishing the Export

Finally, we write the file to disk.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Running this program creates `TableExported.txt`. Each row of the original Excel table will now appear as a line of pipe‑separated values, like:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Notice how the formula in the **Total** column was evaluated before being written—thanks to `setFormulaValueInCell(true)`. That’s the essence of **export excel data as plain text** while preserving calculated results.

## Step 6: Verify the Output – Does It Look Right?

Open the generated `TableExported.txt` in any text editor. You should see:

- One line per Excel row.
- Columns separated by the pipe character you set with `setCellValueSeparator`.
- No stray commas or tabs unless they were part of the original cell values.
- Formula results, not the formulas themselves.

If you spot any unexpected characters, double‑check the separator you chose. Some characters (like the pipe) are safe for most CSV‑style parsers, but if your data already contains pipes, consider a different delimiter such as `~` or a tab (`\t`).

## Tips, Edge Cases, and Best Practices – Export Excel Data as Plain Text

| Situation | What to Do |
|-----------|------------|
| **Data already contains your chosen separator** | Switch to a less common character (`^`, `~`, or Unicode non‑printing chars). |
| **You need UTF‑8 encoding**


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}