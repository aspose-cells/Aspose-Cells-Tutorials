---
category: general
date: 2026-06-18
description: 如何在 Java 中使用序列生成动态数组并将工作簿保存为 xlsx —— 为开发者准备的完整实战教程
draft: false
keywords:
- how to use sequence
- save workbook as xlsx
- use sequence function
- create excel workbook java
- set dynamic array formula
language: zh
og_description: 如何在 Java 中使用序列构建动态数组并将工作簿保存为 xlsx。请遵循本指南获取完整可运行的解决方案。
og_title: 如何在 Java Excel 工作簿中使用 SEQUENCE – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  headline: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  type: TechArticle
- description: how to use sequence in Java to generate dynamic arrays and save workbook
    as xlsx – a complete, hands‑on tutorial for developers
  name: How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide
  steps:
  - name: Generate a Calendar Header
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)"); ```'
  - name: Create a Multiplication Table
    text: '```java sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
      ```'
  - name: Expected Output
    text: '- An `dynamic_sequence_demo.xlsx` file appears in your project directory.
      - Opening the file in Excel shows a 3×2 block of numbers (1‑6) automatically
      filled.'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Dynamic Arrays
title: 如何在 Java Excel 工作簿中使用 SEQUENCE – 步骤指南
url: /zh/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java Excel 工作簿中使用 SEQUENCE – 步骤指南

是否曾想过 **如何使用 sequence** 在不编写循环的情况下填充一系列单元格？你并不是唯一有此疑问的人。在现代 Excel 中，`SEQUENCE` 函数会生成一个溢出范围的数字序列，而使用 Java，你可以直接将这种强大功能写入工作簿。  

在本教程中，我们将演示如何在 Java 中创建 Excel 工作簿、**使用 SEQUENCE 设置动态数组公式**、重新计算工作表，最后 **将工作簿保存为 xlsx**。完成后，你将拥有一个可以直接放入任何项目的可运行程序。

## 你需要准备的环境

- Java 17 或更高版本（代码在 Java 8+ 上也能运行，但最新的 JDK 能提供最佳性能）。  
- Aspose.Cells for Java（或任何支持动态数组公式的库）。  
- 一个 IDE 或简单的文本编辑器——Visual Studio Code 完全足够。  

除上述库外，无需额外的 Maven 插件或其他不常见的依赖。

## 第一步：使用 Java 创建 Excel 工作簿

首先要 **创建 excel workbook java** 风格的工作簿。这一步我们实例化一个全新的 `Workbook` 对象，用来容纳所有工作表。

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();
```

*为什么重要*：`Workbook` 类是进行任何 Excel 操作的入口点。可以把它想象成一本空白笔记本，等待你填入数据。

## 第二步：获取第一个工作表

接下来，需要一个放置公式的地方。默认情况下，新工作簿会带有一个工作表，我们只需获取它即可。

```java
        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*小技巧*：如果需要多个工作表，只需调用 `workbook.getWorksheets().add("Sheet2")` 并重复相同的操作。

## 第三步：使用 SEQUENCE 函数 **设置动态数组公式**

现在进入教程的核心——**如何在单元格中使用 sequence**。公式 `=SEQUENCE(3,2)` 会在放置该公式的单元格处生成一个 3 行 2 列的溢出范围。

```java
        // Step 3: Insert a dynamic array formula that spills into B1:C3
        // This will generate numbers 1‑6 arranged in 3 rows and 2 columns.
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");
```

*发生了什么？*  
- `SEQUENCE(rows, columns)` 告诉 Excel 生成一个顺序数字矩阵。  
- 由于这是一个 **动态数组公式**，Excel 会自动将结果扩展到相邻单元格（本例中为 B1:C3）。  

如果想尝试其他变体，可以使用 `=SEQUENCE(5,1,10,2)`，从 10 开始并以步长 2 递增。

## 第四步：重新计算以确保溢出范围是最新的

Excel 在你请求时才会计算公式。在 Java 中我们需要触发一次计算过程：

```java
        // Step 4: Recalculate formulas so the spilled range is up‑to‑date
        workbook.calculateFormula();
```

*为什么要重新计算？* 如果不调用此方法，单元格里只会保留公式文本，而不会显示数值结果——保存的文件会看起来是空的。

## 第五步：**将工作簿保存为 XLSX**

最后，将文件写入磁盘。这一步演示了 **save workbook as xlsx** 的完整过程。

```java
        // Step 5: Save the workbook with the dynamic array data
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully!");
    }
}
```

当你在 Excel 365 或更高版本中打开 `dynamic_sequence_demo.xlsx` 时，会看到：

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |

*注意*：数字会自动从 A1 向相邻单元格溢出，正如 `SEQUENCE` 函数的行为所示。

## 探索 SEQUENCE 函数的不同用法

既然已经掌握了 **如何使用 sequence**，下面快速了解几种常见场景。

### 生成日历标题行

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(1,12,1,1)");
```

此代码会生成一行 1‑12 的数字——非常适合作为月份标题。

### 创建乘法表

```java
sheet.getCells().get("A1").setFormula("=SEQUENCE(5,5,1,1)*SEQUENCE(5,5,1,1)");
```

这里我们将两个相同的溢出范围相乘，得到一个 5×5 的乘法网格。

## 常见坑点及规避方法

- **旧版 Excel**：动态数组（包括 `SEQUENCE`）仅在 Excel 365/2021 及以上版本可用。旧版本会显示 `#NAME?`。  
- **库的支持情况**：并非所有 Java Excel 库都识别溢出范围。Aspose.Cells 支持；截至 2024 年，Apache POI 尚不支持。  
- **保存格式**：务必使用 `.xlsx` 保存动态数组；旧的 `.xls` 格式会丢失溢出行为。

## 完整可运行示例（复制即用）

下面是完整的、可直接运行的程序代码。只需在 Maven 项目中加入 Aspose.Cells 依赖即可。

```java
import com.aspose.cells.*;

public class SequenceDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Set the SEQUENCE formula – this will spill into B1:C3
        sheet.getCells().get("A1").setFormula("=SEQUENCE(3,2)");

        // Force calculation so the spilled values are stored
        workbook.calculateFormula();

        // Save the workbook as an XLSX file
        workbook.save("dynamic_sequence_demo.xlsx");
        System.out.println("Workbook saved successfully at dynamic_sequence_demo.xlsx");
    }
}
```

### 预期输出

- 项目目录下会生成 `dynamic_sequence_demo.xlsx` 文件。  
- 用 Excel 打开后，会自动填充一个 3×2 的数字块（1‑6）。

## 后续：超越 SEQUENCE 的使用

既然已经掌握了 **如何使用 sequence**，可以尝试将其与其他动态函数组合使用：

- **FILTER** – 提取满足条件的行。  
- **SORT** – 在不使用 VBA 的情况下对溢出范围进行排序。  
- **UNIQUE** – 从列表中提取唯一值。

这些同样可以 **使用动态数组公式** 的方式设置，就像我们对 `SEQUENCE` 所做的那样。将它们组合起来，你就能在 Excel 中构建强大的数据管道，而所有操作都由 Java 驱动。

## 结论

本文完整覆盖了在 Java 生成的 Excel 文件中 **如何使用 sequence**：创建工作簿、**设置动态数组公式**、重新计算以及 **将工作簿保存为 xlsx**。代码已完整提供，解释了每一步的“为什么”，并展示了几种实用的变体。

动手运行示例，修改参数，观察 Excel 为你完成繁重的计算。如果遇到版本不匹配或库限制等问题，欢迎在下方留言。祝编码愉快！

## 接下来你可以学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索项目中的其他实现方式，每篇都包含完整的代码示例和逐步解释。

- [Save Excel Workbook with Aspose.Cells for Java – Complete Guide](/cells/english/java/automation-batch-processing/excel-workbook-automation-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Aspose.Cells Java&#58; How to Add XML Maps and Save as XLSX (2023 Guide)](/cells/english/java/import-export/aspose-cells-java-add-xml-map-save-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}