---
category: general
date: 2026-07-03
description: 创建 Excel 工作簿并以编程方式写入数据。学习如何以编程方式生成 Excel 文件、将值写入特定的 Excel 单元格，以及将 Excel
  工作簿保存到目录中。
draft: false
keywords:
- create excel workbook and write data
- generate excel file programmatically
- put value into specific excel cell
- save excel workbook to directory
language: zh
og_description: 在 C# 中创建 Excel 工作簿并写入数据。本指南展示了如何以编程方式生成 Excel 文件、将值写入特定的 Excel 单元格，以及将
  Excel 工作簿保存到目录中。
og_title: 创建 Excel 工作簿并写入数据 – 完整 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create excel workbook and write data programmatically. Learn how to
    generate excel file programmatically, put value into specific excel cell, and
    save excel workbook to directory.
  headline: Create Excel Workbook and Write Data in C# – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create excel workbook and write data programmatically. Learn how to
    generate excel file programmatically, put value into specific excel cell, and
    save excel workbook to directory.
  name: Create Excel Workbook and Write Data in C# – Full Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: '| A | B | C | |-------|---|---| | ["A","B","C"] | | |'
  - name: Writing Multiple Cells
    text: 'If you need to write more than one value, simply repeat the `PutValue`
      call with different addresses:'
  - name: Using a Different Sheet
    text: 'You can add a new sheet and target it:'
  - name: Handling Large JSON Payloads
    text: When the JSON string exceeds typical cell limits (32,767 characters), consider
      storing it in a hidden sheet or splitting it across cells. Excel will truncate
      anything longer, so plan accordingly.
  - name: Saving to a Stream (e.g., HTTP Response)
    text: 'Instead of writing to disk, you can stream the workbook directly to the
      client:'
  type: HowTo
tags:
- C#
- Excel Automation
- Aspose.Cells
title: 在 C# 中创建 Excel 工作簿并写入数据 – 完整分步指南
url: /zh/net/excel-workbook/create-excel-workbook-and-write-data-in-c-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿并在 C# 中写入数据 – 完整分步指南

有没有想过如何在不打开 Excel 的情况下 **create excel workbook and write data**？你并不是唯一有此需求的人——开发者经常需要直接将 JSON、日志或计算结果导入电子表格。好消息是，只需几行 C# 代码，你就可以生成一个 Excel 文件，将 JSON 数组放入单元格，并将文件保存到任意位置。

在本教程中，我们将完整演示整个过程：从初始化工作簿、**put value into specific excel cell**，到最终 **save excel workbook to directory**。完成后，你将拥有一个可复用的代码片段，可直接嵌入任何 .NET 项目。没有冗余，只提供可立即运行的实用代码。

## 你将学到的内容

- 如何使用 Aspose.Cells 库（或任何兼容的 API）**generate excel file programmatically**。
- **put value into specific excel cell** 的完整步骤——包括处理 JSON 字符串。
- 使用自定义文件名**save excel workbook to directory** 的方法。
- 常见陷阱（如忘记释放对象）以及保持代码整洁的技巧。
- 一个完整的、可直接 **copy‑paste** 到 Visual Studio 的 **ready‑to‑run** 示例。

> **Prerequisites**  
> • .NET 6.0 或更高（代码在 .NET Core 和 .NET Framework 上均可运行）  
> • NuGet 包 `Aspose.Cells`（提供免费试用）  
> • 对 C# 语法有基本了解

让我们动手实践吧。

![Diagram showing the flow to create excel workbook and write data programmatically](excel-workflow.png)

*Image alt text: 创建 Excel 工作簿并写入数据的流程图*

## 步骤 1：设置项目并添加 Excel 库

要 **generate excel file programmatically**，首先需要一个能够处理 Excel 文件格式的库。虽然可以使用 `Microsoft.Office.Interop.Excel`，但它要求服务器上安装 Excel——这对大多数 Web 应用来说是不可接受的。我们改用 **Aspose.Cells**，它是纯托管的 .NET 库。

```csharp
// Install via NuGet Package Manager Console
// PM> Install-Package Aspose.Cells

using Aspose.Cells;   // Namespace that contains Workbook, Worksheet, etc.
using System;        // For basic .NET types
```

> **Pro tip:** 如果你在 CI/CD 流水线中，建议将包引用添加到 `.csproj`，这样构建时会自动恢复该依赖。

## 步骤 2：**Create Excel Workbook and Write Data** – 初始化工作簿

库准备好后，让我们 **create excel workbook and write data**。可以把工作簿想象成一本笔记本；第一页（工作表）会自动为你创建。

```csharp
// Step 2: Initialize a new workbook (the notebook)
Workbook workbook = new Workbook();                // Creates an empty .xlsx file in memory
Worksheet worksheet = workbook.Worksheets[0];      // Grab the first (default) worksheet
```

为什么要获取 `Worksheets[0]`？因为 Aspose 默认创建一个名为 “Sheet1” 的工作表，而大多数简单任务只需要这一个工作表。如果需要更多，可以稍后添加。

## 步骤 3：**Put Value into Specific Excel Cell** – 写入 JSON 数组

假设你有一个 JSON 数组 `["A","B","C"]`，想要存入单元格 **A1**。这正是 **put value into specific excel cell** 的典型场景。

```csharp
// Step 3: Define the JSON string you want to store
string jsonArray = "[\"A\",\"B\",\"C\"]";

// Step 4: Write the JSON string into cell A1
worksheet.Cells["A1"].PutValue(jsonArray);
```

需要注意的几点：

- `PutValue` 会自动检测数据类型。因为我们传入的是字符串，它会以文本形式存储。
- 如果需要存储数字、日期或公式，`PutValue` 也能处理——只需传入相应的 .NET 类型。

## 步骤 4：**Save Excel Workbook to Directory** – 保存文件

最后一步是 **save excel workbook to directory**。你可以将文件保存到应用拥有写权限的任何位置——本地磁盘、网络共享，甚至是云挂载的文件夹。

```csharp
// Step 5: Define the output path (adjust as needed)
string outputPath = @"C:\Temp\SmartMarker.xlsx";

// Step 6: Save the workbook to the specified file
workbook.Save(outputPath);
```

当 `Save` 完成后，你会在 `C:\Temp` 看到一个完整的 `SmartMarker.xlsx` 文件。用 Excel 打开时，JSON 字符串会整齐地出现在单元格 A1 中。

### 预期输出

|   A   | B | C |
|-------|---|---|
| ["A","B","C"] |   |   |

就这样——你的 JSON 现在已经成为 Excel 电子表格的一部分，准备好进行后续处理或人工审阅。

## 完整可运行示例（复制粘贴即可）

下面是 **complete, runnable program**，将所有步骤串联起来。你可以将其放入新的控制台应用项目并按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;   // Make sure Aspose.Cells is installed via NuGet

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook and get its first worksheet
            Workbook workbook = new Workbook();                 // create excel workbook and write data
            Worksheet worksheet = workbook.Worksheets[0];       // first (default) sheet

            // 2️⃣ Define the JSON array you want to store
            string jsonArray = "[\"A\",\"B\",\"C\"]";

            // 3️⃣ Write the JSON string into cell A1 (put value into specific excel cell)
            worksheet.Cells["A1"].PutValue(jsonArray);

            // 4️⃣ Save the workbook to a file (save excel workbook to directory)
            string outputPath = @"C:\Temp\SmartMarker.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Excel file successfully saved to: {outputPath}");
        }
    }
}
```

**Run it**，你会看到控制台输出确认文件位置。打开文件，验证单元格 **A1** 中包含 JSON 数组。

## 常见变体与边缘情况

### 写入多个单元格

如果需要写入多个值，只需对不同的地址重复调用 `PutValue`：

```csharp
worksheet.Cells["B2"].PutValue(123);          // numeric value
worksheet.Cells["C3"].PutValue(DateTime.Now); // date/time
```

### 使用不同的工作表

你可以添加一个新工作表并将其设为目标：

```csharp
int newSheetIndex = workbook.Worksheets.Add();
Worksheet newSheet = workbook.Worksheets[newSheetIndex];
newSheet.Name = "DataExport";
newSheet.Cells["A1"].PutValue(jsonArray);
```

### 处理大型 JSON 负载

当 JSON 字符串超过典型单元格限制（32,767 个字符）时，考虑将其存放在隐藏工作表中或拆分到多个单元格。Excel 会截断超长内容，请相应规划。

### 保存到流（例如 HTTP 响应）

如果不想写入磁盘，可以直接将工作簿流式传输给客户端：

```csharp
using (MemoryStream ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    // Return ms.ToArray() as a file download in ASP.NET Core
}
```

## 专业技巧与注意事项

- **Dispose of the workbook** 当完成后，尤其是在高吞吐服务中。虽然 Aspose 已经很好地管理内存，但使用 `using` 块包装可以避免泄漏：

  ```csharp
  using (Workbook workbook = new Workbook())
  {
      // ... work with workbook
  }
  ```

- **File permissions** 很重要。如果 `Save` 抛出 `UnauthorizedAccessException`，请确认文件夹存在且进程用户拥有写权限。
- **Version compatibility**：Aspose.Cells 23.x 兼容 .NET 6、.NET 5 和 .NET Framework 4.6+。始终引用最新的稳定 NuGet 版本以获取安全补丁。

## 回顾

我们已经介绍了从零开始 **create excel workbook and write data** 所需的全部内容：

1. 安装并引用 Aspose.Cells。  
2. 通过实例化 `Workbook` **generate excel file programmatically**。  
3. 使用 `Cells["A1"].PutValue` **put value into specific excel cell**。  
4. 使用 `workbook.Save` **save excel workbook to directory**。

这四步流程让你能够自动化报表、导出日志或为下游分析管道提供数据——全部无需打开 Excel 界面。

## 接下来可以做什么？

- **Formatting cells**（字体、颜色、边框）以使输出更精致。  
- **Adding tables or charts** 以获得更丰富的可视化。  
- **Reading existing workbooks** 以更新数据，而不是每次都创建新文件。

这些主题都直接基于我们刚才奠定的基础，欢迎继续深入探索。

---

*祝编码愉快！如果遇到问题或有扩展想法，欢迎在下方留言——让我们保持交流。*

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，构建在本教程演示的技巧之上。每篇资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [如何使用 Aspose.Cells for .NET 创建并保存为 ODS 的 Excel 工作簿](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [创建并保存 Excel 工作簿为 PDF（Aspnet Aspose Cells）](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [创建并保存 Excel 工作簿（Aspose Cells .NET）](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}