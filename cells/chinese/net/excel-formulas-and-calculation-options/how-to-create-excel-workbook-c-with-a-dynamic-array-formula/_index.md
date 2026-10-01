---
category: general
date: 2026-10-01
description: 快速使用 C# 创建 Excel 工作簿，并学习在 Aspose.Cells 中编写 Excel 公式的动态数组公式示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- dynamic array formula example
- write excel formula c#
language: zh
lastmod: 2026-10-01
og_description: 快速使用 C# 创建 Excel 工作簿，并查看一个动态数组公式示例，展示如何使用 Aspose.Cells 用 C# 编写 Excel
  公式。按照分步指南生成、计算并保存文件。
og_image_alt: Screenshot of C# code creating an Excel workbook and applying a SORT
  dynamic array formula
og_title: 使用 C# 创建带动态数组公式的 Excel 工作簿
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  headline: How to create Excel workbook C# with a dynamic array formula
  type: TechArticle
- description: Create Excel workbook C# quickly and learn a dynamic array formula
    example to write Excel formula C# in Aspose.Cells.
  name: How to create Excel workbook C# with a dynamic array formula
  steps:
  - name: Verifying the result (expected output)
    text: 'You can print the spilled values to the console to confirm the calculation
      succeeded:'
  - name: What if I need to use a different dynamic array function?
    text: 'Replace the formula string with any other dynamic array function, such
      as `=FILTER(A2:A10, B2:B10>10)` or `=UNIQUE(A2:A10)`. The same **write Excel
      formula C#** pattern applies:'
  - name: How do I handle formulas that reference other worksheets?
    text: 'Reference another sheet by its name:'
  - name: Can I suppress automatic calculation and calculate later?
    text: 'Yes. Set the workbook’s calculation mode to manual:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何使用 C# 创建带有动态数组公式的 Excel 工作簿
url: /zh/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 创建带动态数组公式的 Excel 工作簿

如果您需要 **使用 C# 创建 Excel 工作簿**，本指南将手把手教您如何使用 Aspose.Cells 实现。您还将获得一个 **动态数组公式示例**，演示在现代 Excel 函数（如 `SORT`）中 **使用 C# 编写 Excel 公式** 的最佳实践。

过去，使用 C# 创建 Excel 文件往往需要 COM 互操作或手动生成 XML，这两种方式都脆弱且难以维护。阅读完本教程后，您将拥有一个能够自动计算动态数组的完整工作簿，并了解为何此方法适合生产级自动化。

## 前置条件

开始之前，请确保您具备以下条件：

- 已安装 .NET 6.0 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）
- 有效的 Aspose.Cells 许可证或免费评估密钥
- Visual Studio 2022（或任何支持 C# 的 IDE）
- 对 C# 语法和 Excel 公式有基本了解

除 `Aspose.Cells` 之外无需其他 NuGet 包，可通过以下方式添加：

```bash
dotnet add package Aspose.Cells
```

## 步骤 1：创建 C# 项目并引用 Aspose.Cells

新建一个控制台应用程序并添加 Aspose.Cells 引用。此步骤至关重要，因为该库提供了 `Workbook`、`Worksheet` 以及计算引擎，帮助您 **使用 C# 编写 Excel 公式**。

```csharp
// Program.cs
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // The rest of the tutorial code lives inside this method.
    }
}
```

> **为什么重要：** Aspose.Cells 抽象了底层 OpenXML 细节，让您专注于业务逻辑，而不是文件格式的琐碎问题。

## 步骤 2：创建 Excel 工作簿并获取第一个工作表

现在我们通过实例化 `Workbook` 对象 **创建 Excel 工作簿 C#**。默认工作簿包含一个工作表，我们将其取出以便后续操作。

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates a blank .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet by default
```

> **小技巧：** 如需多个工作表，可在访问之前调用 `workbook.Worksheets.Add()`。

## 步骤 3：为动态数组填充源数据

动态数组函数（如 `SORT`）需要一个源范围。我们将在 *A2:A10* 单元格中填入未排序的数字，以便 `SORT` 公式演示其行为。

```csharp
// Step 3: Fill A2:A10 with sample data
int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
for (int i = 0; i < numbers.Length; i++)
{
    worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // Row i+2, Column A (0‑based index)
}
```

> **这样做的原因：** 提供具体数据后，您即可看到 **动态数组公式示例** 的实际效果，而无需外部输入文件。

## 步骤 4：将动态数组公式写入单元格 A1

下面是 **使用 C# 编写 Excel 公式** 的核心代码。我们将 `SORT` 公式赋给单元格 *A1*。由于 `SORT` 是动态数组函数，Excel 会自动将排序结果溢出到下方单元格。

```csharp
// Step 4: Insert a dynamic array formula (SORT) into cell A1
worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";
```

> **解释：**  
> - `worksheet.Cells[0, 0]` 指向 **A1**（第 0 行，第 0 列）。  
> - 字符串 `=SORT(A2:A10)` 是标准的 Excel 公式。Aspose.Cells 会像 Excel 一样解析它，从而完整支持现代动态数组函数。

## 步骤 5：重新计算工作簿以自动填充公式结果

Aspose.Cells 在写入时不会自动重新计算公式。您必须显式触发计算，才能看到溢出的结果。

```csharp
// Step 5: Recalculate the workbook so the formula evaluates
workbook.Calculate();   // runs the calculation engine once
```

执行此调用后，单元格 **A1:A9** 将包含排序后的列表：5、7、8、14、19、21、27、33、42。

### 验证结果（预期输出）

您可以将溢出的数值打印到控制台，以确认计算成功：

```csharp
Console.WriteLine("Sorted values from A1 down:");
for (int row = 0; row < 9; row++)
{
    Console.WriteLine(worksheet.Cells[row, 0].StringValue);
}
```

**预期的控制台输出**

```
Sorted values from A1 down:
5
7
8
14
19
21
27
33
42
```

> **边缘情况说明：** 若源范围包含非数字数据，`SORT` 将按字典序排序。使用仅限数字的函数前，请务必先验证数据类型。

## 步骤 6：将工作簿保存到磁盘（可选）

持久化文件可让您在 Excel 中直观看到动态数组的效果。此步骤对公式计算本身不是必需的，但对调试和分发非常有用。

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = "SortedNumbers.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

在 Excel 365 或更高版本中打开 *SortedNumbers.xlsx* 时，您会看到从 **A1** 向下自动溢出的排序列表——这正是 **动态数组公式示例** 从 C# 生成的结果。

## 完整可运行示例

将所有代码片段组合起来，即得到完整的可运行程序：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1. Create workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2. Fill source data (A2:A10)
        int[] numbers = { 42, 7, 19, 33, 5, 27, 14, 8, 21 };
        for (int i = 0; i < numbers.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(numbers[i]); // A2:A10
        }

        // 3. Write dynamic array formula (SORT) into A1
        worksheet.Cells[0, 0].Formula = "=SORT(A2:A10)";

        // 4. Force calculation so the array spills
        workbook.Calculate();

        // 5. Display the spilled values in the console
        Console.WriteLine("Sorted values from A1 down:");
        for (int row = 0; row < 9; row++)
        {
            Console.WriteLine(worksheet.Cells[row, 0].StringValue);
        }

        // 6. Save the workbook (optional)
        string outputPath = "SortedNumbers.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

运行程序（`dotnet run`）后，您将看到排序后的数字打印在控制台，并收到文件已保存的确认信息。

## 常见问题与变体

### 如果需要使用其他动态数组函数怎么办？

只需将公式字符串替换为其他动态数组函数，例如 `=FILTER(A2:A10, B2:B10>10)` 或 `=UNIQUE(A2:A10)`。相同的 **使用 C# 编写 Excel 公式** 模式依然适用：

```csharp
worksheet.Cells[0, 0].Formula = "=UNIQUE(A2:A10)";
```

### 如何处理引用其他工作表的公式？

使用工作表名称进行引用：

```csharp
worksheet.Cells[0, 0].Formula = "=SORT('Sheet2'!A2:A10)";
```

Aspose.Cells 会在 `workbook.Calculate()` 时自动解析跨工作表引用。

### 能否关闭自动计算，稍后再手动计算？

可以。将工作簿的计算模式设为手动：

```csharp
workbook.Settings.CalcMode = CalcMode.Manual;
// ... make many changes ...
workbook.Calculate(); // call once when ready
```

在对数千个单元格进行更新后再统一计算，可显著提升性能。

## 结论

现在，您已经掌握了如何使用 Aspose.Cells **创建 Excel 工作簿 C#**、插入 **动态数组公式示例**，以及 **使用 C# 编写 Excel 公式** 并让其自动溢出结果的完整流程。完整方案涵盖了项目设置、数据准备、公式插入、强制计算、结果验证以及可选的文件保存。

接下来，您可以探索更高级的场景：链式使用多个动态数组函数、应用自定义数字格式，或将工作簿生成集成到 Web API 中。请始终在应用公式前验证输入数据，并充分利用 Aspose.Cells 强大的计算引擎，实现可靠的服务器端 Excel 处理。祝编码愉快！

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助您进一步掌握 API 功能并探索替代实现方式：

- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel Automation with Aspose.Cells .NET: Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Create Excel Workbook C# – Complete Guide with Aspose.Cells](/cells/english/net/excel-workbook/create-excel-workbook-c-complete-guide-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}