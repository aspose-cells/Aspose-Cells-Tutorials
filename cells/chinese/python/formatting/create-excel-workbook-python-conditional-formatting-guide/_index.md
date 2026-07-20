---
category: general
date: 2026-07-20
description: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿，设置单元格背景颜色，并添加条件格式化（Python）以按日期为单元格设置样式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: zh
lastmod: 2026-07-20
og_description: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿。学习如何设置单元格背景颜色并添加条件格式，以按日期格式化单元格。
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: 使用 Python 创建 Excel 工作簿 – 添加条件格式
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
title: 使用 Python 创建 Excel 工作簿 – 条件格式化指南
url: /zh/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建 Excel 工作簿 – 条件格式化指南

是否曾想过 **使用 Python 创建 Excel 工作簿**，从零开始并且不打开 UI 就让它看起来很专业？你并不孤单。许多开发者在需要 **设置单元格背景颜色** 或以日期为依据进行样式设置时都会卡住。

在本教程中，我们将通过一个完整、可运行的示例，使用 Aspose.Cells **添加条件格式化 python** 规则，按日期格式化单元格，并将结果保存为现代 XLSX 文件。完成后，你将拥有一个可以直接放入任何项目的独立脚本。

## 你将学到的内容

- 如何初始化工作簿并获取第一个工作表。  
- 为整个范围 **设置单元格背景颜色** 的方法。  
- 使用 **aspose cells 条件格式化** 高亮“昨天”日期。  
- 自动调整列宽并将文件持久化到磁盘。  

无需任何外部配置——只需要 Python 3 和 Aspose.Cells 包。如果你已经安装了 `aspose-cells`，即可直接使用；否则只需执行 `pip install aspose-cells` 即可。

## 前置条件

- Python 3.8+（代码在 3.9、3.10 以及更高版本均可运行）。  
- Aspose.Cells for Python via .NET（`aspose-cells` NuGet 包装器）。  
- 对 Excel 基础概念（单元格、范围、格式）有基本了解。  

准备好了吗？太好了——让我们开始吧。

## 使用 Python 创建 Excel 工作簿 – 初始化和工作表

首先：我们需要一个全新的工作簿对象以及对默认工作表的引用。这就是后续所有操作的画布。

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **为什么重要：** `Workbook()` 在内存中构建 Excel 文件，省去了任何临时文件的需求。`worksheet` 变量是我们进行单元格级别操作的入口。

## 设置单元格背景颜色

在添加任何规则之前，先为目标范围设置一个基础颜色，这样条件格式化才能更突出。下面的辅助函数既会获取（或创建）给定范围的 `FormatConditionCollection`，又会将单元格涂上纯色背景。

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

> **小技巧：** 如果你计划对同一范围使用多个规则，只需调用一次此辅助函数并保留返回的集合；这样可以减少几次 API 调用。

## 为日期范围添加条件格式化 Python

现在进入有趣的部分：我们将创建一个 **时间段条件格式化** 规则，突出显示包含昨天日期的单元格。这演示了使用 Aspose.Cells **按日期格式化单元格** 的强大功能。

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

> **为什么使用 `TIME_PERIOD`？** 它抽象掉了编写自定义公式的需求。Aspose.Cells 会将日期与当前系统日期进行比较，规则始终保持有效。

### 运行规则

```python
apply_yesterday_rule()
```

打开生成的文件后，单元格 `I19` 会呈现粉红色（因为它是“昨天”），而 `K20` 则保持基础的绿色颜色。

## 自动调整列宽并保存工作簿

整洁的电子表格更显专业。自动调整列宽可以确保数据不被压缩。

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **边缘情况：** 如果目标目录不存在，`workbook.save` 会抛出错误。若需要更优雅的处理，请将保存调用包装在 `try/except` 块中。

### 完整脚本（可直接复制粘贴）

下面是完整脚本，已准备好运行。只需将 `YOUR_DIRECTORY` 替换为机器上的有效文件夹路径。

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

运行此脚本后，将生成 `TimePeriodExample.xlsx`，其中包含我们前面描述的条件格式化。

## 常见问题与技巧

- **可以针对不同的日期范围吗？**  
  当然。将 `"I19:K20"` 改为任意 A1 样式的范围，并相应调整示例日期即可。

- **如果需要自定义公式而不是 `YESTERDAY`，该怎么办？**  
  使用 `FormatConditionType.FORMULA` 并设置 `condition.formula1 = "YOUR_FORMULA"`——例如 `=TODAY()-A1=1` 来模拟昨天。

- **如何对同一范围应用多个规则？**  
  再次调用 `conditions.add_condition`，传入不同的 `FormatConditionType`。规则的顺序很重要，后添加的规则可能会覆盖之前的。

- **能同时设置字体颜色和背景颜色吗？**  
  可以——修改 `condition.style.font.color = Color.white`（或其他 `Color`）。

## 结论

现在，你已经掌握了如何使用 Aspose.Cells **使用 Python 创建 Excel 工作簿**、**设置单元格背景颜色**，以及 **添加条件格式化 python** 来按日期格式化单元格。该脚本功能完整，能够处理如缺失目录等边缘情况，并可扩展至更复杂的场景，例如多规则条件逻辑或动态范围检测。

准备好下一步了吗？尝试将 “昨天” 规则替换为 “上周”，实验渐变填充，或生成包含数十个格式化表格的完整报告。所有构建块都已就绪，而你已经掌握了 **aspose cells 条件格式化** 在 Python 中的核心用法。

祝编码愉快，欢迎在评论区分享你的变体！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}