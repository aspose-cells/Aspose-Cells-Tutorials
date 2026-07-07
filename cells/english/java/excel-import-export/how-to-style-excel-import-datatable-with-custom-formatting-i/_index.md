---
category: general
date: 2026-07-03
description: How to style Excel files using Java. Learn to format column date Excel,
  apply number format Excel, export DataTable to XLSX and import DataTable into Excel
  with Aspose Cells.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: en
og_description: How to style Excel files in Java. This tutorial shows how to format
  column date Excel, apply number format Excel, export DataTable to XLSX and import
  DataTable into Excel.
og_title: How to Style Excel – Java Guide for Custom Column Formatting
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: How to Style Excel – Import DataTable with Custom Formatting in Java
url: /java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Style Excel – Import DataTable with Custom Formatting in Java

Ever wondered **how to style Excel** sheets programmatically without opening the file manually? You’re not alone. Many developers need to generate reports where the first column is bold, the second shows dates, and the rest follow a clean layout. In this guide we’ll walk through a complete, runnable example that **imports a DataTable into Excel**, applies a bold header, formats a date column, and finally **exports DataTable to XLSX**.  

We’ll use Aspose.Cells for Java, but the concepts translate to any library that lets you work with styles. By the end you’ll have a reusable pattern for **apply number format Excel** cells, **format column date Excel**, and ship a polished workbook to your users.

## Prerequisites

- Java 17 (or any recent JDK)  
- Aspose.Cells for Java 23.9 or newer (the free trial works fine)  
- A `DataTable`‑like structure (the example uses a simple mock)  
- Your favorite IDE (IntelliJ IDEA, Eclipse, VS Code…)

No additional Maven plugins are required; just add the Aspose.Cells JAR to your classpath.

---

## Step 1: Obtain the Source DataTable – “Export DataTable to XLSX” Preparation

Before we can **import datatable into excel**, we need a `DataTable` object that represents the data you want to export. In real projects you might pull this from a database, CSV file, or an API. For this tutorial we’ll mock a tiny table:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Why this matters:** Getting the data right up front means the rest of the styling logic can focus purely on presentation, not data wrangling.

---

## Step 2: Create an Array to Hold Style Definitions for Each Column

Aspose.Cells lets you pass a **Style[]** array when importing a `DataTable`. Each entry corresponds to a column and determines how that column will look after the import. Let’s allocate the array based on the number of columns:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** If you have many columns, consider building the array in a loop and reusing a single `Style` object where the formatting is identical. This reduces memory overhead.

---

## Step 3: Define the Styles – Bold Header & Date Formatting

Now we answer the classic **format column date excel** question and also demonstrate **apply number format excel** for other columns.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**What’s happening here?**  
- `StyleNumberFormat.DATE` tells Excel to treat the cell’s value as a short date (e.g., *01/31/2024*).  
- `StyleNumberFormat.CURRENCY_USD` automatically adds the `$` symbol and two decimal places.  
- Setting the font to bold on the first column makes the header stand out, which is a frequent requirement when you **how to style excel** spreadsheets for readability.

> **Edge case:** If your source data already contains formatted strings, you may need to convert them to `java.util.Date` objects before import; otherwise Excel will treat them as plain text.

---

## Step 4: Create a New Workbook and Access Its First Worksheet

A fresh workbook gives us a clean canvas. We’ll grab the first worksheet, which is where the import will land.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Why a new workbook?** Starting from scratch guarantees that no leftover styles or hidden rows interfere with the final output—essential when you **how to style excel** files consistently across multiple runs.

---

## Step 5: Import the DataTable with the Column Styles

Here’s the heart of the operation: feeding the `DataTable` into the sheet while applying the style array we built.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Explanation:**  
- `importDataTable` copies both the header row and the data rows.  
- The `columnStyles` array aligns with each column, so the first column’s header becomes bold, the second column shows dates, and the third column appears as currency.  
- This single line replaces dozens of manual cell‑by‑cell formatting steps, illustrating a clean way to **apply number format excel** programmatically.

---

## Step 6: Save the Styled Workbook – Completing the “Export DataTable to XLSX”

Finally we persist the workbook to disk. Adjust the path to a writable folder on your machine.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Open the file in Excel and you should see:

- Column **ID** header in bold.  
- **OrderDate** column formatted as dates (e.g., *04/27/2024*).  
- **Total** column displayed with a dollar sign and two decimals.

> **Pro tip:** If you need to support older Excel versions, call `workbook.save(outputPath, SaveFormat.XLS)` instead of the default XLSX.

---

## Step 7: Verify the Result & Optional Tweaks

It’s good practice to double‑check the generated file, especially when automating reports for stakeholders.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

If `isBold` prints `true`, your **how to style excel** routine worked as intended. From here you can:

- Add conditional formatting (e.g., highlight totals > $200).  
- Freeze the top row for easier scrolling.  
- Insert a chart that references the imported data.

All of these extensions follow the same pattern: define a `Style`, apply it, and save.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I style more than one column the same way?** | Yes—reuse a single `Style` instance for all columns that share formatting. |
| **What if my DataTable has more columns than styles?** | Any column without a corresponding entry in `columnStyles` will use the default style. |
| **How do I change the date format to “dd‑MMM‑yyyy”?** | Use `columnStyles[1].setCustom("#dd-MMM-yyyy#");` instead of the built‑in `DATE`. |
| **Is there a way to auto‑size columns after import?** | Call `worksheet.autoFitColumns();` after `importDataTable`. |
| **Will this work on Linux/macOS?** | Absolutely—Aspose.Cells is platform‑agnostic as long as you have a compatible JDK. |

---

## Conclusion

You now have a solid, end‑to‑end example of **how to style Excel** workbooks by **importing datatable into excel**, **format column date excel**, and **apply number format excel** using Java. The code shows the full flow from **export datatable to xlsx** to opening the file in Excel, covering both the *what* and the *why* behind each step.  

Give it a spin: adjust the style array, add more columns, or plug in a real database query. The same pattern will let you generate professional‑looking reports at the click of a button, no manual formatting required.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Image alt text: “Styled Excel worksheet created using Java and Aspose.Cells, showing bold header and formatted date column.”*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}