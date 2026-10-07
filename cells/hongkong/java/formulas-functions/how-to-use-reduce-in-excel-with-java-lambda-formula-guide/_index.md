---
category: general
date: 2026-06-08
description: 如何在 Excel 中使用 Java 搭配 Aspose.Cells 進行 reduce。學習 Excel 的 lambda 公式、Java
  動態陣列、如何撰寫 lambda，以及使用 reduce 進行加總，提供清晰的逐步教學。
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: zh-hant
og_description: 如何在 Excel 中使用 Java 的 reduce。精通 Lambda 公式、Excel 動態陣列與 Java，並透過完整可執行範例實作
  reduce 求和。
og_title: 如何在 Excel 中使用 Java 的 Reduce – Lambda 公式指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: 如何在 Excel 中使用 Java 的 Reduce – Lambda 公式指南
url: /zh-hant/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Reduce 與 Java – Lambda 公式指南

是否曾經好奇在編寫 Java 程式碼時，**如何在 Excel 中使用 reduce**？你並不孤單。許多開發者在嘗試將 Excel 的新動態陣列函數與基於 Java 的自動化結合時卡住了，而答案並不像最初看起來那麼神祕。

在本教學中，我們將逐步示範一個具體範例，說明 **如何在 Excel 中使用 reduce** 搭配 **lambda formula Excel** 表達式，全部由 Aspose.Cells for Java 函式庫提供支援。完成後，你將能在 Java 中產生動態陣列、撰寫 lambda 函式，並計算 **使用 reduce 的總和**——不需要手動操作試算表。

---

## 您將建立的內容

- 完全由 Java 建立的全新活頁簿。  
- 使用 **EXPAND** 動態陣列在 A1:A5 儲存格中填入 1‑5 的數字。  
- 使用 **REDUCE** 公式，透過 **lambda formula Excel** 計算上述數字的總和。  
- 一個已儲存的 `.xlsx` 檔案，可在任何試算表程式中開啟以驗證結果。

不需要外部巨集、也不需要 VBA——只要純粹的 Java 程式碼與 Excel 的現代函數。

---

## 前置條件

- Java 17（或任何較新的 JDK）——舊版仍可使用，但會失去 `var` 語法的便利。  
- Aspose.Cells for Java（免費試用版已足以完成本示範）。  
- 具備基本的 Java 語法與 Excel 公式概念。  

如果你對 **dynamic arrays java** 還不熟悉，別擔心——本指南會逐一說明每個步驟。

---

## 步驟 1：設定專案並匯入 Aspose.Cells

首先，將 Aspose.Cells 的 Maven 依賴加入 `pom.xml`（或手動下載 JAR）。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **專業提示：** 請保持相依套件為最新版本；較新的版本會提升公式計算速度，這在大型工作表中執行 **how to use reduce** 時相當重要。

---

## 步驟 2：建立活頁簿並存取第一張工作表

接下來，我們會建立一個全新的活頁簿。這是學習 **how to use reduce** 的基礎，因為 workbook 物件提供了一個可以放入公式的沙盒環境。

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*為什麼這很重要：* `Workbook` 類別抽象化整個 Excel 檔案，而 `Worksheet` 代表單一工作表。稍後你會看到 **dynamic arrays java** 能透過在 A1 放置單一公式，就為多個儲存格填值。

---

## 步驟 3：使用 EXPAND 產生垂直陣列

Excel 的 `EXPAND` 函數可以將值溢位到一個範圍。我們將利用它在 A 欄產生 1 到 5 的數字。

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

如果你開啟產生的活頁簿，A1:A5 會分別顯示 1、2、3、4、5。這就是 **dynamic arrays java** 的概念——一個公式即可填滿整個範圍。

---

## 步驟 4：撰寫 REDUCE Lambda 以求陣列總和

這裡就是回答核心問題的地方：**how to use reduce** 在 Excel 中如何透過 Java 實作。`REDUCE` 函數會遍歷陣列，套用你提供的 lambda。此例中我們將它用來加總數字。

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

讓我們拆解說明：

- `0` – 初始累加器值（`acc`）。  
- `A1:A5` – 先前使用 **EXPAND** 產生的陣列。  
- `LAMBDA(acc, x, acc + x)` – **lambda formula Excel**，將每個元素（`x`）加到累加器（`acc`）上。  

公式執行後，`B1` 會顯示 **15**，即 1‑5 的 **sum with reduce**。

> **如何在 Excel 中撰寫 lambda**？把它想成匿名函式，前面的參數是輸入，最後的表達式即為回傳值。在 Java 中我們只需要把文字嵌入，真正的運算由 Excel 引擎完成。

---

## 步驟 5：儲存活頁簿

最後，我們將活頁簿寫入磁碟，讓你可以在 Excel、Google Sheets 或任何支援 `.xlsx` 的檢視器中開啟。

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

開啟檔案後會看到：

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**sum with reduce** 出現在 B1，證明我們已成功示範 **how to use reduce** 搭配 **lambda formula Excel** 的使用方式。

---

## 完整範例程式

以下是可直接執行的完整 Java 程式碼。複製貼上至 IDE，調整輸出目錄後點選 **Run**。

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**預期結果**：開啟 `new-functions.xlsx` 後

- **A1:A5** 儲存格分別為 `1, 2, 3, 4, 5`。  
- **B1** 顯示 `15`，即 **sum with reduce** 的結果。

---

## 常見問題與邊緣情況

### 如果需要水平陣列而非垂直陣列該怎麼做？

只要在 `EXPAND` 中交換列與欄的參數。若要在 B1:F1 產生水平溢位：

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### 能否使用 REDUCE 進行乘法而非加總？

當然可以，只要改變 lambda 的內容：

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

此時 B1 會顯示 `120`（5 ! = 120）。

### Aspose.Cells 支援自訂 LAMBDA 函式嗎？

支援，你可以透過活頁簿的 `Names` 集合定義具名 LAMBDA，之後像內建公式一樣呼叫。這屬於較深入的主題，未來會在 **how to write lambda** 的教學中詳細說明。

### 舊版 Excel 無法辨識 REDUCE 會怎樣？

如果目標是 Excel 2019 或更早的版本，公式會回傳 `#NAME?`。在此情況下

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你對 API 功能的掌握，並探索在專案中實作的其他方式。

- [精通 Aspose.Cells Java：如何在 Excel 活頁簿中中斷公式計算](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [如何使用 Aspose.Cells for Java 將 Excel 儲存格名稱轉換為索引：步驟說明](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 建立與格式化 Excel 儲存格：步驟說明](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}