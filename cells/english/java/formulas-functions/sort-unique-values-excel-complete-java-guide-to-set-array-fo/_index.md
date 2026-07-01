---
category: general
date: 2026-06-30
description: Sort unique values Excel using Java. Learn how to set formula, recalculate
  formulas, and generate unique list Excel with Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: en
og_description: Sort unique values Excel with Java. This guide shows how to set formula,
  recalculate formulas, and generate a unique list Excel in minutes.
og_title: Sort Unique Values Excel – Java Tutorial for Array Formulas
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
url: /java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sort Unique Values Excel – Complete Java Guide to Set Array Formulas

Ever wondered how to **sort unique values Excel** without dragging formulas around? You're not the only one. In many reporting scenarios you need a clean, alphabetically‑sorted list of distinct entries, and doing it manually is a pain.  

The good news? With a few lines of Java code you can **set array formula** on a worksheet, then **recalculate formulas** so the spilled range fills itself automatically. In this tutorial we’ll walk through everything—from creating a workbook to generating a unique list Excel style—so you can embed the solution straight into your application.

## What This Tutorial Covers

- Setting up a Java project with Aspose.Cells (the library that powers the code snippet).  
- Using the `SORT` and `UNIQUE` functions together to **generate unique list Excel** results.  
- Applying an **array formula** to a cell programmatically.  
- Triggering a calculation pass so the **how to recalculate formulas** step happens instantly.  
- Verifying the output and tweaking the solution for edge cases like empty cells or non‑contiguous ranges.

By the end of this guide you’ll be able to drop a ready‑to‑use method into any Java service that needs to export clean Excel sheets.

> **Pro tip:** If you’re already using Maven, adding Aspose.Cells as a dependency saves you from manually handling JAR files.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose.Cells targets Java 8+. |
| Maven (or Gradle) | Simplifies dependency management. |
| Aspose.Cells for Java | Provides the `Workbook`, `Worksheet`, and formula APIs we’ll use. |
| Basic familiarity with Excel functions | Understanding `SORT` and `UNIQUE` helps you adapt the code. |

> *If you don’t have Aspose.Cells yet, add this to your `pom.xml`*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Step 1: Create a New Workbook (How to Set Formula Begins Here)

First we need a blank workbook. Think of it as the empty canvas where we’ll later **set array formula** on cell `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Why create a new workbook?*  
> It guarantees a clean environment, avoiding hidden formulas that could interfere with our test data.

---

## Step 2: Populate Sample Data (Optional but Helpful)

To see the result clearly, let’s fill column **B** with some duplicate entries.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Why use column B?*  
> The formula we’ll write references `B1:B10`, so keeping the data there mirrors the classic Excel example.

---

## Step 3: Set an Array Formula That **Sort Unique Values Excel**

Now the magic happens. We combine `UNIQUE` (to strip duplicates) with `SORT` (to order them alphabetically). The resulting expression is an **array formula**, meaning it will spill into adjacent cells automatically.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### How It Works

- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct strings.  
- `SORT(...)` takes that array and orders it in ascending order.  
- Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells to treat the result as a **spilled array**, just like Excel would.

> **Note:** If you’re using an older version of Excel that lacks `SORT` or `UNIQUE`, you can fall back to `SORT(UNIQUE(...))` with the **LET** function or use legacy array formulas (`=INDEX(...)`). The tutorial focuses on the modern dynamic array approach because it’s the cleanest way to **generate unique list Excel** today.

---

## Step 4: Recalculate Formulas So the Spilled Range Is Populated

After the formula is in place, the workbook doesn’t automatically evaluate it. This is where the **how to recalculate formulas** step comes in.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Calling `calculateFormula()` forces Aspose.Cells to run the Excel engine, filling cells `A1`, `A2`, … with the sorted unique values.

> *Why not rely on lazy evaluation?*  
> In a server‑side context you often need the data ready for export (CSV, PDF, etc.) right after the calculation, so an explicit call guarantees consistency.

---

## Step 5: Verify the Result (Optional Debugging)

It’s always a good idea to print the spilled values to the console—especially when you’re teaching yourself a new API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Running the program prints:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Open `SortedUniqueValues.xlsx` and you’ll see the same data spilling from `A1` downwards.

---

## Handling Edge Cases

### Empty Cells in the Source Range

If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry. To ignore blanks, wrap the range with `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Non‑Contiguous Data

When your data lives in multiple columns, you can join them with `CHOOSE` or `TEXTJOIN` before applying `UNIQUE`. For example:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

These tweaks demonstrate the flexibility of **how to set formula** for more complex scenarios.

---

## Full Working Example (All Steps Combined)

Below is the complete, runnable Java program. Copy‑paste it into your IDE, add the Aspose.Cells dependency, and hit *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Expected output** (shown in console) matches the sorted, deduplicated list we discussed earlier. Opening the generated Excel file reveals the same values spilling from `A1` downwards.

---

## Frequently Asked Questions

**Q: Does this work with older Excel versions (pre‑Office 365)?**  
A: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine introduced in Excel 365. For legacy files you’d need to use classic array formulas like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells can still evaluate them, but the syntax is more verbose.

**Q: Can I set the array formula on a range other than `A1`?**  
A: Absolutely. Just change the address in `cells.get("A1")`. The spilled array will always start at the cell you specify and expand right‑and‑down as needed.

**Q: What if my source data is larger than `B1:B10`?**  
A: Replace the static range with a dynamic one, e.g., `B:B` or a named range. The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references on very large sheets; they can impact performance.

---

## Conclusion

We’ve just covered **how to set formula** in Java to **sort unique values Excel**, how to **recalculate formulas**, and how to **generate unique list Excel** using Aspose.Cells’ powerful API. The steps are straightforward: create a workbook, populate data, apply an array formula, trigger calculation, and verify the result.  

From here you can branch out—add conditional formatting, export to PDF, or integrate the method into a web service that delivers ready‑made reports. The core idea stays the same: let Excel’s own functions do the heavy lifting, and let Java orchestrate the process.

Ready to level up your Excel automation? Try swapping `SORT` for `SORTBY` to order by a secondary column, or experiment with `FILTER` to exclude rows that don’t meet business rules. The possibilities are practically endless.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}