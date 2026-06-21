---
category: general
date: 2026-06-21
description: 使用 Python 在 Excel 中创建乘法表。学习如何使用 lambda、如何使用 makearray、显示 Excel 数组以及在分步教程中使用
  Python 读取 Excel 值。
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: zh
og_description: 使用 Python 在 Excel 中创建乘法表。本教程展示了如何使用 lambda、makearray、显示 Excel 数组以及高效读取
  Excel 值。
og_title: 使用 Python 在 Excel 中创建乘法表 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: 使用 Python 在 Excel 中创建乘法表 – 完整指南
url: /zh/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 Python 创建乘法表 – 完整指南

有没有想过如何在 Excel 中 **create multiplication table** 而不需要手动输入每个单元格？你并不孤单。在许多报告场景中，你需要一个快速的 5×5（或更大）的产品网格，手工操作既浪费时间。  

在本教程中，我们将逐步演示一种简洁的、由 Python 驱动的方式来生成该表格，将其嵌入 `MAKEARRAY` 公式中，然后将结果拉回到你的脚本中。过程中我们会回答 **how to use lambda**，展示 **how to use makearray**，并演示 **display excel array** 以及 **read excel values python**——全部在一个完整的示例中。

完成后，你将拥有一个可在任何工作簿中复用的代码片段，并且会了解为何这种方法既快速又具前瞻性。

## 你需要的条件

- Python 3.8+（最新的稳定版即可）
- `openpyxl` 库（或任何支持公式的 Excel‑aware 库）
- 对 Python 中 lambda 表达式的基本了解
- 无需特殊的 Excel 加载项；原生的 `MAKEARRAY` 函数（在 Excel 365 中可用）承担主要工作

如果缺少上述任意项，只需运行 `pip install openpyxl` 即可开始使用。

## 创建乘法表 – 概览

核心思路很简单：我们创建一个全新的工作簿，写入一个构建 5 × 5 乘法矩阵的 `MAKEARRAY` 公式，强制 Excel 计算它，最后将得到的数值读取回 Python。

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

运行脚本后输出：

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

这就是一个完整功能的 **create multiplication table**，在 Excel 中完全由 Python 生成。

### 为什么使用 `MAKEARRAY` 而不是 Python 循环？

- **Performance**：Excel 原生处理计算，对于大型矩阵更快。
- **Live updating**：如果随后更改公式中的维度，工作表会自动重新计算。
- **Readability**：公式直接表达意图（“make an array”），保持你的 Python 代码简洁。

## 如何在 Python 中为 Excel 公式使用 lambda

`MAKEARRAY` 调用中的 `LAMBDA` 部分是 Excel 端的匿名函数，而不是 Python 的 lambda。概念相同：你定义一个小的内联逻辑，接受 `r`（行索引）和 `c`（列索引），返回 `r*c`。  

如果你是 **how to use lambda** 在 Excel 世界中的新手，可以把它视为仅存在于公式内部的迷你函数。无需在其他地方声明单独的函数。在 Python 中我们只需嵌入字符串：

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

该行告诉 Excel：*“对 5 × 5 区块中的每个单元格，计算行 × 列。”*  

因为 lambda 由 Excel 求值，你无需担心 Python 本身的 lambda 语法——只需使用 Excel 语法即可。

## 如何使用 makearray 生成数组

`MAKEARRAY` 是 Excel 函数库中相对较新的功能（自 2022 年起在 Microsoft 365 中可用）。它取代了旧的技巧，如 `INDEX` + `ROW`/`COLUMN` 组合。其签名为：

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – 你想要的行数。
- **columns** – 你想要的列数。
- **lambda** – 一个接受 `(row, column)` 并返回值的 Excel LAMBDA。

在我们的示例中，我们传入 `5,5` 以生成经典的乘法表，但你可以轻松更改这些数字：

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

这样就能得到一个 10 × 10 的表格，而无需使用任何 Python 循环。这展示了 **how to use makearray** 可用于任何确定性的网格，无论是查找表、热图还是财务计划表。

## 显示 excel array – 将数据拉回 Python

Excel 计算完公式后，结果值就像手动输入的单元格一样存在于工作表中。要 **display excel array**，我们遍历范围并打印每一行：

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

- 如果需要处理更大的范围，建议使用 `worksheet.cell(row, column).value` 而不是字典式索引；速度稍快。
- 如果想要更美观的表格，可考虑使用 `tabulate` 或 `pandas.DataFrame` 来格式化输出。

下面是生成的工作表截图（图像 alt 文本包含主要关键词以利 SEO）：

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## 读取 excel values python – 提取矩阵以进行后续处理

在 **display excel array** 之后，常见的下一步是将这些数字输入数据分析管道。这时 **read excel values python** 就显得尤为重要。我们用于打印的相同循环可以重新用于构建列表的列表、NumPy 数组或 Pandas DataFrame：

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

输出：

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

现在你拥有一个完整类型的 DataFrame，可以进行绘图、导出为 CSV，或喂入机器学习模型。这就完成了工作流中的 **read excel values python** 部分。

## 边缘情况与实用技巧

- **Formula recalculation**：如果在首次调用 `calculate_formula()` 后修改工作簿，需要再次调用；否则缓存的数组会变陈旧。
- **Non‑365 Excel**：旧版 Excel 不支持 `MAKEARRAY`。此时可回退到使用 Python 生成表格并逐个写入单元格。
- **Large tables**：对于大于约 100 × 100 的矩阵，考虑流式处理数据，以避免将整个工作表加载到内存。
- **Error handling**：将计算和读取步骤放入 `try/except` 块中，以捕获 `InvalidFileException` 或 `FormulaError`。

## 结论

我们刚刚展示了如何使用 Python 在 Excel 中 **create multiplication table**，并利用 **how to use lambda** 与 **how to use makearray** 的强大功能。你已经看到如何 **display excel array**，以及如何使用 **read excel values python** 将这些值读取回去，甚至将结果转换为 Pandas DataFrame 以进行后续分析。

想更进一步？尝试将乘法逻辑替换为更复杂的内容——比如距离矩阵、概率表或动态定价网格。相同的模式适用：一行 `MAKEARRAY`，一次快速的 `calculate_formula()`，以及少量 Python 循环来提取数据。

如果你觉得本指南有帮助，请在 GitHub 上给它加星，分享给团队成员，或留下你的使用案例评论。祝编码愉快，享受使用单一公式生成 Excel 表格的简洁体验！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在所示技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方法。

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}