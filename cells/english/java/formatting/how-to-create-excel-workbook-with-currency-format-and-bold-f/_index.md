---
category: general
date: 2026-08-20
description: Create excel workbook in Java using Aspose.Cells, set currency format,
  add bold font, and import style array for styled cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: en
lastmod: 2026-08-20
og_description: Create excel workbook in Java, set currency format, add bold font,
  and learn how to import style using Aspose.Cells.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Create excel workbook with styled currency cells in Java
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: How to create excel workbook with currency format and bold font in Java
url: /java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create excel workbook with currency format and bold font in Java

If you need to **create excel workbook** programmatically, this guide shows you exactly how. We'll walk through building a workbook, applying a currency format, adding a bold font, and using the **how to import style** feature of Aspose.Cells so every imported cell looks consistent.

You’ll finish with a ready‑to‑use `DataTableWithStyleArray.xlsx` file that displays numbers as dollars and highlights them in bold. No manual formatting in Excel is required.

## Prerequisites

Before you start, make sure you have:

- Java 17 or later installed.
- An Aspose.Cells for Java license (or a free evaluation key).
- Maven or Gradle to manage the `aspose-cells` dependency.
- Basic familiarity with Java collections and `DataTable`.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tip:** If you run into a `LicenseException`, place your license file in the classpath and call `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` before creating the workbook.

## How to create excel workbook with styled currency cells

This section contains the core steps. Each step explains **why** it matters, not just **what** to type.

### Step 1: Initialise the workbook and worksheet

Creating a fresh workbook gives you a clean container for all subsequent formatting.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Why:** The `Workbook` object represents the entire Excel file. Accessing the first `Worksheet` lets you start populating data immediately.

### Step 2: Build a DataTable with numeric data

A `DataTable` mimics a database table, making it easy to import rows in bulk.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Why:** Using `DOUBLE` guarantees that the values keep their decimal precision, which is essential when you later **format cells currency**.

### Step 3: Define a style – currency format and bold font

Here we **set currency format** and **add bold font** to a `Style` object.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Why:** The `Number` format string `$#,##0.00` tells Excel to treat the cell as a monetary value, while `setBold(true)` draws attention to the numbers. Placing the style in an array prepares us for the **how to import style** step.

### Step 4: Configure import options to use the style array

Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is the official **how to import style** method.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Why:** Without `ImportTableOptions`, imported cells would inherit the default style, losing the currency formatting and boldness we defined.

### Step 5: Import the DataTable into the worksheet

Now we bring the data into the sheet at cell `A1`, applying the style array automatically.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` indicates that the first row of the `DataTable` contains column headers.
- `"A1"` is the top‑left corner where the import begins.

> **Why:** Importing with the style array guarantees that each imported cell receives the **format cells currency** style we prepared earlier.

### Step 6: Save the workbook to disk

Finally, write the in‑memory workbook to a physical file.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Why:** Saving persists the formatting, allowing you or downstream processes to open the file in Excel with the desired appearance.

## Full source code

Below is the complete, ready‑to‑run Java class. Copy it into your IDE, replace `YOUR_DIRECTORY` with an existing folder, and execute.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Expected output

When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should see:

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- The numbers are displayed with a **currency format** (`$` sign, two decimal places).
- The font for both cells is **bold**, making them stand out.

## Common variations and edge cases

| Scenario | What to change | Reason |
|----------|----------------|--------|
| **Different currency** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Use the Euro symbol or any locale‑specific format. |
| **Multiple columns with different styles** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | Each column can have its own number format, font, background, etc. |
| **Large data sets** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | Improves performance by skipping header rows or unnecessary metadata. |
| **Applying style after import** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | Useful when only a subset of rows needs special formatting. |

## Tips for production use

- **License early**: Register your Aspose.Cells license before creating the workbook to avoid the evaluation watermark.
- **Thread safety**: `Workbook` instances are **not** thread‑safe. Create a separate instance per thread if you generate many files concurrently.
- **Memory management**: For very large sheets, consider using `Workbook`'s streaming API (`Workbook` → `WorkbookDesigner`) to keep memory usage low.
- **Testing**: Include a unit test that opens the saved file with Apache POI and asserts the cell style number format matches `"$#,##0.00"`.

## Conclusion

You now know how to **create excel workbook** in Java, **set currency format**, **add bold font**, and correctly **how to import style** using Aspose.Cells’ `ImportTableOptions`. This end‑to‑end solution eliminates manual Excel steps and guarantees that every imported cell follows the same **format cells currency** styling.

Ready for the next challenge? Try adding conditional formatting, embedding charts, or exporting the workbook to PDF—all while re‑using the same style‑array technique. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}