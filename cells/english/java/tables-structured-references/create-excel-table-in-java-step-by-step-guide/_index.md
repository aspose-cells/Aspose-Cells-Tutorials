---
category: general
date: 2026-08-04
description: Create excel table in Java and learn how to turn off autofilter, define
  cell range, and save workbook as xlsx with a complete code example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel table
- turn off autofilter
- define cell range
- save workbook as xlsx
- disable autofilter in excel
language: en
lastmod: 2026-08-04
og_description: Create excel table in Java, turn off autofilter, define cell range,
  and save workbook as xlsx. Follow this complete tutorial to master Excel automation.
og_image_alt: Image showing how to create excel table without autofilter using Java
og_title: Create excel table in Java – full code walkthrough
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  headline: Create excel table in Java – step‑by‑step guide
  type: TechArticle
- description: Create excel table in Java and learn how to turn off autofilter, define
    cell range, and save workbook as xlsx with a complete code example.
  name: Create excel table in Java – step‑by‑step guide
  steps:
  - name: Define cell range for the table
    text: Next, you must specify the exact area that will become the table. The **define
      cell range** step tells Aspose.Cells which rows and columns to include.
  - name: Add the table and enable its default AutoFilter
    text: Now you add a `ListObject` (the Aspose.Cells representation of an Excel
      table). By default, a new table includes an AutoFilter dropdown for each column.
  - name: Turn off autofilter for the table
    text: If you want a clean table without filter dropdowns, you must **turn off
      autofilter** (or **disable autofilter in excel**). The API call is straightforward.
  - name: Save workbook as xlsx file
    text: Finally, persist the workbook to disk. The **save workbook as xlsx** call
      writes a standard Office Open XML file that any modern spreadsheet program can
      open.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Create excel table in Java – step‑by‑step guide
url: /java/tables-structured-references/create-excel-table-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create excel table in Java – step‑by‑step guide

If you need to **create excel table** in Java, this tutorial shows you exactly how to do it. You’ll learn to **define cell range**, **turn off autofilter**, and **save workbook as xlsx** with a single, runnable program.

The example uses the Aspose.Cells for Java library, which provides a high‑level API for Excel automation. No additional dependencies are required beyond the Aspose.Cells JAR. By the end of the guide you will have a self‑contained solution that you can drop into any Java project.

## What you will build

* A new workbook containing one worksheet.  
* A table (ListObject) that spans a specific **cell range** (A1:D5).  
* The table’s AutoFilter turned **off** (i.e., **disable autofilter in excel**).  
* The workbook saved as an **xlsx** file on disk.

## Prerequisites

* Java 8 or newer installed.  
* Aspose.Cells for Java (download from the official site or add via Maven).  
* Basic familiarity with Java syntax and IDEs such as IntelliJ IDEA or Eclipse.

---

## How to create excel table without autofilter in Java

The first major step is to instantiate a `Workbook` and obtain the default worksheet. This gives you a clean canvas where you can place a table.

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Why this matters:**  
A `Workbook` represents the entire Excel file. The first worksheet (`get(0)`) is created automatically, so you don’t need to add one manually. Starting with a fresh sheet guarantees that no leftover data interferes with the table you will create.

### Define cell range for the table

Next, you must specify the exact area that will become the table. The **define cell range** step tells Aspose.Cells which rows and columns to include.

```java
        // Step 2: Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");
```

**Why this matters:**  
`CellArea` encodes the top‑left and bottom‑right corners of the range. By using `"A1"` and `"D5"` you create a 5‑row × 4‑column block, which is the typical size for a simple data table.

### Add the table and enable its default AutoFilter

Now you add a `ListObject` (the Aspose.Cells representation of an Excel table). By default, a new table includes an AutoFilter dropdown for each column.

```java
        // Step 3: Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is turned on by default
```

**Why this matters:**  
Enabling `setShowAutoFilter(true)` mirrors the default Excel behavior, making the table immediately filterable. This step is optional but clarifies the state before you turn it off.

### Turn off autofilter for the table

If you want a clean table without filter dropdowns, you must **turn off autofilter** (or **disable autofilter in excel**). The API call is straightforward.

```java
        // Step 4: Disable the AutoFilter for the table
        table.setShowAutoFilter(false);
```

**Why this matters:**  
Disabling the AutoFilter improves readability when the table is used for reporting or printing. It also reduces the UI clutter for end‑users who do not need interactive filtering.

### Save workbook as xlsx file

Finally, persist the workbook to disk. The **save workbook as xlsx** call writes a standard Office Open XML file that any modern spreadsheet program can open.

```java
        // Step 5: Save the workbook to a file
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Why this matters:**  
Choosing the `XLSX` format ensures compatibility with Excel 2007+ and with cloud services such as Google Sheets. The file name `TableNoAutoFilter.xlsx` clearly reflects that the AutoFilter has been turned off.

---

## Full source code recap

Putting all the snippets together yields a complete, runnable program:

```java
import com.aspose.cells.*;

public class CreateExcelTable {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the cell range that will become the table (A1:D5)
        CellArea tableRange = CellArea.createCellArea("A1", "D5");

        // Add a table (ListObject) to the worksheet and enable its AutoFilter
        ListObject table = worksheet.getListObjects().add("MyTable", tableRange, true);
        table.setShowAutoFilter(true); // AutoFilter is on by default

        // Disable the AutoFilter for the table
        table.setShowAutoFilter(false);

        // Save the workbook to a file (xlsx format)
        workbook.save("TableNoAutoFilter.xlsx", SaveFormat.XLSX);
    }
}
```

**Expected result:**  
When you open `TableNoAutoFilter.xlsx` in Microsoft Excel, you will see a table named **MyTable** covering cells A1:D5. No filter arrows appear on the column headers, confirming that the **turn off autofilter** step succeeded.

---

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| *Can I add data before creating the table?* | Yes. Fill cells in the defined range first; the table will automatically include the data. |
| *What if the worksheet already contains data?* | Choose a different **cell range** that does not overlap existing content, or clear the area with `worksheet.getCells().clear(A1, D5)`. |
| *Is it possible to keep the AutoFilter for some columns only?* | Aspose.Cells does not support column‑specific AutoFilter toggling; you must keep it on for the whole table or off entirely. |
| *How do I change the table style?* | Use `table.setTableStyleType( TableStyleType.TABLE_STYLE_MEDIUM_2 );` before saving. |
| *Will this work on older Excel versions (xls)?* | Save with `SaveFormat.XLS` instead of `XLSX`, but note that some newer features (like ListObject) may be limited. |

**Pro tip:** Always call `workbook.save(..., SaveFormat.XLSX)` after you finish all table modifications. Saving multiple times can increase file size unnecessarily.

---

## Next steps

Now that you know how to **create excel table**, **define cell range**, **turn off autofilter**, and **save workbook as xlsx**, you can extend the solution:

* **Add formulas** to calculated columns using `table.getListColumns().get(i).setFormula("=SUM(...)")`.  
* **Apply conditional formatting** to highlight rows that meet certain criteria.  
* **Export the workbook to PDF** with `workbook.save("Table.pdf", SaveFormat.PDF)` for reporting purposes.  

Each of these topics builds on the core concepts covered in this tutorial and further demonstrates how to **disable autofilter in excel** when needed.

---

## Conclusion

You now have a complete, production‑ready example that shows how to **create excel table** in Java, **define cell range**, **turn off autofilter**, and **save workbook as xlsx**. By following the step‑by‑step code and explanations, you can integrate Excel table creation into any Java application and control the AutoFilter behavior programmatically. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}