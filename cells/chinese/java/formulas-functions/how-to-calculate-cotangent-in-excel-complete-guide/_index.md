---
category: general
date: 2026-06-27
description: 如何在 Excel 中使用公式计算余切。学习如何设置公式、如何使用 EXPAND，并掌握 Excel 动态数组公式。
draft: false
keywords:
- how to calculate cotangent
- how to set formula
- how to use expand
- excel dynamic array formula
- add expand function
language: zh
og_description: 如何在 Excel 中计算余切并提供清晰示例。本教程展示如何设置公式、使用 EXPAND，以及使用 Excel 动态数组公式。
og_title: 如何在 Excel 中计算余切 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  headline: How to Calculate Cotangent in Excel – Complete Guide
  type: TechArticle
- description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  name: How to Calculate Cotangent in Excel – Complete Guide
  steps:
  - name: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
    text: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
  - name: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
    text: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
  - name: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
    text: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
  - name: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
    text: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
  - name: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
    text: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
  - name: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
    text: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
  - name: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
    text: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
  type: HowTo
tags:
- Excel
- Formulas
- Java
- Aspose.Cells
title: 如何在Excel中计算余切——完整指南
url: /zh/java/formulas-functions/how-to-calculate-cotangent-in-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中计算余切 – 完整指南

有没有想过 **如何在 Excel 中计算余切** 而不必拿出科学计算器？你并不是唯一的。无论是构建金融模型、物理工作表，还是仅仅喜欢玩三角函数，掌握 Excel 中的余切函数都能为你节省大量时间。

在本教程中，我们还将展示 **如何使用 Java 的 Aspose.Cells 库以编程方式设置公式**，深入探讨 **如何使用 EXPAND**，并解释 **excel 动态数组公式** 功能为何重要。完成后，你将拥有一个完整可运行的示例，添加 EXPAND 函数、计算余切并打印结果——全部代码不超过十行。

## 你将学到的内容

- Excel `COT` 函数的语法以及它为何是获取余切值的最快方式。  
- 如何通过 Java 代码 **设置公式** 到工作表单元格。  
- **如何使用 EXPAND** 实现动态数组的工作原理。  
- 何时以及如何 **添加 expand function** 到工作簿以进行溢出范围计算。  
- 处理 **excel 动态数组公式** 常见问题的技巧。

> **先决条件：**  
> - 已安装 Java 8 及以上。  
> - Aspose.Cells for Java（免费试用版或正式授权版）。  
> - 对 Excel 函数有基本了解。

如果你满足以上条件，下面我们开始吧。

---

## 如何在 Excel 中计算余切

`COT` 函数返回以弧度提供的角度的余切值。其语法非常简单：

```excel
=COT(number)
```

其中 *number* 为弧度制的角度。例如，对经典的 45°（π/4 弧度）角度，结果为 `1`，因为 `cot(π/4) = 1`。

### 为什么使用 `COT` 而不是手动计算？

你可以写 `=1/TAN(angle)`，但这会让 Excel 计算两个函数，并且在角度为 π 的整数倍时会出现除以零的错误。`COT` 是内置函数，能够处理边界情况，且更易阅读——尤其是在与团队成员共享工作表时。

---

## 步骤演示：使用 Java 设置公式（How to Set Formula）

下面是一段 **完整、可运行的 Java 程序**，它创建工作簿、在单元格 `B1` 中添加 `COT` 公式并进行求值。我们还会加入 `EXPAND` 函数以演示动态数组。

```java
import com.aspose.cells.*;

public class CotangentDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // 2️⃣ Populate source data for EXPAND (A2:A5)
        for (int i = 0; i < 4; i++) {
            cells.get(i + 1, 0).putValue(i + 1); // A2=1, A3=2, A4=3, A5=4
        }

        // 3️⃣ **How to set formula** – Apply EXPAND to cell A1
        //    EXPAND(source, rows, columns) creates a spill range.
        cells.get("A1").setFormula("=EXPAND(A2:A5,5,2)");

        // 4️⃣ **How to calculate cotangent** – Apply COT to cell B1
        //    COT(PI()/4) = 1 because cot(45°) = 1
        cells.get("B1").setFormula("=COT(PI()/4)");

        // 5️⃣ Recalculate the workbook so formulas resolve
        wb.calculateFormula();

        // 6️⃣ Retrieve and print results
        System.out.println("EXPAND result (A1 spill range):");
        for (int r = 0; r < 5; r++) {
            for (int c = 0; c < 2; c++) {
                System.out.print(cells.get(r, c).getStringValue() + "\t");
            }
            System.out.println();
        }

        System.out.println("\nCotangent of π/4 (B1): " + cells.get("B1").getStringValue());

        // 7️⃣ Save the workbook (optional)
        wb.save("CotangentDemo.xlsx");
    }
}
```

#### 代码说明

1. **Workbook 创建** – `new Workbook()` 为我们提供一个全新的内存 Excel 文件。  
2. **源数据** – 我们在 `A2:A5` 填入数字 1‑4，这些值稍后会被展开。  
3. **如何设置公式** – `setFormula` 将 `EXPAND` 表达式附加到 `A1`。该函数告诉 Excel 基于源范围溢出成一个 5 行 2 列的块。  
4. **如何计算余切** – `COT` 调用使用 `PI()/4`（45°）。这正是 *how to calculate cotangent* 在 Excel 中的核心答案。  
5. **重新计算** – `wb.calculateFormula()` 强制 Aspose.Cells 评估所有公式，就像在 UI 中按 **F9** 一样。  
6. **结果输出** – 我们遍历溢出范围，以证明 `EXPAND` 实际创建了动态数组。  
7. **保存** – 最终工作簿 `CotangentDemo.xlsx` 可在 Excel 中打开，查看实时公式。

> **小贴士：** 如果你使用的 Excel 版本支持动态数组（Office 365 或 Excel 2021 及以上），`EXPAND` 函数会自动“溢出”到相邻单元格。旧版本会返回 `#NAME?` 错误——因此在 **add expand function** 前务必检查 Excel 版本。

---

## 如何使用 EXPAND – 理解 Excel 动态数组公式

`EXPAND` 是 Excel **动态数组** 系列的一部分，旨在取代繁琐的手动范围定义。其签名如下：

```excel
=EXPAND(array, rows, columns, [pad_with])
```

- **array** – 你想要展开的源范围。  
- **rows** – 溢出范围的行数（使用 `0` 保持原始高度）。  
- **columns** – 溢出范围的列数（使用 `0` 保持原始宽度）。  
- **pad_with** – 可选的填充值，用于填充空单元格。

当你写 `=EXPAND(A2:A5,5,2)` 时，Excel 会读取四行单列的数据并将其扩展为 5 行 2 列的矩阵，默认使用 `0` 填充额外单元格。结果会“溢出”到相邻单元格，表现为 **excel 动态数组公式**。

### 何时添加 EXPAND 函数

- **数据标准化** – 只有单列数据但需要矩阵用于图表。  
- **为其他数组函数做预处理** – `FILTER`、`SORT` 等函数直接接受溢出范围。  
- **避免手动向下填充** – 动态数组会在源数据变化时自动调整。

---

## 常见陷阱及解决办法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| `#SPILL!` 错误 | 目标单元格已有数据 | 清除该区域或将公式移动到空白单元格。 |
| `#NAME?` 出现在 `EXPAND` 上 | Excel 版本不支持动态数组 | 升级至 Office 365/Excel 2021，或使用 `INDEX` 等备选方案。 |
| `#DIV/0!` 来自 `COT` | 角度等于 `0` 或 `π`（余切未定义） | 包装公式：`=IF(MOD(angle,PI())=0,NA(),COT(angle))`。 |
| Java 中公式未更新 | 未调用 `Workbook.calculateFormula()` | 确保在设置完所有公式后调用 `calculateFormula()`。 |

---

## 扩展示例 – 更多计算余切的方法

如果需要对 **度数** 值求余切，先进行转换：

```java
cells.get("C1").setFormula("=COT(RADIANS(30))"); // cot(30°) ≈ 1.732
```

或者，将 `COT` 与其他数组函数结合使用：

```excel
=MAP(A2:A5, LAMBDA(x, COT(RADIANS(x))))
```

`MAP` 函数（在较新 Excel 版本中可用）会对范围的每个元素应用 `COT`，返回余切值的动态数组——非常适合批量计算。

---

## 完整示例回顾

下面是 **完整源码文件**，可直接复制粘贴到 IDE 中运行。没有隐藏依赖，所需的一切都在这里。



## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助你在本教程展示的技术基础上进一步深入。每篇资源都提供完整可运行的代码示例，并配有逐步解释，助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Excel IF 函数](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [如何使用 Aspose.Cells for Java 设置 Excel 文档版本](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)
- [如何使用 Aspose.Cells .NET 为多语言支持在 Excel 文件中设置语言](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}