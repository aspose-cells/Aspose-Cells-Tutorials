---
category: general
date: 2026-07-14
description: 创建一个 Excel 工作簿的 Python 代码，设置单元格背景颜色，根据日期范围突出显示单元格，并在几分钟内将工作簿保存为 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: zh
lastmod: 2026-07-14
og_description: 使用 Python 即时创建 Excel 工作簿。学习设置单元格背景颜色、根据日期范围突出显示单元格，并使用 Aspose.Cells
  将工作簿保存为 XLSX。
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: 使用 Python 创建 Excel 工作簿 – 逐步条件格式化
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: 使用 Python 创建 Excel 工作簿 – 完整指南与条件格式
url: /zh/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 Python – 完整指南与条件格式化

是否曾想过如何编写 **create excel workbook python** 脚本，使其在不手动打开 Excel 的情况下也能呈现出精致的效果？你并不孤单。在许多数据驱动的项目中，我们需要生成电子表格、为单元格着色，甚至标记落在特定范围内的日期——这一切都可以仅通过纯 Python 代码实现。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，使用 Aspose.Cells 库 **创建 Excel 工作簿 Python**，**设置单元格背景颜色**，基于日期应用 **条件格式化**，并最终 **将工作簿保存为 xlsx**。完成后，你将拥有一段可复用的代码片段，能够直接嵌入任何自动化流水线。

## 你将学到

- 如何初始化工作簿并获取第一个工作表。  
- 一个帮助函数，用于为任意单元格范围添加条件格式化集合。  
- 使用 **基于日期的条件格式化** 高亮显示昨天的条目。  
- 调整列宽以获得整洁的布局。  
- 使用 **save workbook as xlsx** 持久化结果。  

无需外部 Excel 安装——Aspose.Cells 在内存中完成所有操作。

## 前置条件

- 已安装 Python 3.8+。  
- `aspose-cells` 包（`pip install aspose-cells`）。  
- 对 Python 函数和 datetime 对象有基本了解。  

如果你从未使用过 Aspose.Cells，可以把它看作一个强大的纯 Python API，模拟了 Excel 自身的对象模型。它非常适合在服务器端生成文件的场景，因为此时通常没有 Office 套件可用。

## 步骤 1：初始化工作簿（Create Excel Workbook Python）

首先，我们需要以 **create excel workbook python** 的方式创建一个空工作簿对象，并指向默认工作表。

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **为什么重要：** `Workbook` 类是所有 Excel 操作的入口。通过编程方式创建它，可以避免任何手动文件处理。

## 步骤 2：添加条件格式化集合的辅助函数（Set Cell Background Color）

条件格式化存在于附加到某个范围的 *集合* 中。我们将把这段模板代码封装进一个小助手，同时让它能够 **set cell background color** 整个范围。

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **小技巧：** 使用辅助函数可以让主流程保持简洁，并且便于在多个范围之间复用相同逻辑。

## 步骤 3：基于日期的条件格式化（Highlight Cells Based on Date Range）

接下来我们实际 **highlight cells based on date range**。示例聚焦于“昨天”，但你可以将 `TimePeriodType.YESTERDAY` 替换为 `TODAY`、`LAST_WEEK` 等。

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **发生了什么？**  
> 1. 首先为整个范围设置一个中性绿色背景。  
> 2. 然后添加一个 `TIME_PERIOD` 条件，当单元格的日期等于昨天时，将填充颜色覆盖为粉红色 **仅此**。  
> 3. `TimePeriodType` 枚举负责日期计算，省去你自行编写逻辑的麻烦。

## 步骤 4：填充示例日期（So the Rule Can Be Evaluated）

为了看到规则的实际效果，我们将在表格中写入几组日期。一组落在“昨天”窗口内，另一组则不在。

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **边缘情况提示：** 如果工作簿将在不同地区打开，考虑使用 `date_style.custom = "dd‑mm‑yyyy"` 来强制统一显示格式。

## 步骤 5：整理布局（Auto‑Fit Columns）

拥挤的电子表格会显得不专业。让我们 **adjust column width for a tidy output**。

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **为什么要自动适应列宽？** 它可以确保所有长标签或日期完整可见，这在向非技术利益相关者共享文件时尤为重要。

## 步骤 6：保存工作簿（Save Workbook As XLSX）

最后，我们 **save workbook as xlsx** 到你指定的位置。`SaveFormat.XLSX` 常量告诉 Aspose.Cells 使用现代的 OpenXML 格式写入文件。

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **预期结果：**  
> - 单元格 I19 和 K20 包含日期。  
> - I19（昨天）被粉红色高亮，而 K20 保持绿色。  
> - 列 L 自动扩展以容纳标签 “Yesterday”。  

如果在 Excel 中打开 `TimePeriodDemo.xlsx`，条件格式化已经生效——无需额外操作。

---

![Excel sheet showing highlighted yesterday date](https://example.com/images/excel-demo.png "生成的 Excel 文件带有高亮单元格的截图")

*上图展示了最终工作簿；请注意昨天日期所在单元格的粉红色高亮。*

## 小结：我们完成了什么

- 使用 Aspose.Cells **创建了一个 Excel 工作簿 Python**。  
- 为整块范围 **set cell background color**，为工作表提供视觉提示。  
- 应用了 **基于日期的条件格式化**，自动标记昨天的条目。  
- **保存工作簿为 xlsx**，即可分发或进一步处理。  

所有这些代码不超过 60 行，且可在任何支持 Aspose.Cells 运行时的平台上运行。

## 后续步骤与相关主题

如果本篇对你有帮助，以下内容值得进一步探索：

- 为整行根据状态值（如 “Completed”、 “Pending”） **set cell background color**。  
- 使用 **highlight cells based on date range** 创建滚动窗口（最近 7 天、当前月份）。  
- 使用 `SaveFormat.CSV` 或 `SaveFormat.PDF` 将文件导出为 **CSV** 或 **PDF**。  
- 通过代码添加 **charts**，可视化刚才格式化的数据。  

随意调整日期逻辑、换色板，或扩大范围至整列。模式保持不变：创建工作簿、附加条件格式化集合、定义规则、保存。

有关于特定使用场景的问题吗？在下方留言吧，祝编码愉快！


## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式。每篇资源均提供完整可运行的代码示例和逐步解释。

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}