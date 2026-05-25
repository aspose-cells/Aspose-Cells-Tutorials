---
category: general
date: 2026-02-09
description: 如何在 Excel 中使用 C# 创建数组，几分钟内讲解——学习生成序列号、使用 COT，并将工作簿保存为 XLSX。
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: zh
og_description: 如何使用 C# 在 Excel 中创建数组的步骤详解，包括生成序列号、使用 COT，以及将工作簿保存为 XLSX。
og_title: 如何使用 C# 在 Excel 中创建数组 – 快速指南
tags:
- C#
- Excel
- Aspose.Cells
title: 如何使用 C# 在 Excel 中创建数组 – 步骤指南
url: /zh/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 在 Excel 中创建数组 – 分步指南

是否曾经想过 **how to create array** 在 Excel 中使用 C#，却不想花费数小时翻阅文档？你并不孤单。许多开发者在需要动态溢出范围、快速三角函数值，或仅仅是将干净的 XLSX 文件保存到磁盘时都会遇到瓶颈。在本教程中，我们将立即解决这个问题——通过构建一个小型工作簿，写入展开的数组公式，插入余切计算，并将所有内容保存为 XLSX 文件。  

我们还会加入一些额外技巧：生成序列号、精通 `COT` 函数，以及确保文件保存到你想要的位置。完成后，你将拥有一个可复用的代码片段，可直接放入任何 .NET 项目中。没有废话，只有可运行的代码。

> **Pro tip:** 示例使用流行的 **Aspose.Cells** 库，但这些概念同样适用于其他 Excel 自动化包（EPPlus、ClosedXML），只需做少量修改。

---

## 你需要的环境

- **.NET 6** 或更高版本（代码同样可以在 .NET Framework 4.7+ 上编译）  
- **Aspose.Cells for .NET** – 可从 NuGet 获取（`Install-Package Aspose.Cells`）  
- 文本编辑器或 IDE（Visual Studio、Rider、VS Code…）  
- 对将保存输出文件的文件夹拥有写入权限  

就这么简单——无需额外配置，无需 COM 互操作，只需一个干净的托管程序集。

---

## 步骤 1：How to create array in Excel – 初始化工作簿

当你想在 Excel 工作表中 **how to create array** 时，首先要做的就是创建一个工作簿对象。可以把工作簿看作空白画布；工作表则是你绘制公式的地方。

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

为什么使用不带参数的 `Workbook()`？它会创建一个内存中的工作簿并带有默认工作表，非常适合快速的编程任务。如果需要打开已有文件，只需将文件路径传入构造函数即可。

---

## 步骤 2：使用 EXPAND 和 SEQUENCE 生成序列号

现在我们已经有了工作表，让我们解决 **generate sequence numbers** 这一部分。Excel 的新动态数组函数（`SEQUENCE`、`EXPAND`）让我们可以创建一个 3 行的垂直列表，并自动溢出到 3 × 5 的范围。

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**这里发生了什么？**  
- `SEQUENCE(3,1,1,1)` → 生成一个垂直数组 `{1;2;3}`。  
- `EXPAND(...,5,1)` → 将这三行列扩展为五列，额外的单元格填充为空白。  

当你打开生成的 `output.xlsx` 时，会看到一个从 **A1** 开始的 3 × 5 区块，第一列包含 1、2、3，剩余四列为空。此技术是 **how to create array**‑风格溢出范围的核心，无需手动为每个单元格编写公式。

---

## 步骤 3：How to use COT – 添加三角函数公式

如果你也想了解 **how to use cot** 在 Excel 公式中的用法，`COT` 函数是获取以弧度表示的角度余切的便捷方式。我们来计算 `cot(π/4)`，其结果应为 **1**。

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

请注意我们使用 `PI()` 获取 180° 的弧度值，然后除以 4 得到 45°。Excel 完成了繁重的计算，工作簿打开后单元格 **B1** 将显示 `1`。这展示了 **how to use cot** 在快速工程或金融计算中的应用，无需引入额外的数学库。

---

## 步骤 4：Save workbook as XLSX – 持久化文件

如果从不将文件写入磁盘，创建数组和插入公式的所有工作都将毫无意义。下面是使用 Aspose.Cells **save workbook as xlsx** 的简洁方法：

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

为什么要指定 `SaveFormat.Xlsx`？它确保使用现代的 OpenXML 格式，能够被所有主流软件（Excel、LibreOffice、Google Sheets）读取。如果需要旧的 `.xls` 文件，只需更换枚举即可。

---

## 完整工作示例（所有步骤合并）

下面是完整的可直接运行的程序。将其复制粘贴到控制台项目中，恢复 Aspose.Cells NuGet 包，然后按 **F5** 运行。

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**预期结果** 打开 `output.xlsx` 后：

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- A 列显示由 `SEQUENCE` 生成的数字 1‑3。  
- B 列包含来自 `COT` 公式的值 **1**。  
- C‑E 列为空，展示了 `EXPAND` 的填充效果。

---

## 常见问题与边缘情况

### 如果需要更多行或列怎么办？

只需调整 `SEQUENCE` 和 `EXPAND` 的参数。  
- `SEQUENCE(10,2,5,2)` 将生成一个 10 行 × 2 列的矩阵，起始值为 5，步长为 2。  
- `EXPAND(...,10,5)` 将把结果填充为 10 列 × 5 行。

### 这在旧版本 Excel 中可用吗？

动态数组函数（`SEQUENCE`、`EXPAND`）需要 Excel 365 或 2019+。对于旧版文件，可以回退到传统公式，或通过 `Cells[row, col].PutValue(value)` 直接写入数值。

### 可以使用 R1C1 形式写公式吗？

Absolutely. Replace `A1` with `Cells[0, 0]` and use `FormulaR1C1` property:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### 如何处理特定文化的十进制分隔符？

Aspose.Cells 会遵循工作簿的区域设置。如果需要特定文化，可在写入公式前设置 `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");`。

---

## 可视化摘要

![使用 C# 在 Excel 中创建数组](/images/how-to-create-array-excel-csharp.png "使用 C# 在 Excel 中创建数组")

*该截图显示了最终的溢出范围以及余切结果。*

---

## 结论

就是这样——从头开始使用 C# 在 Excel 中 **how to create array**，生成序列号，利用 `COT` 函数，并在一个简洁的程序中 **save workbook as XLSX**。关键要点如下：

1. 使用 `Workbook` 和 `Worksheet` 对象启动 Excel 自动化。  
2. 利用动态数组函数（`SEQUENCE`、`EXPAND`）实现灵活的溢出范围。  
3. 插入 `COT` 等三角函数，实现快速计算，无需额外库。  
4. 使用 `SaveFormat.Xlsx` 持久化结果，生成通用可读的文件。

准备好下一步了吗？尝试替换 `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}