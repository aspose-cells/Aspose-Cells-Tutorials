---
category: general
date: 2026-06-30
description: 在 Java 中使用動態陣列公式可讓您建立功能強大的 Excel 工作表。學習使用 Java 建立 Excel 工作簿，並快速計算所有公式。
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: zh-hant
og_description: 在 Java 中使用動態陣列公式可簡化 Excel 自動化。本指南說明如何在 Java 中建立 Excel 工作簿、使用 EXPAND
  函數、LAMBDA 公式，並計算所有公式。
og_title: Java 中的動態陣列公式 – 建立工作簿與計算公式
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Java 中的動態陣列公式：建立 Excel 工作簿並計算所有公式
url: /zh-hant/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 中的動態陣列公式：建立 Excel 活頁簿並計算全部公式

有沒有想過在使用 Java 自動化 Excel 時，**動態陣列公式**是如何運作的？你並不孤單——許多開發者在需要將 `EXPAND` 或 `REDUCE` 等進階公式寫入活頁簿而不開啟 Excel 時，常會卡住。

好消息是，只要幾行 Java 程式碼，就能 **以 Java 方式建立 Excel 活頁簿**、加入這些現代陣列函數，然後 **一次計算全部公式**。本教學會逐步說明每個步驟、解釋 *為什麼* 這麼做，並提供完整、可直接複製貼上的範例程式碼。

## 你將學會

- 如何使用 Java 產生全新的 Excel 活頁簿（不需要 Excel UI）。  
- `EXPAND` 函數的運作原理，以及它如何將簡單範圍轉換為動態陣列。  
- 如何使用 **lambda 公式** 語法搭配 `REDUCE` 進行自訂彙總。  
- 加入許多人忘記存在於 Excel 公式集中的三角與雙曲函數（`COT`、`COTH`）。  
- 只需一行程式碼即可 **計算全部公式**，讓活頁簿即時顯示最新結果。  

> **先備條件：** Java 8+（支援 lambda）、Aspose.Cells for Java 套件，以及對 Excel 公式的基本認識。無需其他相依套件。

---

## 動態陣列公式：設定活頁簿

首先，先取得一個活頁簿物件。Aspose.Cells 的 `Workbook` 類別就是你的入口點；把它想成所有動態陣列公式將要存在的空白畫布。

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*為什麼重要：* 以程式方式實例化活頁簿，可完整掌控檔案格式、文化設定，最重要的是能在不觸碰磁碟的情況下評估公式。

---

## 使用 EXPAND 函數擴展範圍

`EXPAND` 函數是 Excel 用來「溢位」(spill) 範圍至更大區域的解答，大小由你指定。當來源資料在執行時可能長度變動時，它非常適合。

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*說明：*  
- `B1:B3` 為來源範圍。  
- `5` 告訴 Excel 產生五列，即使來源較短也會補空白。  
- `1` 強制只有一欄。  

稍後在 **計算全部公式** 後，`A1` 會以垂直方式溢出五個值，必要時以空白填補。

---

## 以 LAMBDA 公式搭配 REDUCE

如果你想對欄位求和，同時需要自訂累加器，`REDUCE` 結合 **lambda 公式** 就是最佳選擇。語法起初看起來有點怪，但它只是 Java 在 Excel 公式中嵌入小型匿名函式的方式。

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*為什麼使用它？*  
- `0` 為初始種子（起始總和）。  
- `B1:B5` 為要折疊的陣列。  
- `LAMBDA(a,b,a+b)` 表示「取累加器 `a` 與下一個元素 `b`，回傳它們的和」。  

你可以把 `a+b` 換成任何自訂邏輯——平均值、最大值，甚至字串串接——讓 `REDUCE` 成為多功能的建構塊。

---

## 加入三角函數 (COT, COTH)

Excel 內建少數常被忽略的三角輔助函數。以下示範如何在工作表中加入簡單的餘切與其雙曲對應函數。

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*小技巧：* 這些函數會自動遵循活頁簿的計算模式，無需額外程式碼將角度轉為弧度——`PI()` 已幫你完成。

---

## 計算活頁簿中的全部公式

公式寫好之後，我們需要 **計算全部公式**，讓儲存格內實際顯示值，而不是僅顯示公式文字。Aspose.Cells 只要呼叫一個方法即可完成。

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*背後發生了什麼？* 函式庫會遍歷每個儲存格、解析相依關係，並在需要時溢出陣列結果。若處理巨量工作表，可調整計算選項以提升效能，但預設設定已能滿足大多數情境。

---

## 完整可執行範例（直接複製貼上）

以下是完整程式碼，直接貼到 IDE 即可執行。內含匯入、`main` 方法，以及最後的 `save` 呼叫，讓你開啟產生的檔案時即可看到溢位結果。

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**開啟 `DynamicArrayDemo.xlsx` 後的預期輸出：**

| A (結果) | B (來源) |
|----------|----------|
| 10       | 10 |
| 20       | 20 |
| 30       | 30 |
| (空白)   | 40 |
| (空白)   | 50 |
| 150 (總和) |   |
| 1 (cot)  |   |
| 1.0373… (coth) |   |

*留意 `A1` 會溢出五列，即使來源只有三個值。這正是 **動態陣列公式** 的威力所在。*

---

## 常見陷阱與專業提示

- **別忘記設定計算模式**，若在其他地方關閉了自動計算，`calculateFormula()` 會變成無效操作。  
- **陣列溢位衝突：** 若其他儲存格已佔用溢位範圍，Excel 會回傳 `#SPILL!` 錯誤。程式碼中可使用 `worksheet.getCells().clear(0, 0, maxRow, maxColumn)` 事先清除目標區域。  
- **Lambda 語法細節：** `LAMBDA` 函數的參數必須以逗號分隔，不能用分號。少寫逗號會導致整個公式無法解析。  
- **效能小技巧：** 處理上千列時，可在大量寫入資料前呼叫 `workbook.getSettings().setCalculateFormulaOnOpen(false)`，最後再在 `calculateFormula()` 前重新啟用。

---

## 往後的步驟

掌握 **動態陣列公式** 後，可進一步探索：

- **`FILTER`** 與 **`SORT`** 函數，用於即時資料重組。  
- **`SEQUENCE`** 產生不需來源範圍的數值陣列。  
- 結合 **具名範圍** 與 `EXPAND`，打造更乾淨、可重用的公式。  

這些都建立在本教學的概念上——只要更換公式字串，讓 Aspose.Cells 處理其餘工作即可。

---

## 結論

在本指南中，我們示範了如何 **以 Java 建立 Excel 活頁簿**、插入動態陣列公式，並一次計算全部公式，使工作簿即時呈現正確結果。

## 接下來該學什麼？

以下教學與本篇內容緊密相關，進一步深化所學技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在專案中探索其他實作方式。

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Calculate Excel Formulas Java: Optimize with Aspose.Cells](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [Master Excel Array Formulas with Aspose.Cells Java: Streamline Calculations and Formatting](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}