---
category: general
date: 2026-05-23
description: 使用模板和 JSON 数据创建动态 Excel 表格。学习如何加载 Excel 模板、自动化 Excel 报告，并快速从 JSON 填充
  Excel。
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: zh
og_description: 使用模板和 JSON 在几分钟内创建动态 Excel 表格。本教程展示如何加载 Excel 模板、自动化 Excel 报告以及从 JSON
  填充 Excel。
og_title: 创建动态 Excel 表格 – 智能标记指南
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: 创建动态 Excel 表格 – 智能标记指南
url: /zh/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建动态 Excel 表格 – Smart Marker 指南

是否曾需要 **创建动态 Excel 表格**，它能为数据集中的每条记录自动扩展？您并非唯一有此需求的人。无论是构建月度销售仪表板还是面向客户的发票包，能够 **从 JSON 填充 Excel** 而无需编写无尽循环，都能节省数小时的工作时间。

在本教程中，我们将一步步演示完整的实战方案，向您展示如何 **加载 Excel 模板**、嵌入 Smart Marker、提供 JSON 数据，最终 **自动生成 Excel 报表**。完成后，您将拥有一个可直接运行的 .NET 项目，能够从单个 JSON 负载生成精美的 Excel 工作簿。

---

## 您需要的条件

- **Aspose.Cells for .NET**（或任何支持 Smart Markers 的库）。示例使用 24.5 版，但任何近期版本均可工作。
- Visual Studio 2022（或您喜欢的 C# IDE）。
- 一个简单的 Excel 模板文件（`template.xlsx`），放置在您可控制的文件夹中。
- 包含名为 `Customers` 的集合的 JSON 字符串。

就这么简单——无需额外服务、无需数据库连接，仅仅是纯代码。

---

## 步骤 1：创建模板工作簿 – 加载 Excel 模板

我们首先要 **加载 Excel 模板** 到内存中。可以把模板视为画布，特殊占位符会告诉处理器在何处重复行。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **为什么这很重要：** 只加载一次模板可以将文件 I/O 降至最低，并让您在多个报表中复用相同布局。它还将 Smart Marker 逻辑与其余代码隔离，实现了关注点的清晰分离。

---

## 步骤 2：插入 Smart Marker – 创建动态 Excel 表格

现在我们嵌入一个 **Smart Marker**，它会为 `Customers` 集合中的每个条目重复一个表格。语法 `${Customers.RepeatWorksheet}` 告诉 Aspose.Cells 为每位客户克隆整个工作表。

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **专业提示：** 如果只需要重复行而不是整张工作表，可在表格的第一行使用 `${Customers.Repeat}`。工作表级别的重复在每位客户需要单独标签页时非常方便。

---

## 步骤 3：准备 SmartMarkerProcessor – 自动化 Excel 报表

标记就位后，我们创建 `SmartMarkerProcessor`。该对象负责在 JSON 与 Excel 模板之间进行数据绑定。

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

该处理器体积轻巧；如果需要，您可以将其复用于多个 JSON 负载。

---

## 步骤 4：提供 JSON 数据 – 从 JSON 填充 Excel

魔法就在这里。我们提供一个包含客户数组的 JSON 字符串。每个客户可以拥有 `Name`、`Email`、`Total` 等字段。

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **为什么使用 JSON？** JSON 与语言无关，且易于从 API、数据库或手动输入生成。使用 `ApplyJson` 意味着您无需手动映射对象，处理器会完成繁重的工作。

---

## 步骤 5：保存结果 – 生成 Excel 报表 JSON

最后，我们将填充好的工作簿写入磁盘。输出文件现在为每位客户包含一个独立的工作表，且每个工作表都填充了来自 JSON 的数据。

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### 预期输出

- **output.xlsx** 将包含三个工作表，名称为 `Sheet1`、`Sheet2`、`Sheet3`（或您模板使用的任何命名规则）。
- 每个工作表将显示单个客户的 `Name`、`Email` 和 `Total` 值。
- 您在 `template.xlsx` 中设计的布局（标题、样式、公式）将在所有生成的工作表中保持不变。

---

## 完整工作示例

下面是完整的、可直接运行的程序。将其复制粘贴到控制台应用中，调整文件路径，然后按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

运行程序，打开 `output.xlsx`，您将看到 **创建动态 Excel 表格** 的实际效果——每位客户都有自己的工作表，且完全按照您设计的格式呈现。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *如果我的 JSON 包含嵌套对象怎么办？* | Smart Markers 支持点表示法（`${Customers.Address.City}`），只要 JSON 层级匹配即可。 |
| *我可以将生成的工作表命名为客户名称吗？* | 可以——在工作表名称单元格中添加 `${Customers.Name}` 标记，或在 `processor.ApplyJson(customersJson, "Customers")` 时使用命名模式。 |
| *大数据集（10 k+ 行）怎么办？* | 处理器会高效流式处理数据，但需关注内存占用。如果达到性能上限，考虑将报表拆分为多个文件。 |
| *是否需要 Aspose.Cells 的许可证？* | 免费评估版可用于测试，但正式许可证会去除评估水印并提供全部功能。 |
| *可以在 .NET Core 中使用此方法吗？* | 当然可以——Aspose.Cells 支持 .NET 6/7/8。只需引用 NuGet 包，代码保持不变。 |

---

## 生产环境实现技巧

- **在将 JSON 提供给 `ApplyJson` 之前进行验证**。格式错误的负载会抛出 `JsonParseException`。
- **缓存模板**，如果在短时间内生成大量报表；反复从磁盘加载会产生不必要的 I/O。
- **在处理期间锁定工作簿**，如果在多线程 Web 服务中运行，以避免竞争条件。
- **在 `workbook.Save` 周围添加错误处理**，以优雅地处理权限问题或文件被锁定的情况。
- **在模板中自定义样式**（条件格式、公式），让生成的工作表在无需额外代码的情况下保留业务逻辑。

---

## 结论

现在，您已经掌握了一套完整的、端到端的模式，能够使用模板、Smart Markers 和 JSON 数据 **创建动态 Excel 表格**。通过 **加载 Excel 模板**、插入重复标记并 **从 JSON 填充 Excel**，您只需几行 C# 代码即可 **自动生成 Excel 报表**。

下一步？尝试添加引用动态表格的图表，或使用 Aspose.Words 将相同的 JSON 导出为 PDF。您还可以尝试从数据库查询 **生成 Excel 报表 JSON**，以完成整个闭环。

## 相关教程

- [使用 Aspose.Cells for .NET 在 Excel 中创建数据透视表](/cells/english/net/pivot-tables/create-pivot-table/)
- [使用 Aspose.Cells for .NET 创建动态折线图：分步指南](/cells/english/net/charts-graphs/create-line-c

arts-excel-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中创建复选框 | 数据验证教程](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}