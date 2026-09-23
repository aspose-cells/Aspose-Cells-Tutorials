---
category: general
date: 2026-03-21
description: 使用 C# 创建 Excel 工作簿，并学习如何向 Excel 添加批注，使用智能标记自动填充批注。面向开发者的逐步指南。
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: zh
og_description: 使用 C# 创建 Excel 工作簿，快速向 Excel 添加批注，然后使用 Smart Markers 填充批注。完整教程及代码。
og_title: 创建 Excel 工作簿 C# – 添加和填充批注
tags:
- C#
- Excel automation
- Aspose.Cells
title: 创建 Excel 工作簿 C# – 添加并填充带智能标记的批注
url: /zh/net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 C# – 添加并填充带有智能标记的批注

是否曾经需要 **create Excel workbook C#** 并想知道如何嵌入一个能够自动更新的批注？你并不是唯一的需求者。在许多报表场景中，你希望单元格批注显示类似 *“Created by Alice on 2024‑07‑15”*，而不必每次都硬编码姓名或日期。  

在本教程中，我们将准确展示 **how to add comment to Excel**，随后展示 **how to fill comment** 使用 Aspose.Cells 的 Smart Markers。完成后，你将拥有一个可直接运行的程序，能够创建工作簿、注入动态批注并保存文件——只需几个简洁的步骤。

> **你将获得：** 一个完整的、可编译的 C# 控制台应用程序，对每行代码的解释，常见陷阱的提示，以及扩展方案的思路。

## 前提条件

- .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 和 .NET Framework）  
- Visual Studio 2022 或你喜欢的任何 IDE  
- **Aspose.Cells for .NET** NuGet 包 (`Install-Package Aspose.Cells`) – 该库提供下面使用的 `Workbook`、`Worksheet` 和 `SmartMarkerProcessor` 类。  
- 对 C# 语法有基本了解 – 如果你写过 `Console.WriteLine`，就可以开始了。

既然前期准备工作已经完成，让我们开始吧。

![Create Excel workbook C# example screenshot](excel-workbook.png "Create Excel workbook C# example")

## 步骤 1：初始化新工作簿 – 创建 Excel 工作簿 C# 基础

首先我们需要一个全新的工作簿对象。把 `Workbook` 看作空白画布；没有它就无法放置任何单元格、行或批注。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**为什么这很重要：** `Workbook` 会自动创建默认工作表，因此除非需要额外的标签页，否则无需调用 `Add`。访问 `Worksheets[0]` 是开始填充数据的最快方式。

## 步骤 2：插入智能标记批注 – 如何使用标记添加批注

接下来我们在单元格 **B2** 中放置一个批注，里面包含 Smart Marker 标记（`«UserName»` 和 `«CreatedDate»`）。这些标记稍后会被实际值替换。

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**说明：**  
- `CreateComment()` 在不存在批注时创建批注对象；如果已存在则返回已有的批注。  
- `Note` 属性保存可见文本。将占位符用 `« »` 包裹，告诉 Aspose.Cells 这些是 **Smart Markers** ——可以一次性替换的占位符。

> **专业提示：** 如果需要多行批注，可在字符串中使用 `\n`，例如 `"Line1\nLine2"`。

## 步骤 3：准备数据对象 – 动态填充批注

Smart Markers 需要数据源。在 C# 中最简便的方式是使用与占位符名称匹配的匿名类型。

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**为什么使用匿名类型？**  
它轻量、无需额外的类文件，并且属性名（`UserName`、`CreatedDate`）与标记名称完全对应。如果你更喜欢强类型模型，只需创建一个具有相同属性的类即可。

## 步骤 4：处理智能标记 – 使用数据对象填充批注

现在魔法出现了。`SmartMarkerProcessor` 会扫描工作簿中所有的 `«…»` 标记，并用 `markerData` 中的值进行替换。

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**内部原理是什么？**  
`SmartMarkerProcessor` 会遍历每个单元格、批注、页眉等，查找 `«Token»` 模式。找到后，它使用反射读取 `markerData` 中对应的属性并写回值。无需手动循环。

## 步骤 5：保存工作簿 – 填充 Excel 批注并持久化文件

最后我们将工作簿写入磁盘。此时批注内容类似于 *“Created by Alice on 03/21/2026 10:15 AM”*。

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**结果验证：** 在 Excel 中打开 `CommentFilled.xlsx`，将鼠标悬停在单元格 **B2** 上，即可看到包含实际用户名和时间戳的批注。以后运行时无需再改动代码，只需更改 `markerData` 的值。

---

## 常见变体与边缘情况

### 使用自定义日期格式

如果希望日期采用 `yyyy‑MM‑dd` 格式，请调整数据对象：

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### 添加多个批注

你可以对其他单元格重复 **步骤 2**。每个批注可以拥有自己的标记集合，若信息通用也可以共享相同的标记。

### 使用已有工作簿

不要使用 `new Workbook()`，而是加载已有文件：

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

其余步骤保持不变——Smart Markers 同样适用于新建和已有的文件。

### 处理空值

如果某个标记可能缺失，可将属性包装为可空类型或提供回退值：

```csharp
UserName = user?.Name ?? "Unknown"
```

当源为 `null` 时，处理器会插入 *“Unknown”*。

## 完整可运行示例（复制粘贴即用）

下面是 **完整程序**，你可以直接放入控制台应用项目并立即运行（只需将 `YOUR_DIRECTORY` 替换为实际的文件夹路径）。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

运行程序，打开生成的文件，即可在单元格 **B2** 中看到动态批注。很简单，对吧？

## 常见问题解答（FAQ）

**Q: 这在 .NET Framework 4.7 上能工作吗？**  
A: 当然可以。Aspose.Cells 支持 .NET Framework 4.0 及以上以及 .NET Core/5/6/7。只需引用相应的 DLL 或 NuGet 包。

**Q: 我能将此方法用于数据验证或条件格式化吗？**  
A: Smart Markers 主要用于向单元格、批注、页眉和页脚插入值。对于条件格式化，仍需使用常规的 `Style` API。

**Q: 如果需要在 **不同** 的工作表上添加批注怎么办？**  
A: 获取目标工作表 (`workbook.Worksheets["MySheet"]`) 并在该工作表的单元格上重复 **步骤 2**。

## 后续步骤与相关主题

- **How to add comment to Excel** 程序化地为多个单元格添加批注（循环遍历范围）。  
- **Fill Excel comment** 使用来自数据库的数据（将 `DataTable` 作为 Smart Markers 的数据源）。  
- 探索 **Smart Marker arrays** 以自动生成表格。  
- 了解 **Aspose.Cells styling**，以设置批注的字体、颜色和大小。

尝试这些代码片段，替换数据源，你将快速掌握在任何 Excel 自动化场景中 **how to fill comment** 的技巧。

### 总结

我们刚刚完整演示了使用 Smart Markers **create excel workbook c#**、**add comment to excel** 和 **fill excel comment** 的全过程。该方案简洁、可复用，已可投入生产。

试一试，调整占位符，让库来完成繁重的工作。如果遇到任何问题，欢迎在下方留言——祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}