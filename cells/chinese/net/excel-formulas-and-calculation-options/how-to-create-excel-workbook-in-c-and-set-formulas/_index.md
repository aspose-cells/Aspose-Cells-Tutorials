---
category: general
date: 2026-10-01
description: 在 C# 中快速创建 Excel 工作簿，学习如何设置公式、计算余切以及在 Aspose.Cells 中使用 PI 函数。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: zh
lastmod: 2026-10-01
og_description: 使用 Aspose.Cells 在 C# 中创建 Excel 工作簿。学习如何设置公式、使用 PI 函数以及仅需几步即可计算余切。
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: 在 C# 中创建 Excel 工作簿 – 设置公式并计算余切
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中创建 Excel 工作簿并设置公式
url: /zh/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建 Excel 工作簿并设置公式

如果你需要 **创建 Excel 工作簿 C#** 的代码来向单元格写入公式，本指南将一步步演示。你将看到如何在工作表中设置公式、使用内置的 PI 函数，以及计算角度的余切——全部使用 Aspose.Cells。

本教程涵盖了从初始化工作簿到获取计算结果的全部过程，你可以直接将完整示例复制到自己的项目中，无需补任何缺失的部分。

## 先决条件

在开始之前，请确保你已经具备：

* 已安装 .NET 6.0 或更高版本  
* 有效的 Aspose.Cells 许可证（或临时评估密钥）  
* Visual Studio 2022 或任意你喜欢的 C# IDE  

除 `Aspose.Cells` 之外，无需额外的 NuGet 包。

## 在 C# 中创建 Excel 工作簿

第一步是实例化一个新的 `Workbook` 对象。该对象在内存中表示整个 Excel 文件，并提供对其工作表的访问。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

以这种方式创建工作簿可确保文件已准备好进行后续操作，例如添加数据、设置单元格样式或写入公式。

## 使用 PI 函数在单元格中设置公式

现在你将 **向单元格写入公式** 到 A1。该公式使用 `PI()` 函数提供常数 π，并使用 `COT` 函数计算其余切。

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*为什么重要*：`PI()` 是 Excel 的内置函数，返回 π 的数值。将其除以 4 即得到 45°，`COT` 返回该角度的余切。这演示了 **如何在 C# 中的 Excel 公式里使用 pi 函数**。

## 如何使用 Aspose.Cells 计算余切

如果你想了解 **如何计算 cot** 而不手动转换角度，`COT` 函数会帮你完成大部分工作。它接受弧度制的角度值，因此可以与 `PI()` 结合使用来处理常见角度。

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

运行程序后会输出：

```
Cotangent of PI/4 = 1
```

因为 `COT(π/4)` 等于 1，输出确认公式已正确 **在单元格中设置公式** 并得到计算结果。

## 向单元格写入公式 – 其他提示

* **多个公式**：你可以使用相同的 `Formula` 属性为任意单元格分配公式，例如 `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`。  
* **国际化设置**：Aspose.Cells 会遵循工作簿的区域设置，函数名称始终保持英文（`PI`、`COT`），不受用户地区设置影响。  
* **性能**：如果需要一次性设置成千上万条公式，建议批量处理并在最后调用一次 `workbook.Calculate()`，以避免重复的重新计算。

## 完整可运行示例

下面是可以直接复制到控制台项目中的完整程序。它包含所有必需的 `using` 语句，并演示了从工作簿创建到结果输出的完整工作流。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**运行程序时的预期输出**：

```
Cotangent of PI/4 = 1
```

生成的 `CotExample.xlsx` 文件在 A1 单元格中包含公式，你可以在 Excel 中打开并看到相同的结果。

## 结论

现在你已经掌握了如何编写 **创建 Excel 工作簿 C#** 的代码来写入公式、使用 `PI` 函数，以及使用 Aspose.Cells **计算 cot**。示例覆盖了整个生命周期：工作簿创建、**在单元格中设置公式**、重新计算以及结果获取。

接下来你可以进一步探索：

* 将 **写入公式到单元格** 用于更复杂的计算，如财务模型。  
* 将 **在单元格中设置公式** 与条件格式相结合，以突出显示结果。  
* 将 **如何使用 pi 函数** 与三角函数图表结合，用于科学报告。

欢迎尝试不同的角度、函数和工作表布局。掌握 C# 中的公式处理后，你就能构建全自动的 Excel 报表流水线。祝编码愉快！


## 接下来你应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，帮助你在自己的项目中进一步使用 API 功能并探索替代实现方式。每篇资源都提供了完整的可运行代码示例和逐步解释。

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}