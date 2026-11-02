---
category: general
date: 2026-07-03
description: 學習如何使用 Java 在 Excel 中展開陣列。本教學涵蓋將陣列展開至列、如何使用展開功能，以及如何高效插入公式。
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: zh-hant
og_description: 使用 Java 在 Excel 中展開陣列。跟隨本指南學習如何使用展開功能、在儲存格設定公式，並即時將陣列展開至多列。
og_title: 在 Excel 中使用 Java 展開陣列 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: 使用 Java 在 Excel 中擴充陣列 – 逐步教學
url: /zh-hant/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 Java 展開陣列 – 完整程式指南

有沒有想過 **在 Excel 中展開陣列** 而不必手動拖曳儲存格？你並不孤單。許多開發者在需要以程式方式產生動態範圍時會卡關——尤其是當全新的 Excel `EXPAND` 函數尚未普及時。在本指南中，我們將完整示範 **如何使用 EXPAND**、將公式插入工作表，並讓結果自動溢位到所需的列。完成後，你將能在一行 Java 程式碼中 **將陣列展開至列**。

我們會一步步走過使用 Aspose.Cells for Java 函式庫的完整可執行範例。沒有模糊的參考，只有可直接複製、編譯、執行的具體程式碼。過程中，我們會說明每一步的意義、探討非連續陣列等邊緣情況，並分享官方文件未提及的幾個小技巧。準備好了嗎？讓我們開始吧。

## 前置條件

在開始之前，請確保你已具備：

* 已安裝 Java 17（或任何較新的 JDK）。
* Maven 或 Gradle 以管理相依性。
* 有效的 Aspose.Cells for Java 授權（免費試用版可用於測試）。
* 基本的 Excel 公式概念——如果你曾使用過 `VLOOKUP` 或 `SUMIF`，就沒問題。

如果上述任一項你不熟悉，請先暫停並完成設定；本教學的後續內容假設這些已就緒。

## 第一步：建立 Maven 專案並加入 Aspose.Cells

為了保持整潔，建立一個名為 `ExpandArrayDemo` 的 Maven 專案，並在 `pom.xml` 中加入 Aspose.Cells 相依性：

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **專業提示：** 若使用 Gradle，對應的相依性寫法為 `implementation 'com.aspose:aspose-cells:23.12'`。

Maven 下載完成後，即可撰寫 **在儲存格設定公式** 的 Java 程式碼。

## 第二步：建立 Workbook 並存取第一張工作表

以下程式碼與前面的片段相同，但我們加入了安全檢查與註解，讓你了解每一行背後的 *原因*。

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*為什麼重要：* 建立 `Workbook` 會配置 Aspose 內部管理儲存格、公式與樣式的結構。存取第一張工作表是最常見的入口，特別是剛開始實驗時。

## 第三步：插入 EXPAND 公式 – 「如何插入公式」

接下來就是本教學的核心：**如何插入公式** 以展開陣列。Excel 的 `EXPAND` 函數接受三個參數——來源陣列、所需列數與所需欄數。我們的目標是將 `{1,2,3}` 展開為 **5 列**、**1 欄**。

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

請注意我們使用 `putFormula` 而非 `putValue`。這會告訴 Aspose 將字串視為真正的 Excel 公式，而非純文字。`putFormula` 會自動解析字串並在內部建立公式樹。

### 為什麼要使用 EXPAND？

`EXPAND` 省去手動拖曳填滿手柄的繁瑣步驟。它也支援動態陣列，意味著來源陣列變動時，溢位範圍會自動更新。對於程式化產生報表而言，這相當便利。

## 第四步：強制計算 – 產生結果

當你透過 API **在儲存格設定公式** 時，工作簿不會自動重新計算。必須觸發一次計算流程，才能讓陣列 **展開至列** 並在工作表中顯示值。

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

若省略此步驟，開啟產生的 `.xlsx` 時會只看到公式，直到按下 **F9** 才會出現溢位值。呼叫 `calculate()` 可確保工作簿直接可用。

## 第五步：儲存工作簿並驗證輸出

最後，將工作簿寫入檔案，並可選擇將溢位值印到主控台以作驗證。

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

執行程式後，主控台應顯示：

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel 會以零填滿剩餘列，因為來源陣列只有三個元素。這是 `EXPAND` 的預設行為。若想要以空白取代零，可將陣列包在 `IFERROR` 中或使用 `CHOOSE` 技巧——稍後的「進階變形」章節會進一步說明。

## 進階變形與邊緣案例

### 1. 將水平陣列展開至多個欄位

若同時需要 **展開陣列至列** 與 **欄**，只要修改第三個參數：

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

此時範圍會溢位成 5 × 3 的區塊，缺少的儲存格同樣以零填補。

### 2. 使用具名範圍作為來源

除了直接寫 `{1,2,3}`，也可以引用在執行時可能變動的具名範圍：

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

請確保 `MySourceRange` 已存在（可透過 `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")` 建立）。

### 3. 處理非數值資料

`EXPAND` 也支援文字。例如：

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

額外的列會顯示空字串，而非零。

### 4. 使用 IFERROR 避免零填充

若希望看到空白而非零，可將 `EXPAND` 包在 `IFERROR` 中：

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

如此第 4、5 列會真正保持空白。

## 常見陷阱與避免方式

| 陷阱 | 為什麼會發生 | 解決方法 |
|---------|----------------|-----|
| **公式未重新計算** | 忘記呼叫 `ws.getCells().calculate()` | 在 `putFormula` 後一定要呼叫 `calculate()`。 |
| **零值出現在預期空白的地方** | `EXPAND` 預設以零填充 | 使用 `IFERROR(..., "")` 或搭配 `CHOOSE`。 |
| **儲存格位址錯誤** | 使用 `"A0"` 或 `"1A"` | Excel 位址從 1 開始；Aspose 需要 `"A1"` 形式。 |
| **函式庫版本不相容** | 使用不支援 `EXPAND` 的舊版 Aspose.Cells | 升級至最新版本（本文撰寫時為 23.12）。 |

## 完整範例（結合所有步驟）

以下是可直接複製貼上的完整程式。存為 `ExpandArrayDemo.java`、編譯並執行。

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

執行此程式會產生一個 Excel 檔案，**A1 儲存格** 內含 `EXPAND` 公式，A 欄第 1‑5 列分別顯示 `1, 2, 3, 0, 0`。開啟檔案即可立即看到相同結果——不需要手動拖曳。

## 結語

你剛剛學會了如何使用 Java **在 Excel 中展開陣列**、**使用 EXPAND**，以及如何 **在儲存格設定公式** 並 **程式化展開陣列至列**。透過 Aspose.Cells，你可以省去繁雜的 UI 操作，讓程式自行完成重活。無論是建構報表引擎、自動化資料輸入工具，或是自訂試算表產生器，此技巧都能為你節省大量時間。

接下來可以嘗試將靜態陣列換成從其他工作表取得的動態範圍、實驗多欄位溢位，或將 `EXPAND` 與 `FILTER` 結合，打造強大的資料轉換。可能性無限，而你現在已擁有堅實的基礎可以持續發展。

有問題或想分享酷炫的使用案例嗎？歡迎留言。

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你對 API 功能的掌握，並提供其他實作方式的範例說明。

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}