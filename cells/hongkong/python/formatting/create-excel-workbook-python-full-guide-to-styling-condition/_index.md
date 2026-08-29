---
category: general
date: 2026-07-06
description: 使用 Python 建立 Excel 活頁簿，並撰寫程式碼設定儲存格背景顏色、程式化設定儲存格樣式，以及加入條件格式化（Python）以突顯今天的日期。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: zh-hant
lastmod: 2026-07-06
og_description: 即時使用 Python 建立 Excel 工作簿。學習如何以程式方式設定儲存格背景顏色、設定儲存格樣式，並加入條件格式化以突顯今天的日期。
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: 使用 Python 建立 Excel 工作簿 – 設定儲存格樣式與標示今天
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: 使用 Python 建立 Excel 工作簿 – 完整樣式與條件格式化指南
url: /zh-hant/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 Python – 完整樣式與條件格式化指南

有沒有想過如何在不打開 Excel 的情況下，從頭 **create Excel workbook Python**？你並不孤單。許多開發人員需要即時產生報告、儀表板，甚至簡單的資料記錄，透過程式自動化可以節省大量手動工作時間。

在本教學中，我們將完整說明整個流程：從建立全新工作簿、**set cell background color**、**set cell style programmatically**，最後使用 **add conditional formatting python** 來 **highlight today date excel**。完成後，你將擁有一支可直接執行的腳本，瞬間產出精美的 .xlsx 檔案。

---

## 您將建立的內容

- 一個全新的 Excel 檔案，內含少量已填入的儲存格。
- 儲存格使用自訂背景色彩。
- 數值與日期以特定數字樣式格式化。
- 一條條件規則，可自動將包含今天日期的儲存格加以突顯。
- 不需要額外安裝 Excel——透過 .NET 的 Aspose.Cells for Python 會處理所有繁重工作。

---

## 前置條件

| 需求 | 為何重要 |
|------|----------|
| Python 3.8+ | 現代語法與型別提示 |
| `aspose-cells` 套件 | 工作簿操作的核心函式庫 |
| `aspose-pydrawing`（隨 Aspose.Cells 安裝） | 提供 `Color` 類別 |
| 基本了解 Excel 概念（儲存格、範圍、格式化） | 讓教學流程更順暢 |

使用以下指令安裝函式庫：

```bash
pip install aspose-cells
```

---

## 步驟 1：初始化工作簿與工作表

在 **create excel workbook python** 時，第一步是實例化一個 `Workbook` 物件，並取得預設的工作表。可將工作簿視為整個 Excel 檔案，而工作表則是其中的一個分頁。

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **專業提示：** 若需要多個工作表，可使用 `book.worksheets.add("MySheet")` 來新增分頁。

---

## 步驟 2：Helper Class for Styling & Conditional Formatting

以下是一個精簡卻完整的 `ConditionalFormatting` 類別。它封裝了以下重複性工作：

1. 將類似 `"A1:C3"` 的範圍轉換為 `CellArea`。
2. 在該區域的每個儲存格填入遞增的數字（僅作示範）。
3. 套用實心 **set cell background color**。
4. 加入一條 **highlight today date excel** 的條件規則。

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### 為何使用 Helper Class？

- **可重用性：** 您可以在任何工作表上呼叫 `add_time_period_1()`，無需重寫程式邏輯。
- **清晰度：** 每個方法只執行單一功能——是乾淨程式碼的標誌。
- **可擴充性：** 想加入更多規則？只需依相同模式新增方法即可。

---

## 步驟 3：套用格式並儲存檔案

現在把所有步驟串起來：實例化 helper、執行格式化例程，最後將工作簿寫入磁碟。

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

開啟 *styled_workbook.xlsx* 後，你應該會看到：

- 儲存格 **A1:C3** 以 0‑8 編號，填滿淡天藍色。
- 儲存格 **I1** 以粉紅背景顯示今天的日期（感謝條件規則）。
- 儲存格 **K2** 顯示固定日期 *2008‑07‑30* 作為比較。
- 儲存格 **I2** 包含文字 “Today”。

這樣的視覺提示正是 **highlight today date excel** 所要求的效果。

---

## 步驟 4：深入探索 – 自訂樣式

如果需要微調字型、邊框或數字格式，可擴充 `fill_cell` 方法或建立新的 helper：

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

之後在迴圈內呼叫 `apply_custom_style(cell, bold=True)`，即可 **set cell style programmatically** 為範圍內的每個儲存格套用自訂樣式。

---

## 常見問題與避免方式

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| 儲存格仍保持白色，即使使用 `Color.light_sky_blue` | 設定 `foreground_color` 後未套用樣式 | 在修改樣式物件後，務必呼叫 `cell.set_style(style)`。 |
| 條件規則永不觸發 | 日期儲存格未設定 `style.number`，導致 Excel 將值視為字串 | 在 `cell.put_value(datetime…)` 之前，設定 `style.number = 30`（或任何日期格式）。 |
| 工作簿仍以 .xls 儲存，即使使用 `SaveFormat.XLSX` | Aspose 版本過舊，預設為舊版格式 | 升級至最新的 `aspose-cells` 套件。 |
| 像 `"A1"` 這樣的範圍拋出索引錯誤 | 在尚未初始化的工作表上使用 `cells.get("A1")` | 確認工作表已存在（在 `Workbook()` 後即已建立），或使用零基索引的 `cells.get(row, col)`。 |

---

## 完整腳本供複製貼上

以下是 **完整** 的腳本，你可以直接存成 `create_excel.py` 後立即執行。

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化所學技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.Cells .NET 進行 Excel 自動化：建立工作簿與設定外部連結](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [精通 Aspose.Cells for .NET 的 Excel 儲存格格式化與工作簿管理](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel 自動化：使用 Aspose.Cells for .NET 建立工作簿並加入 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}