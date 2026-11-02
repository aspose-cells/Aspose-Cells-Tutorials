---
category: general
date: 2026-06-27
description: Open XLSX file in Java quickly. Learn how to read Excel file in Java,
  load Excel workbook, and recalculate all formulas using Apache POI.
draft: false
keywords:
- open xlsx file
- recalculate all formulas
- read excel file in java
- how to recalculate excel formulas
- load excel workbook
language: en
og_description: Open XLSX file in Java and learn how to read Excel file in Java, load
  Excel workbook, then recalculate all formulas with a clear, runnable example.
og_title: Open XLSX File in Java – Step‑by‑Step Workbook Loading & Formula Recalculation
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Open XLSX file in Java quickly. Learn how to read Excel file in Java,
    load Excel workbook, and recalculate all formulas using Apache POI.
  headline: Open XLSX File in Java – Complete Guide to Load Workbook & Recalculate
    Formulas
  type: TechArticle
- questions:
  - answer: Not directly. For older binary formats you’d use `HSSFWorkbook` instead
      of `XSSFWorkbook`. The rest of the code (evaluator, saving) stays the same.
    question: Does this work with `.xls` files?
  - answer: POI does not execute VBA macros, but it can preserve them when you write
      the file back. The formulas will still be recalculated.
    question: What if the workbook contains macros?
  - answer: 'Yes—call `evaluator.evaluateAll()` on the sheet object: `evaluator.evaluateAll(sheet);`.
      ## Wrap‑Up We’ve just shown you how to **open XLSX file in Java**, **load Excel
      workbook**, and **recalculate all formulas** in a clean, production‑ready way.
      The example covers *how to recalculate Excel formula'
    question: Can I recalculate only a single sheet?
  type: FAQPage
tags:
- java
- excel
- apache-poi
title: Open XLSX File in Java – Complete Guide to Load Workbook & Recalculate Formulas
url: /java/calculation-engine/open-xlsx-file-in-java-complete-guide-to-load-workbook-recal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Open XLSX File in Java – Complete Guide to Load Workbook & Recalculate Formulas

Ever needed to **open XLSX file** in Java but weren’t sure which library to pick or how to make the formulas update automatically? You’re not alone. Many developers hit this wall when they try to *read Excel file in Java* for reporting or data‑migration tasks.

In this tutorial we’ll walk through a real‑world solution: loading an Excel workbook, **recalculating all formulas**, and saving the result—no hand‑held spreadsheets required. By the end you’ll know exactly *how to recalculate Excel formulas* programmatically and have a ready‑to‑run code sample.

## What You’ll Need

- Java 8 or newer (the code works on Java 11, 17, etc.)  
- Apache POI 5.x (the de‑facto library for Excel handling in Java)  
- A simple `dynamic.xlsx` file placed somewhere you can reference it from your project  
- Your favorite IDE or a plain text editor—doesn’t matter, the code is straightforward  

If you already have those, great—let’s dive in.

## Open XLSX File in Java – Load Excel Workbook

The first step is to **load excel workbook** from disk. Think of this as opening the door to the spreadsheet; without it you can’t see any of the cells or formulas inside.

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/**
 * Demonstrates opening an XLSX file, recalculating formulas, and saving the result.
 */
public class ExcelFormulaRecalc {

    public static void main(String[] args) throws Exception {
        // Path to the file you want to open
        String inputPath = "dynamic.xlsx";

        // Step 1: Load the workbook (open xlsx file)
        try (FileInputStream fis = new FileInputStream(inputPath);
             Workbook workbook = new XSSFWorkbook(fis)) {

            // The workbook is now in memory – ready for further actions
            System.out.println("Workbook loaded successfully.");
```

> **Why XSSFWorkbook?**  
> `XSSFWorkbook` handles the modern OOXML `.xlsx` format, while `HSSFWorkbook` is for the legacy `.xls`. Using the right class ensures you actually **open XLSX file** without hitting `InvalidFormatException`.

## Recalculate All Formulas in the Workbook

Now that the file is open, the next logical question is *“how to recalculate Excel formulas?”* The answer lives in POI’s `FormulaEvaluator`. It walks the entire sheet graph, evaluating each cell that contains a formula.

```java
            // Step 2: Create a FormulaEvaluator (how to recalculate excel formulas)
            FormulaEvaluator evaluator = workbook.getCreationHelper().createFormulaEvaluator();

            // Step 3: Force POI to evaluate every formula cell (recalculate all formulas)
            evaluator.evaluateAll();

            System.out.println("All formulas have been recalculated.");
```

> **Pro tip:** If you only need to update a single sheet, call `evaluator.evaluateAll()` on that sheet instead of the whole workbook. This can save memory on gigantic files.

### Edge Cases & Common Pitfalls

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| Very large workbooks (hundreds of MB) | POI may exhaust heap memory | Use `SXSSFWorkbook` for streaming write‑back, or increase `-Xmx` |
| Cells contain external references | POI cannot resolve them automatically | Pre‑populate required data or avoid external links |
| Custom functions (UDFs) | POI doesn’t know how to evaluate them | Implement a `UDFFinder` or skip those cells |

## Verify and Save the Updated Workbook

Recalculation is only useful if you can see the result. Let’s write the updated workbook back to disk. You could overwrite the original file, but the example below writes to a new file to keep things safe.

```java
            // Step 4: Write the updated workbook to a new file
            String outputPath = "dynamic_updated.xlsx";
            try (FileOutputStream fos = new FileOutputStream(outputPath)) {
                workbook.write(fos);
            }

            System.out.println("Updated workbook saved as " + outputPath);
        }
    }
}
```

Running the program prints:

```
Workbook loaded successfully.
All formulas have been recalculated.
Updated workbook saved as dynamic_updated.xlsx
```

Open `dynamic_updated.xlsx` in Excel and you’ll see that every formula now reflects the latest data—exactly what you’d expect after a manual **recalculate all formulas** operation.

## Reading Specific Cells (Optional)

If your goal is to *read Excel file in Java* after recalculation, you can fetch cell values like this:

```java
Sheet sheet = workbook.getSheetAt(0); // first sheet
Row row = sheet.getRow(1); // second row (0‑based)
Cell cell = row.getCell(2); // third column

if (cell.getCellType() == CellType.NUMERIC) {
    double value = cell.getNumericCellValue();
    System.out.println("Recalculated value: " + value);
}
```

This snippet shows how to pull a single, freshly‑calculated value out of the workbook—handy for feeding data into other Java components.

## Full Working Example Recap

Putting it all together, here’s the complete, self‑contained program you can copy‑paste into `ExcelFormulaRecalc.java` and run:

```java
import java.io.FileInputStream;
import java.io.FileOutputStream;
import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

public class ExcelFormulaRecalc {
    public static void main(String[] args) throws Exception {
        String inputPath = "dynamic.xlsx";
        String outputPath = "dynamic_updated.xlsx";

        try (FileInputStream fis = new FileInputStream(inputPath);
             Workbook workbook = new XSSFWorkbook(fis)) {

            // Load the workbook (open xlsx file)
            System.out.println("Workbook loaded successfully.");

            // Recalculate all formulas (how to recalculate excel formulas)
            FormulaEvaluator evaluator = workbook.getCreationHelper().createFormulaEvaluator();
            evaluator.evaluateAll();
            System.out.println("All formulas have been recalculated.");

            // Optional: read a specific cell after recalculation
            Sheet sheet = workbook.getSheetAt(0);
            Row row = sheet.getRow(1);
            Cell cell = row.getCell(2);
            if (cell != null && cell.getCellType() == CellType.NUMERIC) {
                System.out.println("Recalculated cell value: " + cell.getNumericCellValue());
            }

            // Save the updated workbook
            try (FileOutputStream fos = new FileOutputStream(outputPath)) {
                workbook.write(fos);
            }
            System.out.println("Updated workbook saved as " + outputPath);
        }
    }
}
```

Save the file, add Apache POI to your project’s classpath (Maven users can add the `poi-ooxml` dependency), and run `java ExcelFormulaRecalc`. That’s it—you’ve **opened an XLSX file**, **recalculated all formulas**, and **saved the changes**.

![Open XLSX file in Java example](/images/open-xlsx-java.png "open xlsx file")

*Image alt text: open xlsx file in Java example showing code editor and console output.*

## Frequently Asked Questions

**Q: Does this work with `.xls` files?**  
A: Not directly. For older binary formats you’d use `HSSFWorkbook` instead of `XSSFWorkbook`. The rest of the code (evaluator, saving) stays the same.

**Q: What if the workbook contains macros?**  
A: POI does not execute VBA macros, but it can preserve them when you write the file back. The formulas will still be recalculated.

**Q: Can I recalculate only a single sheet?**  
A: Yes—call `evaluator.evaluateAll()` on the sheet object: `evaluator.evaluateAll(sheet);`.

## Wrap‑Up

We’ve just shown you how to **open XLSX file in Java**, **load Excel workbook**, and **recalculate all formulas** in a clean, production‑ready way. The example covers *how to recalculate Excel formulas*, demonstrates *reading Excel file in Java*, and highlights the nuances of *load excel workbook* for both small and large files.

Next, you might want to explore:

- Adding styles or charts with POI’s `XSSF` classes  
- Streaming large workbooks with `SXSSFWorkbook` for low‑memory writes  
- Integrating the solution into a Spring Boot service that processes uploads on the fly  

Give those a try, and you’ll soon be automating Excel‑heavy workflows like a pro. Got more questions? Drop a comment, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Excel File Manipulation Using Aspose.Cells for Java | Workbook Operations Guide](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Master Excel File Operations in Java Using Aspose.Cells](/cells/english/java/workbook-operations/excel-file-operations-aspose-cells-java/)
- [Master Excel XLSB File Management in Java with Aspose.Cells: Load and Modify DB Connections](/cells/english/java/workbook-operations/excel-xlsb-management-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}