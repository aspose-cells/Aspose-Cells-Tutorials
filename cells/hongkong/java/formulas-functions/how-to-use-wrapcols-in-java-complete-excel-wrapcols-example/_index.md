---
category: general
date: 2026-06-21
description: 如何在 Aspose.Cells Java 中使用 WRAPCOLS 將陣列轉換為列、將公式寫入儲存格，並以公式填充儲存格——逐步指南。
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: zh-hant
og_description: 如何在 Java 中使用 Aspose.Cells 的 WRAPCOLS 將陣列轉換為行、將公式寫入儲存格，並一次性為儲存格填入公式。
og_title: 如何在 Java 中使用 WRAPCOLS – 完整的 Excel WRAPCOLS 範例
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
title: 如何在 Java 中使用 WRAPCOLS – 完整的 Excel WRAPCOLS 範例
url: /zh-hant/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 WRAPCOLS – 完整的 Excel WRAPCOLS 範例

有沒有想過 **如何使用 WRAPCOLS**，當你需要將簡單的陣列轉換成 Excel 中整齊的表格時？你並不是唯一有此疑問的人。許多開發者在第一次看到 `WRAPCOLS` 函式時會卡住，心想「我要怎麼從 Java 把這個公式寫入儲存格？」好消息是？只要掌握正確步驟，其實相當簡單。

在本教學中，我們將逐步說明一個可完整執行的 Aspose.Cells Java 範例，該範例 **將陣列轉換為列**，直接將公式寫入儲存格，並示範如何在實務情境中 **以公式填充儲存格**。完成後，你將對 **excel wrapcols 範例** 有清晰的了解，並能將其套用到自己的專案中。

## 前置條件

- Java 17 或更新版本（程式碼相容於任何近期的 JDK）。
- Aspose.Cells for Java 函式庫（可從 Maven Central 取得最新的 JAR）。
- 具備 Java 語法與 Excel 公式的基本認識。
- IDE 或簡易文字編輯器皆可——不需要特殊工具。

全部準備好了嗎？太好了，讓我們開始吧。

## 步驟 1：設定專案並載入活頁簿

首先——建立一個新的 Maven（或 Gradle）專案，並加入 Aspose.Cells 相依性：

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

現在我們可以載入既有的活頁簿（或建立新的），並取得第一個工作表：

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

> **為什麼要載入活頁簿** – Aspose.Cells 以記憶體中的 Excel 檔案表示方式運作。透過載入（或建立）活頁簿，我們即可存取儲存格、列與公式，這對任何 **write formula to cell** 操作都是必須的。

## 步驟 2：將 WRAPCOLS 公式插入儲存格

本教學的核心在於 `WRAPCOLS` 函式。它接受一維陣列，並將其「包裝」成指定的欄數，剩餘的資料會自動溢位到新列。以下是我們將使用的語法：

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

請注意公式是以純字串傳遞給 `setFormula`。Aspose.Cells 會負責繁重的工作——解析公式、計算結果，並將結果溢位至工作表。這是 **populate cells with formula** 的最直接方式，無需手動遍歷列與欄。

### 公式功能說明

- `{1,2,3}` – 包含三個數字的文字陣列。
- `2` – 每列的欄數。
- 結果：
  - **A1** = 1，**B1** = 2
  - **A2** = 3，**B2** = （空白）

如果想要三欄，只需將第二個參數改為 `3`，陣列就會填滿單一列。

## 步驟 3：儲存活頁簿並驗證輸出

既然公式已放在 **A1**，讓我們將活頁簿寫入磁碟，這樣你就能在 Excel 中開啟並看到溢位結果：

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

開啟 `output.xlsx`，你會看到正如說明所述——第一列有兩欄，剩餘的值出現在第二列。這就是 **excel wrapcols example** 的核心。

## 步驟 4：擴充範例 – 轉換較大的陣列

實務專案很少只處理三個數字。假設你有較大的集合，例如 `{10,20,30,40,50,60,70}`，且希望每列有三欄。以下說明如何調整程式碼：

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

現在溢位會從 **C5** 開始，產生以下結果：

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

這說明了如何透過調整公式字串，動態 **convert array to rows**。不需要迴圈或手動指定儲存格——Aspose.Cells 會處理其餘工作。

## 步驟 5：處理邊緣情況與常見陷阱

### 1. 空陣列

如果陣列文字是空的（`{}`），`WRAPCOLS` 會回傳 `#VALUE!` 錯誤。為避免破壞工作表，請在產生公式時加以防護：

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. 非數值資料

`WRAPCOLS` 也支援文字。例如，`WRAPCOLS({"A","B","C","D"},2)` 會產生兩欄的字串佈局。只要記得在陣列文字內為字串加上引號即可。

### 3. 相容性

`WRAPCOLS` 函式在 Excel 365 以及 Excel 2019 以上（Office 2019、Excel 網頁版）皆可使用。若需支援較舊版本，則必須改用手動迴圈或其他支援溢位的函式。

## 步驟 6：實用技巧與進階竅門

- **進階技巧：** 若需依使用者的區域設定使用特定分隔符（逗號或分號），可使用 `Cell.setFormulaLocal`。
- **注意：** 可能會覆寫既有資料。溢位區域會取代目標範圍內已存在的內容。
- **效能說明：** 設定公式的成本很低，主要工作發生在 **save** 或 **recalculate** 活頁簿時。若產生數千個公式，建議關閉自動計算（稍後呼叫 `wb.calculateFormula()`）以提升效能。

## 完整可執行範例

以下是完整、可直接執行的 Java 類別，包含我們前面討論的所有內容：

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

**預期輸出：** 開啟 `output.xlsx`，你會看到三個不同的溢位區域：

- **A1:B2** – 數字 1‑3 包裝成兩欄。
- **C5:E7** – 數字 10‑70 包裝成三欄。
- **G1:H2** – 水果名稱包裝成兩欄。

## 結論

我們剛剛說明了如何在 Aspose.Cells for Java 中 **使用 WRAPCOLS**，展示了如何 **convert array to rows**、**write formula to cell**，以及 **populate cells with formula**，以簡潔且可重複使用的方式完成。此方法省去繁瑣的迴圈，利用 Excel 原生的溢位行為，讓程式碼保持精簡。

準備好接受下一個挑戰了嗎？試著將 `WRAPCOLS` 與動態資料來源結合——例如從資料庫取得值、即時組合陣列字串，讓 Excel 完成排版。你也可以嘗試其他溢位函式，如 `SEQUENCE` 或 `FILTER`，以建立更豐富的報表。

如果遇到任何問題，歡迎在下方留言或參考 Aspose 的完整文件。祝開發順利，盡情體驗從 Java 操作現代 Excel 公式的威力！

![如何使用 wrapcols 範例](/images/wrapcols-demo.png "在 Java 中使用 wrapcols – 溢位資料的螢幕截圖")


## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何在 Excel 中使用 Aspose.Cells for Java 選取儲存格範圍（2023 指南）](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [如何在 Excel 中使用 Aspose.Cells for Java 設定作用中儲存格：完整指南](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [如何在 Excel 活頁簿中使用 Aspose.Cells for Java 插入列](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}