---
category: general
date: 2026-11-22
description: Learn how to use a custom number format to format a column as currency
  in Excel using Java. Set Excel number format quickly with a simple style.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: en
lastmod: 2026-11-22
og_description: Apply a custom number format in Excel with Java. This tutorial shows
  how to set Excel number format and style the first column as currency.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Apply a custom number format in Excel with Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: How to apply a custom number format in Excel with Java
url: /java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to apply a custom number format in Excel with Java

If you need to **custom number format** a column in an Excel worksheet, this guide shows you exactly how to do it using Java. Whether you are generating financial reports or exporting accounting data, formatting the first column as currency makes the output instantly readable.

In the example below we will **format column as currency**, apply the style to the first column, and then import a `DataTable` into the worksheet. The same approach works for any numeric format you want to display.

## What you’ll learn

* How to create a **custom number format** with Apache POI’s `Style` object.  
* How to **set Excel number format** for a specific column, including the **set currency format** case.  
* How to **style first column** while importing a `DataTable`.  
* How to save the workbook and verify that the formatting appears correctly.

### Prerequisites

* Java 17 or newer.  
* Apache POI 5.x (the library that provides `Workbook`, `Worksheet`, and `Style`).  
* A `DataTable` implementation that can be iterated like the one in the code sample.  
* Basic familiarity with Java and Excel concepts.

---

## Step 1: Set up the project and import the data

First, add Apache POI to your project. If you use Maven, include the following dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Next, obtain the source data as a `DataTable`. In a real‑world scenario this might come from a database query, a CSV file, or an API response.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** Ensure that the `DataTable` columns have the correct Java types (`Integer`, `Double`, etc.) because the number format only affects numeric cells.

---

## Step 2: Create a **custom number format** for the first column

A **custom number format** tells Excel how to display numeric values. To show values as currency we use the built‑in `CURRENCY` format, but you can also define patterns such as `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Why this works:**  
* `createCellStyle()` returns a reusable style object.  
* `setDataFormat()` attaches the **set currency format** to the style, which Excel then applies to every cell that uses this style.  
* By storing the style in `columnStyles[0]` we guarantee that only the first column receives the currency formatting.

---

## Step 3: Import the `DataTable` while applying the column styles

Now we import the data into the worksheet. The `importDataTable` method accepts the style array, allowing us to **style first column** and leave the remaining columns with default formatting.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

The call above **sets Excel number format** for the first column only. All other columns inherit the workbook’s default style, which keeps the code simple and efficient.

---

## Step 4: Save the workbook and verify the result

Finally, write the workbook to a file and open it in Excel to confirm that the first column shows currency symbols.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Expected output:**  
When you open *FormattedReport.xlsx*, the values in column A appear with the appropriate currency symbol (e.g., `$1,234.00`). All other columns retain their original numeric representation.

---

## Common variations and edge cases

| Situation | Adjustment |
|-----------|------------|
| **Different currency** (e.g., Euro) | Replace `Style.CustomNumberFormat.CURRENCY` with a custom pattern: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **More than one styled column** | Populate additional entries in `columnStyles[]` with their own `CellStyle` objects. |
| **Large data sets** | Use `importDataTable` in batches or stream rows to avoid `OutOfMemoryError`. |
| **Locale‑specific separators** | Use `java.text.NumberFormat` to generate a locale‑aware pattern and pass it to `setDataFormat`. |

> **Watch out for:** Reusing a single `CellStyle` object across many columns can cause unexpected formatting because Excel limits the number of distinct styles per workbook. Create a separate style for each unique format you need.

---

## Full runnable example

Below is a self‑contained program that demonstrates the entire workflow, from data creation to saving the formatted workbook.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Running the program creates **FormattedReport.xlsx** where column A (the “Amount” column) is displayed with a **custom number format** that shows a dollar sign and two decimal places.

---

## Conclusion

You now know how to **custom number format** an Excel worksheet from Java, **format column as currency**, and **style first column** while importing data. By creating a reusable `CellStyle` and passing it to `importDataTable`, you can **set Excel number format** for any column without looping over each cell manually.

Next, try:

* Using `setDataFormat` with locale‑specific patterns to **set currency format


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}