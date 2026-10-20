---
category: general
date: 2026-10-10
description: 在 C# 中创建 Excel 工作簿，并使用 WRAPCOLS 函数将数组数据拆分为列。遵循完整的逐步指南，提供可运行的代码。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: zh
lastmod: 2026-10-10
og_description: 在 C# 中创建 Excel 工作簿并使用 WRAPCOLS 函数将数组数据拆分到列中。本指南展示完整代码并解释每一步。
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: 在 C# 中创建 Excel 工作簿并使用 WRAPCOLS 拆分数据
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中创建 Excel 工作簿并使用 WRAPCOLS 拆分数据
url: /zh/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建 Excel 工作簿并使用 WRAPCOLS 拆分数据

如果您需要**以编程方式创建 Excel 工作簿**，本指南将一步步演示如何实现，并说明如何使用 `WRAPCOLS` 函数将**数组数据**拆分到多列中。您将获得一个完整、可运行的示例，生成的 `.xlsx` 文件会将数据分布到三列。

本教程涵盖您所需的一切：必备的 NuGet 包、每行代码、`WRAPCOLS` 公式的工作原理，以及如何针对不同的数组大小或列数进行适配。阅读完毕后，您即可在任何生成 Excel 文件的 C# 项目中嵌入**使用 wrapcols 函数**的技术。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 .NET 6.0 SDK 或更高版本  
* 一个 C# IDE（Visual Studio、VS Code、Rider 等）  
* **Aspose.Cells for .NET** NuGet 包——本示例中使用的 `Workbook` 类即来自该库  

您无需安装 Office；Aspose.Cells 会直接写入 `.xlsx` 文件。

## 第一步 – 创建 Excel 工作簿

首要任务是实例化一个新的工作簿对象，并获取对第一个工作表的引用。这一步是后续所有操作的基础。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` 代表整个文件，而 `Worksheet` 代表单个工作表。将工作簿创建在内存中可以避免磁盘 I/O，直到您显式保存为止。

## 第二步 – 使用 WRAPCOLS 拆分数组列

接下来，您将在 **A1** 单元格中放置一个使用 `WRAPCOLS` 的公式。该函数接受两个参数：源数组和希望数组换行的列数。

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**工作原理说明：**`WRAPCOLS` 将平面数组 `{1,2,3,4,5,6}` 按行填充工作表，每行生成三列。第一个参数可以是任意 Excel 数组文字、命名范围或动态数组公式。第二个参数（`3`）告诉 Excel 在生成多少列后换到下一行。

### 使用不同数据类型的示例

`WRAPCOLS` 并不限于数字。您可以拆分文本、日期或混合类型的数据：

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

当源数组包含字符串时，Excel 会自动将结果视为文本单元格。这种灵活性让您能够**excel 公式拆分数据**用于报表、仪表盘或数据迁移任务。

## 第三步 – 计算公式以填充工作表

公式在工作簿中以字符串形式存储，直到您调用计算。调用 `CalculateFormula` 会强制求值，并将结果写入单元格。

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

如果不调用此方法，保存的文件只会包含公式文本，而不是计算后的数值。该方法会遍历整个工作簿，因此您可以在其他位置放置额外公式，并通过一次调用全部解析。

## 第四步 – 保存工作簿以查看结果

最后，将工作簿写入磁盘。请选择您拥有写入权限的文件夹，并为文件取一个明确的名称。

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

在 Excel（或任何兼容的查看器）中打开 `output.xlsx`，您会看到：

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

如果使用了混合类型示例，第 3、4 行将相应显示文本和数字。

## 高级变体与边缘情况处理

### 运行时动态列数

列数常常取决于用户输入。您可以动态构建公式字符串：

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### 大数组与性能

`WRAPCOLS` 能处理成千上万的元素，但在单个单元格中评估极大数组可能会增加计算时间。如果出现卡顿：

* 将源数组拆分为更小的块，并分别写入不同的起始单元格。  
* 使用 `WorkbookSettings` 启用多线程计算：

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### 处理空单元格

如果源数组包含空字符串 (`""`) 或 `NULL` 值，`WRAPCOLS` 会插入空白单元格，保持列布局不变。这在需要为后续数据录入预留占位列时非常有用。

### 使用命名范围代替文字数组

为提升可维护性，您可以定义一个包含源数据的命名范围，然后在公式中引用它：

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

这样公式就直接读取工作表中的数据，使得在**如何使用 wrapcols**进行动态报表时更加灵活。

## 常见坑点与专业提示

* **不要省略第二个参数。** `WRAPCOLS(array)` 未指定列数时只会返回单列，失去拆分数据的意义。  
* **避免混用数组维度。** 源数组必须是一维的；提供二维数组（例如 `{ {1,2},{3,4} }`）会触发 `#VALUE!` 错误。  
* **计算后再保存。** 若在 `CalculateFormula` 之前调用 `wb.Save`，文件只会包含公式文本。  
* **检查文件权限。** 在受限环境（如 ASP.NET）下运行时，确保进程身份有权写入目标文件夹。  

## 完整可运行示例

下面是完整的程序代码，您可以直接复制、粘贴并运行。示例包含所有引用、错误处理以及注释。

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

运行程序后会生成 `output.xlsx`，其中包含三个独立区域，演示了使用 `WRAPCOLS` **excel 公式拆分数据** 的效果。

## 结论

现在，您已经掌握了在 C# 中**创建 Excel 工作簿**以及**使用 wrapcols 函数**高效**拆分数组列**的技巧。实例化 `Workbook`、插入 `WRAPCOLS` 公式、计算并保存的主要步骤，构成了任何需要将数据分布到多列的自动化任务的可复用模式。

接下来您可以：

* 将 `WRAPCOLS` 与其他动态数组函数（如 `FILTER`、`SORT`）组合使用。  
* 从数据库导出大数据集，让 Excel 自动处理布局。  
* 构建用户驱动的报表，列数通过 UI 控件进行选择。

尝试不同的数组来源、列数以及额外公式，进一步扩展此基础。祝编码愉快！


## 接下来该学习什么？

以下教程与本指南紧密相关，进一步深化所示技术。每篇资源均提供完整可运行的代码示例和逐步解释，帮助您掌握更多 API 功能并探索在项目中的替代实现方式。

- [如何在 C# 中使用 WRAPCOLS – 使用包装函数创建 Excel 工作簿](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [创建 Excel 工作簿 – 使用 WRAPCOLS 将数组转换为矩阵](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [C# 创建 Excel 工作簿 – 步骤指南](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}