---
category: general
date: 2026-09-05
description: 在 Python 中创建 Excel 工作簿并添加条件格式以突出显示昨天的单元格。了解完整代码以及每一步的重要性。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: zh
lastmod: 2026-09-05
og_description: 在 Python 中创建 Excel 工作簿并添加条件格式以突出显示昨天的单元格。请按照此分步指南获取完整解决方案。
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: 在 Python 中创建 Excel 工作簿 – 添加条件格式
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
title: 在 Python 中创建带条件格式的 Excel 工作簿
url: /zh/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中创建带条件格式的 Excel 工作簿

如果您需要 **create Excel workbook python** 来完成报告任务，本指南将向您展示如何生成工作簿并应用条件格式规则，以突出显示昨天的日期。您将看到完整的代码、每行代码的作用以及如何将解决方案适配到其他日期范围。

条件格式是一种强大的方式，用于突出满足特定条件的数据。在本教程中，我们使用 Aspose.Cells 库（通过 .NET 的 Python 版），它提供完整的 Excel 功能支持，无需 Microsoft Office。完成本指南后，您将得到一个文件，其中范围 *I19:K20* 内的单元格在包含昨天的日期时会变为粉红色。

## 前提条件

* 已安装 Python 3.9+ 
* `aspose-cells` 包（使用 `pip install aspose-cells` 安装）
* 对 Python 语法有基本了解
* 对将保存工作簿的目录拥有写入权限

只要 .NET 运行时可用，该代码即可在 Windows、macOS 和 Linux 上运行。

## 在 Python 中创建 Excel 工作簿

第一步是实例化一个 `Workbook` 对象并获取默认工作表。该对象在内存中表示整个 Excel 文件。

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*为什么这很重要*：`Workbook()` 创建一个包含单个工作表的空工作簿。访问 `worksheets[0]` 可获得句柄，以便后续添加数据、样式和格式。

## 添加条件格式范围

接下来我们定义将由条件规则评估的区域。范围 `I19:K20` 包含两行共六个单元格。

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*为什么这很重要*：将条件格式集合添加到特定范围可将规则隔离，防止其影响无关单元格。这满足 **add conditional formatting range** 的要求。

## 定义规则：基于日期突出显示单元格

现在我们创建一种类型为 `TIME_PERIOD` 的条件。这告诉 Excel 将每个单元格的值与预定义的时间窗口进行比较。

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*为什么这很重要*：`TIME_PERIOD` 是唯一直接支持 “Yesterday”、 “Today”、 “Last Week”等的内置类型。将 `condition.time_period` 设置为 `YESTERDAY`，规则会自动将每个单元格的日期值与当前日期的前一天进行比较。

## 为满足条件的单元格设置样式

条件格式还需要视觉样式。这里我们选择粉红色实心填充，使匹配的单元格突出显示。

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*为什么这很重要*：样式对象定义了 Excel 如何渲染满足条件的单元格。使用实心粉红填充满足 **highlight cells based on date** 的要求，并使结果易于验证。

## 填充示例日期以进行评估

为了看到规则的实际效果，我们插入两个日期——一个是昨天的日期，另一个不是。`number` 格式 `30` 对应内置日期格式 `mm-dd-yy`。

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

*为什么这很重要*：提供匹配和不匹配的日期可让您验证条件格式是否正常工作。运行脚本时请将日期调整为当前月份，或使用动态值替代。

## 保存工作簿

最后我们将文件写入磁盘。`SaveFormat.XLSX` 常量确保输出为现代 Excel 文件。

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*为什么这很重要*：持久化工作簿后，您可以在 Excel、LibreOffice 或任何支持 XLSX 的查看器中打开它。打印的路径确认了文件的写入位置。

## 完整脚本

将所有部分组合在一起，完整且可运行的脚本如下：

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

### 预期输出

打开 `TimePeriodExample.xlsx` 时：

* 单元格 **I19** 因其值匹配昨天而显示粉红色背景。
* 单元格 **K20** 保持默认背景，因为其日期不在该时间段内。
* 标签 **“Yesterday”** 位于单元格 I20，以示说明。

## 常见变体和边缘情况

| 情况 | 调整 |
|-----------|------------|
| **将高亮显示改为今天而非昨天** | 将 `condition.time_period = TimePeriodType.TODAY` |
| **将规则应用于更大区域** | 将 `add("I19:K20")` 中的范围字符串更新为类似 `"A1:Z100"` 的值。 |
| **使用不同的填充颜色** | 将 `DrawingColor.pink` 替换为其他任意 `DrawingColor`（例如 `DrawingColor.light_green`）。 |
| **使用动态日期** | 计算 `datetime.now() - timedelta(days=1)` 以获取昨天的日期，并在应用规则前将该值写入单元格。 |

**技巧提示：** 当您为大量用户以编程方式生成工作簿时，请将条件格式定义与数据插入分离。这样可以在多个工作表之间复用相同的样式，而无需重复代码。

## 以编程方式验证结果（可选）

如果您想在不打开 Excel 的情况下确认格式，可以在保存后检查单元格的样式：



## 接下来您应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [Excel 自动化：使用 Aspose.Cells for .NET 创建工作簿并添加 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [使用 Aspose.Cells for Java 创建 Excel 工作簿并添加标签](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel 自动化 创建工作簿 添加 ListBox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}