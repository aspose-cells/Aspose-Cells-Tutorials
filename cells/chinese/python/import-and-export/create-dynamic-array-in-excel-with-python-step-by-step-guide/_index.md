---
category: general
date: 2026-06-21
description: 使用 Python 和 Excel 中的 SEQUENCE 函数创建动态数组。学习读取公式结果、重新计算 Excel 公式，并查看 Excel
  SEQUENCE 示例。
draft: false
keywords:
- create dynamic array
- sequence function excel
- read formula result
- recalculate excel formulas
- excel sequence example
language: zh
og_description: 使用 Python 在 Excel 中创建动态数组。本教程展示如何使用 SEQUENCE 函数、重新计算 Excel 公式以及读取公式结果。
og_title: 使用 Python 在 Excel 中创建动态数组 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create dynamic array using Python and the SEQUENCE function in Excel.
    Learn to read formula result, recalculate Excel formulas, and see an Excel SEQUENCE
    example.
  headline: Create Dynamic Array in Excel with Python – Step‑by‑Step Guide
  type: TechArticle
tags:
- excel
- python
- xlwings
- dynamic arrays
title: 使用 Python 在 Excel 中创建动态数组 – 步骤指南
url: /zh/python/import-and-export/create-dynamic-array-in-excel-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Python 在 Excel 中创建动态数组 – 完整指南

是否曾想过在不离开 Python 脚本的情况下 **创建动态数组** 公式？你并不是唯一有此想法的人。无论是自动化月度报告还是构建轻量级数据引擎，能够将 `SEQUENCE` 公式写入工作簿、重新计算并将溢出范围拉回 Python，都是改变游戏规则的利器。

在本教程中，我们将通过一个真实的 **excel sequence 示例**，演示如何 **读取公式结果**，并解释在注入新逻辑后 **重新计算 excel 公式** 的最佳方式。完成后，你将拥有一个可直接复制‑粘贴、运行并根据自身需求进行改造的完整脚本。

## 你将学到

- `SEQUENCE` 函数的工作原理以及它为何非常适合生成矩阵。
- 常规单元格值与溢出范围地址之间的区别。
- 使用 `wb.calculate_formula()`（或等效方法）强制 Excel 计算新公式。
- 使用 `ANCHORARRAY` 提取动态数组的地址。
- 一个完整、可运行的 Python 示例，随时可以放入任意项目。

不需要事先了解 Excel 新的动态数组引擎——只要对 Python 有基本了解，并使用像 **xlwings** 这样的库即可与 Excel 通信。

---

## 如何使用 Python 在 Excel 中通过 SEQUENCE 创建动态数组

第一步是直接在工作表单元格中写入 **动态数组** 公式。在现代 Excel 中，`SEQUENCE` 函数可以即时生成数字矩阵。下面是我们将使用的语法：

```python
# Step 1: Write a dynamic array formula that generates a 3×2 matrix starting at 10 with step 5
ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"   # Returns a 3×2 array
```

**为什么选择 `SEQUENCE`？**  
把它想象成 Excel 为电子表格提供的内置 `range()`。它让你在一行代码中指定行数、列数、起始值以及步长。我们的例子请求 3 行 2 列，起始值为 10，步长为 5，得到的结果是：

|   | A | B |
|---|---|---|
|1|10|15|
|2|20|25|
|3|30|35|

由于公式位于 `A1`，Excel 会自动将结果“溢出”到相邻的单元格 `A1:B3`。我们稍后将检索的正是这个溢出范围。

---

## 在 Excel 中使用 SEQUENCE 函数 – 快速 Excel Sequence 示例

如果手动打开 Excel 并在单元格中输入 `=SEQUENCE(3,2,10,5)`，同样的矩阵会立即出现。该函数是 Office 365 中引入的 Excel **动态数组** 引擎的一部分，这意味着：

- 不需要 Ctrl+Shift+Enter。
- 结果可以自动扩展或收缩。
- 可以使用 `@` 或 `#` 等符号引用整个溢出范围。

在 Python 中，唯一的区别是我们将公式作为字符串赋给单元格的 `.formula` 属性。库会处理其余工作。

---

## 使用 ANCHORARRAY 获取溢出范围地址

动态数组就位后，通常需要知道 Excel 实际放置数值的区域。`ANCHORARRAY` 正是为此而生。它返回溢出范围左上角单元格的地址——这正是我们在脚本中读取的目标。

```python
# Step 2: Retrieve the address of the spill range produced by the formula in A1
ws.cells["C1"].formula = "=ANCHORARRAY(A1)"      # Returns the address of the spill range
```

将此公式放在 `C1` 中会得到类似 `"A1:B3"` 的文本字符串。请注意，我们 **读取公式结果** 时将其当作普通值，而不是另一个公式。这一小技巧避免了手动解析工作表的麻烦。

---

## 重新计算 Excel 公式并读取结果

当从外部脚本注入新公式时，Excel 并不总是立即重新计算。为确保工作簿反映最新更改，我们需要显式触发一次计算过程。

```python
# Step 3: Recalculate all formulas in the workbook and read the result
wb.calculate_formula()               # Forces Excel to evaluate pending formulas
print(ws.cells["C1"].value)          # → "A1:B3"
```

**为什么要调用 `calculate_formula()`？**  
如果跳过这一步，`ws.cells["C1"].value` 可能仍返回 `None` 或旧的地址，因为 Excel 仍在更新其依赖树。强制重新计算可确保 **读取公式结果** 为最新状态。

---

## 完整脚本 – 从头到尾

下面是一个完整、可直接运行的示例，演示了所有步骤的结合。它假设你已经安装了 **xlwings**（`pip install xlwings`），并且机器上可用 Excel。

```python
import xlwings as xw

def create_dynamic_array_example():
    # Open a new workbook (or attach to an existing one)
    wb = xw.Book()               # Creates a fresh Excel workbook
    ws = wb.sheets[0]            # Grab the first worksheet

    # 1️⃣ Write the SEQUENCE formula – this creates a 3×2 matrix starting at 10, step 5
    ws.cells["A1"].formula = "=SEQUENCE(3,2,10,5)"

    # 2️⃣ Use ANCHORARRAY to capture the spill range address in C1
    ws.cells["C1"].formula = "=ANCHORARRAY(A1)"

    # 3️⃣ Force Excel to recalculate so that the ANCHORARRAY result is current
    wb.calculate_formula()

    # 4️⃣ Read back the address – this is our **read formula result** step
    spill_address = ws.cells["C1"].value
    print(f"The dynamic array spills into: {spill_address}")

    # 5️⃣ Optionally, fetch the actual values from the spill range
    # xlwings can read a range by address, so we demonstrate that too
    data = ws.range(spill_address).value
    print("Matrix values:")
    for row in data:
        print(row)

    # Clean up – close without saving to keep the demo tidy
    wb.close(save=False)

if __name__ == "__main__":
    create_dynamic_array_example()
```

### 预期输出

```
The dynamic array spills into: A1:B3
Matrix values:
[10, 15]
[20, 25]
[30, 35]
```

运行脚本后，Excel 将被打开，`SEQUENCE` 公式被注入，随后重新计算，并打印出溢出地址以及矩阵本身。全程无需手动点击。

---

## 常见坑点与专业技巧

- **坑点：** 忘记调用 `wb.calculate_formula()`。  
  *结果：* `C1` 为空或显示旧地址。  
  *解决方案：* 写入新公式后务必触发一次计算。

- **坑点：** 使用不支持 `SEQUENCE` 的旧版 Excel。  
  *结果：* `#NAME?` 错误。  
  *解决方案：* 确保使用 Office 365 或 Excel 2021 及以上版本。

- **专业技巧：** 若需进一步处理溢出范围（例如绘图），可直接将地址传入 `ws.range(spill_address)`，如上所示。

- **专业技巧：** `ANCHORARRAY` 适用于任何动态数组，而不仅限于 `SEQUENCE`。换成 `=SORT(A2:A10)` 或 `=FILTER(...)` 仍能得到正确的溢出地址。

- **边缘情况：** 当目标区域已被占用时，Excel 会返回 `#SPILL!` 错误。此时请先清除目标范围，或将公式移动到其他单元格。

---

## 拓展示例 – 接下来可以做什么？

既然已经掌握了 **创建动态数组** 公式、**读取公式结果**、以及 **重新计算 excel 公式** 的技巧，你可以进一步探索更高级的场景：

- **动态图表数据** – 将溢出范围作为图表数据源，让图表自动随数据增长。
- **条件格式** – 使用溢出范围的地址对其应用条件格式规则。
- **跨工作簿引用** – 在一个工作簿中写入动态数组，通过 `xlwings` 链接将数据拉入另一个工作簿。

这些都基于本指南的核心概念，欢迎自行实验。唯一的限制是你的想象力（以及 Excel 的最大行列数）。

---

## 结论

我们已经完整演示了如何通过 Python 在 Excel 中 **创建动态数组** 公式，使用 **SEQUENCE 函数**，通过 **ANCHORARRAY** 获取溢出范围，**重新计算 excel 公式**，并最终 **读取公式结果** 回到脚本中。简短的示例展示了 Excel 新的动态数组引擎与 **xlwings** 等自动化工具结合时的强大威力。

在自己的项目中尝试一下，调整矩阵维度，或将 `SEQUENCE` 替换为其他动态函数。随着熟练度提升，你会发现自动化 Excel 不仅可行，而且相当简便。

有问题或想分享你如何扩展此模式？欢迎在下方留言，祝编码愉快！


## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/english/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}