---
category: general
date: 2026-08-08
description: 使用 Python 创建 Excel 工作簿并根据日期添加条件格式。使用 Aspose.Cells 的逐步指南，突出显示昨天的单元格。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: zh
lastmod: 2026-08-08
og_description: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿，并根据日期应用条件格式，以实现动态电子表格。
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: 使用 Python 创建 Excel 工作簿 – 日期条件格式化
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
title: 使用Python创建Excel工作簿的日期条件格式
url: /zh/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建 Excel 工作簿的日期条件格式化

如果您需要 **create Excel workbook Python** 并自动突出显示匹配特定日期的单元格，本教程将准确展示操作方法。您将学习如何使用 **conditional formatting based on date**，使昨天的日期以粉红色显示，使用 Aspose.Cells 库。

本指南逐步演示每一步——从安装 SDK 到保存最终的 .xlsx 文件——您可以将可运行的示例直接复制粘贴到自己的项目中。无需外部文档；所有代码和说明都是自包含的。

## 前置条件

* 已安装 Python 3.8 或更高版本。
* `aspose-cells` 包（Aspose.Cells 的 Python 包装器）。使用以下方式安装：
  ```bash
  pip install aspose-cells
  ```
* 对 Python 和 Excel 概念（如工作表和单元格样式）有基本了解。

> **Pro tip:** Aspose.Cells 在未安装 Microsoft Excel 的情况下也能工作，非常适合服务器端自动化。

## 步骤 1：在 Python 中创建 Excel 工作簿

第一步是实例化一个新工作簿并获取默认工作表。该对象代表整个 Excel 文件，并提供对行、列和格式化 API 的访问。

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

创建工作簿是后续所有操作的基础，无论是添加数据、公式还是格式化规则。

## 步骤 2：定义基于日期的条件格式

现在我们添加 **conditional formatting based on date**。`FormatConditionType.TIME_PERIOD` 枚举允许我们指定内置的时间段，如 Yesterday、Today 或 LastWeek。

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

此步骤的重要性在于：Excel 会对范围内的每个单元格评估条件。当单元格的值落在定义的时间段（昨天）内时，我们分配的样式会自动应用。

## 步骤 3：使用示例日期填充范围

为了看到规则的实际效果，我们将几个 `datetime` 对象写入目标单元格。其中一个特意设置为相对于工作簿内部日期系统的昨天日期。

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

`number = 30` 行告诉 Excel 使用其标准的短日期格式显示值。如果您希望不同的显示方式，可以将此索引更改为任何内置的数字格式。

## 步骤 4：调整列宽以提升可读性

对包含日期的列进行自动适应宽度，可使输出更易阅读，尤其是在 Excel 或查看器中打开工作簿时。

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## 步骤 5：将工作簿保存到磁盘

最后，将工作簿保存为 .xlsx 文件。将 `"YOUR_DIRECTORY"` 替换为您机器上的实际路径。

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

当您在 Excel 中打开 `TimePeriodDemo.out.xlsx` 时，单元格 **I19** 将因其值匹配 “Yesterday” 规则而显示粉红色背景，而 **K20** 则保持不变。

### 预期输出

| I19（日期） | I20（标签） | J19 | J20 | K19 | K20（日期） |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30*（粉红色背景） | 昨天 | – | – | – | *2008‑08‑03*（无格式） |

粉红色的阴影确认 **conditional formatting based on date** 按预期工作。

## 常见变体和边缘情况

| 情况 | 如何调整代码 |
|-----------|-----------------------|
| **将 “Today” 替代 “Yesterday” 进行高亮** | Change `condition.time_period = TimePeriodType.TODAY` |
| **将规则应用于整列** | Use `worksheet.get_range("A:A").format_conditions` |
| **使用自定义日期范围（例如最近 7 天）** | Replace the time‑period condition with a formula condition: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **不同的背景颜色** | Set `condition.style.background_color = Color.light_green` (or any `Color` you prefer) |
| **在没有显示器的 Linux 上运行** | Aspose.Cells is fully headless; no extra configuration required. |

## 完整、可运行的示例

下面是完整的脚本，您可以直接执行（在更新输出目录后）。其中包含所有导入、注释和错误处理的基础内容。

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

运行脚本会生成一个 Excel 文件，其中 “Yesterday” 单元格会自动高亮，演示了 **create Excel workbook Python** 与 **conditional formatting based on date** 的结合。

## 结论

您现在已经了解如何 **create Excel workbook Python** 对象，定义 **date‑based conditional formatting

## 接下来应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和一步步的解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方法。

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}