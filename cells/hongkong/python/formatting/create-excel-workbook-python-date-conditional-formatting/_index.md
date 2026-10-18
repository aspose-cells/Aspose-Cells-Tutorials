---
category: general
date: 2026-08-08
description: 使用 Python 建立 Excel 工作簿並根據日期加入條件格式化。一步一步的指南，使用 Aspose.Cells 突顯昨天的儲存格。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: zh-hant
lastmod: 2026-08-08
og_description: 使用 Python 及 Aspose.Cells 建立 Excel 工作簿，並根據日期套用條件格式，以製作動態試算表。
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: 使用 Python 建立 Excel 工作簿 – 日期條件格式設定
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: 使用 Python 為 Excel 工作簿設定日期條件格式
url: /zh-hant/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中建立 Excel 工作簿的日期條件格式化

如果你需要 **create Excel workbook Python** 並自動突顯符合特定日期的儲存格，本教學將完整示範。你將學會套用 **conditional formatting based on date**，讓昨天的日期以粉紅色顯示，使用 Aspose.Cells 函式庫。

本指南逐步說明從安裝 SDK 到儲存最終 .xlsx 檔案的每個步驟，讓你可以直接複製貼上可執行範例到自己的專案。無需外部文件說明；所有程式碼與解說皆完整自足。

## 前置條件

* 已安裝 Python 3.8 或更新版本。
* `aspose-cells` 套件（Aspose.Cells 的 Python 包裝器）。使用以下方式安裝：
  ```bash
  pip install aspose-cells
  ```
* 具備 Python 與 Excel 基本概念，例如工作表與儲存格樣式。

> **Pro tip:** Aspose.Cells 可在未安裝 Microsoft Excel 的情況下運作，非常適合伺服器端自動化。

## 步驟 1：在 Python 中建立 Excel 工作簿

第一步是建立一個新的工作簿實例，並取得預設工作表。此物件代表整個 Excel 檔案，並提供存取列、欄與格式化 API 的功能。

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

建立工作簿是後續任何操作的基礎，無論是加入資料、公式或格式規則。

## 步驟 2：定義基於日期的條件格式

現在我們加入 **conditional formatting based on date**。`FormatConditionType.TIME_PERIOD` 列舉允許我們指定內建的時間區段，例如 Yesterday、Today 或 LastWeek。

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

此步驟的重要性：Excel 會對範圍內的每個儲存格評估條件。當儲存格的值屬於定義的區段（昨天）時，系統會自動套用我們指定的樣式。

## 步驟 3：以範例日期填充範圍

為了觀察規則效果，我們將幾個 `datetime` 物件寫入目標儲存格。其中一個特意設定為相對於工作簿內部日期系統的昨天日期。

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

`number = 30` 這一行指示 Excel 使用其標準的短日期格式顯示值。若想要其他呈現方式，可將此索引更改為任何內建的數字格式。

## 步驟 4：調整欄寬以提升可讀性

自動調整包含日期的欄寬可使輸出更易閱讀，特別是在 Excel 或檢視器中開啟工作簿時。

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## 步驟 5：將工作簿儲存至磁碟

最後，將工作簿儲存為 .xlsx 檔案。將 `"YOUR_DIRECTORY"` 替換為你機器上的實際路徑。

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

當你在 Excel 中開啟 `TimePeriodDemo.out.xlsx` 時，儲存格 **I19** 會因其值符合「Yesterday」規則而呈現粉紅背景，而 **K20** 則保持不變。

### 預期輸出

| I19（日期） | I20（標籤） | J19 | J20 | K19 | K20（日期） |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30*（粉紅背景） | Yesterday | – | – | – | *2008‑08‑03*（無格式） |

粉紅色陰影證實 **conditional formatting based on date** 正常運作。

## 常見變化與邊緣情況

| 情況 | 如何調整程式碼 |
|-----------|-----------------------|
| **將「Yesterday」改為「Today」的突顯** | Change `condition.time_period = TimePeriodType.TODAY` |
| **將規則套用至整欄** | Use `worksheet.get_range("A:A").format_conditions` |
| **使用自訂日期範圍（例如最近 7 天）** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **不同的背景顏色** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **在無顯示介面的 Linux 上執行** | Aspose.Cells is fully headless; no extra configuration required. |

## 完整、可執行範例

以下為完整腳本，可直接執行（更新輸出目錄後）。已包含所有匯入、註解與錯誤處理的基本寫法。

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

執行此腳本會產生一個 Excel 檔案，將「Yesterday」儲存格自動突顯，展示 **create Excel workbook Python** 與 **conditional formatting based on date** 的結合應用。

## 結論

現在你已了解如何 **create Excel workbook Python** 物件，並定義 **date‑based conditional formatting**

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建構於所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}