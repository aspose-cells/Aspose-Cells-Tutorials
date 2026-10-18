---
category: general
date: 2026-06-21
description: 學習如何在 Excel 中使用 Python 撰寫 lambda。本教學亦涵蓋使用 Python 建立 Excel 工作簿以及如何使用 Aspose.Cells
  讀取儲存格。
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: zh-hant
og_description: 說明如何在 Excel 中使用 Python 撰寫 lambda。跟隨我們的清晰步驟，建立 Excel 工作簿（Python），套用
  BYROW，並讀取儲存格結果。
og_title: 如何在 Excel 中使用 Python 撰寫 Lambda – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: 如何在 Excel 中使用 Python 撰寫 Lambda – 步驟指南
url: /zh-hant/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Python 撰寫 Lambda – 步驟指南

有沒有想過在使用 Python 自動化試算表時，**how to write lambda** 在 Excel 公式中會是什麼樣子？你並不孤單。許多開發者在嘗試結合 Excel 全新動態陣列函數與 Python 工作流程時卡住了。在本教學中，我們將逐步示範一個完整、可執行的範例，正好展示這點 — 同時也會提到 **create excel workbook python**、**how to read cells**，以及方便的 **how to use byrow** 模式。

完成本指南後，你將擁有一個全新的工作簿、一個利用 lambda 的 BYROW 公式，以及一個簡單的方法將結果拉回 Python 程式碼中。無需額外的 Excel 外掛，只要使用 Aspose.Cells for Python 加上一點程式碼即可。

## 先決條件

在開始之前，請確保你已具備：

- 已安裝 Python 3.8 或更新版本。
- 已安裝 `aspose-cells` 套件（`pip install aspose-cells`）。
- 具備 Python 串列與函式的基本概念。
- （可選）一個你熟悉的 IDE 或文字編輯器。

就這樣。如果上述任一項你不熟悉，請先暫停並安裝套件；其餘步驟在任何能執行 Python 的平台上皆可運作。

## 建立 Excel 工作簿（Python）

首先，我們需要一個乾淨的工作簿物件。Aspose.Cells 提供的 `Workbook` 類別代表記憶體中的整個 Excel 檔案。

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

為什麼要從全新工作簿開始？因為它保證環境可預測——沒有隱藏公式、沒有雜亂格式，只有一張空白畫布。這是任何 **create excel workbook python** 教學的基礎。

## 填入工作表資料

接著，我們在 **A1** 起始位置填入一個 5 × 3 的數值表格。資料刻意簡單，方便你清楚看到計算過程。

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

請注意，我們使用 `put_value` 搭配巢狀的 Python 串列；Aspose.Cells 會自動對應列與欄。如果你需要從 CSV 或資料庫匯入資料，只要把 `table_data` 換成相應來源即可，其他程式碼不需變動。

## 如何在 BYROW 公式中撰寫 Lambda（Python）

現在進入重點：**how to write lambda** 讓 Excel 引擎評估。Excel 的 `BYROW` 函式會對指定範圍的每一列呼叫你提供的 `LAMBDA`。在此範例中，我們要計算每列的平均值。

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

說明如下：

- `BYROW(A1:C5, …)` 告訴 Excel 檢視 A1:C5 範圍內的每一列。
- `LAMBDA(r, AVERAGE(r))` 定義了一個匿名函式（`r` 為列陣列），回傳該列的平均值。
- 結果會自動溢位到 D1:D5，因為 BYROW 會回傳一個陣列。

這一行即是 **how to write lambda** 於列向計算的答案。你可以把 `AVERAGE` 換成 `SUM`、`MAX` 或其他聚合函式，只要修改 lambda 的主體即可。

## 強制計算公式

Aspose.Cells 在設定公式時不會自動求值，我們必須指示它重新計算。

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

如果省略此步驟，D 欄的儲存格仍只會顯示公式文字，而非計算後的數值。這是許多人在 **how to use byrow** 時忘記觸發計算階段的常見陷阱。

## 計算完成後讀取儲存格

最後，將結果拉回 Python。這示範了 **how to read cells** 的通用寫法，適用於任何公式輸出。

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

簡單的 list‑comprehension 會遍歷五列，取得每個儲存格的 `.value`，並存入 `row_averages`。印出的串列證實我們的 lambda 正確執行。

### 小技巧
如果需要一次讀取大量結果，可使用 `worksheet.cells.get_range("D1:D5").value` 一次取得整個陣列——對於大型工作表來說速度更快。

## 使用 Lambda 函式於 Excel 計算列平均（完整腳本）

將上述所有步驟整合，以下是完整、可直接執行的腳本：

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

執行此腳本會印出：

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

這就是完整流程：**create excel workbook python**、填入資料、**how to use byrow**、**how to write lambda**，最後 **how to read cells**。

## 邊緣情況與常見問題

- **如果我的資料不是連續的呢？**  
  BYROW 可作用於任何矩形範圍。若有空格，只要引用較大的範圍，並在 lambda 中忽略空白（例如 `AVERAGEIF(r, "<>")`）。

- **可以傳遞多個參數給 lambda 嗎？**  
  可以。第一個參數永遠是列（或 `BYCOL` 的欄），額外參數可在範圍之後提供，例如 `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`。

- **這能相容於較舊的 Excel 版本嗎？**  
  BYROW 與 LAMBDA 從 Excel 365（動態陣列）開始支援。若需相容舊版，必須使用 VBA 或多個輔助欄位自行模擬相同邏輯。

- **需要將工作簿存檔嗎？**  
  本示範不需要，但若想產生實體檔案，只要呼叫 `workbook.save("output.xlsx")` 即可。

## 結論

我們已說明 **how to write lambda** 在 Excel BYROW 公式中的使用方式，示範完整的 **create excel workbook python** 工作流程，並展示最簡單的 **how to read cells** 讀取方法。透過 Aspose.Cells，你可以避免任何 COM 互操作的麻煩，同時此模式可輕鬆擴展至數千列，只需少量程式碼變更。

準備好接受下一個挑戰了嗎？試著把 `AVERAGE` 換成 `MEDIAN`、在 lambda 中加入條件判斷，或自動產生完整的報告套件。Python 與 Excel 現代函式的結合，為資料驅動的自動化開啟無限可能。

有任何問題或想分享自己的 lambda 小技巧嗎？歡迎在下方留言，祝開發愉快！  

![how to write lambda in Excel using Python](image.png){alt="使用 Python 在 Excel 中撰寫 lambda 的方法"}

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步深化技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 建立並儲存 Excel 工作簿為 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [如何在 Aspose.Cells for .NET 中載入未定義名稱的 Excel 工作簿](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [如何在 Excel 中使用 Aspose.Cells .NET 建立工作簿範圍的命名區域](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}