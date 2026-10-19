---
category: general
date: 2026-06-08
description: 建立 Excel 工作簿的 Python 範例，示範如何在 Excel 中使用 lambda、使用 BYROW 求和列，並在幾個步驟內自動化計算。
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: zh-hant
og_description: 使用 Python 建立 Excel 工作簿，並學習如何在 Excel 中使用 lambda 透過 BYROW 公式有效地對列求和。
og_title: 使用 Python 建立 Excel 工作簿 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: 使用 Python 建立 Excel 活頁簿 – 完整指南與 Lambda
url: /zh-hant/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 建立 Excel 工作簿 – 完整指南與 Lambda

有沒有想過如何 **create Excel workbook Python** 腳本來自動化乏味的數字運算？你並不孤單——許多開發者在需要產生工作表、插入公式，並將結果拉回程式碼時，常會卡住。

在本教學中，我們還會示範 **how to use lambda** 在 Excel 中的使用方式，說明如何使用現代的 `BYROW` 函數 **how to sum rows**，並提供一個整潔、端到端的範例，讓你今天就能複製貼上並執行。

## 你將學會

- 從 Python 建立全新的工作簿，無需手動開啟 Excel。  
- 以 3 × 3 數字矩陣填滿範圍。  
- 插入利用 **use lambda excel** 語法的 `BYROW` 公式，以求每列總和。  
- 重新計算工作表使公式求值，然後將結果讀回 Python。  

完成本指南後，你將擁有一個獨立的腳本，可用於發票、成績卡或任何需要即時 **sum rows** 的情境。

### 前置條件

- 已安裝 Python 3.8+。  
- `openpyxl` 函式庫（或若你偏好基於 COM 的方式可使用 `xlwings`）。我們將使用 `openpyxl`，因為它是純 Python 且可在所有平台上運作。  
- Microsoft Excel 的近期版本（365 或 2021），支援 `BYROW` 函數與 Lambda 公式。  

Install the library with:

```bash
pip install openpyxl
```

> **小技巧：** 若在 Windows 上遇到權限問題，請使用 `python -m pip install --user openpyxl`。

---

## 使用 Python 建立 Excel 工作簿 – 初始化工作簿

我們首先需要的是一個完全存在於記憶體中的全新工作簿物件。使用 `openpyxl` 只需一行程式碼：

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

為什麼使用 `wb.active` 而不是索引 `Worksheets[0]`？`openpyxl` 直接公開了活動工作表，這樣更清晰且避免額外的列表查找。如果你需要處理多個工作表，隨時可以使用 `wb.create_sheet(title="MySheet")` 來新增。

---

## 填入工作表資料 – 簡易 3×3 矩陣

接著，我們在工作表中填入一個小矩陣。這呼應了經典的「每列求和」範例，且程式碼保持簡潔。

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

你可能會想，為什麼不直接使用 `ws.append()` 或 `ws.values` 而手動迴圈？明確的迴圈讓我們能完整控制起始儲存格，且日後調整偏移量更方便——在需要保留標題列或欄位空白時特別實用。

---

## 如何在 Excel 公式中使用 Lambda

Excel 的 **use lambda excel** 功能允許你直接在儲存格中撰寫匿名函式。可將其視為 Python 的 `lambda`，但運作於試算表引擎內。語法如下：

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

結合 `BYROW` 後，你可以將該 lambda 套用於範圍的每一列，產生一欄結果。這正是我們的 **how to sum rows** 技巧核心。

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

發生了什麼事？

- `A1:C3` 是來源範圍（我們的矩陣）。  
- `LAMBDA(r, SUM(r))` 定義了一個暫時函式，接收單一列 (`r`) 並回傳其總和。  
- `BYROW` 為 **each row** 執行該 lambda，並將結果溢位至 D 欄，從 `D1` 開始。  

因為 `BYROW` 是 *dynamic array* 函式，Excel 會自動在 `D1:D3` 填入三個總和。

> **注意：** `BYROW` 與 Lambda 公式僅在 Excel 365/2021 及更新版本可用。若使用較舊版本，需改用傳統的 `SUM` 公式或 VBA。

---

## 使用 BYROW 與 Lambda 進行列求和

公式已寫入工作表後，我們必須讓 Excel 執行計算。`openpyxl` 本身不會計算公式；它僅負責讀寫。要觸發計算，我們可以：

1. 將工作簿儲存並在 Excel 中開啟（手動）。  
2. 使用 `xlwings` COM 引擎強制重新計算（需安裝 Excel）。  

為了提供純 Python 解決方案，我們僅在計算步驟使用 `xlwings`——不做其他操作。

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

為什麼不直接呼叫 `wb.calculate()`？`openpyxl` 缺乏原生計算引擎，所以我們透過 `xlwings` 借助 Excel 本身。對於小型工作表而言，額外負擔很小，且能得到 Excel 真正顯示的結果。

---

## 重新計算並取得結果 – 將總和拉回 Python

最後，我們從 D 欄讀取溢位的結果。`openpyxl` 讓這個步驟相當簡單：

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

如果你想只使用 `openpyxl`，也可以在 Excel 重新計算後讀取儲存格：

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

兩種方式皆會得到相同的列表 `[6, 15, 24]`，證實 **how to sum rows** 搭配 `BYROW` + Lambda 如預期運作。

---

## 邊緣情況與常見陷阱

| 情況 | 需要留意的地方 | 解決方案 |
|-----------|-------------------|-----|
| Excel 版本低於 365 | `BYROW` 與 `LAMBDA` 顯示為 `#NAME?` | 使用傳統的 `=SUM(A1:C1)` 手動向下複製，或升級 Excel。 |
| 大型矩陣（10 k+ 列） | 重新計算可能變慢 | 僅呼叫 `book.api.CalculateFullRebuild()` 一次，或將工作簿拆分。 |
| 在無 Excel 的無頭伺服器上執行 | `xlwings` 無法啟動 Excel | 改用純 Python 函式庫如 `pandas` + `numpy` 進行計算，然後寫入結果。 |
| 區域設定問題（逗號 vs 分號） | 公式可能被拒絕 | 使用 `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` 針對使用 `;` 的區域設定。 |

---

## 完整可執行範例（直接複製貼上）



## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.Cells Java 建立 Excel 工作簿 - 完整指南](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [使用 Aspose.Cells 建立 Excel 工作簿與自動化報告](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [如何使用 Aspose.Cells for .NET 建立並儲存 Excel 工作簿為 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}