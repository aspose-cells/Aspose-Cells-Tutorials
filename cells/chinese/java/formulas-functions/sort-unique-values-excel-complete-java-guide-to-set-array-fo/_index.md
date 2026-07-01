---
category: general
date: 2026-06-30
description: 使用 Java 对 Excel 中的唯一值进行排序。了解如何设置公式、重新计算公式，并使用 Aspose.Cells 生成唯一列表。
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: zh
og_description: 使用 Java 对 Excel 中的唯一值进行排序。本指南展示了如何设置公式、重新计算公式，并在几分钟内生成唯一列表。
og_title: Excel 排序唯一值 – Java 数组公式教程
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
title: Excel 排序唯一值 – 完整的 Java 指南：设置数组公式
url: /zh/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 排序唯一值 – 完整的 Java 指南：设置数组公式

Ever wondered how to **sort unique values Excel** without dragging formulas around? You're not the only one. In many reporting scenarios you need a clean, alphabetically‑sorted list of distinct entries, and doing it manually is a pain.  

The good news? With a few lines of Java code you can **set array formula** on a worksheet, then **recalculate formulas** so the spilled range fills itself automatically. In this tutorial we’ll walk through everything—from creating a workbook to generating a unique list Excel style—so you can embed the solution straight into your application.

## 本教程涵盖内容

- 使用 Aspose.Cells 设置 Java 项目（为代码片段提供支持的库）。  
- 将 `SORT` 和 `UNIQUE` 函数结合使用，以 **generate unique list Excel** 结果。  
- 以编程方式向单元格应用 **array formula**。  
- 触发计算过程，使 **how to recalculate formulas** 步骤即时完成。  
- 验证输出并针对空单元格或非连续范围等边缘情况微调解决方案。

By the end of this guide you’ll be able to drop a ready‑to‑use method into any Java service that needs to export clean Excel sheets.

> **Pro tip:** If you’re already using Maven, adding Aspose.Cells as a dependency saves you from manually handling JAR files.

---

## 前提条件

| 要求 | 原因/重要性 |
|-------------|----------------|
| Java 8 或更高 | Aspose.Cells 目标是 Java 8+. |
| Maven（或 Gradle） | 简化依赖管理。 |
| Aspose.Cells for Java | 提供我们将使用的 `Workbook`、`Worksheet` 和公式 API。 |
| 基本的 Excel 函数熟悉度 | 了解 `SORT` 和 `UNIQUE` 有助于你适配代码。 |

> *如果你还没有 Aspose.Cells，请将以下内容添加到你的 `pom.xml` 中：*

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## 步骤 1：创建新工作簿（设置公式的开始）

First we need a blank workbook. Think of it as the empty canvas where we’ll later **set array formula** on cell `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *为什么要创建新工作簿？*  
> It guarantees a clean environment, avoiding hidden formulas that could interfere with our test data.

---

## 步骤 2：填充示例数据（可选但有帮助）

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

> *为什么使用 B 列？*  
> The formula we’ll write references `B1:B10`, so keeping the data there mirrors the classic Excel example.

---

## 步骤 3：设置一个 **Sort Unique Values Excel** 的数组公式

Now the magic happens. We combine `UNIQUE` (to strip duplicates) with `SORT` (to order them alphabetically). The resulting expression is an **array formula**, meaning it will spill into adjacent cells automatically.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### 工作原理

- `UNIQUE(B1:B10)` 扫描该范围并返回一个垂直的唯一字符串数组。  
- `SORT(...)` 对该数组进行升序排序。  
- 将整个表达式用 `=` 包裹并调用 `setFormulaArray`，告诉 Aspose.Cells 将结果视为 **spilled array**，就像 Excel 一样。

> **注意：**如果你使用的 Excel 版本较旧，缺少 `SORT` 或 `UNIQUE`，可以使用 **LET** 函数回退到 `SORT(UNIQUE(...))`，或使用传统的数组公式（`=INDEX(...)`）。本教程侧重于现代的动态数组方法，因为它是当今 **generate unique list Excel** 最简洁的方式。

---

## 步骤 4：重新计算公式以填充溢出范围

After the formula is in place, the workbook doesn’t automatically evaluate it. This is where the **how to recalculate formulas** step comes in.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Calling `calculateFormula()` forces Aspose.Cells to run the Excel engine, filling cells `A1`, `A2`, … with the sorted unique values.

> *为什么不依赖惰性求值？*  
> In a server‑side context you often need the data ready for export (CSV, PDF, etc.) right after the calculation, so an explicit call guarantees consistency.

---

## 步骤 5：验证结果（可选调试）

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

## 处理边缘情况

### 源范围中的空单元格

If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry. To ignore blanks, wrap the range with `FILTER`:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### 非连续数据

When your data lives in multiple columns, you can join them with `CHOOSE` or `TEXTJOIN` before applying `UNIQUE`. For example:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

These tweaks demonstrate the flexibility of **how to set formula** for more complex scenarios.

---

## 完整工作示例（所有步骤合并）

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

## 常见问题

**问：这在旧版 Excel（Office 365 之前）能工作吗？**  
答：`SORT` 和 `UNIQUE` 函数是 Excel 365 引入的动态数组引擎的一部分。对于旧版文件，需要使用传统的数组公式，如 `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`。Aspose.Cells 仍然可以求值，但语法更冗长。

**问：我可以在除 `A1` 之外的范围设置数组公式吗？**  
答：当然可以。只需更改 `cells.get("A1")` 中的地址即可。溢出数组始终从你指定的单元格开始，并根据需要向右和向下扩展。

**问：如果我的源数据大于 `B1:B10`，怎么办？**  
答：将静态范围替换为动态范围，例如 `B:B` 或命名范围。公式变为 `=SORT(UNIQUE(B:B))`。在非常大的工作表上使用整列引用时要小心，因为可能影响性能。

---

## 结论

We’ve just covered **how to set formula** in Java to **sort unique values Excel**, how to **recalculate formulas**, and how to **generate unique list Excel** using Aspose.Cells’ powerful API. The steps are straightforward: create a workbook, populate data, apply an array formula, trigger calculation, and verify the result.  

From here you can branch out—add conditional formatting, export to PDF, or integrate the method into a web service that delivers ready‑made reports. The core idea stays the same: let Excel’s own functions do the heavy lifting, and let Java orchestrate the process.

Ready to level up your Excel automation? Try swapping `SORT` for `SORTBY` to order by a secondary column, or experiment with `FILTER` to exclude rows that don’t meet business rules. The possibilities are practically endless.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}