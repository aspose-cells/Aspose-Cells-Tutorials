---
category: general
date: 2026-08-24
description: 在 Python 中使用 Aspose.Cells 建立條件格式規則，以突顯日期，並自動調整欄寬及設定背景顏色格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: zh-hant
lastmod: 2026-08-24
og_description: 在 Python 中使用 Aspose.Cells 建立條件格式規則。學習如何突出顯示日期、設定背景顏色，並只需幾行程式碼即可自動調整欄寬。
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: 在 Python 中為日期建立條件格式規則 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: 如何在 Python 中為日期建立條件格式化規則
url: /zh-hant/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Python 中建立日期的條件格式規則

如果您需要**建立條件格式規則**以回應日期，本指南將向您展示如何使用 Aspose.Cells for Python 完成。無論您是在構建報告儀表板或自動化試算表，您都會看到如何突出顯示昨天的日期、套用自訂背景顏色，以及**自動調整欄寬**，使結果看起來更精緻。

在本教學中，我們將介紹**依日期的條件格式**、示範**背景顏色條件格式**，並以將活頁簿儲存為 XLSX 檔案作結。完成後，您將擁有一個可重複使用的輔助函式，能依需求套用任何**基於日期的條件格式**。

## 您將學會

* 使用 Aspose.Cells 設定活頁簿與工作表。  
* 編寫輔助函式，將**基於日期的條件格式**新增至任意儲存格範圍。  
* 以範例日期填入儲存格，使規則得以評估。  
* 套用**自動調整欄寬**，使內容易於閱讀。  
* 儲存活頁簿並驗證已突出顯示的儲存格。

唯一的前置條件是具備可運作的 Python 環境，且已安裝 `aspose-cells` 套件。

## 前置條件

| 需求 | 細節 |
|------|------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Basic knowledge of Excel concepts | worksheets, cells, formatting |
| 可選：IDE (VS Code, PyCharm, etc.) | any editor that can run Python scripts |

## 步驟 1：建立活頁簿並取得第一個工作表

第一步是建立**可套用條件格式規則**的物件：`Workbook` 與其預設的 `Worksheet`。這些物件是所有後續操作的入口。

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*為何重要：* `Workbook` 包含整個 Excel 檔案，而 `Worksheet` 則是您套用儲存格、樣式以及**依日期的條件格式**的地方。若沒有這些物件，其餘程式碼將無從執行。

## 步驟 2：建立輔助函式以新增 TIME_PERIOD 條件格式

為避免對每個範圍重複相同的樣板程式碼，我們將邏輯封裝於輔助函式中。此函式會附加一個**背景顏色條件格式**，根據 `TimePeriodType`（例如 Yesterday、Today、LastWeek）為儲存格著色。

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*為何使用輔助函式：* 它將**基於日期的條件格式**邏輯隔離，使程式碼更易閱讀、測試，且可在多個工作表或專案間重複使用。

## 步驟 3：將條件格式規則套用至特定範圍

現在我們使用輔助函式來突出顯示包含「Yesterday」的儲存格。這是我們**建立條件格式規則**操作的核心。

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

當活頁簿開啟時，`I19:K20` 中任何日期等於昨天的儲存格都會以粉紅色填滿（即我們在輔助函式中設定的樣式）。`bg_color` 參數示範了若需要，如何在條件顏色之下加上一層預設背景。

## 步驟 4：以範例日期填入範圍

條件規則只有在工作表包含符合條件的資料時才會顯示。我們將插入兩個日期：一個符合「Yesterday」，另一個則不在此期間內。

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*為何重要：* 透過使用 `datetime` 物件，我們確保 Excel 將這些值視為真實日期，這是**依日期的條件格式**正確運作的前提。數值格式（`30`）保證儲存格顯示為可辨識的日期。

## 步驟 5：自動調整欄寬並儲存活頁簿

在資料與格式設定完成後，最後的潤飾是**自動調整欄寬**，使日期完整顯示。接著將檔案寫入磁碟。

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

`auto_fit_column` 會檢查第 12 欄（即 Excel 中的 **L** 欄）中最長的內容，並相應地擴展寬度。此小步驟可防止日期被截斷，並使**背景顏色條件格式**清晰可見。

### 預期結果

當您開啟 `TimePeriodDemo.out.xlsx`：

| I19（日期） | I20（標籤） | K20（日期） |
|------------|------------|------------|
| 30‑Jul‑2008（粉紅色突出顯示） | Yesterday | 03‑Aug‑2008（未突出顯示） |

* 昨天日期的儲存格會顯示粉紅色背景，因為**建立條件格式規則**匹配了 `YESTERDAY` 期間。  
* 其他所有儲存格保留預設背景（或您提供的可選 `medium_sea_green`）。  
* L 欄會自動加寬，使日期完整可讀。

## 常見變形與邊緣情況

| 情況 | 如何調整程式碼 |
|-----------|-----------------------|
| **將「Today」而非「Yesterday」突出顯示** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **使用不同的背景顏色** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **將規則套用至非連續範圍** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **使用已存在的活頁簿** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **在同一範圍上使用多個基於日期的條件** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## 結論

您現在已了解如何使用 Aspose.Cells for Python **建立條件格式規則**以回應日期、套用**背景顏色條件格式**，以及 **自動調整欄寬**。此輔助函式抽象化了邏輯，讓您能在任何**依日期的條件格式**情境（如「Yesterday」、「LastWeek」或自訂範圍）中重複使用相同模式。

接下來，您可以探索：

* 在日期規則旁加入**圖示集合**或**資料條**。  
* 產生從資料庫提取日期的動態報告。  
* 在同一工作表上結合多個**基於日期的條件格式**規則。

歡迎隨意嘗試不同的顏色、期間與範圍，以符合您的專案需求。祝開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆包含完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [精通 Aspose.Cells .NET 在 Excel 中的條件格式：完整指南](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [如何使用 Aspose.Cells for .NET 提取條件格式顏色](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [精通 Aspose.Cells for .NET 與 C# 在 Excel 中使用自訂字型的條件格式](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}