---
category: general
date: 2026-11-16
description: 在 Excel 中使用 Python 建立條件格式化。學習如何新增條件格式化範圍、突顯日期，並以程式方式建立工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: zh-hant
lastmod: 2026-11-16
og_description: 使用 Python 在 Excel 中建立條件格式化。本教學示範如何新增條件格式化範圍、突出顯示日期，以及產生工作簿。
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: 使用 Python 在 Excel 中創建條件格式化 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: 如何使用 Python 在 Excel 中建立條件格式
url: /zh-hant/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Python 建立條件格式

如果你需要在 Python 中 **建立條件格式** 於 Excel 檔案，本指南將一步步示範操作方式。你將學會 **create excel workbook python** 風格的建立方式、定義格式範圍，並在不離開 IDE 的情況下高亮顯示日期。

條件格式可視覺化標記符合特定條件的儲存格——非常適合儀表板、報告或資料驗證工作表。完成本教學後，你將擁有一個完整的活頁簿，能將「昨天」的日期儲存格以粉紅色標示，而其餘範圍則保持綠色。

## 你將完成的工作

* 從頭建立一個新活頁簿。  
* 為特定儲存格區塊加入條件格式集合。  
* 套用 **TIME_PERIOD** 規則以高亮日期（即「如何高亮日期」情境）。  
* 將檔案儲存為 XLSX 活頁簿，供後續處理使用。

**先決條件**  
* Python 3.8+  
* `aspose-cells` Python 套件（`pip install aspose-cells`）  
* 基本了解 Python 的 `datetime` 模組  

---

## 如何在 Python 中建立條件格式

第一步是設定活頁簿與工作表，讓它們承載格式規則。

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**為什麼這很重要** – `Workbook` 是所有 Excel 操作的入口點。以程式方式建立活頁簿可取代手動的「檔案 → 新增」步驟，讓報告流程自動化。

---

## 準備條件格式集合 – 新增條件格式範圍

接著我們定義將套用規則的儲存格區塊。本例的範圍為 **I19:K20**。

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**說明** – `conditional_formattings.add` 會將新集合註冊至指定的位址字串。第一個條件 (`conds[0]`) 作為「預設」樣式；之後的規則在符合條件時會覆寫它。

---

## 新增 TIME_PERIOD 條件 – 如何高亮日期

現在加入實際的邏輯，找出「昨天」的日期並將其塗成粉紅色。

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**為什麼使用 TIME_PERIOD？** – Aspose.Cells 提供內建列舉，如 `YESTERDAY`、`TODAY`、`LAST_WEEK`。它們會將儲存格的日期值與系統當前日期比較，免除自行撰寫公式的需求。

---

## 填入範例資料 – 示範規則

為了看到格式效果，我們插入一筆符合規則的日期與一筆不符合的日期。

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**邊緣情況說明** – `TIME_PERIOD` 規則僅對*真實*日期有效。若儲存格內是文字（例如「N/A」），規則會被忽略，避免產生意外的顏色變化。

---

## 儲存活頁簿 – add conditional formatting python

最後，將活頁簿寫入磁碟。此檔案可在任何試算表程式中開啟，以驗證顏色是否正確。

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**預期結果**  

| I19（綠 → 粉紅） | J19（綠） | K19（綠） |
|--------------------|------------|------------|
| 7/30/2008（昨天） | – | – |
| **I20**： “昨天” 標籤 | – | – |
| I21‑K21（綠） | – | – |

儲存格 **I19** 會因日期符合「昨天」期間而呈現粉紅背景，而 **K20** 則保持綠色。

---

## 常見問題與實用技巧

* **我可以使用自訂日期範圍而非內建期間嗎？**  
  可以。將 `condition.time_period` 改為 `condition.formula1 = "TODAY()-1"`，並將 `condition.type = FormatConditionType.FORMULA`。

* **如果我的活頁簿已經有資料該怎麼辦？**  
  使用 `worksheet.cells.import_data` 先批次匯入資料，再加入條件格式集合。

* **大量工作表的效能如何？**  
  添加過多條件會降低渲染速度。將具有相同規則的儲存格合併為單一範圍（例如 “A1:C1000”）以降低條件數量。

* **跨平台相容性如何？**  
  產生的 XLSX 檔案遵循 Office Open XML 標準，於 Windows、macOS 及 Linux 的試算表應用程式皆可正常使用。

---

## 結論

現在你已掌握如何在 Excel 活頁簿中使用 Python **建立條件格式**。本教學涵蓋了建立活頁簿、定義 **add conditional formatting range**、套用 **how to highlight dates** 規則，以及以 **add conditional formatting python** 方式儲存檔案的完整流程，全部皆透過 Aspose.Cells 完成。

接下來你可以：

* 使用其他 `TimePeriodType` 值（例如 `TODAY`、`LAST_MONTH`）擴充規則集合。  
* 在同一範圍內結合多個條件，提供更豐富的視覺提示。  
* 將此工作流程整合至自動化報告管線或 Web 服務中。

祝開發順利，歡迎隨意嘗試不同的顏色、範圍與日期邏輯，以符合你的報告需求！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並探索在專案中實作的其他方式。

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}