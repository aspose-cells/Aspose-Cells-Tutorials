---
category: general
date: 2026-09-21
description: 学习如何在 Python 中创建 Excel 工作簿、设置单元格背景颜色，并使用 Aspose.Cells 应用基于日期的条件格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: zh
lastmod: 2026-09-21
og_description: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿，设置单元格背景颜色，并应用基于日期的条件格式。请按照分步指南操作。
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: 使用 Python 创建带条件格式的 Excel 工作簿
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
title: 使用条件格式在Python中创建Excel工作簿
url: /zh/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用条件格式在 Python 中创建 Excel 工作簿

如果你需要 **create Excel workbook python** 脚本来自动高亮日期，本指南将一步步演示。你将看到如何 **set cell background color**、添加 “Yesterday” 规则并保存文件——全部使用 Aspose.Cells for Python。

以编程方式处理 Excel 文件通常意味着在多个工作表中重复相同的格式化逻辑。阅读完本教程后，你将拥有一个可复用的 **excel conditional formatting python** 模式，能够直接嵌入任何项目。

## 前置条件

- 已安装 Python 3.8+  
- `aspose-cells` 包（`pip install aspose-cells`）  
- 对 Python 函数和 datetime 模块有基本了解  

无需其他库；Aspose.Cells 已经处理所有 Excel 操作。

## 第一步：创建工作簿并访问第一个工作表

首先 **create excel workbook python** 对象并获取默认工作表。这为后续样式提供了干净的画布。

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

*为什么重要：* `Workbook()` 会创建一个内存中的 Excel 文件。访问 `worksheets[0]` 可以避免硬编码工作表名称，即使默认名称发生变化也能正常工作。

## 第二步：添加 TIME_PERIOD 条件格式的辅助函数

为了保持代码整洁，我们将条件格式的创建封装在一个辅助函数中。它接受单元格范围、背景颜色和期望的时间段规则。

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

*为什么重要：* 该辅助函数抽象了创建条件格式的重复步骤，便于在其他基于日期的规则（如 “Today” 或 “Last Week”）中复用。

## 第三步：对指定范围应用 “Yesterday” 规则

现在使用辅助函数来高亮包含昨天日期的单元格。范围 `I19:K20` 在满足条件时会显示 **medium sea green**。

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*为什么重要：* `TimePeriodType.YESTERDAY` 是 Aspose.Cells 内置的枚举成员，无需手动计算日期。库会在每次打开工作簿时自动评估该规则。

## 第四步：向范围填充示例日期

为了看到规则的实际效果，我们写入两个日期——一个匹配 “Yesterday”，一个不匹配。`number` 样式 `30` 对应内置的日期格式。

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

*为什么重要：* 通过插入具体日期，你可以在任意时间验证条件格式是否生效，而无需在特定日期打开文件。

## 第五步：添加说明标签并自动调整列宽

一个简短的标签可以说明格式化范围的用途，`auto_fit_column` 则让工作表更易阅读。

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## 第六步：保存工作簿

最后，将工作簿写入磁盘。`os.makedirs` 调用确保目标文件夹已存在。

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

打开 *TimePeriodDemo.xlsx* 时，你会看到：

- 单元格 **I19** 被 **medium sea green** 着色，因为其值匹配 “Yesterday” 规则。  
- 单元格 **K20** 保持默认背景，因为其日期不满足条件。  

这演示了使用一行 Python 代码 **format cells by date** 的方法。

## 完整可运行示例

将所有部分组合在一起，下面是可以直接复制粘贴运行的完整脚本：

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

运行脚本，打开生成的文件，即可看到条件格式的实际效果。

## 常见变体和边缘情况

| 变体 | 实现方式 | 适用场景 |
|------|----------|----------|
| **高亮 “Today”** | 将 `TimePeriodType.YESTERDAY` 替换为 `TimePeriodType.TODAY` | 实时仪表盘 |
| **多个范围** | 为每个范围调用 `add_time_period`，并传入不同颜色 | 复杂报表 |
| **动态日期范围** | 使用 `TimePeriodType.LAST_7_DAYS` 或 `TimePeriodType.NEXT_MONTH` | 滚动报表 |
| **自定义颜色** | 使用 `Color.from_argb(255, r, g, b)` 创建任意色调 | 品牌统一的样式 |

**小技巧：** 当你希望填充为纯色时，请始终设置 `condition.style.pattern = BackgroundType.SOLID`；否则 Excel 可能会显示渐变，导致不同版本之间外观不一致。

## 结论

现在你已经掌握了如何编写 **create Excel workbook python** 脚本来 **set cell background color**、应用 **excel conditional formatting python**，以及使用 Aspose.Cells 实现 **format cells by date**。本示例展示了 **date based conditional formatting** 场景，但相同模式同样适用于任何时间段规则。

接下来，你可以进一步探索：

- 添加数据条或图标集（`FormatConditionType.DATA_BAR`）  
- 在同一范围内组合多个条件规则  
- 将工作簿导出为 PDF（`SaveFormat.PDF`）以用于报告  

欢迎尝试不同的颜色、范围和时间段类型，以满足你的特定报表需求。祝编码愉快！

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式，每篇资源均包含完整可运行的代码示例和逐步解释。

- [掌握 Aspose.Cells for .NET 的 Excel 单元格格式化与工作簿管理](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [使用 Aspose.Cells .NET 实现 Excel 自动化：创建工作簿并设置外部链接](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [使用 Aspose.Cells .NET 在 Excel 中创建工作簿范围命名](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}