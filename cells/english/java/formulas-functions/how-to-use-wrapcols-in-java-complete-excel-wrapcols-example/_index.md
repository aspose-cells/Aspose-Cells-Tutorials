---
category: general
date: 2026-06-21
description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
  write formula to cell, and populate cells with formula – step‑by‑step guide.
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: en
og_description: How to use WRAPCOLS in Java with Aspose.Cells to convert an array
  into rows, write a formula to a cell, and populate cells with formula—all in one
  guide.
og_title: How to Use WRAPCOLS in Java – Full Excel WRAPCOLS Example
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
url: /java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example

Ever wondered **how to use WRAPCOLS** when you need to transform a simple array into a tidy table in Excel? You're not the only one. Many developers hit a wall when they first see the `WRAPCOLS` function and think, “How do I actually write this formula to a cell from Java?” The good news? It’s pretty straightforward once you know the right steps.

In this tutorial we’ll walk through a fully runnable Aspose.Cells Java example that **converts an array to rows**, writes the formula directly into a cell, and shows you how to **populate cells with formula** for real‑world scenarios. By the end you’ll have a clear picture of the **excel wrapcols example** and be ready to adapt it to your own projects.

## Prerequisites

Before we dive in, make sure you have:

- Java 17 or later (the code works with any recent JDK).
- Aspose.Cells for Java library (you can grab the latest JAR from Maven Central).
- A basic understanding of Java syntax and Excel formulas.
- An IDE or simple text editor—no special tooling required.

Got everything? Great, let’s get started.

## Step 1: Set Up the Project and Load a Workbook

First things first—create a new Maven (or Gradle) project and add the Aspose.Cells dependency:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Now we can load an existing workbook (or create a fresh one) and grab the first worksheet:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Why we load a workbook** – Aspose.Cells works with an in‑memory representation of an Excel file. By loading (or creating) a workbook we gain access to cells, rows, and formulas, which is essential for any **write formula to cell** operation.

## Step 2: Insert the WRAPCOLS Formula into a Cell

The heart of the tutorial lies in the `WRAPCOLS` function. It takes a one‑dimensional array and “wraps” it into a specified number of columns, automatically spilling the remainder into new rows. Here’s the syntax we’ll use:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Notice how the formula is a plain string passed to `setFormula`. Aspose.Cells does the heavy lifting—parsing the formula, evaluating it, and spilling the results into the worksheet. This is the most direct way to **populate cells with formula** without manually iterating over rows and columns.

### What the Formula Does

- `{1,2,3}` – a literal array containing three numbers.
- `2` – the number of columns per row.
- Result:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (blank)

If you wanted three columns instead, simply change the second argument to `3`, and the array would fill a single row.

## Step 3: Save the Workbook and Verify the Output

Now that the formula sits in **A1**, let’s persist the workbook to disk so you can open it in Excel and see the spill:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Open `output.xlsx` and you’ll see exactly what the comment described—two columns in the first row and the remaining value in the second row. That’s the essence of the **excel wrapcols example**.

## Step 4: Extending the Example – Converting Larger Arrays

Real projects rarely work with just three numbers. Suppose you have a larger collection, say `{10,20,30,40,50,60,70}` and you want three columns per row. Here’s how you’d adjust the code:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Now the spill starts at **C5**, producing:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

This demonstrates how you can **convert array to rows** dynamically, simply by tweaking the formula string. No loops, no manual cell assignments—Aspose.Cells handles the rest.

## Step 5: Handling Edge Cases and Common Gotchas

### 1. Empty Arrays

If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error. To avoid breaking your sheet, guard the formula generation:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Non‑Numeric Data

`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)` produces a two‑column layout of strings. Just remember to quote strings inside the array literal.

### 3. Compatibility

The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office 2019, Excel for the web). If you need to support older versions, you’ll have to fall back to manual looping or use a different spill‑compatible function.

## Step 6: Practical Tips and Pro Tricks

- **Pro tip:** Use `Cell.setFormulaLocal` if you need a locale‑specific separator (comma vs semicolon) depending on the user’s regional settings.
- **Watch out for:** Overwriting existing data. The spill area will replace any content that already exists in the target range.
- **Performance note:** Setting a formula is cheap; the heavy lifting occurs when you **save** or **recalculate** the workbook. If you’re generating thousands of formulas, consider disabling automatic calculation (`wb.calculateFormula()` later) to speed up processing.

## Full Working Example

Below is the complete, ready‑to‑run Java class that incorporates everything we’ve discussed:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Expected output:** Open `output.xlsx` and you’ll see three distinct spill regions:

- **A1:B2** – numbers 1‑3 wrapped into two columns.
- **C5:E7** – numbers 10‑70 wrapped into three columns.
- **G1:H2** – fruit names wrapped into two columns.

## Conclusion

We’ve just covered **how to use WRAPCOLS** with Aspose.Cells for Java, showing you how to **convert array to rows**, **write formula to cell**, and **populate cells with formula** in a clean, repeatable fashion. The approach eliminates tedious looping, leverages Excel’s native spill behavior, and keeps your code concise.

Ready for the next challenge? Try combining `WRAPCOLS` with dynamic data sources—perhaps pulling values from a database, constructing the array string on the fly, and letting Excel do the layout work. You can also experiment with other spill functions like `SEQUENCE` or `FILTER` to build even richer reports.

If you hit any snags, drop a comment below or explore Aspose’s extensive documentation. Happy coding, and enjoy the power of modern Excel formulas right from Java! 

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}