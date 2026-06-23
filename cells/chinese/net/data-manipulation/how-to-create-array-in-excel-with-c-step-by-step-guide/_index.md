---
category: general
date: 2026-02-28
description: 如何使用 C# 在 Excel 中创建数组。学习生成数字、评估公式、创建 Excel 工作簿并在几分钟内保存 Excel 文件。
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: zh
og_description: 如何使用 C# 在 Excel 中创建数组。本教程展示了如何生成数字、计算公式、创建工作簿并保存文件。
og_title: 使用 C# 在 Excel 中创建数组 – 完整指南
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: 如何使用 C# 在 Excel 中创建数组 – 步骤指南
url: /zh/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 C# 创建数组 – 完整编程教程

是否曾经想过 **how to create array** 在 Excel 中使用 C# 以编程方式实现？你并不是唯一的——开发者们经常寻求一种快速生成数字块而无需手动输入的方法。在本指南中，我们将逐步演示如何 **create excel workbook**，插入一个 **generates numbers** 的公式，**evaluate the formula**，以及最终 **save excel file**，以便在 Excel 中打开并查看结果。

我们将使用 Aspose.Cells 库，因为它让我们能够在无需安装 Excel 的情况下完全控制公式和计算。如果你更喜欢其他库，概念保持不变——只需替换 API 调用即可。

## 本教程涵盖内容

- 设置带有所需 NuGet 包的 C# 项目。  
- 创建新的工作簿（即 *create excel workbook* 部分）。  
- 编写使用 `SEQUENCE` 和 `WRAPCOLS` 构建 4 行 × 3 列数组的公式。  
- 强制引擎 **evaluate the formula**，使数组生成。  
- 将工作簿保存到磁盘（**save excel file**）并检查输出。  

完成后，你将拥有一个可运行的程序，生成如下所示的 Excel 工作表：

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![How to create array in Excel – 运行 C# 代码后生成的工作表](image.png)

（图片 alt 文本包含主要关键词 “how to create array”，用于 SEO。）

## 前提条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Framework 4.6+）。  
- Visual Studio 2022 或任何你喜欢的编辑器。  
- NuGet 包 **Aspose.Cells**（提供免费试用）。  

无需额外安装 Excel，因为 Aspose.Cells 在内部提供计算引擎。

## 步骤 1：设置项目并导入 Aspose.Cells

首先，创建一个控制台应用并添加该库：

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

现在打开 **Program.cs** 并添加命名空间：

```csharp
using Aspose.Cells;
```

*Why this matters*：导入 `Aspose.Cells` 为我们提供了 `Workbook`、`Worksheet` 和计算类，后续我们将需要它们来 **create excel workbook** 并处理公式。

## 步骤 2：创建工作簿和目标工作表

我们需要一个全新的工作簿对象；第一个工作表（`Worksheets[0]`）将承载我们的数组。

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*Explanation*：`Workbook` 类代表整个 Excel 文件。默认情况下它包含一个工作表，非常适合简单演示。如果需要更多工作表，可以稍后调用 `workbook.Worksheets.Add()`。

## 步骤 3：编写一个 **Generates Numbers** 并形成数组的公式

Excel 的动态数组函数（`SEQUENCE` 和 `WRAPCOLS`）让我们能够通过单个公式生成一块数值。以下是我们将要赋值的完整字符串：

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*Why this works*：  
- `SEQUENCE(12,1,1,1)` 返回 1‑12 的垂直列表。  
- `WRAPCOLS(...,3)` 将该列表按三列填充，并自动溢出到后续行。  

如果在 Excel 中 **未** 先评估公式就打开工作簿，你只会在 `A1` 中看到公式文本。下一步将强制进行计算。

## 步骤 4：**Evaluate the Formula** 使数组生成

Aspose.Cells 在写入时不会自动重新计算公式，因此我们需要显式调用计算引擎：

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*What’s happening*：`Calculate()` 会遍历所有包含公式的单元格，计算其结果并写回数值。这就是本教程中 **how to evaluate formula** 的部分。调用后，A1:C4 单元格将包含 1‑12 的数字，正如原生 Excel 的溢出效果。

## 步骤 5：**Save Excel File** 并验证结果

最后我们将工作簿保存到磁盘：

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

在 Excel 中打开 `output.xlsx`，你会看到我们生成的 4 × 3 数组。如果使用的 Excel 版本早于 365/2019，动态数组函数将无法识别——Aspose.Cells 仍会写入已计算的数值，文件仍可使用。

*Pro tip*：如果需要强制使用特定格式，请使用 `SaveFormat.Xlsx`，例如 `workbook.Save(outputPath, SaveFormat.Xlsx);`。

## 完整可运行示例（复制粘贴即可）

下面是完整程序。将其粘贴到 **Program.cs**，运行 `dotnet run`，即可在项目文件夹中得到 `output.xlsx`。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**Expected output**（控制台）：

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

打开文件，你会看到数字 1‑12 按照前面所示的方式排列。

## 变体与边缘情况

### 1. 旧版 Excel 不支持动态数组

如果你的用户使用 Excel 2016 或更早版本，`SEQUENCE` 和 `WRAPCOLS` 不存在。一个快速的变通办法是直接在 C# 中生成数字并写入：

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

此手动循环实现相同的结果，虽然代码更多。**how to generate numbers** 的概念保持不变。

### 2. 更改数组大小

想要一个 5 × 5 的 1‑25 数字网格？只需调整 `SEQUENCE` 参数和 `WRAPCOLS` 的列数：

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. 使用命名范围以便复用

你可以将溢出的范围赋予一个名称，以便后续公式使用：

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

现在任何其他工作表都可以直接引用 `MyArray`。

## 常见陷阱及避免方法

| 常见问题 | 原因 | 解决方案 |
|---|---|---|
| **Formula not spilling** | `Calculate()` omitted or called before setting the formula. | Always call `workbook.Calculate()` **after** assigning the formula. |
| **File saved but empty** | Using `SaveFormat.Csv` accidentally. | Use `SaveFormat.Xlsx` or omit the format to let Aspose infer. |
| **Dynamic

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}