---
category: general
date: 2026-09-15
description: 學習如何在 Python 中使用 Aspose.Cells 套用時間段條件格式化，並將工作簿儲存為 XLSX。內含逐步程式碼示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: zh-hant
lastmod: 2026-09-15
og_description: 使用 Python 在 Excel 中套用時間段條件格式，並將工作簿儲存為 XLSX。請參考 Aspose.Cells 完整指南。
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: 使用 Python 在 Excel 中套用時間區間條件格式
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: 如何在 Excel 中使用 Python 套用時間段條件格式
url: /zh-hant/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Python 套用時間區間條件格式化

如果您需要在 Excel 檔案中使用 **time period conditional formatting**，本教學將完整示範如何使用 Python 來實作。您將看到一個完整且可執行的範例，會建立工作簿、標示昨天的日期，並在幾行程式碼內 **save workbook as XLSX**。

條件格式化是一種強大的方式，可將符合特定規則的資料凸顯出來。在本指南中，我們聚焦於「Yesterday」時間區間，但相同的模式亦適用於其他內建區間，如 Today、LastWeek、以及 NextMonth。完成本教學後，您將能夠撰寫 **how to create excel workbook python**‑style 的腳本，並可直接投入生產環境。

## 前置條件

- 已安裝 Python 3.8+  
- `aspose-cells` 與 `aspose-pydrawing` 套件（`pip install aspose-cells aspose-pydrawing`）  
- 具備 Python 語法的基本熟悉度  

不需要額外安裝 Office，因為 Aspose.Cells 會在內部處理檔案產生。

## 使用 Aspose.Cells 於 Python 進行時間區間條件格式化

本節將逐行說明完成主要任務所需的程式碼。以下程式碼區塊即為完整腳本，註解說明每一步的目的。

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### 為何每一步都很重要

1. **Creating the workbook** 為您提供一個記憶體中的 Excel 檔案，無需開啟 Excel 即可操作。  
2. **Defining the range** (`I19:K20`) 告訴 Aspose.Cells 規則適用的範圍，讓邏輯保持獨立。  
3. **Adding a TIME_PERIOD condition** 使用 Aspose 內建的列舉 `TimePeriodType.YESTERDAY`。此方式避免手動計算日期，且在不同日期開啟檔案時會自動更新。  
4. **Setting the style** (`background_color` 與 `pattern`) 決定被標示儲存格的外觀。使用 `Color.pink` 可讓規則更易辨識。  
5. **Writing sample dates** 並設定數字格式 30，可確保 Excel 以短日期顯示，而非序列號。  
6. **Auto‑fitting the column** 提升日後開啟檔案者的可讀性。  
7. **Saving as XLSX** 產生高度相容的檔案，可在 Excel、Google Sheets 或任何現代試算表程式中開啟。

## 如何使用 Aspose.Cells 以 Python‑style 建立 Excel 工作簿

上述腳本已示範了 **how to create excel workbook python** 的最小步驟。實務上您可能還想要：

- 新增多個工作表 (`workbook.worksheets.add("Report")`)。  
- 使用迴圈或 pandas DataFrames 填充大型資料表 (`worksheet.cells.import_data_table`)。  
- 使用 `cell.get_style()` 套用額外的格式（字型、框線）。

所有這些操作皆遵循相同模式：取得物件、修改其屬性，然後呼叫 `set_style` 或 `save`。

## 新增條件格式化 Python – 其他實用模式

除了「Yesterday」範例外，Aspose.Cells 亦支援多種條件格式化類型：

| FormatConditionType | Typical use case |
|---------------------|------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | 自訂公式 (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | 簡單比較 (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | 漸層色彩比例 |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | 內嵌條形圖視覺化 |

若要 **add conditional formatting python** 針對數值門檻，您可以將 `FormatConditionType.TIME_PERIOD` 替換為 `FormatConditionType.CELL_VALUE`，並設定 `condition.operator_type` 與 `condition.formula1`。

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## 儲存工作簿為 XLSX – 最佳實踐

在 **save workbook as xlsx** 時，請考慮以下事項：

- **指定正確的 `SaveFormat`** (`SaveFormat.XLSX`) 以避免使用舊版格式。  
- **使用確定性的檔名**，若腳本在迴圈中執行（`f"report_{datetime.now():%Y%m%d}.xlsx"`）。  
- **關閉資源**（`workbook.dispose()`），在長時間執行的服務中釋放原生記憶體。

本範例已使用 `SaveFormat.XLSX`，會產生以 zip 為基礎的現代工作簿，且保留所有條件格式化規則。

## 在 Excel 中標示昨天 – 驗證步驟

執行腳本後，開啟 `TimePeriodExample.xlsx`：

1. 儲存格 `I19` 與 `K20` 包含日期 `30‑07‑2008` 與 `03‑08‑2008`。  
2. 儲存格 `I20` 顯示文字 “Yesterday”。  
3. 若將系統日期改為 **July 30 2008** 並重新開啟檔案，符合日期的儲存格會自動以粉紅色填滿。  
4. 將系統日期改為其他任何一天，粉紅色填滿會消失，證實規則會依據 **time period conditional formatting** 邏輯作出反應。

## 常見陷阱與避免方法

- **缺少 `aspose-pydrawing`** – `Color` 類別位於此套件；若忘記安裝會拋出 `ImportError`。  
- **數字格式不正確** – 使用預設的 General 格式會顯示序列號（例如 39822）。請務必將 `style.number = 30` 設為短日期格式。  
- **範圍不匹配** – 條件格式化的範圍必須包含您欲標示的儲存格，否則規則不會生效。

## 專業提示：重複使用格式化例程

若需在多個工作簿中使用相同的 “Yesterday” 規則，可將邏輯封裝於輔助函式中：

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

在需要的地方呼叫 `apply_yesterday_highlight(worksheet, "A1:A10")`。

## 結論

本指南示範了如何在 Excel 中使用 Python 實作 **time period conditional formatting**、如何 **save workbook as XLSX**，以及如何以單一可重用的腳本 **highlight yesterday in Excel**。您現在已具備堅實的基礎，能在任何自動化專案中加入 **add conditional formatting python** 程式碼，無論是產生每日報表、建置儀表板，或是匯出資料。

**下一步**

- 探索其他 `TimePeriodType` 值，如 `TODAY` 或 `LAST_WEEK`。  
- 在相同範圍內結合多個條件規則，以獲得更豐富的視覺提示。  
- 將工作簿產生整合至 Web 服務或排程工作中。

祝程式開發順利，並享受條件格式化為您的 Excel 自動化帶來的視覺清晰度！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [精通使用 Aspose.Cells .NET 於 Excel 進行條件格式化：完整指南](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [精通 Aspose.Cells .NET：在 Excel 中對交錯列套用條件格式化](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [精通使用 Aspose.Cells for .NET 與 C# 在 Excel 中以自訂字型套用條件格式化](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}