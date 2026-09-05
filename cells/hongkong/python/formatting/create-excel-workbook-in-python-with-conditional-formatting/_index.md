---
category: general
date: 2026-09-05
description: 在 Python 中建立 Excel 工作簿，並加入條件格式以突顯昨天的儲存格。了解完整程式碼以及每一步的重要性。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: zh-hant
lastmod: 2026-09-05
og_description: 在 Python 中建立 Excel 工作簿，並加入條件格式以突出顯示昨天的儲存格。請跟隨此一步一步的指南，獲得完整解決方案。
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: 在 Python 中建立 Excel 工作簿 – 加入條件格式
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: 使用 Python 建立具條件格式的 Excel 活頁簿
url: /zh-hant/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 建立 Excel 活頁簿並套用條件格式化

如果您需要 **create Excel workbook python** 來完成報告任務，本指南將示範如何產生活頁簿並套用條件格式化規則，以突顯昨天的日期。您將看到完整程式碼、每行程式碼的目的，以及如何將此解決方案套用到其他日期範圍。

條件格式化是一種強大的方式，可將注意力聚焦在符合特定條件的資料上。在本教學中，我們使用 Aspose.Cells 的 Python via .NET 函式庫，該函式庫提供完整的 Excel 功能支援，且不需安裝 Microsoft Office。完成本指南後，您將得到一個檔案，當 *I19:K20* 範圍內的儲存格包含昨天的日期時，會自動變成粉紅色。

## 前置條件

* 已安裝 Python 3.9+
* `aspose-cells` 套件（使用 `pip install aspose-cells` 安裝）
* 具備基本的 Python 語法知識
* 具有寫入活頁簿將儲存之目錄的權限

只要 .NET 執行環境可用，程式碼即可在 Windows、macOS 與 Linux 上執行。

## 使用 Python 建立 Excel 活頁簿

第一步是實例化一個 `Workbook` 物件，並取得預設工作表。此物件在記憶體中代表整個 Excel 檔案。

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*此處重要性*：`Workbook()` 會建立一個僅含單一工作表的空白活頁簿。存取 `worksheets[0]` 可取得操作該工作表的句柄，以便稍後加入資料、樣式與格式設定。

## 新增條件格式化範圍

接下來我們定義將由條件規則評估的區域。範圍 `I19:K20` 包含兩列共六個儲存格。

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*此處重要性*：將條件格式化集合加入特定範圍可將規則隔離，避免影響其他無關儲存格。這符合 **add conditional formatting range** 的需求。

## 定義規則：根據日期突顯儲存格

現在我們建立一個類型為 `TIME_PERIOD` 的條件。此設定會指示 Excel 將每個儲存格的值與預先定義的時間區間進行比較。

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*此處重要性*：`TIME_PERIOD` 是唯一內建支援「Yesterday」「Today」「Last Week」等的類型。將 `condition.time_period` 設為 `YESTERDAY` 後，規則會自動將每個儲存格的日期值與當前日期的前一天進行比較。

## 為符合條件的儲存格設定樣式

條件格式化同時需要視覺樣式。此處我們選擇粉紅色實心填滿，以突顯符合條件的儲存格。

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*此處重要性*：樣式物件定義了 Excel 如何呈現符合條件的儲存格。使用實心粉紅填色即可滿足 **highlight cells based on date** 的需求，且讓結果易於驗證。

## 填入樣本日期以供評估

為了觀察規則的實際效果，我們插入兩個日期——一個為昨天的日期，另一個則不是。`number` 格式 `30` 對應內建的日期格式 `mm-dd-yy`。

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*此處重要性*：同時提供符合與不符合的日期，可讓您驗證條件格式化是否正確運作。執行腳本時請將日期調整為當月，或改為使用動態值。

## 儲存活頁簿

最後，我們將檔案寫入磁碟。`SaveFormat.XLSX` 常數確保輸出為現代的 Excel 檔案格式。

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*此處重要性*：將活頁簿持久化後，即可在 Excel、LibreOffice 或任何支援 XLSX 的檢視器中開啟。印出的路徑可確認檔案寫入的位置。

## 完整腳本

將所有部件組合起來，完整且可執行的腳本如下：

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### 預期輸出

當您開啟 `TimePeriodExample.xlsx` 時：

* 儲存格 **I19** 會呈現粉紅背景，因為其值符合昨天的日期。
* 儲存格 **K20** 保持預設背景，因為其日期不在指定期間內。
* 標籤 **“Yesterday”** 置於儲存格 I20，以示說明。

## 常見變化與邊緣情況

| Situation | Adjustment |
|-----------|------------|
| **將突顯今天而非昨天** | 將 `condition.time_period = TimePeriodType.TODAY`。 |
| **將規則套用至更大範圍** | 將 `add("I19:K20")` 中的範圍字串更新為類似 `"A1:Z100"` 的範圍。 |
| **使用不同的填色** | 將 `DrawingColor.pink` 替換為其他任意 `DrawingColor`（例如 `DrawingColor.light_green`）。 |
| **使用動態日期** | 計算 `datetime.now() - timedelta(days=1)` 取得昨天的日期，並在套用規則前將該值寫入儲存格。 |

**小技巧：** 當您為大量使用者程式化產生活頁簿時，請將條件格式化的定義與資料插入分開。如此即可在多個工作表間重複使用相同樣式，避免程式碼重複。

## 以程式方式驗證結果（可選）

如果您想在不開啟 Excel 的情況下確認格式化結果，可在儲存後檢查儲存格的樣式：



## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並在此基礎上進一步說明。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Excel Automation：使用 Aspose.Cells for .NET 建立活頁簿並加入 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [使用 Aspose.Cells for Java 建立 Excel 活頁簿並加入標籤](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation 建立活頁簿並加入 ListBox（Aspose Cells）](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}