---
category: general
date: 2026-09-15
description: 学习如何在 Python 中使用 Aspose.Cells 应用时间段条件格式并将工作簿保存为 XLSX。包括逐步代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: zh
lastmod: 2026-09-15
og_description: 使用 Python 在 Excel 中应用时间段条件格式并将工作簿保存为 XLSX。请参考 Aspose.Cells 的完整指南。
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: 使用 Python 在 Excel 中应用时间段条件格式
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
title: 如何使用 Python 在 Excel 中应用时间段条件格式
url: /zh/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 在 Excel 中应用时间段条件格式

如果你需要 **time period conditional formatting**（时间段条件格式），本教程将向你展示如何使用 Python 完成。你将看到一个完整、可运行的示例，它创建工作簿、突出显示昨天的日期，并 **save workbook as XLSX**（将工作簿保存为 XLSX），代码仅需几行。

条件格式是一种强大的方式，用于突出满足特定规则的数据。在本指南中我们聚焦于 “Yesterday”（昨天）时间段，但相同的模式同样适用于其他内置时间段，如 Today（今天）、LastWeek（上周）和 NextMonth（下月）。教程结束后，你将能够 **how to create excel workbook python**‑style（使用 Python 创建 Excel 工作簿）的脚本，并可直接投入生产使用。

## 前置条件

- 已安装 Python 3.8+  
- `aspose-cells` 与 `aspose-pydrawing` 包（`pip install aspose-cells aspose-pydrawing`）  
- 对 Python 语法有基本了解  

无需额外的 Office 安装，因为 Aspose.Cells 在内部处理文件生成。

## 使用 Aspose.Cells 在 Python 中实现时间段条件格式

本节逐行讲解完成主要任务所需的代码。下面的代码块即为完整脚本，注释说明了每一步的作用。

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

### 每一步的意义

1. **Creating the workbook**（创建工作簿）为你提供一个内存中的 Excel 文件，无需打开 Excel 即可操作。  
2. **Defining the range**（定义范围）(`I19:K20`) 告诉 Aspose.Cells 规则适用的单元格区域，使逻辑保持独立。  
3. **Adding a TIME_PERIOD condition**（添加 TIME_PERIOD 条件）使用 Aspose 的内置枚举 `TimePeriodType.YESTERDAY`。这避免了手动日期计算，并在文件于不同日期打开时自动更新。  
4. **Setting the style**（设置样式）(`background_color` 和 `pattern`) 决定高亮单元格的显示方式。使用 `Color.pink` 使规则易于辨认。  
5. **Writing sample dates**（写入示例日期）并将数字格式设为 30，确保 Excel 将其显示为短日期而非序列号。  
6. **Auto‑fitting the column**（自动列宽）提升后续打开文件时的可读性。  
7. **Saving as XLSX**（保存为 XLSX）生成兼容性广的文件，可在 Excel、Google Sheets 或任何现代电子表格程序中打开。

## 如何使用 Aspose.Cells 以 Python‑style 创建 Excel 工作簿

上面的脚本已经演示了 **how to create excel workbook python** 的最小步骤。实际使用中，你可能需要：

- 添加多个工作表（`workbook.worksheets.add("Report")`）。  
- 使用循环或 pandas DataFrame 填充大型数据表（`worksheet.cells.import_data_table`）。  
- 使用 `cell.get_style()` 应用额外的格式（字体、边框）等。

所有这些操作遵循相同的模式：获取对象、修改属性，然后调用 `set_style` 或 `save`。

## 添加条件格式 Python – 其他实用模式

除了 “Yesterday” 示例，Aspose.Cells 还支持多种条件格式类型：

| FormatConditionType | 典型用例 |
|---------------------|----------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | 自定义公式（`=A1>100`） |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | 简单比较（`>`、`<`、`=`） |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | 渐变颜色刻度 |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | 单元格内条形图可视化 |

要 **add conditional formatting python**（添加 Python 条件格式）以实现数值阈值，你需要将 `FormatConditionType.TIME_PERIOD` 替换为 `FormatConditionType.CELL_VALUE`，并设置 `condition.operator_type` 与 `condition.formula1`。

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## 将工作簿保存为 XLSX – 最佳实践

当你 **save workbook as xlsx** 时，请考虑：

- **指定正确的 `SaveFormat`**（`SaveFormat.XLSX`），以避免使用旧版格式。  
- **使用确定性的文件名**，如果脚本在循环中运行（`f"report_{datetime.now():%Y%m%d}.xlsx"`）。  
- **关闭资源**（`workbook.dispose()`），在长时间运行的服务中释放本地内存。

示例已经使用 `SaveFormat.XLSX`，生成基于 ZIP 的现代工作簿，保留所有条件格式规则。

## 在 Excel 中突出显示昨天 – 验证步骤

运行脚本后，打开 `TimePeriodExample.xlsx`：

1. 单元格 `I19` 与 `K20` 包含日期 `30‑07‑2008` 和 `03‑08‑2008`。  
2. 单元格 `I20` 显示文本 “Yesterday”。  
3. 若将系统日期改为 **2008 年 7 月 30 日** 并重新打开文件，匹配的日期单元格会自动填充为粉红色。  
4. 将系统日期改为其他任意日期，粉红填充会消失，验证了 **time period conditional formatting**（时间段条件格式）逻辑的响应。

## 常见陷阱及规避方法

- **缺少 `aspose-pydrawing`** – `Color` 类位于该包中，未安装会抛出 `ImportError`。  
- **数字格式不正确** – 使用默认的 General 格式会显示序列号（如 39822），务必设置 `style.number = 30` 以显示短日期。  
- **范围不匹配** – 条件格式的范围必须包含你希望高亮的单元格，否则规则无效。

## 专业技巧：复用格式化例程

如果需要在多个工作簿中使用相同的 “Yesterday” 规则，可将逻辑封装为辅助函数：

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

在需要的地方调用 `apply_yesterday_highlight(worksheet, "A1:A10")`。

## 结论

本指南展示了如何使用 Python 在 Excel 中实现 **time period conditional formatting**（时间段条件格式），如何 **save workbook as XLSX**（将工作簿保存为 XLSX），以及如何使用单一可复用脚本 **highlight yesterday in Excel**（在 Excel 中突出显示昨天）。现在，你已经具备了将 **add conditional formatting python**（添加 Python 条件格式）代码集成到任何自动化项目中的坚实基础，无论是生成每日报告、构建仪表盘，还是准备数据导出。

**后续步骤**

- 探索其他 `TimePeriodType` 值，如 `TODAY` 或 `LAST_WEEK`。  
- 在同一范围内组合多个条件规则，以获得更丰富的视觉提示。  
- 将工作簿生成集成到 Web 服务或计划任务中。

祝编码愉快，享受条件格式为 Excel 自动化带来的清晰可视化效果！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式。每个资源均提供完整可运行的代码示例和逐步解释。

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}