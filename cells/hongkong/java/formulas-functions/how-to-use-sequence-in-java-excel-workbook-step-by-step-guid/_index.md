---
category: general
date: 2026-06-18
description: 在 Java 中使用序列生成動態陣列並將工作簿另存為 xlsx – 完整、實作導向的開發者教學
draft: false
keywords:
- how to use sequence
- save workbook as xlsx
- use sequence function
- create excel workbook java
- set dynamic array formula
language: zh-hant
og_description: 如何在 Java 中使用序列來建立動態陣列並將工作簿另存為 xlsx。請參考本指南，獲得完整且可執行的解決方案。
og_title: 在 Java Excel 活頁簿中使用 SEQUENCE 的方法 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  headline: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  type: TechArticle
- description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  name: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  steps:
  - name: Generate a Calendar Header
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)"); ```'
  - name: Create a Multiplication Table
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
      ```'
  - name: Expected Output
    text: '- An `dynamic_sequence_demo.xlsx` file appears in your project directory.
      - Opening the file in Excel shows a 3×2 block of numbers (1‑6) automatically
      filled.'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Dynamic Arrays
title: 如何在 Java Excel 工作簿中使用 SEQUENCE – 逐步指南
url: /zh-hant/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java Excel 工作簿中使用 SEQUENCE – 步驟指南

有沒有想過 **如何使用 sequence** 在不寫迴圈的情況下填滿一系列儲存格？你並不是唯一有此疑問的人。在現代 Excel 中，`SEQUENCE` 函數會產生一個溢位範圍（spill‑range）的數字列，而透過 Java，你可以直接把這股力量寫入工作簿。

在本教學中，我們將一步步示範如何在 Java 中建立 Excel 工作簿、**設定動態陣列公式**（使用 `SEQUENCE`）、重新計算工作表，最後 **將工作簿另存為 xlsx**。完成後，你將得到一個可直接放入任何專案的可執行程式碼範例。

## 您需要的環境

- Java 17 或更新版本（程式碼在 Java 8+ 皆可執行，但使用最新 JDK 可獲得最佳效能）。  
- Aspose.Cells for Java（或任何支援動態陣列公式的函式庫）。  
- IDE 或簡易文字編輯器——Visual Studio Code 亦可。  

除上述函式庫外，無需額外的 Maven 外掛或不常見的相依套件。

## 步驟 1：使用 Java 建立 Excel 工作簿

首先，我們要 **create excel workbook java**。在此步驟中，我們會建立一個全新的 `Workbook` 物件，作為所有工作表的容器。

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();
```

*為什麼這很重要*：`Workbook` 類別是任何 Excel 操作的入口點。把它想像成一本空白筆記本，等著你寫入資料。

## 步驟 2：取得第一張工作表

接下來，我們需要一個放置公式的地方。預設情況下，新工作簿會自動帶有一張工作表，我們只要把它取出即可。

```java
        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*小技巧*：如果需要多張工作表，只要呼叫 `workbook.getWorksheets().add("Sheet2")` 並重複相同的流程。

## 步驟 3：**設定動態陣列公式** 使用 SEQUENCE 函數

現在進入本教學的核心——**如何在儲存格內使用 sequence**。公式 `=SEQUENCE(3,2)` 會在放置該公式的儲存格起始位置，產生一個 3 行 2 欄的溢位範圍。

```java
        // Step 3: Insert a dynamic array formula that spills into B1:C3
        // This will generate numbers 1‑6 arranged in 3 rows and 2 columns.
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");
```

*發生了什麼事？*  
- `SEQUENCE(rows, columns)` 告訴 Excel 產生一個連續數字的矩陣。  
- 由於這是 **動態陣列公式**，Excel 會自動將結果展開到相鄰的儲存格（本例為 B1:C3）。  

如果想嘗試其他變化，可使用 `=SEQUENCE(5,1,10,2)`，從 10 開始、每次遞增 2。

## 步驟 4：重新計算以確保溢位範圍即時更新

Excel 不會在未被要求時評估公式。於 Java 中，我們需要觸發一次計算：

```java
        // Step 4: Recalculate formulas so the spilled range is up‑to‑date
        workbook.calculateFormula();
```

*為什麼要重新計算*？若不呼叫此方法，儲存格只會保留公式文字，沒有數值結果——導致儲存的檔案看起來是空的。

## 步驟 5：**將工作簿另存為 XLSX**

最後，我們把檔案寫入磁碟。這一步示範了 **save workbook as xlsx** 的完整流程。

```java
        // Step 5: Save the workbook with the dynamic array data
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully!");
    }
}
```

當你在 Excel 365 或更新版本開啟 `dynamic_sequence_demo.xlsx` 時，會看到：

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |

*注意*：數字會自動從 A1 溢位到相鄰儲存格，正如 `SEQUENCE` 函數所指定的行為。

## 探索 SEQUENCE 函數的變化

既然你已掌握 **如何使用 sequence**，接下來快速看看幾個常見的應用情境。

### 產生月份標題列

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)");
```

此程式碼會產生一列 1‑12 的數字，非常適合作為月份標題。

### 建立乘法表

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
```

這裡我們將兩個相同的溢位範圍相乘，得到一個 5×5 的乘法格子。

## 常見陷阱與避免方法

- **舊版 Excel**：動態陣列（包括 `SEQUENCE`）僅在 Excel 365/2021 以上版本支援。較舊版本會顯示 `#NAME?`。  
- **函式庫支援**：並非所有 Java Excel 函式庫都了解溢位範圍。Aspose.Cells 支援；截至 2024 年，Apache POI 尚未支援。  
- **儲存格式**：動態陣列必須使用 `.xlsx`；舊的 `.xls` 格式會失去溢位行為。

## 完整可執行範例（直接複製貼上）

以下是完整、可直接執行的程式碼。只要在 Maven 專案中加入 Aspose.Cells 依賴，即可使用。

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Set the SEQUENCE formula – this will spill into B1:C3
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");

        // Force calculation so the spilled values are stored
        workbook.calculateFormula();

        // Save the workbook as an XLSX file
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully at dynamic_sequence_demo.xlsx");
    }
}
```

### 預期輸出

- 專案目錄下會產生 `dynamic_sequence_demo.xlsx` 檔案。  
- 開啟該檔案時，Excel 會自動顯示一個 3×2 的數字區塊（1‑6）。

## 下一步：超越 SEQUENCE

既然你已掌握 **如何使用 sequence**，可以嘗試將它與其他動態函數結合：

- **FILTER** – 依條件抽取符合的列。  
- **SORT** – 在不使用 VBA 的情況下排序溢位範圍。  
- **UNIQUE** – 從清單中挑出唯一值。

這些同樣可以 **設定動態陣列公式**，只要像使用 `SEQUENCE` 那樣寫入即可。結合使用可讓你在 Excel 內直接建構強大的資料管線，全部由 Java 驅動。

## 結論

我們已完整說明在 Java 產生的 Excel 檔案中 **如何使用 sequence**：建立工作簿、**設定動態陣列公式**、重新計算，最後 **將工作簿另存為 xlsx**。程式碼已備妥，說明也解釋了每一步的「為什麼」，並示範了幾個實用變化。

試著執行範例、調整參數，讓 Excel 為你自動完成繁重的計算。如果遇到版本不符或函式庫限制等問題，歡迎在下方留言討論。祝開發順利！

## 接下來您應該學習什麼？

以下教學與本指南緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在專案中探索其他實作方式。

- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Aspose.Cells Java&#58; How to Add XML Maps and Save as XLSX (2023 Guide)](/cells/english/java/import-export/aspose-cells-java-add-xml-map-save-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}