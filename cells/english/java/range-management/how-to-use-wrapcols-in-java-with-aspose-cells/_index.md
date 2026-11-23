---
category: general
date: 2026-11-22
description: Learn how to use wrapcols in Java to convert a range to columns using
  Aspose.Cells. This guide walks through the wrap columns excel function step by step.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: en
lastmod: 2026-11-22
og_description: How to use wrapcols in Java to convert a range to columns. Follow
  this tutorial to master the wrap columns excel function with Aspose.Cells.
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: How to use wrapcols in Java – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: How to use wrapcols in Java with Aspose.Cells
url: /java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to use wrapcols in Java with Aspose.Cells

If you need to **how to use wrapcols** to reshape data in an Excel workbook, this tutorial shows the complete process. You'll see how the WRAPCOLS formula turns a vertical range into a set of columns, making it easy to present lists side‑by‑side.

The guide covers everything you need: loading a workbook, applying the WRAPCOLS formula, and saving the result. No external references are required, so you can copy the code and run it immediately. Along the way we also explain the *wrap columns excel function* and demonstrate how to **convert range to columns** for common reporting scenarios.

## What you’ll need

- Java 17 or newer  
- Aspose.Cells for Java (latest version)  
- A Java IDE (IntelliJ IDEA, Eclipse, or VS Code)  
- An input Excel file (`input.xlsx`) containing data in column A  

## How to use wrapcols in Java with Aspose.Cells

The following four steps implement the **how to use wrapcols** workflow. Each step includes a code snippet, an explanation of why it matters, and a tip for avoiding common pitfalls.

### Step 1: Load the workbook

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Why this step matters*: `Workbook` is the entry point for all Excel operations in Aspose.Cells. Loading the file gives you access to worksheets, cells, and formulas.  

**Pro tip**: Use an absolute path during development to avoid `FileNotFoundException`. Switch to a relative path once the project is packaged.

### Step 2: Access the first worksheet

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

The first worksheet (`index 0`) typically holds the data you want to transform. If your data lives on a different sheet, change the index or use `get("SheetName")`.  

**Why this step matters**: Working with the correct worksheet ensures the WRAPCOLS formula references the intended range.

### Step 3: Set the WRAPCOLS formula

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` is the **wrap columns excel function** that distributes the values from `range` across the specified number of columns. In this example we take the values from `A1:A10` and wrap them into three columns, starting at `A1`.  

**Why this step matters**: The formula does the heavy lifting—no manual looping or array handling is required.  

**Tip for convert range to columns**: Adjust the second argument (`3`) to match the number of columns you need. If the range length isn’t a multiple of the column count, the last column will contain the remaining items.

### Step 4: Save the workbook

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Saving writes the WRAPCOLS formula into `output.xlsx`. When you open the file in Excel, the formula will evaluate and display the data wrapped into columns.  

**Why this step matters**: Persisting the workbook lets you verify the result and share the file with non‑Java users.

![Wrapcols formula applied in Excel](wrapcols-example.png){: .align-center alt="How to use wrapcols in Excel screenshot"}

### Expected output

When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed) will contain the original list from `A1:A10` spread across three columns. The layout looks like this:

| A | B | C |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
| Item 10 |   |   |

The **wrap columns excel function** automatically fills empty cells with blanks, so you don’t need additional cleanup code.

## Understanding the wrap columns excel function

The WRAPCOLS formula is part of Excel’s dynamic array functions introduced in Excel 365. It works similarly to `TEXTSPLIT` but focuses on column‑wise distribution.  

- **Syntax**: `=WRAPCOLS(source_range, columns)`  
- **Parameters**:  
  - `source_range` – the vertical range you want to reshape.  
  - `columns` – the number of columns to wrap the data into.  

When you call `=WRAPCOLS(A1:A10, 3)`, Excel treats the source as a one‑dimensional array and fills the first column, then the second, and so on, until all values are placed. This makes **how to use wrapcols** a perfect tool for converting a single column list into a multi‑column report without VBA.

## Convert range to columns without formulas (optional)

If you prefer to perform the **convert range to columns** operation entirely in Java—without relying on Excel’s calculation engine—you can read the source values, build a two‑dimensional array, and write it back manually:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

This snippet shows an alternative way to **convert range to columns** when you need full control over the output (e.g., applying custom formatting per column). However, using the **wrap columns excel function** via WRAPCOLS is usually more concise and lets Excel handle recalculation automatically.

## Edge cases and best practices

- **Empty cells**: WRAPCOLS treats empty cells as blanks. If your source range contains gaps, the output will preserve those blanks.  
- **Dynamic ranges**: Use a named range or a table reference (`Table1[Column]`) to make the formula adapt when rows are added.  
- **Performance**: Applying the formula is O(1) because Excel evaluates it lazily. The programmatic conversion shown above is O(n) and may be slower for very large ranges.  
- **Version compatibility**: The WRAPCOLS function requires Excel 365 or later. If you need to support older versions, rely on the Java‑side conversion method.

## How to use wrapcols in other scenarios

- **Reporting dashboards**: Turn a vertical list of KPI names into a compact table with three columns per row.  
- **Data entry forms**: Convert a column of user inputs into a side‑by‑side layout for easier visual comparison.  
- **Exporting to CSV**: After applying WRAPCOLS, save the workbook as CSV to get a delimited view that matches the column layout.

Each of these cases follows the same **how to use wrapcols** pattern: load, reference, set formula, save.

## Conclusion

You now know **how to use wrapcols** in Java with Aspose.Cells to **convert range to columns** efficiently. By applying the `WRAPCOLS` formula you leverage the native *wrap columns excel function*, keeping your code concise while giving Excel full control over calculation and display.  

Experiment with different column counts, dynamic ranges, or the optional Java‑only conversion to fit your project’s needs. When you master this technique, reshaping data in Excel becomes a one‑line operation rather than a manual chore.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to use wrapcols to convert a list into multiple columns in Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}