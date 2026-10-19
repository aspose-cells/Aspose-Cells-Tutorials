---
category: general
date: 2026-10-04
description: 使用 Aspose.Cells 用 Python 创建 Excel 工作簿。学习 Excel 条件格式化（Python）、单元格背景颜色（Python）以及在完整示例中使用
  Python 格式化单元格日期。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: zh
lastmod: 2026-10-04
og_description: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿。本教程逐步展示 Excel 条件格式化（Python）、单元格背景颜色（Python）以及日期格式化（Python）。
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: 使用 Python 创建 Excel 工作簿 – 完整指南与条件格式
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: 使用 Python 创建 Excel 工作簿并添加条件格式和单元格背景颜色
url: /zh/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建 Excel 工作簿并添加条件格式及单元格背景颜色

如果你需要 **create Excel workbook python**，本指南将一步步演示完整可运行的示例，展示如何添加 **excel conditional formatting python**、更改 **cell background color python**，以及为 “Yesterday” 高亮设置 **format cells date python**。

在许多报表场景中，彩色单元格的视觉提示能让数据一目了然。本教程将逐行讲解代码，说明每一步的意义，并提供一个可直接运行的脚本，方便你在自己的项目中进行改造。

## 你将实现的目标

阅读完本文后，你将能够：

1. 使用 Aspose.Cells 库 **create Excel workbook python**。  
2. 应用 **excel conditional formatting python**，自动高亮显示日期为 “Yesterday” 的单元格。  
3. 将 **cell background color python** 设置为粉色（或任意你喜欢的颜色）。  
4. 使用 **format cells date python** 让日期以标准 Excel 日期样式显示。  

无需事先了解 Aspose.Cells——只要有可用的 Python 3 环境并能使用 pip 即可。

## 前置条件

- 已安装 Python 3.8 或更高版本。  
- 通过 `pip install aspose-cells aspose-pydrawing` 安装 `aspose-cells` 与 `aspose-pydrawing` 包。  
- 对 Python 语法和 Excel 基础概念（工作簿、工作表、单元格）有基本了解。  

> **小贴士：** 在虚拟环境中运行脚本可避免与其他项目的版本冲突。

## 步骤 1：设置项目并导入所需类

在 **create Excel workbook python** 时，首先需要导入 Aspose.Cells 中用到的类。这些类让你直接操作工作簿创建、条件格式和样式。

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*为什么重要：* 只导入必要的符号可以保持命名空间整洁，使脚本更易阅读。`Workbook` 是 **create Excel workbook python** 的入口，而 `FormatConditionType` 与 `TimePeriodType` 则是实现 **excel conditional formatting python** 的关键。

## 步骤 2：创建新工作簿并获取第一个工作表

现在我们真正 **create Excel workbook python**。`Workbook()` 构造函数会生成一个空的 Excel 文件，默认包含一个工作表。

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*说明：* 每个 Excel 文件至少有一个工作表。默认情况下 Aspose.Cells 将其命名为 “Sheet1”。后续可以添加更多工作表，但本示例只使用单个工作表，以保持焦点明确。

## 步骤 3：定义条件格式的目标范围

条件格式作用于矩形区域。这里我们选择范围 `I19:K20`，即三列两行的区域。

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*为什么这样做：* `get` 方法返回与指定范围关联的 `ConditionalFormatting` 对象。如果该范围尚未有任何格式，Aspose.Cells 会自动创建一个新集合。

## 步骤 4：添加 TIME_PERIOD 条件并设置背景颜色

这一步是 **excel conditional formatting python** 的核心。我们添加一个 `TIME_PERIOD` 规则，使包含 “Yesterday” 日期的单元格高亮。

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*深入解析：*  
- `FormatConditionType.TIME_PERIOD` 告诉 Excel 按相对日期进行评估。  
- `TimePeriodType.YESTERDAY` 是内置枚举，会每日自动更新，因此工作簿始终高亮最近的 “Yesterday”。  
- 将 `background_color` 设为 `Color.pink` 并将图案设为 `SOLID`，即可实现 **cell background color python** 效果，无需额外 VBA 代码。

## 步骤 5：向范围填充示例日期并应用日期格式

为了看到条件格式的效果，需要实际的日期值。同时要 **format cells date python**，让 Excel 将其识别为日期而非普通数字。

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*说明：*  
- `style.number = 30` 行即为 **format cells date python** 步骤。代码 30 对应短日期格式 (`m/d/yy`)。  
- 使用辅助函数可以保持代码 DRY（Don’t Repeat Yourself），并便于以后添加更多日期。

## 步骤 6：添加说明标签

一个简短的标签可以帮助打开工作簿的用户理解为何单元格被着色。

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## 步骤 7：将工作簿保存到磁盘

最后，通过调用 `save` 将 **create Excel workbook python** 写入磁盘。`SaveFormat.XLSX` 常量确保文件采用现代的 Office Open XML 格式。

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

打开 `TimePeriodDemo.xlsx` 时，你会看到：

- 单元格 `I19` 和 `K20` 包含日期。  
- 与 “Yesterday” 匹配的单元格（在本静态示例中为 `I19`）被粉色高亮。  
- 标签 “Yesterday” 出现在 `I20`。  

> **提示：** 若在其他日期运行脚本，条件格式仍会高亮当前系统日期前一天的单元格——无需修改代码。

## 完整脚本 – 直接复制运行

下面是完整的、可独立运行的程序，包含上述所有步骤。复制到名为 `conditional_format_demo.py` 的文件中，修改 `YOUR_DIRECTORY`，然后使用 `python conditional_format_demo.py` 执行。

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### 预期输出

运行脚本后会打印确认信息：

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

打开生成的文件后，可看到符合 “Yesterday” 规则的单元格背景为粉色，证明 **excel conditional formatting python** 与 **cell background color python** 已成功协同工作。

## 常见变体与边缘情况

| 情况 | 如何调整代码 |
|-----------|-----------------------|
| **更换高亮颜色** | 将 `Color.pink` 改为其他 `Color` 常量，例如 `Color.light_green`。 |
| **将 “Yesterday” 改为 “Today”** | 将 `condition.time_period = TimePeriodType.TODAY`。 |
| **对整列应用格式** | 使用类似 `"A:A"` 的范围，并相应修改 `target_range` 变量。 |
| **使用自定义日期格式** | 将 `style.number = 30` 替换为 `style.custom = "dd-mmm-yyyy"`，以获得更易读的格式。 |
| **在同一范围内添加多个条件** | 继续调用 `target_range.add`，为同一 `ConditionalFormatting` 对象添加其他 `FormatCondition`。 |

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索在项目中的不同实现方式：

- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}