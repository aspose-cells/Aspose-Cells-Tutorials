---
category: general
date: 2026-07-20
description: 使用 Aspose.Cells 於 Python 建立 Excel 活頁簿，設定儲存格背景顏色，並加入條件格式化（Python）以依日期樣式化儲存格。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: zh-hant
lastmod: 2026-07-20
og_description: 使用 Aspose.Cells 於 Python 建立 Excel 工作簿。學習如何設定儲存格背景顏色，並在 Python 中加入條件格式，以依日期格式化儲存格。
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: 使用 Python 建立 Excel 工作簿 – 添加條件格式
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: 使用 Python 建立 Excel 工作簿 – 條件格式設定指南
url: /zh-hant/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿（Python） – 條件格式化指南

有沒有想過如何從頭開始 **create Excel workbook Python**，且在不開啟介面的情況下讓它看起來更精緻？你並不孤單。許多開發者在需要 **set cell background color** 或以程式方式套用基於日期的樣式時，常會卡關。  

在本教學中，我們將逐步說明一個完整且可執行的範例，使用 Aspose.Cells 來 **add conditional formatting python** 規則，依日期格式化儲存格，並將結果儲存為現代的 XLSX 檔案。完成後，你將擁有一個可直接放入任何專案的獨立腳本。

## 你將學到什麼

- 如何初始化工作簿並取得第一個工作表。  
- 為整個範圍 **set cell background color** 的方法。  
- 使用 **aspose cells conditional formatting** 來突顯「Yesterday」日期。  
- 自動調整欄寬並將檔案持久化至磁碟。  

不需要任何外部設定——只要 Python 3 與 Aspose.Cells 套件即可。若你已安裝 `aspose-cells`，即可直接使用；否則只需執行 `pip install aspose-cells` 即可。

## 前置條件

- Python 3.8+（程式碼在 3.9、3.10 及更新版本皆可執行）。  
- Aspose.Cells for Python via .NET（`aspose-cells` NuGet 包裝器）。  
- 具備 Excel 基本概念（儲存格、範圍、格式化）的基礎知識。  

都有了嗎？太好了——讓我們開始吧。

## 建立 Excel 工作簿（Python） – 設定與工作表

首先，我們需要一個全新的 workbook 物件，並取得預設的 worksheet 參考。這是之後所有操作的畫布。

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **為什麼重要：** `Workbook()` 會在記憶體中建立 Excel 檔案，省去任何暫存檔的需求。`worksheet` 變數是我們進行儲存格層級操作的入口。

## 設定儲存格背景顏色

在加入任何規則之前，先為目標範圍設定基礎顏色，讓條件格式化更為顯眼會比較好。以下的輔助函式會取得（或建立）指定範圍的 `FormatConditionCollection`，並以實心背景為儲存格上色。

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **專業提示：** 若打算在同一範圍內使用多個規則，請只呼叫一次此輔助函式並保留回傳的 collection；這樣可減少 API 呼叫次數。

## 為日期範圍加入 Conditional Formatting Python

現在進入有趣的部分：我們將建立一個 **time‑period conditional formatting** 規則，突顯包含「昨天」日期的儲存格。這展示了使用 Aspose.Cells 進行 **format cells by date** 的威力。

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **為什麼使用 `TIME_PERIOD`？** 它抽象化了自訂公式的需求。Aspose.Cells 會將日期與系統當前日期比較，使規則始終保持有效。

### 執行規則

```python
apply_yesterday_rule()
```

當你開啟產生的檔案時，儲存格 `I19` 會呈現粉紅色（因為它是「Yesterday」），而 `K20` 則保留基礎的綠色。

## 自動調整欄寬並儲存工作簿

整潔的試算表更顯專業。自動調整欄寬可確保資料不會擠在一起。

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **邊緣情況：** 若指定的目錄不存在，`workbook.save` 會拋出錯誤。若需要優雅的處理，請將儲存呼叫包在 `try/except` 區塊中。

### 完整腳本（直接複製貼上）

以下是完整腳本，已可直接執行。只需將 `YOUR_DIRECTORY` 替換為你機器上有效的資料夾路徑。

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

執行此腳本將產生 `TimePeriodExample.xlsx`，其中包含我們先前描述的條件格式化。

## 常見問題與技巧

- **我可以針對不同的日期範圍嗎？**  
  當然可以。將 `"I19:K20"` 改成任何 A1 形式的範圍，並相應調整樣本日期。

- **如果我需要自訂公式而不是 `YESTERDAY` 該怎麼做？**  
  使用 `FormatConditionType.FORMULA`，並設定 `condition.formula1 = "YOUR_FORMULA"`——例如 `=TODAY()-A1=1` 以模擬昨天。

- **如何在同一範圍套用多個規則？**  
  再次呼叫 `conditions.add_condition`，傳入不同的 `FormatConditionType`。規則的順序很重要；後加入的規則可能會覆蓋先前的。

- **能否同時設定字型顏色與背景顏色？**  
  可以——修改 `condition.style.font.color = Color.white`（或其他任意 `Color`）。

## 結論

現在你已了解如何使用 Aspose.Cells **create Excel workbook Python**、**set cell background color**，以及 **add conditional formatting python** 以依日期格式化儲存格。此腳本功能完整，能處理如目錄缺失等邊緣情況，亦可延伸至更複雜的情境，例如多規則條件邏輯或動態範圍偵測。

準備好進一步了嗎？試著將「Yesterday」規則換成「Last Week」、實驗漸層填色，或產生包含數十個已格式化表格的完整報告。所有基礎構件已備妥，而你也剛剛掌握了 Python 中 **aspose cells conditional formatting** 的核心。

祝程式開發順利，歡迎在留言中分享你的各種變化！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [精通 Aspose.Cells for .NET 的 Excel 儲存格格式化與工作簿管理](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 建立並儲存 Excel 工作簿為 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [如何在 Excel 中使用 Aspose.Cells .NET 建立工作簿範圍限定的命名範圍](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}