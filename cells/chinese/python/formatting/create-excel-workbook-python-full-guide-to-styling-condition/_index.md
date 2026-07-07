---
category: general
date: 2026-07-06
description: 使用 Python 创建 Excel 工作簿，包含设置单元格背景颜色、以编程方式设置单元格样式，以及添加条件格式（Python）以突出显示今天的日期。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: zh
lastmod: 2026-07-06
og_description: 即时使用 Python 创建 Excel 工作簿。学习如何编程设置单元格背景颜色、设置单元格样式，以及添加条件格式（Python）以突出显示今天的日期。
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: 使用 Python 创建 Excel 工作簿 – 设置单元格样式并突出显示今天
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
title: 使用 Python 创建 Excel 工作簿 – 样式与条件格式完整指南
url: /zh/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建 Excel 工作簿 – 样式与条件格式完整指南

Ever wondered how to **create Excel workbook Python** from scratch without opening Excel yourself? You’re not alone. Many developers need to generate reports, dashboards, or even simple data logs on the fly, and doing it programmatically saves hours of manual work.

在本教程中，我们将完整演示整个过程：从创建全新的工作簿，到 **set cell background color**，再到 **set cell style programmatically**，最后使用 **add conditional formatting python** 来 **highlight today date excel**。完成后，你将拥有一个可直接运行的脚本，能够在几秒钟内生成精美的 .xlsx 文件。

---

## 你将构建的内容

- 一个包含若干已填充单元格的全新 Excel 文件。
- 单元格使用自定义背景颜色。
- 数值和日期使用特定的数字样式进行格式化。
- 一个条件规则，自动高亮包含今天日期的单元格。

无需外部安装 Excel——通过 .NET 的 Aspose.Cells for Python 完成所有繁重工作。

---

## 前置条件

| 要求 | 原因 |
|------|------|
| Python 3.8+ | 现代语法和类型提示 |
| `aspose-cells` package | 用于工作簿操作的核心库 |
| `aspose-pydrawing` (installed with Aspose.Cells) | 提供 `Color` 类 |
| Basic familiarity with Excel concepts (cells, ranges, formatting) | 熟悉 Excel 概念（单元格、范围、格式化），使教程更流畅 |

Install the library with:

```bash
pip install aspose-cells
```

---

## 步骤 1：初始化工作簿和工作表

在 **create excel workbook python** 时，首先要实例化一个 `Workbook` 对象并获取默认工作表。可以将工作簿视为整个 Excel 文件，而工作表则是其中的一个标签页。

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **技巧提示：** 如果需要多个工作表，可使用 `book.worksheets.add("MySheet")` 添加更多标签页。

---

## 步骤 2：用于样式和条件格式的辅助类

下面是一个紧凑而完整的 `ConditionalFormatting` 类。它封装了以下重复性任务：

1. 将类似 `"A1:C3"` 的范围转换为 `CellArea`。
2. 为该区域的每个单元格填充递增的数字（仅作演示）。
3. 应用实心的 **set cell background color**。
4. 添加一个 **highlight today date excel** 的条件规则。

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

### 为什么使用辅助类？

- **可复用性：** 你可以在任何工作表上调用 `add_time_period_1()`，无需重新编写逻辑。
- **清晰性：** 每个方法只做一件事——这是简洁代码的标志。
- **可扩展性：** 想添加更多规则？只需按照相同模式再添加一个方法即可。

---

## 步骤 3：应用格式并保存文件

现在我们把所有内容串联起来：实例化辅助类，运行格式化例程，最后将工作簿写入磁盘。

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

打开 *styled_workbook.xlsx* 时，你应该看到：

- 单元格 **A1:C3** 编号 0‑8，填充浅天蓝色。
- 单元格 **I1** 显示今天的日期，背景为粉红色（得益于条件规则）。
- 单元格 **K2** 显示静态日期 *2008‑07‑30* 以作对比。
- 单元格 **I2** 包含文本 “Today”。

这正是 **highlight today date excel** 要求的可视化提示。

---

## 步骤 4：深入探索 – 自定义样式

如果需要调整字体、边框或数字格式，可以扩展 `fill_cell` 方法或创建新的辅助类：

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

然后可以在循环中调用 `apply_custom_style(cell, bold=True)`，对范围内的每个单元格 **set cell style programmatically**。

---

## 常见陷阱及避免方法

| 症状 | 可能原因 | 解决办法 |
|------|----------|----------|
| 即使使用 `Color.light_sky_blue`，单元格仍保持白色 | 在设置 `foreground_color` 后未应用样式 | 在修改样式对象后始终调用 `cell.set_style(style)`。 |
| 条件规则从未触发 | `style.number` 未为日期单元格设置，导致 Excel 将值视为字符串 | 在 `cell.put_value(datetime…)` 之前设置 `style.number = 30`（或任意日期格式）。 |
| 尽管使用 `SaveFormat.XLSX`，工作簿仍保存为 .xls | Aspose 版本较旧，默认使用旧格式 | 升级到最新的 `aspose-cells` 包。 |
| 类似 `"A1"` 的范围抛出索引错误 | 在尚未初始化的工作表上使用 `cells.get("A1")` | 确保工作表已存在（在 `Workbook()` 后即已创建），或使用基于零索引的 `cells.get(row, col)`。 |

---

## 完整脚本，复制粘贴使用

下面是 **完整** 脚本，你可以直接保存为 `create_excel.py` 并立即运行。

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


## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术。每个资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能，并在自己的项目中探索替代实现方式。

- [使用 Aspose.Cells .NET 的 Excel 自动化：创建工作簿并设置外部链接](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [精通 Aspose.Cells for .NET 的 Excel 单元格格式化与工作簿管理](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel 自动化：使用 Aspose.Cells for .NET 创建工作簿并添加 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}