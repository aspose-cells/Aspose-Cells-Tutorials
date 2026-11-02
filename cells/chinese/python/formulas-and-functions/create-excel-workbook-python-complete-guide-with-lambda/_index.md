---
category: general
date: 2026-06-08
description: 创建一个 Excel 工作簿的 Python 示例，展示如何在 Excel 中使用 lambda，使用 BYROW 求行和，并在几步内实现自动计算。
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: zh
og_description: 使用 Python 创建 Excel 工作簿，并学习在 Excel 中使用 lambda 通过 BYROW 公式高效求和行。
og_title: 使用 Python 创建 Excel 工作簿 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: 使用 Python 创建 Excel 工作簿 – 完整指南（含 Lambda）
url: /zh/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 创建 Excel 工作簿 – 完整指南与 Lambda

有没有想过如何 **create Excel workbook Python** 脚本来自动化枯燥的数字运算？你并不孤单——许多开发者在需要生成工作表、插入公式并将结果拉回代码时都会卡住。  

在本教程中，我们还将展示 **how to use lambda** 在 Excel 中的用法，解释使用现代 `BYROW` 函数的 **how to sum rows** 方法，并为您提供一个整洁的端到端示例，您可以直接复制粘贴并立即运行。

## 您将学习

- 从 Python 设置一个全新的工作簿，而无需手动打开 Excel。  
- 用 3 × 3 的数字矩阵填充一个范围。  
- 插入利用 **use lambda excel** 语法的 `BYROW` 公式，以对每行求和。  
- 重新计算工作表使公式求值，然后将结果读取回 Python。  

在本指南结束时，您将拥有一个独立的脚本，可用于发票、计分卡或任何需要即时 **sum rows** 的场景。

### 前置条件

- Python 3.8+ 已安装。  
- `openpyxl` 库（如果你更喜欢基于 COM 的方式，也可以使用 `xlwings`）。我们使用 `openpyxl` 因为它纯 Python，且跨平台。  
- 支持 `BYROW` 函数和 Lambda 公式的最新 Microsoft Excel（365 或 2021）。

使用以下命令安装库：

```bash
pip install openpyxl
```

> **专业提示：** 如果在 Windows 上遇到权限问题，请使用 `python -m pip install --user openpyxl`。

---

## 使用 Python 创建 Excel 工作簿 – 初始化工作簿

我们首先需要一个完全在内存中的全新工作簿对象。使用 `openpyxl`，只需一行代码即可实现：

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

为什么使用 `wb.active` 而不是索引 `Worksheets[0]`？`openpyxl` 直接公开活动工作表，这样更清晰且避免额外的列表查找。如果需要处理多个工作表，随时可以使用 `wb.create_sheet(title="MySheet")` 添加。

---

## 用数据填充工作表 – 简单的 3×3 矩阵

接下来，我们用一个小矩阵填充工作表。这对应经典的“对每行求和”示例，并保持代码简洁。

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

你可能会想，为什么不使用 `ws.append()` 或 `ws.values` 而手动循环。显式循环让我们完全控制起始单元格，并且以后可以轻松调整偏移量——在需要保留标题行或列为空时非常方便。

---

## 在 Excel 公式中如何使用 Lambda

Excel 的 **use lambda excel** 功能允许你直接在单元格中编写匿名函数。可以把它看作是位于电子表格引擎内部的 Python `lambda`。语法如下：

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

当与 `BYROW` 结合使用时，你可以将该 lambda 应用于范围的每一行，生成一列结果。这就是我们 **how to sum rows** 技巧的核心。

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

底层发生了什么？

- `A1:C3` 是源范围（我们的矩阵）。  
- `LAMBDA(r, SUM(r))` 定义了一个临时函数，接收单行 (`r`) 并返回其求和结果。  
- `BYROW` 对 **每行** 运行该 lambda，并将结果溢出到 D 列，从 `D1` 开始。  

由于 `BYROW` 是一个 *动态数组* 函数，Excel 会自动在 `D1:D3` 中填入这三个求和结果。

> **注意：** `BYROW` 和 Lambda 公式仅在 Excel 365/2021 及更高版本可用。如果使用旧版本，需要回退到传统的 `SUM` 公式或 VBA。

---

## 使用 BYROW 和 Lambda 对行求和

现在公式已经写入工作表，我们必须让 Excel 对其求值。`openpyxl` 本身不计算公式，只负责读取/写入。要触发计算，可以：

1. 保存工作簿并在 Excel 中打开（手动）。  
2. 使用 `xlwings` COM 引擎强制重新计算（需要安装 Excel）。  

对于纯 Python 方案，我们仅在计算步骤使用 `xlwings`——不做其他操作。

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

为什么不调用 `wb.calculate()`？`openpyxl` 没有内置计算引擎，所以我们通过 `xlwings` 借助 Excel 本身。对于小型工作表来说开销很小，并且能得到 Excel 实际显示的精确结果。

---

## 重新计算并获取结果 – 将求和结果拉回 Python

最后，我们读取 D 列溢出的结果。`openpyxl` 使这一步非常直接：

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

如果你更倾向于只使用 `openpyxl`，可以在 Excel 重新计算后读取单元格：

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

两种方法都会得到相同的列表 `[6, 15, 24]`，证明使用 `BYROW` + Lambda 的 **how to sum rows** 如宣传的那样有效。

---

## 边缘情况与常见陷阱

| 情况 | 需要注意的点 | 解决方案 |
|-----------|-------------------|-----|
| Excel 版本低于 365 | `BYROW` 和 `LAMBDA` 显示为 `#NAME?` | 使用传统的 `=SUM(A1:C1)` 手动向下复制，或升级 Excel。 |
| 大型矩阵（10 k+ 行） | 重新计算可能变慢 | 仅调用一次 `book.api.CalculateFullRebuild()`，或拆分工作簿。 |
| 在无 Excel 的无头服务器上运行 | `xlwings` 无法启动 Excel | 改用纯 Python 库，如 `pandas` + `numpy` 进行计算，然后写入结果。 |
| 区域设置问题（逗号 vs 分号） | 公式可能被拒绝 | 对于使用 `;` 的区域设置，使用 `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"`。 |

---

## 完整工作示例（可直接复制粘贴）

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.Cells Java 创建 Excel 工作簿 - 完整指南](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [使用 Aspose.Cells 创建 Excel 工作簿并自动化报告](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [如何使用 Aspose.Cells for .NET 将 Excel 工作簿创建并保存为 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}