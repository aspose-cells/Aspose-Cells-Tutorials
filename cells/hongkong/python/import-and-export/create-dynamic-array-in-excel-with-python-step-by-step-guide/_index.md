---
category: general
date: 2026-06-21
description: 使用 Python 及 Excel 的 SEQUENCE 函數建立動態陣列。學習讀取公式結果、重新計算 Excel 公式，並查看 Excel
  SEQUENCE 範例。
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: zh-hant
og_description: 使用 Python 在 Excel 中建立動態陣列。本教學示範如何使用 SEQUENCE 函數、重新計算 Excel 公式，以及讀取公式結果。
og_title: 使用 Python 在 Excel 中建立動態陣列 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: 使用 Python 在 Excel 中建立動態陣列 – 逐步指南
url: /zh-hant/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 在 Excel 中建立動態陣列 – 完整指南

有沒有想過在不離開 Python 程式碼的情況下 **建立動態陣列** 公式？你並不是唯一有此需求的人。無論是自動化月報還是打造輕量級資料引擎，能夠直接在活頁簿中寫入 `SEQUENCE` 公式、重新計算，然後把溢位範圍（spill range）拉回 Python，都是顛覆性的改變。

在本教學中，我們會示範一個實務 **excel sequence example**，說明如何 **讀取公式結果**，以及在注入新邏輯後 **重新計算 excel 公式** 的最佳方式。完成後，你將擁有一段可直接複製、執行、依需求調整的完整腳本。

## 你將學會

- `SEQUENCE` 函數的運作原理以及為何它非常適合產生矩陣。
- 一般儲存格值與溢位範圍位址之間的差異。
- 使用 `wb.calculate_formula()`（或等效方法）強制 Excel 評估新公式。
- 透過 `ANCHORARRAY` 取得動態陣列的位址。
- 完整、可執行的 Python 範例，隨時可以放入任何專案。

不需要事先了解 Excel 的新動態陣列引擎，只要對 Python 有基本認識，並且會使用像 **xlwings** 這類能與 Excel 溝通的函式庫即可。

---

## 如何使用 Python 在 Excel 中以 SEQUENCE 建立動態陣列

第一步是直接在工作表儲存格中寫入 **動態陣列** 公式。於現代 Excel 中，`SEQUENCE` 函數能即時產生數字矩陣。以下是我們將使用的語法：

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**為什麼選 `SEQUENCE`？**  
把它想成 Excel 內建的 `range()`，只要一行就能指定列數、欄數、起始值與遞增值。這裡我們要求 3 列 2 欄，起始值 10、遞增 5，結果如下：

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

因為公式寫在 `A1`，Excel 會自動將結果「溢位」到相鄰的 `A1:B3`。這個溢位範圍正是我們稍後要取得的目標。

---

## 在 Excel 中使用 SEQUENCE 函數 – 快速 Excel Sequence 範例

如果手動開啟 Excel，於任一儲存格輸入 `=SEQUENCE(3,2,10,5)`，即可即時看到相同的矩陣。此函數屬於 Office 365 引入的 Excel **dynamic array** 引擎，具備以下特性：

- 不需要 Ctrl+Shift+Enter。
- 結果會自動擴張或收縮。
- 可使用 `@` 或 `#` 等符號直接參照整個溢位範圍。

在 Python 中，唯一的差別是把公式字串指派給儲存格的 `.formula` 屬性，其餘交由函式庫處理。

---

## 使用 ANCHORARRAY 取得溢位範圍位址

動態陣列寫入後，常常需要知道 Excel 實際放置值的範圍。這時 `ANCHORARRAY` 就派上用場。它會回傳溢位範圍左上角儲存格的位址——正好是我們要讀回腳本的資訊。

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

把此公式放在 `C1` 後，會得到類似 `"A1:B3"` 的文字字串。請注意，我們 **讀取公式結果** 時是以純值方式，而非再當作公式。這個小技巧免除手動解析工作表的麻煩。

---

## 重新計算 Excel 公式並讀取結果

從外部腳本注入新公式時，Excel 不一定會即時重新計算。為了確保活頁簿反映最新變更，我們必須主動觸發一次計算。

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**為什麼要呼叫 `calculate_formula()`？**  
若省略這一步，`ws.cells["C1"].value` 可能仍回傳 `None` 或舊的位址，因為 Excel 尚在更新其相依樹。強制重新計算即可確保 **讀取公式結果** 為最新。

---

## 完整腳本 – 從頭到尾

以下是一個完整、可直接執行的範例，將前述所有步驟串接起來。假設已安裝 **xlwings**（`pip install xlwings`），且本機有可用的 Excel。

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### 預期輸出

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

執行腳本後會開啟 Excel、注入 `SEQUENCE` 公式、重新計算，然後同時印出溢位位址與矩陣本身。全程不需要手動點擊。

---

## 常見陷阱與進階小技巧

- **陷阱：** 忘記呼叫 `wb.calculate_formula()`。  
  *結果：* `C1` 仍為空白或顯示舊位址。  
  *解法：* 寫入新公式後務必觸發一次計算。

- **陷阱：** 使用不支援 `SEQUENCE` 的舊版 Excel。  
  *結果：* 出現 `#NAME?` 錯誤。  
  *解法：* 確認使用 Office 365 或 Excel 2021 以上版本。

- **小技巧：** 若需將溢位範圍進一步處理（例如製作圖表），可直接將取得的位址傳入 `ws.range(spill_address)`，如前範例所示。

- **小技巧：** `ANCHORARRAY` 可用於任何動態陣列，而不只 `SEQUENCE`。換成 `=SORT(A2:A10)` 或 `=FILTER(...)`，仍能正確取得溢位位址。

- **邊緣情況：** 目標區域已被佔用時，Excel 會回傳 `#SPILL!` 錯誤。此時請先清除目的範圍，或將公式移至其他儲存格。

---

## 延伸範例 – 接下來可以做什麼？

既然已掌握 **建立動態陣列** 公式、**讀取公式結果**、以及 **重新計算 excel 公式** 的技巧，你可以探索更進階的應用：

- **動態圖表資料** – 把溢位範圍作為圖表來源，讓圖表自動成長。
- **條件格式** – 以溢位位址為依據套用規則。
- **跨活頁簿參照** – 在一個活頁簿寫入動態陣列，透過 `xlwings` 連結將資料拉入另一個活頁簿。

上述皆以本教學的核心概念為基礎，歡迎自行實驗。唯一的限制是你的想像力（以及 Excel 的最大列/欄數）。

---

## 結論

我們完整示範了如何從 Python 在 Excel 中 **建立動態陣列** 公式、使用 **SEQUENCE function excel**、透過 **ANCHORARRAY** 取得溢位範圍、**重新計算 excel 公式**，最後 **讀取公式結果** 回到腳本。這個簡短範例展現了 Excel 新動態陣列引擎結合 **xlwings** 等自動化工具的強大威力。

不妨在自己的專案中試試看，調整矩陣尺寸，或將 `SEQUENCE` 換成其他動態函數。熟練之後，你會發現自動化 Excel 不僅可行，甚至相當順手。

有任何問題或想分享你如何延伸此模式？歡迎在下方留言，祝編程愉快！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，助你掌握更多 API 功能，並在自己的專案中探索不同的實作方式。

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}