---
category: general
date: 2026-11-16
description: 使用 SmartMarker 从 JSON 创建 Excel。了解如何将 JSON 转换为 Excel、在 Excel 中嵌入 JSON，并在几分钟内将工作簿保存为
  xlsx。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: zh
lastmod: 2026-11-16
og_description: 快速从 JSON 创建 Excel。本教程展示如何将 JSON 转换为 Excel、在 Excel 中嵌入 JSON，以及使用 Aspose.Cells
  将工作簿保存为 xlsx。
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: 使用 SmartMarker 从 JSON 创建 Excel – 步骤式 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: 在 C# 中使用 SmartMarker 从 JSON 创建 Excel
url: /zh/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 SmartMarker 在 C# 中从 JSON 创建 Excel

如果您需要在 .NET 项目中**从 JSON 创建 Excel**，本指南提供了一个完整、可运行的解决方案。使用 Aspose.Cells 的 Smart Marker 处理器，您可以**将 JSON 转换为 Excel**，将 JSON 字符串直接嵌入单元格，并**保存工作簿为 xlsx**，无需编写任何手动解析代码。

您将看到如何注册 JSON 数据源、插入一个将整个数组输出为单个 JSON 字符串的 Smart Marker、处理工作表，最后将文件写入磁盘。教程结束时，您可以生成一个 Excel 文件，其中原始 JSON 负载位于单元格 A1，准备好用于下游处理或报告。

## 前提条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7+）
- Aspose.Cells for .NET（NuGet 包 `Aspose.Cells`）
- 基本的 C# 与 JSON 格式知识
- Visual Studio 或 VS Code 等 IDE

## 第一步：设置项目并导入命名空间

创建一个新的控制台应用程序并添加 Aspose.Cells 包：

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

然后在 `Program.cs` 顶部加入所需的命名空间：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**为什么？**  
`Aspose.Cells` 提供工作簿模型，而 `Aspose.Cells.SmartMarkers` 包含解释工作表中 `&=` 标记的 `SmartMarkerProcessor` 类。

## 第二步：定义 JSON 数据源

将 JSON 字符串放入变量中。本例中我们使用一个订单数组：

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**为什么？**  
Smart Marker 可以处理任何格式正确的 JSON。将 JSON 保存在字符串中可以直接注册，无需在磁盘上准备文件。

## 第三步：使用 SmartMarkerProcessor 注册 JSON 数据

创建 `SmartMarkerProcessor` 实例，并将 JSON 字符串关联一个稍后在工作表中引用的名称：

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**为什么？**  
`RegisterJsonDataSource` 会解析 JSON 并将其层次结构提供给 Smart Marker。名称 `"OrdersJson"` 成为标记表达式中的根对象。

## 第四步：创建工作簿并插入 Smart Marker

实例化一个新工作簿，获取其第一个工作表，并在单元格 A1 中写入一个 Smart Marker，以输出整个 `Orders` 数组为单个 JSON 字符串：

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**为什么？**  
表达式 `OrdersJson.Orders.ArrayAsSingle` 告诉 Smart Marker 取 `Orders` 数组并重新序列化为 JSON，将结果放入目标单元格。这是**在 Excel 中嵌入 JSON**的最直接方式。

## 第五步：处理工作表

运行处理器，使其用实际的 JSON 字符串替换标记：

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**为什么？**  
处理过程会检查每个单元格中的 `&=` 标记，根据已注册的数据源求值，并将求值结果写回工作表。

## 第六步：将工作簿保存为 .xlsx 文件

最后，将工作簿写入磁盘。将路径修改为您有写入权限的文件夹：

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**为什么？**  
`SaveFormat.Xlsx` 确保文件以现代的 Office Open XML 格式存储，满足**保存工作簿 xlsx**的需求。

## 完整源代码

将所有部分组合在一起，下面是完整的、可直接运行的程序：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Excel 中的预期输出

打开 `JsonArraySingleCell.xlsx`。单元格 A1 将包含：

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

该 JSON 字符串是原始 `Orders` 数组的紧凑表示，便于在后续基于 Excel 的工作流中传输或消费。

## 常见变体和边缘情况

| 情形 | 调整 |
|-----------|------------|
| **多个 JSON 对象** | 使用不同的名称注册每个对象（例如 `processor.RegisterJsonDataSource("CustomerJson", customerJson);`），并在标记中分别引用。 |
| **在单元格中使用美化的 JSON** | 使用 `ArrayAsSinglePretty` 选项：`ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **大型 JSON 负载** | 考虑将 JSON 写入隐藏工作表，或使用 `DataTable` 转换以获得更好性能。 |
| **在多个单元格中嵌入 JSON** | 在其他单元格放置不同的标记，例如 `&=OrdersJson.Orders[0].Id` 以提取单个字段。 |

**专业提示：** 处理非常大的 JSON 时，增加工作簿的内存缓冲区 (`WorkbookSettings.MemorySetting`) 可避免 `OutOfMemoryException`。

## 测试解决方案

1. 构建并运行控制台应用 (`dotnet run`)。  
2. 验证控制台打印出生成文件的完整路径。  
3. 在 Excel 或任意电子表格查看器中打开该文件。  
4. 确认单元格 A1 正好包含上面显示的 JSON 数组字符串。

如果单元格中出现标记文本（`&=OrdersJson...`）而不是 JSON，请再次检查处理器是否在标记放置 **之后** 被调用，以及 JSON 字符串是否有效。

## 结论

现在您已经掌握了如何使用 Aspose.Cells Smart Markers **从 JSON 创建 Excel**、**将 JSON 转换为 Excel**、将 JSON 负载直接嵌入单元格，并通过一行代码 **保存工作簿 xlsx**。此方法消除了手动解析的需求，适用于任何 JSON 结构，并生成符合标准的干净 Excel 文件。

### 后续步骤

- 探索 **Smart Marker 循环**（`&=OrdersJson.Orders`）以为每个订单生成一行，而不是单个 JSON 字符串。  
- 将此技术与 **Excel 公式** 结合，以从嵌入的数据中计算总计。  
- 研究 **从 Excel 读取 JSON**，使用 `Workbook.Load` 与 `SmartMarkerProcessor` 进行逆向操作。

欢迎尝试不同的 JSON 形状、多个工作表，或导出为 CSV、PDF 等其他格式。祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，每个资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方式。

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}