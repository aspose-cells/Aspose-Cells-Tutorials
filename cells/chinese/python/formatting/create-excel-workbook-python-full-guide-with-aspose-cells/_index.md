---
category: general
date: 2026-08-01
description: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿——学习自动调整列宽、按日期格式化单元格、设置单元格日期格式以及应用条件格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- auto fit excel column
- format cells by date
- set cell date format
- aspose cells conditional formatting
language: zh
lastmod: 2026-08-01
og_description: 立即使用 Python 创建 Excel 工作簿。按照本指南自动调整 Excel 列宽、按日期格式化单元格、设置单元格日期格式，并精通
  Aspose Cells 条件格式化。
og_image_alt: Screenshot showing a Python script that creates an Excel workbook using
  Aspose.Cells
og_title: 使用 Aspose.Cells 在 Python 中创建 Excel 工作簿——一步一步教程
schemas:
- author: Aspose
  dateModified: '2026-08-01'
  description: Create Excel workbook python using Aspose.Cells – learn auto fit excel
    column, format cells by date, set cell date format and apply conditional formatting.
  headline: Create Excel Workbook Python – Full Guide with Aspose.Cells
  type: TechArticle
tags:
- Aspose Cells
- Python
- Excel automation
- Conditional Formatting
- Date handling
title: 使用 Python 创建 Excel 工作簿 – Aspose.Cells 完整指南
url: /zh/python/formatting/create-excel-workbook-python-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 完整指南创建 Excel 工作簿（Python）

是否曾想过如何编写 **create Excel workbook python** 脚本，使其在不手动打开 Excel 的情况下也能生成精美的工作簿？你并不是唯一有此需求的人。无论是构建报表仪表盘，还是自动化每日数据导出，能够从 Python 生成 Excel 文件都是改变游戏规则的关键。

在本教程中，我们将逐步演示一个完整、可直接运行的示例，它不仅可以创建工作簿，还演示了 **auto fit excel column**、**format cells by date**、**set cell date format**，以及 **aspose cells conditional formatting** 的使用。完成后，你将拥有一个可直接放入任何项目的独立脚本。

> **小贴士：** Aspose.Cells for Python via .NET 让你无需 COM 依赖即可操作 Excel 文件，特别适合 Linux 容器或 CI 流水线。

## 你需要准备的环境

- **Python 3.8+**（代码在任何近期版本均可运行）  
- **Aspose.Cells for Python via .NET** – 使用 `pip install aspose-cells` 安装  
- 一个可写入的文件夹（本文中称为 `YOUR_DIRECTORY`）  
- 对 Python 函数和对象的基本了解（不需要深入的 Excel 知识）  

如果你已经具备上述条件，太好了——让我们开始吧。

## 第一步：创建 Excel Workbook Python – 初始化工作簿

首先我们要实例化一个全新的工作簿对象。可以把它想象成一块空白画布，后续的每一步操作都会在其上绘制元素。

```python
from aspose.cells import Workbook, SaveFormat, FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color
from datetime import datetime
import os

# Create a new workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

> **为什么重要：** `Workbook()` 会在内存中创建一个 `.xlsx` 文件的表示。通过访问 `worksheets[0]`，我们得到默认工作表，准备好写入数据和格式。

## 第二步：定义目标范围和基础颜色 – 为条件格式做准备

在添加任何条件逻辑之前，需要先确定一个将承载规则的范围。这里使用 `I19:K20` 作为示例范围，足够展示多个单元格的效果。

```python
# Add a conditional formatting collection to the range and set a base colour
conds = worksheet.conditional_formattings.add("I19:K20", Color.medium_sea_green)
```

`add` 方法既创建了格式对象，又为其设置了默认背景，使后续的规则更加醒目。

## 第三步：Aspose Cells 条件格式 – 为 YESTERDAY 应用 TIME_PERIOD 规则

现在进入演示的核心：使用 **TIME_PERIOD** 条件高亮显示包含昨天日期的单元格。

```python
# Insert a TIME_PERIOD condition for YESTERDAY
condition_index = conds.add_condition(FormatConditionType.TIME_PERIOD)
condition = conds[condition_index]

# Configure the rule – yesterday, pink background, solid fill
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

> **解释：** `FormatConditionType.TIME_PERIOD` 告诉 Aspose 我们使用的是基于日期的规则。将 `time_period` 设置为 `YESTERDAY`，引擎会自动将每个单元格的值与前一天进行比较。

## 第四步：填充示例日期 – 设置单元格日期格式并验证规则

为了看到规则的实际效果，需要写入真实的日期。同时 **set cell date format** 让这些值以可读的日期形式显示。

```python
# Cell I19 – a date that falls on “yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))          # July 30, 2008 is “yesterday” for demo purposes
style_i19 = cell_i19.get_style()
style_i19.number = 30          # 30 = built‑in Excel date format (e.g., mm/dd/yyyy)
cell_i19.set_style(style_i19)

# Cell K20 – a date outside the period (no formatting applied)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)
```

注意我们对两个单元格都使用了相同的 **format cells by date** 编号（`30`），这样可以确保日期在不同系统区域设置下保持一致显示。

## 第五步：添加说明标签 – 让工作表自解释

一个简短的标签可以帮助打开文件的任何人快速了解彩色单元格的含义。

```python
worksheet.cells.get("I20").put_value("Yesterday")
```

## 第六步：Auto Fit Excel Column – 自动调整列宽

当你以编程方式生成数据时，列宽往往保持默认的窄小。**auto fit excel column** 方法会根据内容自动扩展列宽。

```python
# Auto‑fit the 12th column (which corresponds to column L) so the label is fully visible
worksheet.auto_fit_column(12)
```

> **为什么是第 12 列？** 在零基索引中，列 `12` 对应 Excel 的 `L` 列。如果你更改了布局，请相应调整索引。

## 第七步：保存工作簿 – 导出为真实文件

最后，将所有内容持久化到磁盘。`SaveFormat.XLSX` 标志确保生成的是现代的基于 ZIP 的工作簿。

```python
output_file = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_file, SaveFormat.XLSX)
print(f"Workbook saved to {output_file}")
```

### 预期结果

在 Excel（或任意查看器）中打开 `TimePeriodDemo.out.xlsx`，你应该看到：

- 单元格 **I19** 因日期为“昨天”而以 **粉红色** 高亮。  
- 单元格 **K20** 未被改变，说明条件规则正确地忽略了不在时间范围内的日期。  
- 列 **L** 已自动调整宽度，标签 “Yesterday” 不会被截断。

![Create Excel workbook python example](/images/create_excel_workbook_python.png){: .center-image alt="创建 Excel 工作簿 Python 示例，展示对昨天日期的条件格式"}

## 常见变体与边缘情况

| 情形 | 调整方法 |
|-----------|---------------|
| **不同的日期范围** | 将 `condition.time_period` 改为 `TimePeriodType.TODAY`、`TimePeriodType.LAST_7_DAYS` 等。 |
| **多个条件** | 再次调用 `conds.add_condition()` 并配置新的 `FormatConditionType`（例如 `FORMAT_CONDITION_TYPE.EXPRESSION`）。 |
| **自定义日期格式** | 使用 `style_i19.number = 14` 表示 `mm-dd-yy`，或通过 `style_i19.custom = "dd-mmm-yyyy"` 设置自定义格式字符串。 |
| **大型工作表** | 将 `auto_fit_column` 调用包装在 try/except 块中，以避免在超大文件上造成性能问题。 |
| **在无头 CI 环境运行** | 不需要 UI；Aspose 完全在内存中工作，能够在没有安装 Excel 的 Docker 容器中生成文件。 |

## 小结 – 我们覆盖了哪些内容

- 使用 Aspose.Cells 从零 **create Excel workbook python**。  
- 使用 **auto fit excel column** 保持输出整洁。  
- 使用 **format cells by date** 与 **set cell date format** 实现一致的日期显示。  
- 通过 `TIME_PERIOD` 类型应用 **aspose cells conditional formatting**。

所有内容都浓缩在一个易于运行的脚本中，你可以将其改编用于发票、每日日志或任何日期驱动的可视化场景。

## 后续步骤

如果已经掌握基础，可进一步探索：

- **数据条、颜色刻度和图标集**，实现更丰富的条件样式。  
- 通过 `worksheet.pivot_tables.add()` 生成 **PivotTable**。  
- 使用 `workbook.save("report.pdf", SaveFormat.PDF)` **导出为 PDF**。  

这些主题都基于本指南使用的相同基础概念，学习起来会非常顺畅。

---

*祝编码愉快！如果遇到问题，欢迎在下方留言，或查阅 Aspose.Cells for Python 文档获取更深入的内容。*


## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你在项目中进一步运用所学技术。每篇资源都提供完整可运行的代码示例，并配有逐步解释，帮助你掌握更多 API 功能并探索替代实现方案。

- [Auto-Fit Rows & Columns in Excel using Aspose.Cells Java for Seamless Workbook Management](/cells/english/java/range-management/aspose-cells-java-auto-fit-rows-columns/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Automate Excel Column Widths&#58; Auto-Fit Columns using Aspose.Cells for .NET](/cells/english/net/range-management/excel-automation-auto-fit-columns-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}