---
category: general
date: 2026-07-14
description: 建立 Excel 工作簿的 Python 程式碼，設定儲存格背景顏色、根據日期範圍突顯儲存格，並在數分鐘內將工作簿另存為 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: zh-hant
lastmod: 2026-07-14
og_description: 即時使用 Python 建立 Excel 工作簿。學習設定儲存格背景顏色、根據日期範圍突出顯示儲存格，並使用 Aspose.Cells
  將工作簿另存為 XLSX。
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: 使用 Python 建立 Excel 工作簿 – 逐步條件格式設定
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Python 建立 Excel 活頁簿 – 完整指南與條件格式化
url: /zh-hant/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – 完整指南與條件格式化

有沒有想過如何在不手動開啟 Excel 的情況下，編寫看起來精緻的 **create excel workbook python** 腳本？你並不孤單。在許多資料驅動的專案中，我們需要產生試算表、為儲存格上色，甚至標記落在特定範圍內的日期——全部僅使用純 Python 程式碼。

在本教學中，我們將逐步說明一個完整、可直接執行的範例，該範例 **creates an Excel workbook python** 使用 Aspose.Cells 函式庫，**sets cell background color**，套用 **conditional formatting based on date**，最後 **saves workbook as xlsx**。完成後，你將擁有一段可重複使用的程式碼片段，能直接放入任何自動化流程中。

## 你將學到什麼

- 如何初始化工作簿並取得第一個工作表。  
- 一個協助函式，可為任意儲存格範圍新增 conditional‑formatting collection。  
- 使用 **conditional formatting based on date** 來突顯昨天的項目。  
- 調整欄寬以獲得整齊的版面配置。  
- 以 **save workbook as xlsx** 保存結果。  

不需要安裝任何外部的 Excel——Aspose.Cells 會在記憶體中處理所有工作。

## 前置條件

- 已安裝 Python 3.8 以上。  
- `aspose-cells` 套件（`pip install aspose-cells`）。  
- 具備 Python 函式與 datetime 物件的基本概念。  

如果你從未使用過 Aspose.Cells，可以把它想像成一個功能強大、純 Python 的 API，模擬 Excel 本身的物件模型。它非常適合在沒有 Office 套件的伺服器端產生檔案。

## 第一步：初始化工作簿（Create Excel Workbook Python）

首先，我們需要以 **create excel workbook python** 方式建立。此步驟會產生一個空的 workbook 物件，並指向預設的工作表。

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **為何重要：** `Workbook` 類別是所有 Excel 操作的入口點。以程式方式建立它，我們即可避免任何手動檔案處理。

## 第二步：協助函式以新增 Conditional‑Formatting Collection（Set Cell Background Color）

條件格式化存在於附加於範圍的 *collection* 中。讓我們將這段樣板包裝成一個小協助函式，同時讓我們能為整個範圍 **set cell background color**。

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **專業提示：** 使用協助函式可讓主要流程保持簡潔，且易於在多個範圍間重複使用相同的邏輯。

## 第三步：套用基於日期的條件格式化（Highlight Cells Based on Date Range）

現在我們實際上會 **highlight cells based on date range**。此範例以「昨天」為焦點，但你可以將 `TimePeriodType.YESTERDAY` 替換為 `TODAY`、`LAST_WEEK` 等。

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **發生了什麼？**  
> 1. 我們先為整個範圍設定中性的綠色背景。  
> 2. 接著加入一個 `TIME_PERIOD` 條件，僅在儲存格的日期等於昨天時，將填色改為粉紅色 **only**。  
> 3. `TimePeriodType` 列舉抽象化了日期計算，讓你不必自行撰寫自訂邏輯。

## 第四步：填入樣本日期（以評估規則）

為了觀察規則的實際效果，我們會在工作表中放入幾個日期。一個落在「昨天」的時間窗口內，另一個則不在。

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **邊緣案例說明：** 若工作簿會在不同語系環境開啟，建議使用 `date_style.custom = "dd‑mm‑yyyy"` 以確保顯示一致。

## 第五步：整理版面（Auto‑Fit Columns）

擁擠的試算表會顯得不專業。讓我們 **adjust column width for a tidy output**。

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **為何使用 auto‑fit？** 它可確保任何較長的標籤或日期完整顯示，這在與非技術利害關係人共享檔案時尤其重要。

## 第六步：儲存工作簿（Save Workbook As XLSX）

最後，我們 **save workbook as xlsx** 到你選擇的位置。`SaveFormat.XLSX` 常數告訴 Aspose.Cells 以現代的 OpenXML 格式寫入。

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **你應該看到的結果：**  
> - 儲存格 I19 與 K20 含有日期。  
> - I19（昨天）被粉紅色突顯，而 K20 保持綠色。  
> - L 欄會自動展開以容納「Yesterday」標籤。  

如果你在 Excel 中開啟 `TimePeriodDemo.xlsx`，條件格式化已自動套用——不需要額外步驟。

---

![顯示已突顯昨天日期的 Excel 工作表](https://example.com/images/excel-demo.png "產生的 Excel 檔案之螢幕截圖，顯示已突顯的儲存格")

*上圖說明最終的工作簿；請注意含有昨天日期的儲存格被粉紅色突顯。*

## 回顧：我們完成了什麼

- **Created an Excel workbook python** 從頭使用 Aspose.Cells 建立。  
- **Set cell background color** 為整個範圍設定背景色，以提供視覺提示。  
- 套用 **conditional formatting based on date** 自動標記昨天的項目。  
- **Saved workbook as xlsx**，即可供分發或進一步處理。  

以上全部在不到 60 行的 Python 程式碼內完成，且此程式碼可在任何支援 Aspose.Cells 執行環境的平台上運作。

## 往後步驟與相關主題

如果你覺得此內容有幫助，亦可進一步探索：

- 為整列根據狀態值（例如「Completed」「Pending」） **set cell background color**。  
- 使用 **highlight cells based on date range** 建立滾動視窗（最近 7 天、當月）。  
- 以 `SaveFormat.CSV` 或 `SaveFormat.PDF` 匯出至其他格式，如 **CSV** 或 **PDF**。  
- 程式化加入 **charts** 以視覺化剛剛格式化的資料。  

隨意調整日期邏輯、變更色彩調色盤，或擴大範圍以涵蓋整欄。模式保持不變：建立工作簿、附加 conditional‑formatting collection、定義規則，最後儲存。

對特定使用情境有疑問嗎？在下方留下評論，祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.Cells .NET 進行 Excel 自動化：建立工作簿與設定外部連結](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [建立與儲存 Excel 工作簿（Aspose Cells Java）](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [建立與儲存 Excel 工作簿（Aspose Cells .NET）](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}