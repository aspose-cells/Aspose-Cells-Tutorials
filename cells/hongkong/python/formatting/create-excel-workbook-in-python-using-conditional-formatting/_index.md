---
category: general
date: 2026-09-21
description: 學習如何在 Python 中建立 Excel 工作簿、設定儲存格背景顏色，並使用 Aspose.Cells 套用基於日期的條件格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: zh-hant
lastmod: 2026-09-21
og_description: 在 Python 中建立 Excel 工作簿，設定儲存格背景色，並使用 Aspose.Cells 套用基於日期的條件格式化。請跟隨逐步指南。
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: 使用 Python 建立具條件格式的 Excel 工作簿
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: 在 Python 中使用條件格式建立 Excel 活頁簿
url: /zh-hant/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用條件格式在 Python 中建立 Excel 工作簿

如果你需要 **create Excel workbook python** 腳本自動突顯日期，本指南會一步步示範。你將會看到如何 **set cell background color**、加入「Yesterday」規則，並儲存檔案——全部使用 Aspose.Cells for Python。

以程式方式操作 Excel 檔案通常意味著在多個工作表中重複相同的格式化邏輯。完成本教學後，你將擁有一套可重複使用的 **excel conditional formatting python** 模式，隨時可以套用到任何專案。

## 前置條件

- 已安裝 Python 3.8+  
- `aspose-cells` 套件（`pip install aspose-cells`）  
- 具備 Python 函式與 datetime 模組的基本概念  

不需要額外的函式庫；Aspose.Cells 會處理所有 Excel 操作。

## 第一步：建立工作簿並取得第一個工作表

第一步是 **create excel workbook python** 物件，並抓取預設工作表。這樣就能得到一個乾淨的畫布，供後續樣式使用。

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*為什麼這很重要：* `Workbook()` 會在記憶體中建立 Excel 檔案。存取 `worksheets[0]` 可避免硬編碼工作表名稱，即使預設名稱變更也能正常運作。

## 第二步：加入 TIME_PERIOD 條件格式的輔助函式

為了讓程式碼保持整潔，我們將條件格式的建立封裝在一個輔助函式中。它接受儲存格範圍、背景顏色以及欲套用的時間區間規則。

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*為什麼這很重要：* 這個輔助函式抽象化了建立條件格式的重複步驟，讓你可以輕鬆重複使用於其他基於日期的規則，例如「Today」或「Last Week」。

## 第三步：將「Yesterday」規則套用到特定範圍

現在使用輔助函式，將符合昨天日期的儲存格以 **medium sea green** 進行突顯。範圍 `I19:K20` 會在條件符合時變成該顏色。

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*為什麼這很重要：* `TimePeriodType.YESTERDAY` 是 Aspose.Cells 內建的列舉值，無需自行計算日期。程式庫會在每次開啟工作簿時自動評估此規則。

## 第四步：在範圍內填入示範日期

為了觀察規則效果，我們寫入兩個日期——一個符合「Yesterday」，另一個不符合。`number` 樣式 `30` 代表內建的日期格式。

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*為什麼這很重要：* 透過寫入具體日期，你可以在任意時間驗證條件格式是否正確，而不必在特定日期才打開檔案。

## 第五步：加入說明標籤並自動調整欄寬

簡短的標籤說明格式化範圍的用途，`auto_fit_column` 則讓工作表更易閱讀。

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## 第六步：儲存工作簿

最後，將工作簿寫入磁碟。`os.makedirs` 呼叫會確保目標資料夾已存在。

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

開啟 *TimePeriodDemo.xlsx* 後，你會看到：

- 儲存格 **I19** 以 **medium sea green** 著色，因為其值符合「Yesterday」規則。  
- 儲存格 **K20** 保持預設背景，因為其日期不符合條件。  

這示範了如何使用單行 Python 程式碼 **format cells by date**。

## 完整可執行範例

將所有片段組合起來，以下是完整腳本，你可以直接複製貼上執行：

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

執行腳本、開啟產生的檔案，即可看到條件格式的實際效果。

## 常見變化與邊緣案例

| 變化 | 實作方式 | 使用時機 |
|-----------|------------------|-------------|
| **突顯「Today」** | 將 `TimePeriodType.YESTERDAY` 改為 `TimePeriodType.TODAY` | 即時儀表板 |
| **多個範圍** | 為每個範圍呼叫 `add_time_period`，傳入不同顏色 | 複雜報表 |
| **動態日期範圍** | 使用 `TimePeriodType.LAST_7_DAYS` 或 `TimePeriodType.NEXT_MONTH` | 滾動報表 |
| **自訂顏色** | 使用 `Color.from_argb(255, r, g, b)` 產生任意色階 | 符合品牌風格的樣式 |

**專業小技巧：** 當你想要純色填滿時，務必設定 `condition.style.pattern = BackgroundType.SOLID`；否則 Excel 可能會顯示漸層，導致不同版本間外觀不一致。

## 結論

現在你已掌握如何撰寫 **create Excel workbook python** 腳本，能 **set cell background color**、套用 **excel conditional formatting python**，以及使用 Aspose.Cells 進行 **format cells by date**。本範例說明了 **date based conditional formatting** 的情境，但相同模式同樣適用於任何時間區間規則。

接下來，你可以探索：

- 加入資料條或圖示集合 (`FormatConditionType.DATA_BAR`)  
- 在同一範圍上結合多個條件規則  
- 將工作簿匯出為 PDF (`SaveFormat.PDF`) 以供報表使用  

歡迎自行嘗試不同顏色、範圍與時間區間類型，讓報表更貼合你的需求。祝開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化你對 API 功能的掌握，並探索在專案中實作的其他方式。

- [精通 Aspose.Cells for .NET 的 Excel 儲存格格式化與工作簿管理](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [使用 Aspose.Cells .NET 進行 Excel 自動化：建立工作簿與設定外部連結](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [使用 Aspose.Cells .NET 在 Excel 中建立工作簿範圍命名](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}