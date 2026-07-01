---
category: general
date: 2026-06-30
description: 使用 Java 排序 Excel 中的唯一值。學習如何設定公式、重新計算公式，以及使用 Aspose.Cells 產生唯一清單於 Excel。
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: zh-hant
og_description: 使用 Java 排序 Excel 唯一值。本指南示範如何設定公式、重新計算，以及在數分鐘內於 Excel 產生唯一清單。
og_title: Excel 排序唯一值 – 陣列公式的 Java 教學
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
title: Excel 排序唯一值 – 完整 Java 指南：設定陣列公式
url: /zh-hant/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 排序唯一值 – 完整 Java 指南：設定陣列公式

有沒有想過如何在 Excel 中 **排序唯一值** 而不必拖曳公式？你並不是唯一有此需求的人。在許多報表情境下，你需要一個乾淨、按字母順序排列的唯一條目清單，手動操作相當麻煩。  

好消息是？只需幾行 Java 程式碼，你就可以在工作表上 **設定陣列公式**，再 **重新計算公式**，讓溢位範圍自動填入。本教學將逐步說明全部流程——從建立活頁簿到產生 Excel 風格的唯一清單——讓你可以直接將解決方案嵌入應用程式中。

## 本教學涵蓋內容

- 使用 Aspose.Cells 建立 Java 專案（此程式碼片段所依賴的函式庫）。  
- 結合 `SORT` 與 `UNIQUE` 函數以 **產生 Excel 唯一清單** 結果。  
- 以程式方式將 **陣列公式** 套用至儲存格。  
- 觸發計算，使 **如何重新計算公式** 步驟即時執行。  
- 驗證輸出，並針對空白儲存格或非連續範圍等邊緣情況調整解決方案。  

完成本指南後，你將能將即用即拋的方法嵌入任何需要匯出乾淨 Excel 工作表的 Java 服務中。

> **專業提示：** 若你已在使用 Maven，將 Aspose.Cells 加入為相依性即可免除手動管理 JAR 檔案的麻煩。

---

## 前置條件

| 需求 | 為何重要 |
|------|----------|
| Java 8 或更新版本 | Aspose.Cells 以 Java 8+ 為目標。 |
| Maven（或 Gradle） | 簡化相依性管理。 |
| Aspose.Cells for Java | 提供我們將使用的 `Workbook`、`Worksheet` 與公式 API。 |
| 基本熟悉 Excel 函數 | 了解 `SORT` 與 `UNIQUE` 有助於調整程式碼。 |

> *如果尚未取得 Aspose.Cells，請將以下內容加入你的 `pom.xml`*：

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

## 步驟 1：建立新活頁簿（設定公式的起點）

首先，我們需要一個空白的活頁簿。可以把它想成未來要在儲存格 `A1` 上 **設定陣列公式** 的空白畫布。

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *為何要建立新活頁簿？*  
> 這可確保環境乾淨，避免隱藏的公式干擾測試資料。

## 步驟 2：填入範例資料（可選但有助於說明）

為了清楚觀察結果，讓我們在 **B** 欄填入一些重複的資料。

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

> *為何使用 B 欄？*  
> 我們即將撰寫的公式會參照 `B1:B10`，將資料放在此欄可呼應經典的 Excel 範例。

## 步驟 3：設定 **排序唯一值 Excel** 的陣列公式

現在魔法發生了。我們將 `UNIQUE`（去除重複）與 `SORT`（按字母順序排序）結合。產生的表達式是一個 **陣列公式**，表示它會自動溢位到相鄰儲存格。

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### 工作原理

- `UNIQUE(B1:B10)` 會掃描該範圍，回傳一個垂直的唯一字串陣列。  
- `SORT(...)` 取得該陣列並以升冪排序。  
- 將整個表達式以 `=` 包起來，並呼叫 `setFormulaArray`，告訴 Aspose.Cells 將結果視為 **溢位陣列**，就像 Excel 的行為一樣。

> **注意：** 若使用較舊版的 Excel，沒有 `SORT` 或 `UNIQUE`，可改用搭配 **LET** 函數的 `SORT(UNIQUE(...))`，或使用傳統陣列公式（`=INDEX(...)`）。本教學著重於現代動態陣列方式，因為它是目前 **產生 Excel 唯一清單** 最簡潔的做法。

## 步驟 4：重新計算公式，使溢位範圍被填入

公式寫入後，活頁簿不會自動評估。這時就需要 **如何重新計算公式** 的步驟。

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

呼叫 `calculateFormula()` 會強制 Aspose.Cells 執行 Excel 引擎，將排序後的唯一值填入 `A1`、`A2` … 等儲存格。

> *為何不依賴延遲評估？*  
> 在伺服器端情境下，你通常需要在計算完成後立即取得可匯出的資料（CSV、PDF 等），因此明確呼叫可保證一致性。

## 步驟 5：驗證結果（可選除錯）

將溢位的值印到主控台總是個好方法——特別是當你自學新 API 時。

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

執行程式會印出：

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

開啟 `SortedUniqueValues.xlsx`，即可看到相同的資料從 `A1` 向下溢位。

## 處理邊緣案例

### 來源範圍中的空白儲存格

若 `B1:B10` 含有空白，`UNIQUE` 會將其視為一個獨立條目。若要忽略空白，可將範圍包在 `FILTER` 中：

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### 非連續資料

當資料分散於多個欄位時，可在套用 `UNIQUE` 前使用 `CHOOSE` 或 `TEXTJOIN` 進行合併。例如：

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

這些調整展示了 **如何設定公式** 在更複雜情境下的彈性。

## 完整範例（結合所有步驟）

以下是完整、可執行的 Java 程式。將它複製貼上至 IDE，加入 Aspose.Cells 相依性，然後點選 *Run*。

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

**預期輸出**（在主控台顯示）與先前討論的已排序、去重清單相符。開啟產生的 Excel 檔案，即可看到相同的值從 `A1` 向下溢位。

## 常見問題

**Q: 這在較舊的 Excel 版本（Office 365 之前）是否可用？**  
A: `SORT` 與 `UNIQUE` 函數屬於 Excel 365 引入的動態陣列引擎。對於舊版檔案，需要使用傳統陣列公式，例如 `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`。Aspose.Cells 仍能評估它們，但語法較冗長。

**Q: 我可以將陣列公式設定在除 `A1` 之外的其他儲存格嗎？**  
A: 當然可以。只要將 `cells.get("A1")` 的地址改成你想要的儲存格即可。溢位陣列會從你指定的儲存格開始，依需求向右與向下展開。

**Q: 若我的來源資料超過 `B1:B10` 該怎麼辦？**  
A: 可將固定範圍改為動態範圍，例如 `B:B` 或命名範圍。公式則變為 `=SORT(UNIQUE(B:B))`。在極大工作表上使用整欄參照需留意效能影響。

## 結論

我們剛剛說明了在 Java 中 **如何設定公式** 以 **排序 Excel 唯一值**，以及 **如何重新計算公式**，並使用 Aspose.Cells 強大的 API **產生 Excel 唯一清單**。步驟相當簡單：建立活頁簿、填入資料、套用陣列公式、觸發計算，最後驗證結果。  

從此你可以延伸應用——加入條件格式、匯出為 PDF，或將此方法整合至提供即時報表的 Web 服務。核心概念不變：讓 Excel 自身的函數負責繁重運算，讓 Java 來協調整個流程。  

準備好提升 Excel 自動化的層次了嗎？可以嘗試將 `SORT` 換成 `SORTBY` 以依次要欄位排序，或使用 `FILTER` 排除不符合業務規則的列。可能性幾乎無限。

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}