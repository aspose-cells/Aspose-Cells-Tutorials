---
category: general
date: 2026-06-30
description: Java 中的动态数组公式让您能够构建强大的 Excel 表格。学习如何使用 Java 创建 Excel 工作簿，并快速计算所有公式。
draft: false
keywords:
- dynamic array formulas
- calculate all formulas
- use lambda formula
- use expand function
- create excel workbook java
language: zh
og_description: Java 中的动态数组公式简化了 Excel 自动化。本指南展示了如何在 Java 中创建 Excel 工作簿，使用 expand
  函数、lambda 公式，并计算所有公式。
og_title: Java 中的动态数组公式 – 创建工作簿并计算公式
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Dynamic array formulas in Java let you build powerful Excel sheets.
    Learn to create Excel workbook Java and calculate all formulas quickly.
  headline: 'Dynamic Array Formulas in Java: Create Excel Workbook and Calculate All
    Formulas'
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Java中的动态数组公式：创建Excel工作簿并计算所有公式
url: /zh/java/calculation-engine/dynamic-array-formulas-in-java-create-excel-workbook-and-cal/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 中的动态数组公式：创建 Excel 工作簿并计算所有公式

是否曾好奇在使用 Java 自动化 Excel 时，**动态数组公式**是如何工作的？你并不孤单——许多开发者在需要在不打开 Excel 的情况下向工作簿中写入诸如 `EXPAND` 或 `REDUCE` 之类的高级公式时都会卡住。

好消息是，只需几行 Java 代码，你就可以 **以 Java 方式创建 Excel 工作簿**，插入这些现代数组函数，然后 **一次性计算所有公式**。本教程将逐步演示每一步，解释 *为什么* 每个环节重要，并提供一个完整、可直接复制粘贴到项目中的可运行示例。

## 你将学到

- 如何使用 Java 创建全新的 Excel 工作簿（是的，不需要 Excel UI）。  
- `EXPAND` 函数的工作原理以及它如何将普通范围转换为动态数组。  
- 如何使用 **lambda 公式** 语法配合 `REDUCE` 实现自定义聚合。  
- 添加许多人忘记存在的三角函数和双曲函数（`COT`、`COTH`）。  
- 只需一行代码即可 **计算所有公式**，让工作簿显示最新结果。  

> **先决条件：** Java 8+（支持 lambda），Aspose.Cells for Java 库，以及对 Excel 公式的基本了解。无需其他依赖。

---

## 动态数组公式：设置工作簿

首先，先获取一个工作簿对象。Aspose.Cells 的 `Workbook` 类是入口点；把它想象成每个动态数组公式将要存在的空白画布。

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // default sheet is Sheet1
```

*为什么重要：* 以编程方式实例化工作簿让你完全掌控文件格式、区域设置，最关键的是可以在不触及磁盘的情况下进行公式求值。

---

## 使用 EXPAND 函数扩展范围

`EXPAND` 函数是 Excel 用来根据指定大小“溢出”范围的答案。当源数据在运行时可能改变长度时，它非常适用。

```java
        // Step 2: Add a formula that expands B1:B3 into a 5‑row, 1‑column array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");
```

*解释：*  
- `B1:B3` 是源范围。  
- `5` 告诉 Excel 生成五行，即使源范围更短。  
- `1` 强制只有一列。  

当你随后 **计算所有公式** 时，`A1` 的结果将是一个垂直溢出的五个值，必要时用空白填充。

---

## 使用 REDUCE 应用 LAMBDA 公式

如果你想对一列求和但又需要自定义累加器，`REDUCE` 搭配 **lambda 公式** 就是最佳方案。语法起初看起来有点不寻常，但这只是 Java 在 Excel 公式中嵌入小匿名函数的方式。

```java
        // Step 3: Add a REDUCE formula that sums the values in B1:B5
        worksheet.getCells().get("A2").setFormula(
            "=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))"
        );
```

*为什么使用它？*  
- `0` 是初始种子（起始总和）。  
- `B1:B5` 是我们要折叠的数组。  
- `LAMBDA(a,b,a+b)` 表示“取累加器 `a` 和下一个元素 `b`，返回它们的和”。  

你可以将 `a+b` 替换为任何自定义逻辑——平均值、最大值，甚至字符串拼接——使 `REDUCE` 成为多功能的构建块。

---

## 添加三角函数（COT、COTH）

Excel 自带一小部分常被忽视的三角函数。下面演示如何在工作表中插入简单的余切及其双曲函数。

```java
        // Step 4: COT of π/4 (equals 1)
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 5: COTH of 2 (hyperbolic cotangent)
        worksheet.getCells().get("A4").setFormula("=COTH(2)");
```

*提示：* 这些函数会自动遵循工作簿的计算模式，无需额外代码将角度转换为弧度——`PI()` 已经完成了繁重的工作。

---

## 计算工作簿中的所有公式

公式就位后，需要 **计算所有公式**，让单元格保存实际数值而不是公式文本。Aspose.Cells 只需一次方法调用即可完成。

```java
        // Step 6: Force evaluation of every formula in the workbook
        workbook.calculateFormula();

        // Optional: Save to disk to see the result
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

*内部发生了什么？* 库会遍历每个单元格，解析依赖关系，并在需要时溢出数组结果。如果处理的是超大工作表，可以调节计算选项以提升性能，但默认设置对大多数场景已足够。

---

## 完整可运行示例（复制粘贴即用）

下面是完整程序，直接粘贴到 IDE 中即可运行。它包含导入语句、`main` 方法以及最终的 `save` 调用，方便你在 Excel 中打开生成的文件并查看溢出效果。

```java
import com.aspose.cells.*;

public class DynamicArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Populate source data for demonstration
        worksheet.getCells().get("B1").putValue(10);
        worksheet.getCells().get("B2").putValue(20);
        worksheet.getCells().get("B3").putValue(30);
        worksheet.getCells().get("B4").putValue(40);
        worksheet.getCells().get("B5").putValue(50);

        // EXPAND: spill B1:B3 into a 5‑row array
        worksheet.getCells().get("A1").setFormula("=EXPAND(B1:B3,5,1)");

        // REDUCE with LAMBDA: sum B1:B5
        worksheet.getCells().get("A2").setFormula("=REDUCE(0,B1:B5,LAMBDA(a,b,a+b))");

        // Trig functions
        worksheet.getCells().get("A3").setFormula("=COT(PI()/4)");
        worksheet.getCells().get("A4").setFormula("=COTH(2)");

        // Evaluate everything
        workbook.calculateFormula();

        // Save the file for inspection
        workbook.save("DynamicArrayDemo.xlsx");
    }
}
```

**打开 `DynamicArrayDemo.xlsx` 时的预期输出：**

| A（结果） | B（来源） |
|-----------|-----------|
| 10        | 10 |
| 20        | 20 |
| 30        | 30 |
| （空白）  | 40 |
| （空白）  | 50 |
| 150（求和）|   |
| 1（cot）  |   |
| 1.0373…（coth）| |

*注意 `A1` 会溢出五行，即使源数据只有三条。这正是 **动态数组公式** 的强大之处。*

---

## 常见陷阱与专业技巧

- **别忘了设置计算模式**，如果在其他地方关闭了自动计算；否则 `calculateFormula()` 将不起作用。  
- **数组溢出冲突：** 若已有单元格占据溢出范围，Excel 会返回 `#SPILL!` 错误。代码中可使用 `worksheet.getCells().clear(0, 0, maxRow, maxColumn)` 预先清除目标区域。  
- **Lambda 语法细节：** `LAMBDA` 函数要求参数之间用逗号分隔，而不是分号。少写逗号会导致整个公式解析失败。  
- **性能技巧：** 处理数千行数据时，可在批量插入前调用 `workbook.getSettings().setCalculateFormulaOnOpen(false)`，在最终 `calculateFormula()` 前再重新启用。

---

## 后续步骤

掌握了 **动态数组公式** 后，建议进一步探索：

- **`FILTER`** 与 **`SORT`** 用于即时数据整形。  
- **`SEQUENCE`** 用于在没有源范围的情况下生成数值数组。  
- 将 **命名范围** 与 `EXPAND` 结合使用，以获得更简洁、可复用的公式。  

这些都基于本教程中讲解的概念——只需替换公式字符串，让 Aspose.Cells 完成繁重的工作。

---

## 结论

在本指南中我们展示了如何 **以 Java 方式创建 Excel 工作簿**，

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方案，每篇都提供完整可运行的代码示例和逐步解释。

- [使用 Aspose.Cells for Java 创建 Excel 工作簿：分步指南](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Java 中的 Excel 公式计算：使用 Aspose.Cells 优化](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [使用 Aspose.Cells Java 精通 Excel 数组公式：简化计算与格式化](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}