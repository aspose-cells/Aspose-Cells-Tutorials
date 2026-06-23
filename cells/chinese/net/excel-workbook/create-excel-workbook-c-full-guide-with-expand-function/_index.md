---
category: general
date: 2026-06-08
description: 使用 C# 步骤创建 Excel 工作簿，并学习在 Excel 中使用 expand 函数实现动态范围。非常适合 .NET 开发者。
draft: false
keywords:
- create excel workbook c#
- use expand function in excel
language: zh
og_description: 使用 C# 创建 Excel 工作簿并提供清晰示例，了解如何在 Excel 中使用 EXPAND 函数生成动态数组。
og_title: 使用 C# 创建 Excel 工作簿 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  headline: Create Excel Workbook C# – Full Guide with Expand Function
  type: TechArticle
- description: Create Excel workbook C# step‑by‑step and learn how to use expand function
    in Excel for dynamic ranges. Perfect for .NET developers.
  name: Create Excel Workbook C# – Full Guide with Expand Function
  steps:
  - name: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
    text: '`SEQUENCE(3)` produces a vertical array `{1;2;3}`.'
  - name: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
    text: '`EXPAND(...,5,5)` tells Excel to grow that array to 5 rows and 5 columns.'
  - name: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
    text: The result is a 5 × 5 grid where the first three rows contain the numbers
      1‑3 repeated across columns, and the remaining two rows are blank.
  - name: '**Creates an Excel workbook C#** using Aspose.Cells.'
    text: '**Creates an Excel workbook C#** using Aspose.Cells.'
  - name: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
    text: '**Uses the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5
      block.'
  - name: Adds a cotangent formula (`COT(PI()/4)`).
    text: Adds a cotangent formula (`COT(PI()/4)`).
  - name: Saves the file and optionally auto‑fits columns.
    text: Saves the file and optionally auto‑fits columns.
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells targets .NET Standard 2.0, which is compatible
      with both .NET Core and the classic Framework.
    question: Does this work with .NET Framework 4.8?
  - answer: Use `ws.Protect(ProtectionType.All, "yourPassword");` before saving.
    question: What if I need to protect the sheet?
  - answer: 'Yes—`workbook.Save(stream, SaveFormat.Xlsx);` is handy for web APIs that
      return the file as a download. --- ## TL;DR We built a **complete C# console
      app** that: 1. **Creates an Excel workbook C#** using Aspose.Cells. 2. **Uses
      the EXPAND function in Excel** to turn a 3‑row array into a 5 × 5 block.'
    question: Can I write the workbook directly to a `MemoryStream`?
  type: FAQPage
tags:
- csharp
- excel
- aspose-cells
- .net
title: 使用 C# 创建 Excel 工作簿 – 完整指南与展开功能
url: /zh/net/excel-workbook/create-excel-workbook-c-full-guide-with-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 C# – 完整指南与 EXPAND 函数

有没有想过如何 **create Excel workbook C#** 而不必与 COM interop 斗争或摆弄 XML？你并不是唯一的。在许多 .NET 项目中，我们需要导出电子表格，填入公式，并交给非技术用户。好消息是？使用像 **Aspose.Cells** 这样的现代库，整个过程轻而易举。

在本教程中，我们将演示一个完整且可运行的示例，**creates an Excel workbook C#**，插入几个公式——包括如何 **use expand function in Excel**——并保存文件，以便您可以立即在 Excel 中打开。完成后，您不仅会知道该输入 *什么*，还会了解每行代码的 *原因*，并拥有一个可以复制到任何项目的模板。

## 前提条件

- 已安装 .NET 6 SDK（或任何近期的 .NET 版本）。
- 支持 NuGet 的 IDE（Visual Studio、VS Code、Rider 等）。
- **Aspose.Cells** NuGet 包——它提供代码中使用的 `Workbook` 和 `Worksheet` 类。
- 基础的 C# 知识；不需要 Excel 相关经验。

都准备好了吗？太好了——让我们开始吧。

## 步骤 1：设置项目并添加 Aspose.Cells

首先，创建一个控制台应用并引入该库。

```bash
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

> **专业提示：** 如果您在公司网络中，可能需要配置 NuGet 代理。Aspose.Cells 包体积轻巧，安装在几秒钟内完成。

现在打开 `Program.cs`。您会看到默认的 `Main` 方法——请将其替换为下面的骨架代码。

```csharp
using System;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // All of our Excel logic will go here.
        }
    }
}
```

`using Aspose.Cells;` 行将电子表格类引入作用域。如果忘记此行，编译器会抱怨 `Workbook` 未定义——我们稍后会避免这种情况。

## 步骤 2：创建 Excel 工作簿 C# 并访问第一个工作表

项目准备就绪后，我们终于可以 **create Excel workbook C#**。`Workbook` 构造函数会创建一个全新的空工作簿，`Worksheets[0]` 索引返回默认工作表（名称为 “Sheet1”）。

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx file in memory
Worksheet ws = workbook.Worksheets[0];            // reference to the first (default) sheet
```

为什么要显式获取第一个工作表？因为许多下游 API（例如设置公式）需要 `Worksheet` 对象，而不仅仅是 `Workbook`。这也让后续阅读代码的人更清晰。

## 步骤 3：在 Excel 中使用 EXPAND 函数填充动态范围

现在登场的是本教程的亮点：**use expand function in Excel**。`EXPAND` 函数（从 Excel 365 开始可用）接受一个源数组并将其填充到指定大小。在本例中，我们将使用 `SEQUENCE(3)` 生成的 3 行垂直数组，并将其展开为 5 × 5 的块。

```csharp
// Step 3: Insert the EXPAND formula into cell A1
ws.Cells["A1"].Formula = "EXPAND(SEQUENCE(3),5,5)";
```

实际会发生什么？

1. `SEQUENCE(3)` 生成一个垂直数组 `{1;2;3}`。  
2. `EXPAND(...,5,5)` 告诉 Excel 将该数组扩展为 5 行 5 列。  
3. 结果是一个 5 × 5 的网格，前三行在各列中重复数字 1‑3，剩余两行为空。

因为我们将公式写成字符串，Excel 会在 *打开文件时* 进行求值，而不是在运行时。这意味着工作簿保持轻量，且对源数组的任何更改都会自动传播。

> **边缘情况：** 如果用户在不支持 `EXPAND` 的旧版 Excel 中打开工作簿，单元格会显示 `#NAME?`。为防止这种情况，您可以将公式包装在 `IFERROR` 中，但在现代环境下直接使用该函数是安全的。

## 步骤 4：添加余切公式以作示例

让我们再加入一个公式，展示添加数学表达式是多么简单。我们将计算 π/4 的余切，其值恰好为 `1`。

```csharp
// Step 4: Insert a cotangent calculation in cell B1
ws.Cells["B1"].Formula = "COT(PI()/4)";
```

Excel 的 `COT` 函数不像 `SIN` 或 `COS` 那样常用，但它非常适合三角函数工作流。打开工作簿时，单元格 **B1** 将显示 `1`。

## 步骤 5：保存工作簿并验证结果

如果不将文件持久化，所有工作都毫无意义。`Save` 方法会将内存中的工作簿写入磁盘。请选择一个您有写入权限的文件夹，并为文件起一个友好的名称。

```csharp
// Step 5: Save the workbook to the output folder
string outputPath = @"./output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

运行程序：

```bash
dotnet run
```

您应该会看到控制台消息确认已保存。用 Excel 打开 `output.xlsx`，您会注意到：

- 单元格 **A1:E5** 填充了展开的序列（前三行是 1、2、3，第四、五行为空）。  
- 单元格 **B1** 显示来自余切公式的值 `1`。

![生成的 Excel 工作簿截图，显示展开的数组和余切结果](/images/create-excel-workbook-csharp.png "创建 excel 工作簿 c# 示例")

*图片说明：create excel workbook c# – 已填充的电子表格视图。*

## 步骤 6：可选 – 自动调整列宽以获得更佳外观

如果您计划将文件分发给最终用户，快速的自动调整列宽可以让它看起来更专业。

```csharp
// Optional: Auto‑fit all columns in the used range
ws.AutoFitColumns(0, ws.Cells.MaxColumn);
```

此行代码遍历所有包含数据的列，并将宽度调整为最长条目的长度。这是一个小细节，但可以防止当数字宽于默认列宽时出现的 “…###” 溢出。

## 步骤 7：总结与后续步骤

恭喜——您已经掌握了如何从头 **create excel workbook c#**，并学会了 **use expand function in excel** 来生成动态数组。代码故意保持简洁，方便您复制粘贴到任何项目中，但其概念是可扩展的：

- **动态数据源：** 将 `SEQUENCE(3)` 替换为对其他范围或命名表的引用。  
- **条件格式化：** 使用 `ws.Cells["A1:E5"].Style` 根据数值添加颜色。  
- **图表和图形：** Aspose.Cells 可以嵌入图表、图片，甚至数据透视表。

随意尝试——更改 `EXPAND` 的维度，尝试 `FILTER` 或 `SORT`，或将多个公式串联。该库会处理所有这些，您无需直接操作底层的 OpenXML 格式。

---

### 常见问题

**Q: 这在 .NET Framework 4.8 上能工作吗？**  
A: 当然可以。Aspose.Cells 面向 .NET Standard 2.0，兼容 .NET Core 和经典 Framework。

**Q: 如果需要保护工作表怎么办？**  
A: 在保存之前使用 `ws.Protect(ProtectionType.All, "yourPassword");`。

**Q: 能否直接将工作簿写入 `MemoryStream`？**  
A: 可以——`workbook.Save(stream, SaveFormat.Xlsx);` 对于返回文件下载的 Web API 非常方便。

## TL;DR

我们构建了一个 **完整的 C# 控制台应用**，实现了：

1. 使用 Aspose.Cells **Creates an Excel workbook C#**。  
2. **Uses the EXPAND function in Excel** 将 3 行数组转换为 5 × 5 块。  
3. 添加余切公式 (`COT(PI()/4)`)。  
4. 保存文件并可选地自动调整列宽。

现在，您拥有了一个坚实的基础，可用于任何涉及从 .NET 生成 Excel 文件的自动化任务。祝编码愉快，愿您的电子表格永远无错误！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方式。

- [如何使用 Aspose.Cells .NET 在 Excel 中创建工作簿范围的命名范围](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [如何在 Excel 中使用 Aspose.Cells .NET 创建和使用联合范围（C# 指南）](/cells/english/net/range-management/excel-union-range-aspose-cells-net/)
- [使用 Aspose.Cells .NET 创建带图表的 Excel 工作簿 | 步骤指南](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}