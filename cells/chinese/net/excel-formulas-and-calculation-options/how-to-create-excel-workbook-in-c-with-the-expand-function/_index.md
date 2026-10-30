---
category: general
date: 2026-10-04
description: 学习如何在 C# 中创建 Excel 工作簿，使用 EXPAND，强制公式计算，并在填充数字列的同时将工作簿保存为 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- how to use expand
- force formula calculation
- save workbook as xlsx
- populate column with numbers
language: zh
lastmod: 2026-10-04
og_description: 使用 Aspose.Cells 在 C# 中创建 Excel 工作簿。本教程展示如何使用 EXPAND、强制公式计算，并在填充列数字的同时将工作簿保存为
  XLSX。
og_image_alt: Screenshot of a C# program that creates an Excel workbook and applies
  the EXPAND function
og_title: 在 C# 中创建 Excel 工作簿 – 包含 EXPAND 和 XLSX 保存的完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to create Excel workbook in C# and use EXPAND, force formula
    calculation, and save workbook as XLSX while populating a column with numbers.
  headline: How to create Excel workbook in C# with the EXPAND function
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: 如何在 C# 中使用 EXPAND 函数创建 Excel 工作簿
url: /zh/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-with-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 EXPAND 函数创建 Excel 工作簿

如果您需要以编程方式**创建 Excel 工作簿**，本指南提供了一个完整、可直接运行的解决方案。您将看到如何**用数字填充列**，应用**EXPAND**函数水平展开数据，**强制公式计算**，以及最终**将工作簿保存为 XLSX**。  

本教程涵盖了您所需的每一步，从初始化工作簿到验证结果。无需外部文档——只需复制代码，运行它，您就会得到一个功能完整的 Excel 文件。

## 前提条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）
- Aspose.Cells for .NET NuGet 包 (`Install-Package Aspose.Cells`)
- 对 C# 语法的基本了解
- 如 Visual Studio 或 VS Code 等 IDE

## 第一步：创建 Excel 工作簿并访问第一个工作表

首先要**创建 Excel 工作簿**并获取其默认工作表的引用。Aspose.Cells 会自动在索引 0 处添加工作表，您可以立即使用它。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();          // create Excel workbook
        Worksheet sheet = workbook.Worksheets[0];   // first (default) worksheet
```

*为什么这很重要：* 实例化 `Workbook` 会分配内部文件结构，获取 `Worksheets[0]` 则得到一个具体的 `Worksheet` 对象，以便操作行、列和单元格。

## 第二步：用数字填充列

接下来，在 A 列填充一个垂直列表。这演示了**用数字填充列**，并为 EXPAND 函数提供源范围。

```csharp
        // Step 2: Fill a vertical list of values in column A
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);
```

*专业提示：* 使用 `PutValue` 来写入原始数字、字符串、日期或任何 .NET 基元类型。该方法会自动确定单元格类型。

## 第三步：如何使用 EXPAND – 将列表水平展开

**如何使用 expand** 部分是本教程的核心。`EXPAND` 函数将源范围展开为新的形状。这里我们将垂直范围 `A1:A3` 展开为单行，跨越三列，从 `B1` 开始。

```csharp
        // Step 3: Apply the EXPAND function to spill the list horizontally starting at B1
        // The formula expands the range A1:A3 into 1 row and 3 columns (B1:D1)
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";
```

*解释：*  
- 第一个参数 (`A1:A3`) 是源范围。  
- 第二个参数 (`1`) 强制结果为 **1** 行。  
- 第三个参数 (`3`) 强制结果为 **3** 列。  

当工作簿重新计算时，单元格 `B1`、`C1` 和 `D1` 将分别包含 `1`、`2` 和 `3`。

## 第四步：强制公式计算

Aspose.Cells 在您设置公式后不会自动求值，因此在保存之前必须**强制公式计算**。这可确保 EXPAND 的结果在文件中被实际写入。

```csharp
        // Step 4: Force calculation of all formulas in the workbook
        workbook.CalculateFormula();   // triggers calculation engine
```

*为什么需要这样做：* 如果不调用 `CalculateFormula`，保存的文件将只包含原始公式字符串，Excel 只会在打开文件时重新计算。对于自动化流水线，通常希望值立即写入。

## 第五步：将工作簿保存为 XLSX

现在工作簿已完全准备好，**将工作簿保存为 XLSX** 到您选择的位置。文件扩展名决定输出格式；`.xlsx` 会创建 Office Open XML 工作簿。

```csharp
        // Step 5: Save the workbook to a file
        string outputPath = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(outputPath);   // save workbook as XLSX
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

*提示：* 如果需要其他格式（CSV、PDF 等），只需更改文件扩展名，或使用 `workbook.Save(outputPath, SaveFormat.Xls)` 保存为旧版 Excel 格式。

## 完整、可运行的示例

将所有代码组合在一起，您将得到一个自包含的程序，能够**创建 Excel 工作簿**、填充列、使用 **EXPAND**、强制计算，并**将工作簿保存为 XLSX**。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create Excel workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2. Populate column with numbers
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // 3. How to use EXPAND – spill horizontally
        sheet.Cells["B1"].Formula = "=EXPAND(A1:A3, 1, 3)";

        // 4. Force formula calculation
        workbook.CalculateFormula();

        // 5. Save workbook as XLSX
        string path = @"C:\Temp\ExpandFunction.xlsx";
        workbook.Save(path);
        System.Console.WriteLine($"Workbook saved to {path}");
    }
}
```

### 预期输出

运行程序后，在 Excel 中打开 `ExpandFunction.xlsx`。您应该看到：

| A | B | C | D |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |   |   |   |
| 3 |   |   |   |

单元格 `B1:D1` 中的值 `1`、`2`、`3` 证明 **EXPAND** 函数已生效，并且 **强制公式计算** 步骤成功将结果写入。

## 常见变体和边缘情况

| 场景 | 调整 |
|----------|------------|
| **动态源范围** | 使用 `=EXPAND(A1:INDEX(A:A, COUNTA(A:A)), 1, 0)` 将范围扩展为已填充的行数。 |
| **不同的输出维度** | 更改 `EXPAND` 的第二和第三个参数以控制行数和列数。 |
| **多个工作表** | 遍历 `workbook.Worksheets` 并对每个工作表应用相同的逻辑。 |
| **大数据集** | 在设置完所有公式后调用一次 `workbook.CalculateFormula()`，以避免重复计算。 |
| **保存到内存流** | 当需要在 Web API 响应中返回文件时，将 `workbook.Save(path)` 替换为 `workbook.Save(stream, SaveFormat.Xlsx)`。 |

## 故障排查清单

- **公式未展开：** 确认在设置公式后调用 `CalculateFormula()` *之后*。  
- **保存时文件未找到：** 确保目标目录存在且进程具有写入权限。  
- **数据类型不正确：** 对数字使用 `PutValue`；对日期使用 `PutValue(DateTime.Now)` 或 `PutDateTime`。  
- **版本不匹配：** EXPAND 函数需要兼容 Excel 365 的计算引擎；Aspose.Cells 23.9+ 已支持。

## 结论

您现在已经掌握了如何在 C# 中**创建 Excel 工作簿**、**用数字填充列**、应用 **EXPAND** 函数、**强制公式计算**，以及**将工作簿保存为 XLSX**。此端到端示例可用于报告、数据转换或任何需要动态 Excel 输出的自动化场景。

### 接下来的步骤

- 探索其他动态数组函数，如 `FILTER`、`SORT` 和 `UNIQUE`。  
- 将工作簿生成集成到 ASP.NET Core API 中，以按需提供 Excel 文件。  
- 用从数据库或 CSV 文件读取的数据替换硬编码的数字，以实现真实场景的报告。

随意尝试不同的范围、工作表名称和输出格式。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [如何在 Excel 中使用 C# 计算余切 – 创建工作簿，使用 EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [如何在 C# 中使用 WRAPCOLS – 创建带有包装函数的 Excel 工作簿](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [如何使用 Aspose.Cells for .NET 创建并保存为 ODS 的 Excel 工作簿](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}