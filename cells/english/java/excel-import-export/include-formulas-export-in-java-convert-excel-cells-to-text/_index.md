---
category: general
date: 2026-07-03
description: Include formulas export in Java to convert Excel cells to text using
  Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: en
og_description: Include formulas export in Java to convert Excel cells to text. Step‑by‑step
  guide showing how to print Excel range and retrieve cell values as a string.
og_title: Include Formulas Export in Java – Convert Excel Cells to Text
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Include Formulas Export in Java – Convert Excel Cells to Text
url: /java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Include Formulas Export in Java – Convert Excel Cells to Text

Ever needed to **include formulas export** when pulling data out of an Excel workbook? Maybe you’re building a reporting service that must preserve the original formulas while still delivering a tidy text blob. In that case, you’re in the right spot. This guide walks you through converting Excel cells to plain text—*including* any embedded formulas—using Aspose.Cells for Java.

We’ll also touch on how to **print Excel range**, tweak **export table options**, and finally **get cell values string** that you can log, send over an API, or stash in a database. By the end you’ll have a fully runnable snippet and a solid grasp of the why behind each call.

## What You’ll Walk Away With

- A complete, copy‑paste‑ready Java program that reads an `.xlsx` file, selects a range, and exports it as a formatted string.
- An understanding of the `ExportTableOptions` class and why toggling `setExportAsString` and `setIncludeFormula` matters.
- Tips for handling large worksheets, dealing with different data types, and customizing the output format.
- A quick checklist for common pitfalls (think merged cells, hidden rows, and locale‑specific number formats).

### Prerequisites

- Java 17 or newer (the code compiles with older versions but we’ll stick to the latest LTS).
- Aspose.Cells for Java 23.10 (or any recent release)—you can grab it from Maven Central.
- A sample `input.xlsx` placed in a folder you control (the path is hard‑coded in the example for clarity).

If you already have those, let’s dive in.

## Step 1: Set Up the Project and Add Dependencies

First, create a Maven project (or Gradle, if you prefer). Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** If you’re using a corporate proxy, make sure the repository is reachable; otherwise the build will fail with a “Could not resolve dependencies” error.

Once Maven finishes downloading, you’re ready to write some Java.

## Step 2: Load the Workbook and Grab the Desired Worksheet

The first line of the code example shows how to open an existing workbook:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Replace `YOUR_DIRECTORY` with the absolute or relative path to your file. The `Workbook` constructor automatically detects the file format (XLS, XLSX, CSV, etc.), so you don’t need to specify it.

Next, we fetch the first sheet:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Why the first sheet? In many templates the data lives on the first tab, but you can pass any index or even use `get("SheetName")` if you prefer a named approach.

## Step 3: Define the Range You Want to Export

Now comes the heart of the **convert excel cells text** operation. You tell Aspose.Cells which cells to pull by creating a `Range` object:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

The string `"A1:C3"` is a classic A1‑style address. It can also be built programmatically:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

That flexibility helps when the range size is dynamic—say, you read the last used row with `ws.getCells().getMaxDataRow()`.

## Step 4: Configure Export Table Options to Include Formulas

Here’s where the **include formulas export** magic lives. By default, Aspose.Cells returns the *displayed* values. If a cell contains `=SUM(A1:A3)`, you’ll get the calculated number, not the formula text. To change that, set up `ExportTableOptions`:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Why both flags? `setExportAsString(true)` tells the API to concatenate the cells using the default delimiter (tab for columns, newline for rows). `setIncludeFormula(true)` flips the value source from “displayed value” to “raw formula”. If you only want values, leave it `false`.

### Optional Tweaks

- `eto.setExportHiddenRows(true);` – include rows hidden in Excel.
- `eto.setExportHiddenColumns(true);` – same for columns.
- `eto.setExportAsHTML(true);` – get HTML instead of plain text.

Feel free to experiment; the options class is a **export table options** playground.

## Step 5: Retrieve the Range as a Formatted String

Now we pull the data:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

The returned `txt` looks something like this (assuming A1:C3 contains a mix of values and formulas):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Notice the tab (`\t`) separating columns and newline (`\n`) separating rows. You can split the string later if you need a 2‑D array:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Step 6: Print the Result – “Print Excel Range” Made Simple

Finally, we dump the string to the console:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Running the program prints the exact output shown above. From here you could write the string to a log file, send it over HTTP, or store it in a NoSQL document.

## Full, Ready‑to‑Run Example

Putting it all together, here’s the complete program. Copy, paste, and hit **Run**—no missing imports.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Expected Output (sample)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

If your workbook contains numbers formatted as dates, they’ll appear in the locale‑specific format (e.g., `2026‑07‑03`). To force ISO dates, you can tweak the `ExportTableOptions` with a custom `NumberFormat`.

## Handling Edge Cases and Common Questions

### What if the range contains merged cells?

Merged cells are treated as the value of the top‑left cell. The rest of the merged area will appear as empty strings. If you need the merged region’s address, query `Cell.getMergedRange()` before export.

### Can I export a massive sheet (hundreds of thousands of rows)?

Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` to let Aspose.Cells stream data to disk. Also, consider exporting in chunks (e.g., 10 000 rows at a time) to keep the string manageable.

### How do I change the column delimiter?

`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style output, set it to `','`:

```java
eto.setSeparator(',');
```

### Do formulas respect external references?

If a formula points to another workbook, Aspose.Cells will keep the reference text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless you load that workbook as well.

## Pro Tips for Production‑Ready Code

- **Cache the workbook** if you’re reading the


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}