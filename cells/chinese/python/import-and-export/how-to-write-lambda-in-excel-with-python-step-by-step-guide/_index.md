---
category: general
date: 2026-06-21
description: 学习如何使用 Python 在 Excel 中编写 lambda。本教程还涵盖了使用 Python 创建 Excel 工作簿以及如何使用
  Aspose.Cells 读取单元格。
draft: false
keywords:
- how to write lambda
- create excel workbook python
- how to read cells
- how to use byrow
- use lambda function excel
language: zh
og_description: 如何使用 Python 在 Excel 中编写 lambda 的详细说明。按照我们的清晰步骤创建 Excel 工作簿、应用 BYROW
  并读取单元格结果。
og_title: 如何使用 Python 在 Excel 中编写 Lambda – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to write lambda in Excel using Python. This tutorial also
    covers create excel workbook python and how to read cells with Aspose.Cells.
  headline: How to Write Lambda in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: BYROW works on any rectangular range. If you have gaps, just reference
      a larger range and let the lambda ignore blanks (`AVERAGEIF(r, "<>")`).
    question: What if my data isn’t contiguous?
  - answer: Yes. The first argument is always the row (or column for `BYCOL`). Additional
      arguments can be supplied after the range, like `BYROW(A1:C5, LAMBDA(r, factor,
      AVERAGE(r)*factor), 2)`.
    question: Can I pass more than one argument to the lambda?
  - answer: BYROW and LAMBDA are available starting with Excel 365 (dynamic arrays).
      If you need legacy support, you’d have to emulate the logic with VBA or multiple
      helper columns.
    question: Is this compatible with older Excel versions?
  - answer: Not for this demo, but you can call `workbook.save("output.xlsx")` if
      you want a physical file.
    question: Do I need to save the workbook to disk?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
- Lambda
- BYROW
title: 如何在 Excel 中使用 Python 编写 Lambda – 步骤指南
url: /zh/python/import-and-export/how-to-write-lambda-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Python 编写 Lambda – 步骤指南

有没有想过在使用 Python 自动化电子表格时，**如何编写 lambda** 作为 Excel 公式的一部分？你并不孤单。许多开发者在尝试将 Excel 新的动态数组函数与 Python 工作流结合时会遇到障碍。在本教程中，我们将演示一个完整、可运行的示例，准确展示这一过程——并顺带涉及 **create excel workbook python**、**how to read cells** 以及实用的 **how to use byrow** 模式。

阅读完本指南后，你将拥有一个全新的工作簿、一个利用 lambda 的 BYROW 公式，以及一种将结果拉回 Python 脚本的简便方法。无需额外的 Excel 插件，只需 Aspose.Cells for Python 和少量代码即可。

## 前置条件

在开始之前，请确保你已经：

- 安装了 Python 3.8 或更高版本。
- 安装了 `aspose-cells` 包（`pip install aspose-cells`）。
- 对 Python 列表和函数有基本了解。
- （可选）使用你熟悉的 IDE 或文本编辑器。

就这些。如果其中有不熟悉的，请先暂停并安装相应的包；其余步骤在任何支持 Python 的平台上均可运行。

## Create Excel Workbook Python

我们首先需要一个全新的工作簿对象。Aspose.Cells 为我们提供了 `Workbook` 类，用于在内存中表示整个 Excel 文件。

```python
import aspose.cells as cells

# Step 1: Instantiate a new workbook and grab the first worksheet
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]
```

为什么要从空工作簿开始？因为这能保证环境确定性——没有隐藏公式，没有杂乱的格式，只有一块空白画布。这是任何 **create excel workbook python** 教程的基础。

## 向工作表填充数据

接下来，我们在 **A1** 单元格开始填充一个 5 × 3 的数值表格。数据 deliberately 简单，便于清晰看到计算过程。

```python
# Step 2: Define a 5x3 table and write it to A1
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]

worksheet.cells["A1"].put_value(table_data)
```

请注意我们使用 `put_value` 并传入嵌套的 Python 列表；Aspose.Cells 会自动为我们映射行列。如果你需要从 CSV 或数据库导入数据，只需将 `table_data` 替换为相应的数据源——其他代码保持不变。

## 在 BYROW 公式中编写 Lambda（Python）

现在进入关键部分：**如何编写 lambda** 让 Excel 引擎进行求值。Excel 的 `BYROW` 函数会遍历指定范围的每一行，并将该行传递给你提供的 `LAMBDA`。在本例中，我们希望计算每行的平均值。

```python
# Step 3: Insert a BYROW formula that uses a lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"
```

逐项解释如下：

- `BYROW(A1:C5, …)` 告诉 Excel 检查范围 A1:C5 中的每一行。
- `LAMBDA(r, AVERAGE(r))` 定义了一个匿名函数（`r` 为行数组），返回该行的平均值。
- 结果会自动溢出到 D1:D5，因为 BYROW 返回的是一个数组。

这行代码就是 **如何编写 lambda** 用于按行计算的答案。你可以将 `AVERAGE` 替换为 `SUM`、`MAX` 或其他聚合函数——只需修改 lambda 的主体即可。

## 强制计算公式

Aspose.Cells 在设置公式时不会自动求值，因此我们必须显式触发重新计算。

```python
# Step 4: Force the workbook to evaluate all formulas
workbook.calculate_formula()
```

如果跳过此步骤，D 列的单元格仍只会显示公式文本，而不是计算后的数值。这是很多人在 **how to use byrow** 时忘记触发计算的常见陷阱。

## 计算后读取单元格

最后，让我们把结果拉回 Python。这展示了 **how to read cells** 的通用做法，适用于任何公式输出。

```python
# Step 5: Retrieve the average values from D1:D5
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print(row_averages)  # Expected output: [20.0, 15.0, 12.0, 0.0, 200.0]
```

一个简短的列表推导遍历五行，获取每个单元格的 `.value`，并存入 `row_averages`。打印出的列表验证了我们的 lambda 正常工作。

### 小技巧
如果需要一次读取大量结果，可使用 `worksheet.cells.get_range("D1:D5").value` 一次性获取整个数组——对大表格而言速度更快。

## 使用 Lambda 函数在 Excel 中计算行平均值（完整脚本）

将所有内容整合在一起，下面是完整的可直接运行的脚本：

```python
import aspose.cells as cells

# Create a new workbook
workbook = cells.Workbook()
worksheet = workbook.worksheets[0]

# Populate the table
table_data = [
    [10, 20, 30],
    [5,  15, 25],
    [8,  12, 16],
    [0,  0,  0],
    [100, 200, 300]
]
worksheet.cells["A1"].put_value(table_data)

# Write BYROW with lambda to calculate row averages
worksheet.cells["D1"].formula = "=BYROW(A1:C5, LAMBDA(r, AVERAGE(r)))"

# Recalculate so the formula resolves
workbook.calculate_formula()

# Read the results back into Python
row_averages = [worksheet.cells[f"D{i}"].value for i in range(1, 6)]
print("Row averages:", row_averages)
```

运行该脚本后会输出：

```
Row averages: [20.0, 15.0, 12.0, 0.0, 200.0]
```

这就是完整的工作流：**create excel workbook python**、填充数据、**how to use byrow**、**how to write lambda**，以及最后的 **how to read cells**。

## 边缘情况与常见问题

- **如果我的数据不是连续的怎么办？**  
  BYROW 适用于任意矩形范围。如果存在空白，只需引用更大的范围，并让 lambda 忽略空值（`AVERAGEIF(r, "<>")`）。

- **可以向 lambda 传递多个参数吗？**  
  可以。第一个参数始终是行（或 `BYCOL` 时的列）。额外参数可以在范围后面提供，例如 `BYROW(A1:C5, LAMBDA(r, factor, AVERAGE(r)*factor), 2)`。

- **这在旧版 Excel 中可用吗？**  
  BYROW 和 LAMBDA 从 Excel 365（动态数组）开始支持。如果需要兼容旧版，必须使用 VBA 或多个辅助列来模拟相同逻辑。

- **需要将工作簿保存到磁盘吗？**  
  本示例不需要，但如果想生成实体文件，可调用 `workbook.save("output.xlsx")`。

## 结论

我们已经演示了 **如何在 Excel BYROW 公式中使用 Python 编写 lambda**，完整展示了 **create excel workbook python** 的工作流，并说明了 **how to read cells** 的最简方法。借助 Aspose.Cells，你可以避免任何 COM 互操作的麻烦，同样的模式可以轻松扩展到数千行，只需极少的代码改动。

准备好迎接下一个挑战了吗？尝试将 `AVERAGE` 换成 `MEDIAN`，在 lambda 中加入条件逻辑，或自动生成完整的报告文档。Python 与 Excel 现代函数的组合，为数据驱动的自动化打开了无限可能。

有问题或想分享自己的 lambda 技巧？在下方留言吧，祝编码愉快！  

![how to write lambda in Excel using Python](image.png){alt="在 Excel 中使用 Python 编写 Lambda 的方法"}

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中实现的替代方案，每篇均提供完整可运行的代码示例和逐步解释。

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Load an Excel Workbook Without Defined Names Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/load-excel-workbook-without-defined-names-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}