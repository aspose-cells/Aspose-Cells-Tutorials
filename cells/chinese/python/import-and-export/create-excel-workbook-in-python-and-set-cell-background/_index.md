---
category: general
date: 2026-10-07
description: 在 Python 中创建 Excel 工作簿，设置单元格背景颜色，自动调整列宽，并使用简洁的代码示例填充日期。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: zh
lastmod: 2026-10-07
og_description: 在 Python 中创建 Excel 工作簿，然后设置单元格背景颜色、自动调整列宽，并在 Excel 中填充日期。按照本分步指南生成
  TimePeriodDemo.xlsx 文件。
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: 在 Python 中创建 Excel 工作簿 – 设置背景并自动调整列宽
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: 在 Python 中创建 Excel 工作簿并设置单元格背景
url: /zh/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Python 中创建 Excel 工作簿并设置单元格背景

在 Python 中创建 Excel 工作簿，并仅用几行代码即可应用条件格式。本教程向您展示 **如何以编程方式创建 Excel** 文件、设置单元格背景颜色、自动调整 Excel 列宽，以及使用 Aspose.Cells 库在 Excel 中填充日期。

您将学习如何：
* 初始化工作簿并获取第一个工作表。  
* 定义一个条件格式，以突出显示 “昨天” 的日期。  
* 将示例日期插入特定单元格。  
* 自动调整列宽，使数据清晰可见。  
* 将工作簿保存到指定文件夹。

唯一的前提是已安装 `aspose-cells` 和 `aspose-pydrawing` 包的可用 Python 3 环境：

```bash
pip install aspose-cells aspose-pydrawing
```

---

## 在 Python 中创建 Excel 工作簿 – 步骤详解

以下章节将整个过程拆分为可管理的步骤。每一步都包含所需代码、**为什么**重要的解释，以及避免常见陷阱的提示。

### 步骤 1：导入所需命名空间并定义辅助函数

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*为什么重要*：导入正确的类后，您才能使用工作簿创建、条件格式和颜色处理功能。  
**专业提示**：将导入语句放在文件顶部；这使脚本更易阅读，并防止循环导入错误。

### 步骤 2：创建工作簿并获取第一个工作表

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

`Workbook()` 构造函数在内存中创建一个空的 Excel 工作簿。  
**原因**：从全新的工作簿开始，可确保没有上一次运行遗留下的格式。

### 步骤 3：使用条件格式设置单元格背景颜色

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*原因*：使用 **时间段** 条件可自动突出显示包含昨天日期的任何单元格，免去手动日期检查。  
**提示**：`Color.pink` 仅为示例，您可以使用任何 `Color` 对象（如 `Color.yellow`、`Color.light_green` 等）。

### 步骤 4：在 Excel 中填充日期

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

这里我们在单元格 `I19` 和 `K20` 中 **填充日期**。第一个日期会触发条件格式，第二个则不会。  
**为什么重要**：展示匹配和值不匹配的情况，可帮助您验证规则是否按预期工作。

### 步骤 5：自动调整 Excel 列宽以获得更好可视性

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` 根据最长单元格内容自动调整列宽。  
**提示**：在写入所有数据后再调用此方法；否则宽度可能基于不完整的内容计算。

### 步骤 6：保存工作簿

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

保存文件会将内存中的工作簿写入磁盘，采用现代的 XLSX 格式。

### 完整脚本 – 综合示例

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**预期输出**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

在 Excel 中打开生成的文件 – 单元格 `I19:K20` 将对“昨天”日期显示粉红色背景，列 L 的宽度足以完整显示标签而不被截断。

---

## 为什么这种方法是最佳实践

* **单次遍历工作流** – 所有操作均在同一个 `Workbook` 实例上完成，避免不必要的 I/O。  
* **条件格式** – 使用 `FormatConditionType.TIME_PERIOD` 让 Excel 处理日期逻辑，比自行编写 Python 日期检查更可靠。  
* **显式样式** – 设置 `background_color` 和 `pattern` 可确保在不同 Excel 版本中呈现一致的视觉效果。  
* **数据写入后再自动调整列宽** – 确保列宽基于完整内容计算。

## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您在已有技术基础上进一步深入。每个资源都提供完整的可运行代码示例，并配有逐步解释，助您掌握更多 API 功能并在项目中探索替代实现方式。

- [Create Excel Workbook Python – Full Guide](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Create Excel Workbook Python – Complete Step‑by‑Step Guide](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Create Excel Workbook Python – Complete Guide with Lambda](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}