---
category: general
date: 2026-06-30
description: Java を使用して Excel のユニークな値をソートします。式の設定方法、式の再計算方法、そして Aspose.Cells を使ってユニークなリストを
  Excel に生成する方法を学びましょう。
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: ja
og_description: JavaでExcelのユニークな値をソートする。このガイドでは、数式の設定、数式の再計算、そして数分でユニークなリストをExcelで生成する方法を示します。
og_title: Excelでユニーク値を並べ替える – 配列数式のためのJavaチュートリアル
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
title: Excelでユニーク値を並べ替える – 配列数式設定の完全Javaガイド
url: /ja/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sort Unique Values Excel – Complete Java Guide to Set Array Formulas

Excel で **sort unique values Excel** を、数式をドラッグせずに実現したいと思ったことはありませんか？ あなたは一人ではありません。多くのレポートシナリオでは、重複のないエントリをアルファベット順に整列したクリーンなリストが必要ですが、手作業で行うのは面倒です。  

良いニュースです。数行の Java コードでワークシートに **set array formula** を設定し、**recalculate formulas** を実行すれば、スピル範囲が自動的に埋まります。このチュートリアルでは、ワークブックの作成から Excel スタイルのユニークリスト生成まで、すべての手順を解説します。これにより、ソリューションをそのままアプリケーションに組み込むことができます。

## What This Tutorial Covers

- Aspose.Cells（コードスニペットの基盤となるライブラリ）を使用した Java プロジェクトのセットアップ。  
- `SORT` と `UNIQUE` 関数を組み合わせて **generate unique list Excel** の結果を作成。  
- プログラムから **array formula** をセルに適用。  
- 計算パスをトリガーして **how to recalculate formulas** のステップを即座に実行。  
- 出力を検証し、空セルや非連続範囲といったエッジケースに対応する方法を調整。

このガイドを終える頃には、クリーンな Excel シートをエクスポートする必要がある任意の Java サービスに、すぐに使えるメソッドを組み込めるようになります。

> **Pro tip:** すでに Maven を使用している場合、Aspose.Cells を依存関係として追加すれば JAR ファイルを手動で扱う手間が省けます。

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose.Cells は Java 8+ を対象としています。 |
| Maven (or Gradle) | 依存関係管理が簡素化されます。 |
| Aspose.Cells for Java | `Workbook`、`Worksheet`、数式 API を提供します。 |
| Basic familiarity with Excel functions | `SORT` と `UNIQUE` の理解がコードの適応に役立ちます。 |

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

まず空のワークブックを作成します。これは、後でセル `A1` に **set array formula** を設定するための空白キャンバスと考えてください。

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

結果をはっきり確認できるよう、列 **B** に重複エントリをいくつか入力します。

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

ここで魔法が起きます。`UNIQUE`（重複除去）と `SORT`（アルファベット順ソート）を組み合わせます。得られる式は **array formula** であり、隣接セルへ自動的にスピルします。

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### How It Works

- `UNIQUE(B1:B10)` は範囲を走査し、重複しない文字列の縦配列を返します。  
- `SORT(...)` はその配列を昇順に並べ替えます。  
- 全体を `=` で囲み、`setFormulaArray` を呼び出すことで、Aspose.Cells に **spilled array** として扱わせます。  

> **Note:** If you’re using an older version of Excel that lacks `SORT` or `UNIQUE`, you can fall back to `SORT(UNIQUE(...))` with the **LET** function or use legacy array formulas (`=INDEX(...)`). The tutorial focuses on the modern dynamic array approach because it’s the cleanest way to **generate unique list Excel** today.

---

## Step 4: Recalculate Formulas So the Spilled Range Is Populated

数式を設定しただけではワークブックは自動的に評価されません。ここで **how to recalculate formulas** のステップが必要です。

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

`calculateFormula()` を呼び出すことで、Aspose.Cells が Excel エンジンを実行し、セル `A1`、`A2`、… にソートされたユニーク値が埋め込まれます。

> *Why not rely on lazy evaluation?*  
> In a server‑side context you often need the data ready for export (CSV, PDF, etc.) right after the calculation, so an explicit call guarantees consistency.

---

## Step 5: Verify the Result (Optional Debugging)

新しい API を学習中は、スピルされた値をコンソールに出力して確認すると安心です。

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

プログラムを実行すると次が表示されます：

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

`SortedUniqueValues.xlsx` を開くと、`A1` から下方向に同じデータがスピルしていることが確認できます。

---

## Handling Edge Cases

### Empty Cells in the Source Range

`B1:B10` に空白が含まれると、`UNIQUE` はそれも別個のエントリとして扱います。空白を除外したい場合は、`FILTER` で範囲をラップします：

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Non‑Contiguous Data

データが複数列にまたがる場合は、`CHOOSE` や `TEXTJOIN` で結合してから `UNIQUE` を適用できます。例：

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

これらの調整により、**how to set formula** をより複雑なシナリオにも応用できることが分かります。

---

## Full Working Example (All Steps Combined)

以下は完全に実行可能な Java プログラムです。IDE に貼り付け、Aspose.Cells の依存関係を追加して *Run* をクリックしてください。

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