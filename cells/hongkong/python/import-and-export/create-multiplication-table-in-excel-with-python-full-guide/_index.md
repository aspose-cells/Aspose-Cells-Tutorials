---
category: general
date: 2026-06-21
description: 使用 Python 在 Excel 中建立乘法表。學習如何使用 lambda、如何使用 makearray、顯示 Excel 陣列以及在一步一步的教學中讀取
  Excel 數值。
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: zh-hant
og_description: 使用 Python 在 Excel 中建立乘法表。本教學示範如何使用 lambda、makearray、顯示 Excel 陣列以及高效讀取
  Excel 數值。
og_title: 使用 Python 在 Excel 中建立乘法表 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: 使用 Python 在 Excel 中建立乘法表 – 完整指南
url: /zh-hant/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 在 Excel 中建立乘法表 – 完整指南

有沒有想過 **在 Excel 中建立乘法表** 而不必手動輸入每個儲存格？你並不孤單。在許多報表情境下，你需要快速產生 5×5（或更大）的產品格子，手動操作實在浪費時間。  

在本教學中，我們將一步步示範如何以 Python 產生這個表格、使用 `MAKEARRAY` 公式嵌入，然後把結果讀回腳本。過程中會說明 **如何使用 lambda**、展示 **如何使用 makearray**，以及示範 **display excel array** 與 **read excel values python**——全部在同一個完整範例中完成。

完成後，你將擁有一段可重複使用的程式碼，適用於任何活頁簿，並且了解此方法為何既快速又具未來延展性。

## 你需要的條件

- Python 3.8+（最新版即可）
- `openpyxl` 套件（或任何支援公式的 Excel 函式庫）
- 基本的 Python lambda 表達式概念
- 不需要額外的 Excel 外掛；內建的 `MAKEARRAY` 函式（Excel 365 可用）會負責主要運算

如果缺少上述任一項，只要執行 `pip install openpyxl` 即可開始使用。

## 建立乘法表 – 概觀

核心概念很簡單：我們建立一個全新的活頁簿，寫入 `MAKEARRAY` 公式以產生 5 × 5 乘法矩陣，強制 Excel 計算，最後把計算結果讀回 Python。

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

執行腳本後會印出：

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

這就是一個完整可用的 **create multiplication table**，全部由 Python 產生於 Excel。

### 為什麼使用 `MAKEARRAY` 而不是 Python 迴圈？

- **效能**：Excel 內建計算，對大型矩陣更快。
- **即時更新**：日後若在公式中變更尺寸，工作表會自動重新計算。
- **可讀性**：公式直接表達「產生陣列」的意圖，讓 Python 程式碼保持簡潔。

## 如何在 Python 中為 Excel 公式使用 lambda

`MAKEARRAY` 呼叫中的 `LAMBDA` 部分是 Excel 端的匿名函式，並非 Python 的 lambda。概念相同：你在公式內定義一段小型、內嵌的邏輯，接受 `r`（列索引）與 `c`（欄索引），回傳 `r*c`。  

如果你對 **how to use lambda** 在 Excel 中還不熟悉，可以把它想成只存在於公式內的迷你函式，無需在其他地方另行宣告。於 Python 中，我們只需要把字串嵌入：

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

這行告訴 Excel：「*對於 5×5 區塊中的每個儲存格，計算列 × 欄*。」  

因為 lambda 由 Excel 評估，你不必在此處考慮 Python 的 lambda 語法，只要遵守 Excel 的語法即可。

## 如何使用 makearray 產生陣列

`MAKEARRAY` 是 Excel 函式庫較新的功能（2022 年起在 Microsoft 365 中提供）。它取代了過去使用 `INDEX` 搭配 `ROW`/`COLUMN` 的技巧。其語法如下：

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – 你想要的列數。
- **columns** – 你想要的欄數。
- **lambda** – 接收 `(row, column)` 並回傳值的 Excel LAMBDA。

在本例中，我們傳入 `5,5` 產生經典的乘法表，但你可以輕鬆改變這兩個數字：

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

如此一來即可得到 10 × 10 的表格，完全不需要寫任何 Python 迴圈。這示範了 **how to use makearray** 可用於任何決定性的格子，無論是查詢表、熱度圖或財務排程。

## Display excel array – 把資料拉回 Python

Excel 計算完公式後，結果會像手動輸入的儲存格一樣存於工作表中。要 **display excel array**，只要遍歷範圍並印出每一列：

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

小提醒：

- 若需處理較大範圍，建議使用 `worksheet.cell(row, column).value` 取代字典式索引，效能稍佳。
- 若想要更美觀的表格，可考慮使用 `tabulate` 或 `pandas.DataFrame` 來格式化輸出。

以下是產生後工作表的螢幕截圖（圖片 alt 文字已包含主要關鍵字以利 SEO）：

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## Read excel values python – 把矩陣抽取出來做後續處理

在 **display excel array** 之後，通常會把這些數字送入資料分析流程。這時 **read excel values python** 就派上用場。先前用來印出的迴圈可以改寫成建立二維列表、NumPy 陣列，或 Pandas DataFrame：

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

輸出結果：

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

現在你已擁有完整類型的 DataFrame，能夠繪圖、匯出 CSV，或作為機器學習模型的輸入。這就完成了工作流程中的 **read excel values python** 部分。

## 邊緣情況與實務技巧

- **公式重新計算**：若在首次 `calculate_formula()` 之後修改活頁簿，必須再次呼叫計算，否則快取的陣列會保持舊值。
- **非 365 版 Excel**：舊版 Excel 不支援 `MAKEARRAY`。此時可改用 Python 產生表格，逐格寫入。
- **大型表格**：若矩陣超過約 100 × 100，建議採用串流方式避免一次載入整個工作表佔用過多記憶體。
- **錯誤處理**：將計算與讀取步驟包在 `try/except` 中，以捕捉 `InvalidFileException` 或 `FormulaError`。

## 結論

我們已示範如何使用 Python 在 Excel 中 **create multiplication table**，並運用 **how to use lambda** 與 **how to use makearray** 的威力。你也看到了如何 **display excel array**、以 **read excel values python** 讀回資料，甚至把結果轉成 Pandas DataFrame 供後續分析。

想更進一步嗎？試著把乘法邏輯換成更複雜的運算——例如距離矩陣、機率表或動態定價格子。相同的模式依舊適用：一行 `MAKEARRAY`、一次快速的 `calculate_formula()`，再以少量 Python 迴圈把資料抽出。

如果這篇指南對你有幫助，請在 GitHub 上給個星星、分享給同事，或留下你的使用案例評論。祝編程愉快，享受只需一條公式就能產生 Excel 表格的簡潔體驗！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}