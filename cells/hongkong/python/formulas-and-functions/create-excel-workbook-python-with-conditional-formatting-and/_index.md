---
category: general
date: 2026-10-04
description: 使用 Aspose.Cells 在 Python 中建立 Excel 工作簿。學習 Excel 條件格式化（Python）、儲存格背景顏色（Python）以及日期儲存格格式化（Python）的完整範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: zh-hant
lastmod: 2026-10-04
og_description: 使用 Aspose.Cells 建立 Excel 工作簿（Python）。本教學逐步說明 Excel 條件格式化（Python）、儲存格背景顏色（Python）以及儲存格日期格式化（Python）。
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: 使用 Python 建立 Excel 工作簿 – 完整指南與條件格式設定
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: 使用 Python 建立 Excel 工作簿，並套用條件格式與儲存格背景顏色
url: /zh-hant/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用條件格式化與儲存格背景色的 Python 建立 Excel 活頁簿

如果您需要快速 **create Excel workbook python**，本指南會精確說明如何操作。您將看到一個完整、可執行的範例，加入 **excel conditional formatting python**、變更 **cell background color python**，以及 **format cells date python** 以突顯「Yesterday」的日期。

在許多報表情境中，彩色儲存格的視覺提示能讓資料即時易於理解。本教學會逐行說明程式碼，解釋每一步的重要性，並提供一個可直接執行的腳本，讓您能依需求套用於自己的專案。

## 您將完成的目標

1. 使用 Aspose.Cells 函式庫 **create Excel workbook python**。  
2. 套用會自動突顯「Yesterday」日期的 **excel conditional formatting python**。  
3. 將 **cell background color python** 設為粉紅色（或任何您喜好的顏色）。  
4. 使用 **format cells date python** 使日期顯示為標準的 Excel 日期格式。  

不需要事先具備 Aspose.Cells 的使用經驗——只要有可運作的 Python 3 環境與 pip 取得權限即可。

## 前置條件

- 已安裝 Python 3.8 或更新版本。  
- `aspose-cells` 與 `aspose-pydrawing` 套件已透過 `pip install aspose-cells aspose-pydrawing` 安裝。  
- 具備基本的 Python 語法與 Excel 概念（活頁簿、工作表、儲存格）認識。  

> **專業提示：** 若在虛擬環境中執行腳本，可避免與其他專案的版本衝突。

## 步驟 1：設定專案並匯入所需類別

當您 **create Excel workbook python** 時，第一步是匯入所需的 Aspose.Cells 類別。這些類別讓您直接操作活頁簿建立、條件格式化與樣式設定。

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*為什麼這很重要：* 只匯入必要的符號可保持命名空間整潔，讓程式碼更易閱讀。`Workbook` 是 **create Excel workbook python** 的入口，而 `FormatConditionType` 與 `TimePeriodType` 則是 **excel conditional formatting python** 所必需的。

## 步驟 2：建立新活頁簿並取得第一個工作表

現在我們真正 **create Excel workbook python**。`Workbook()` 建構子會產生一個空的 Excel 檔案，並包含預設的工作表。

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*說明：* 每個 Excel 檔案至少會有一個工作表。預設情況下 Aspose.Cells 會將其命名為「Sheet1」。您之後可以加入更多工作表，但在此示範中使用單一工作表可使範例更聚焦。

## 步驟 3：定義條件格式化的目標範圍

條件格式化作用於矩形範圍。此處我們選擇 `I19:K20` 範圍，提供三欄兩列可供使用。

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*為什麼這樣做：* `get` 方法會回傳與指定範圍相關聯的 `ConditionalFormatting` 物件。若該範圍尚未有任何格式，Aspose.Cells 會自動建立新的集合。

## 步驟 4：新增 TIME_PERIOD 條件並設定背景色

這是 **excel conditional formatting python** 的核心。我們加入一個 `TIME_PERIOD` 規則，以突顯包含「Yesterday」日期的儲存格。

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*深入探討：*  
- `FormatConditionType.TIME_PERIOD` 告訴 Excel 以相對於當前日期的方式評估日期。  
- `TimePeriodType.YESTERDAY` 是內建的列舉，會每日自動更新，使活頁簿始終突顯最近的「Yesterday」。  
- 將 `background_color` 設為 `Color.pink` 並將圖樣設為 `SOLID`，即可在不使用額外 VBA 程式碼的情況下實現 **cell background color python** 效果。

## 步驟 5：以範例日期填充範圍並套用日期格式

為了觀察條件格式化的效果，我們需要真實的日期值。同時必須 **format cells date python**，讓 Excel 將其視為日期而非純數字。

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*說明：*  
- `style.number = 30` 這行即為 **format cells date python** 的步驟。格式代碼 30 代表短日期格式（`m/d/yy`）。  
- 使用輔助函式可保持程式碼 DRY（不要重複自己），且日後加入更多日期時更為便利。

## 步驟 6：加入說明標籤

一個小標籤可協助任何開啟活頁簿的人了解儲存格被染色的原因。

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## 步驟 7：將活頁簿儲存至磁碟

最後，我們透過呼叫 `save` 在磁碟上 **create Excel workbook python**。`SaveFormat.XLSX` 常數確保檔案為現代的 Office Open XML 格式。

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

當您在 Excel 中開啟 `TimePeriodDemo.xlsx` 時，您會看到：  

- 儲存格 `I19` 與 `K20` 含有日期。  
- 符合「Yesterday」的儲存格（在此靜態範例中為 `I19`）被標示為粉紅色。  
- 標籤「Yesterday」出現在 `I20`。  

> **提示：** 若您在其他日期執行腳本，條件格式化仍會突顯日期恰好比系統當前日期早一天的儲存格——無需修改程式碼。

## 完整腳本 – 可直接複製執行

以下為完整且獨立的程式，結合上述所有步驟。將其複製到名為 `conditional_format_demo.py` 的檔案中，調整 `YOUR_DIRECTORY`，然後以 `python conditional_format_demo.py` 執行。

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### 預期輸出

執行腳本會印出確認訊息：

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

開啟產生的檔案會看到符合「Yesterday」規則的儲存格呈現粉紅背景，證實 **excel conditional formatting python** 與 **cell background color python** 正常運作。

## 常見變化與例外情況

| 情況 | 如何調整程式碼 |
|-----------|-----------------------|
| **不同的突顯顏色** | 將 `Color.pink` 改為其他 `Color` 常數，例如 `Color.light_green`。 |
| **將突顯目標改為「Today」而非「Yesterday」** | 設定 `condition.time_period = TimePeriodType.TODAY`。 |
| **將格式套用於整欄** | 使用類似 `"A:A"` 的範圍，並相應調整 `target_range` 變數。 |
| **使用自訂日期格式** | 將 `style.number = 30` 改為 `style.custom = "dd-mmm-yyyy"`，以獲得更易讀的格式。 |
| **在同一範圍上使用多個條件** |  |


## 接下來您可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}