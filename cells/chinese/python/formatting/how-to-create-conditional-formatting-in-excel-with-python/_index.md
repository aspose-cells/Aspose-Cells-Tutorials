---
category: general
date: 2026-11-16
description: 使用 Python 在 Excel 中创建条件格式。学习添加条件格式范围、突出显示日期，并以编程方式构建工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: zh
lastmod: 2026-11-16
og_description: 使用 Python 在 Excel 中创建条件格式。本教程展示如何添加条件格式范围、突出显示日期以及生成工作簿。
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: 使用 Python 在 Excel 中创建条件格式——一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: 如何使用Python在Excel中创建条件格式
url: /zh/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Python 在 Excel 中创建条件格式

如果您需要在使用 Python 时 **创建条件格式** 于 Excel 文件，本指南将准确展示如何操作。您将学习 **create excel workbook python** 风格地创建工作簿，定义格式范围，并在不离开 IDE 的情况下突出显示日期。

条件格式可以让您直观地标记满足特定条件的单元格——非常适用于仪表盘、报告或数据验证表格。完成本教程后，您将拥有一个功能完整的工作簿，其中标记为“Yesterday”的日期单元格会显示为粉红色，而其余范围保持绿色。

## 您将完成的工作

* 从头创建一个新的工作簿。  
* 为特定单元格块添加条件格式集合。  
* 应用一个 **TIME_PERIOD** 规则来突出显示日期（“如何突出显示日期”场景）。  
* 将文件保存为 XLSX 工作簿，以便后续处理。

**先决条件**  
* Python 3.8+  
* `aspose-cells` Python package (`pip install aspose-cells`)  
* 对 Python 的 `datetime` 模块有基本了解  

---

## 如何在 Python 中创建条件格式

第一步是设置工作簿和将承载格式规则的工作表。

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**为什么这很重要** – `Workbook` 是所有 Excel 操作的入口点。以编程方式创建工作簿取代了手动的 “File → New” 步骤，从而实现自动化报告流水线。

---

## 准备条件格式集合 – 添加条件格式范围

接下来我们定义将接受规则的单元格块。在本例中范围为 **I19:K20**。

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**说明** – `conditional_formattings.add` 注册一个与地址字符串关联的新集合。第一个条件 (`conds[0]`) 充当“默认”样式；后续规则在满足其条件时会覆盖它。

---

## 添加 TIME_PERIOD 条件 – 如何突出显示日期

现在我们添加实际逻辑，以识别“Yesterday”日期并将其涂成粉红色。

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**为什么使用 TIME_PERIOD?** – Aspose.Cells 提供了内置枚举，如 `YESTERDAY`、`TODAY` 和 `LAST_WEEK`。它们将单元格的日期值与当前系统日期进行比较，省去了自定义公式的需求。

---

## 填充示例数据 – 演示规则

为了看到格式的实际效果，我们插入一个符合规则的日期和一个不符合的日期。

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**边缘情况说明** – `TIME_PERIOD` 规则仅适用于 *真实* 日期。如果单元格包含文本（例如 “N/A”），该规则将被忽略，从而防止意外的颜色变化。

---

## 保存工作簿 – 添加条件格式 python

最后，将工作簿写入磁盘。该文件可以在任何电子表格程序中打开，以验证颜色效果。

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**预期结果**  

| I19（绿色 → 粉红） | J19（绿色） | K19（绿色） |
|--------------------|------------|------------|
| 7/30/2008（昨天） | – | – |
| **I20**： “Yesterday” 标签 | – | – |
| I21‑K21（绿色）    | – | – |

单元格 **I19** 因其日期匹配 “Yesterday” 时段而显示粉红背景，而 **K20** 则保持绿色。

---

## 常见问题与实用技巧

* **我可以使用自定义日期范围而不是内置时段吗？**  
  可以。将 `condition.time_period` 替换为 `condition.formula1 = "TODAY()-1"` 并将 `condition.type = FormatConditionType.FORMULA`。

* **如果我的工作簿已经包含数据怎么办？**  
  在添加条件格式集合之前，使用 `worksheet.cells.import_data` 批量加载数据。

* **大表格的性能如何？**  
  添加大量条件会减慢渲染速度。将使用相同规则的单元格合并为单一范围（例如 “A1:C1000”），以保持条件数量低。

* **跨平台兼容性如何？**  
  生成的 XLSX 文件遵循 Office Open XML 标准，可在 Windows、macOS 和 Linux 的电子表格应用程序中使用。

---

## 结论

现在您已经了解如何使用 Python 在 Excel 工作簿中 **创建条件格式**。本教程涵盖了创建工作簿、定义 **add conditional formatting range**、应用 **how to highlight dates** 规则以及保存文件——全部采用 Aspose.Cells 提供的 **add conditional formatting python** 方法。

从这里您可以：

* 使用其他 `TimePeriodType` 值（例如 `TODAY`、`LAST_MONTH`）扩展规则集。  
* 在同一范围内组合多个条件，以获得更丰富的视觉提示。  
* 将此工作流集成到自动化报告流水线或 Web 服务中。

祝编码愉快，欢迎尝试不同的颜色、范围和日期逻辑，以满足您的报告需求！

## 接下来您应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方法。

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}