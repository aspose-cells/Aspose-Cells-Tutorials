---
category: general
date: 2026-06-08
description: Excel REDUCE 函數範例，示範如何在 Excel 中使用 SEQUENCE 函數、在 Excel 公式中產生序列，以及使用 Python
  取得儲存格值。
draft: false
keywords:
- excel reduce function example
- how to use sequence function excel
- generate sequence in excel formula
- retrieve cell value python
language: zh-hant
og_description: Excel REDUCE 函數範例示範如何在 Excel 中使用 SEQUENCE，於 Excel 公式中產生序列，並使用 Python
  取得結果。
og_title: Excel REDUCE 函數範例：使用 Python 計算階乘
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Excel REDUCE function example showing how to use the SEQUENCE function
    in Excel, generate a sequence in an Excel formula, and retrieve cell value with
    Python.
  headline: 'Excel REDUCE Function Example: Compute Factorial with Python'
  type: TechArticle
tags:
- excel
- python
- aspose-cells
- formula
title: Excel REDUCE 函數範例：使用 Python 計算階乘
url: /zh-hant/python/formulas-and-functions/excel-reduce-function-example-compute-factorial-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel REDUCE 函數範例：使用 Python 計算階乘

有沒有想過如何在不與 VBA 巨集糾纏的情況下取得一個簡潔的 **Excel REDUCE function example**？你並不孤單。在本指南中，我們將示範如何結合 REDUCE 函數與 SEQUENCE 函數來計算階乘——全部透過與 Excel 活頁簿互動的 Python 程式碼完成。

有什麼好處？你將看到一段完整、可執行的程式碼片段，該片段 **在 Excel 公式中產生序列**、將其套用至 REDUCE、強制重新計算，最後 **使用 Python 取得儲存格值**。不需要手動複製貼上，也沒有隱藏步驟——只要純粹的程式碼即可直接嵌入你的專案。

## 需要的條件

* 已安裝 Python 3.8 以上（任何較新的版本皆可）
* `aspose-cells` 套件（`pip install aspose-cells`）——它是讓 Python 讀寫 Excel 檔案的橋樑。
* 具備基本的 Excel 公式概念——只要曾輸入過 `=SUM(A1:A5)` 即可。
* 任一 IDE 或文字編輯器——VS Code、PyCharm，甚至簡單的 Notepad 都行。

就這樣。無需額外 DLL，也不需要安裝 Office。讓我們動手實作吧。

## 步驟 1：建立活頁簿 – Excel REDUCE 函數範例

首先，我們在記憶體中建立一個全新的活頁簿，並取得預設工作表。魔法就會在此發生。

```python
import aspose.cells as cells

# Create a new workbook and reference the first sheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

*為什麼這很重要*：`aspose-cells` 為我們提供完整功能的 Excel 引擎，無需啟動 Excel 本身。`Workbook` 物件就是你的沙盒；所有加入的內容都只存在於記憶體中，直到我們決定儲存為止。

## 步驟 2：在 Excel 中使用 SEQUENCE 函數

SEQUENCE 函數可以透過單一公式產生一串數字。這裡我們將該串列的長度（即階乘的「n」）存入 **A1** 儲存格。

```python
# Put the number of terms (5) into cell A1
worksheet.cells["A1"].put_value(5)   # n = 5
```

現在 A1 內的值為 5，告訴 SEQUENCE 與 REDUCE 要處理多少個數字。如果需要計算其他階乘，只要在此更改數值即可。很簡單，對吧？

## 步驟 3：在 Excel 公式中套用 REDUCE 產生序列

這就是 **excel reduce function example** 的核心。我們在 B1 中寫入公式，建立從 1 到 *n* 的序列，並將其折疊為乘積。

```python
# Set a REDUCE formula in B1 that multiplies the sequence 1..n (computes factorial)
worksheet.cells["B1"].formula = "=REDUCE(1, SEQUENCE(A1,1,1,1), LAMBDA(acc, x, acc*x))"
```

讓我們拆解說明：

* `SEQUENCE(A1,1,1,1)` – 從 1 開始，每次遞增 1，並建立 *A1* 列（因此產生 5 列：1,2,3,4,5）。
* `REDUCE(1, …, LAMBDA(acc, x, acc*x))` – 以 1 為累加器起點，將每個元素 (`x`) 乘入，實際上計算 `1*2*3*4*5`。

如果你對 `LAMBDA` 不熟悉，可以把它視為一個內嵌函式，接受兩個參數：累積值 (`acc`) 與當前元素 (`x`)。函式本體 `acc*x` 告訴 Excel 如何將兩者結合。

## 步驟 4：重新計算公式並使用 Python 取得儲存格值

Aspose 不會即時自動計算公式，我們必須手動觸發一次計算。

```python
# Recalculate all formulas in the workbook
workbook.calculate_formula()
```

現在引擎已完成計算，B1 中存放著階乘結果。讓我們把這個值取回到 Python。

```python
# Retrieve and display the result (120)
result = worksheet.cells["B1"].value
print(result)   # → 120
```

你應該會在主控台看到 **120**——正好是 5! 的結果。這行程式碼示範了 **retrieve cell value python** 步驟，以簡潔的一行程式完成。

## 步驟 5：驗證結果並嘗試變化

快速驗證：將 A1 的值改為 7，重新執行計算，即可得到 5040。這正是使用 **generate sequence in excel formula** 的好處——相同的 REDUCE 邏輯可適用於任何規模。

```python
worksheet.cells["A1"].put_value(7)   # Change n to 7
workbook.calculate_formula()
print(worksheet.cells["B1"].value)  # → 5040
```

*小技巧*：如果你打算將活頁簿匯出供人檢視，計算完成後呼叫 `workbook.save("factorial.xlsx")`。檔案將同時保留公式與計算結果，能在任何試算表程式中直接開啟。

## 常見陷阱與邊緣案例

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **公式未更新** | 你呼叫了 `put_value` 但忘記執行 `calculate_formula()` | 每次資料變更後都要重新計算。 |
| **大型 *n* 造成溢位** | Excel 的數值精度上限約為 10^308；階乘增長極快。 | 使用 `DOUBLE` 精度，或改用基於 `LOG` 的計算方式處理極大數值。 |
| **缺少 Aspose 授權** | 免費評估版會顯示警告橫幅。 | 購買授權或在非商業測試時使用試用版。 |

## 更進一步 – 接下來做什麼？

既然你已掌握完整的 **excel reduce function example**，可以考慮以下延伸應用：

* **Array‑level calculations** – 使用 REDUCE 於產生的序列上執行加總、平均或文字串接等陣列層級計算。
* **Dynamic ranges** – 將硬編碼的 `A1` 參照改為使用者可編輯的命名範圍。
* **Cross‑language integration** – 將 Python 換成 C# 或 Java，仍可使用相同的 REDUCE 公式；活頁簿本身不受語言限制。

如果你對其他 Excel 函數感興趣，`SCAN` 函數可與 `REDUCE` 搭配使用以取得累積結果，而 `LET` 則能讓複雜公式更整潔。上述所有功能皆可透過 Python 以我們剛才示範的相同模式驅動。

---

### 重點回顧

我們從清晰的 **excel reduce function example** 開始，示範了 **how to use sequence function excel** 來建立數值列表，**generated a sequence in excel formula** 供 REDUCE 使用，強制重新計算，最後 **retrieved the cell value python**。整個工作流程僅需幾行簡潔程式碼，卻展現了結合強大 API 時，現代 Excel 公式的威力。

隨意複製程式碼、調整 `A1` 的數值，或將此片段嵌入更大的資料處理管線。無論是自動化報表、計算金融模型，或純粹玩玩試算表，都沒有任何限制。

有任何問題或想分享自己的變化嗎？在下方留言吧，祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [How to Use Excel IF Function](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [How To Use Excel If Function](/cells/german/java/basic-excel-functions/how-to-use-excel-if-function/)
- [How To Use Excel If Function](/cells/french/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}