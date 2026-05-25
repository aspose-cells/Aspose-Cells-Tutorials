---
category: general
date: 2026-05-23
description: 在 C# 中快速从 JSON 生成 Excel。学习如何将 JSON 加载到 Excel，以编程方式创建 Excel 工作簿，并将工作簿保存到文件。
draft: false
keywords:
- generate excel from json
- load json into excel
- save workbook to file
- create excel workbook programmatically
language: zh
og_description: 使用 C# 从 JSON 生成 Excel。本指南展示了如何将 JSON 加载到 Excel、以编程方式创建 Excel 工作簿，并将工作簿保存到文件。
og_title: 使用 C# 从 JSON 生成 Excel – 完整编程教程
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Generate Excel from JSON in C# quickly. Learn how to load JSON into
    Excel, create Excel workbook programmatically, and save workbook to file.
  headline: Generate Excel from JSON with C# – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- JSON
- Excel Automation
title: 使用 C# 从 JSON 生成 Excel – 完整分步指南
url: /zh/net/data-loading-and-parsing/generate-excel-from-json-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 从 JSON 生成 Excel – 完整分步指南

是否曾想过 **从 JSON 生成 Excel** 而无需手动打开 Excel？你并不是唯一有此需求的人。许多开发者需要将 API 响应、配置文件或简单的数据转储转换为可直接使用的电子表格——快速、可靠且无需用户交互。  

在本教程中，我们将一步步演示一个简洁的端到端解决方案，**将 JSON 加载到 Excel**，在代码中完整构建工作簿，最后 **将工作簿保存为文件**。完成后，你将拥有一段可在任何 .NET 项目中直接使用的可复用代码片段。

> **小贴士：** 该方法适用于映射为平面表格的任意 JSON 结构。对于嵌套对象，我们将在后面讨论一个快速的解决方案。

---

## 你需要准备的环境

- **.NET 6+**（或 .NET Framework 4.6+）。  
- **Aspose.Cells for .NET** —— 我们将使用的 Smart Marker 引擎所在的库。  
- 一个 JSON 数据负载（示例使用一个小型订单列表）。  
- 你喜欢的 IDE（Visual Studio、Rider 或 VS Code）。  

无需其他第三方工具；所有操作均在内存中完成。

---

## 第一步 – 以代码方式创建 Excel 工作簿

任何 Excel 自动化的第一步都是实例化一个工作簿对象。可以把它想象成一块可以随意绘制的空白画布。

```csharp
using Aspose.Cells;          // Excel manipulation
using Aspose.Cells.Tables;   // Smart Marker support
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook in memory
        Workbook workbook = new Workbook();
```

为什么要在代码中创建工作簿？这可以确保文件 **通过程序创建**，避免文件系统竞争条件，并且能够在没有 UI 的服务器上完整运行整个流水线。

---

## 第二步 – 插入 Smart Marker 占位符

Smart Markers 是 Aspose 为电子表格提供的邮件合并功能。只需在单元格中放置 `${Orders:ArrayAsSingle}` 这样的占位符，库就会自动将 JSON 数组展开为多行。

```csharp
        // Step 2: Put a Smart Marker into cell A1 (first worksheet, first cell)
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");
```

如果你对 Smart Markers 还不熟悉，可以把 `${Orders:ArrayAsSingle}` 想象成一个模板标签，意思是“当看到这里时，把 *Orders* 集合的每一项分别写入一行”。

---

## 第三步 – 绑定 SmartMarkerProcessor

处理器是读取占位符、解析 JSON 并填充工作表的核心引擎。

```csharp
        // Step 3: Initialise the processor with the workbook we just prepared
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

为什么不直接调用 `Workbook.Save`？因为此时数据尚未写入。处理器负责在原始 JSON 与 Excel 布局之间搭建桥梁。

---

## 第四步 – 定义要加载的 JSON 数据

下面是一个包含两个订单的简短 JSON 数组。实际场景中，你可能会从 REST API 获取、读取文件，或动态生成它。

```csharp
        // Step 4: JSON that will populate the Smart Marker
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";
```

请注意，这里的 JSON **是平面的**——每个对象只包含基本字段。这是最干净的 “将 JSON 加载到 Excel” 模式。如果你的 JSON 包含嵌套对象，需要先将其扁平化（请参见文末的 *高级技巧*）。

---

## 第五步 – 将 JSON 应用于工作簿

现在魔法开始发挥作用。处理器读取 JSON，展开 Smart Marker，并为每个对象写入行。

```csharp
        // Step 5: Apply JSON – the Smart Marker expands automatically
        processor.ApplyJson(jsonData);
```

在内部，Aspose 会创建一个临时数据表，将每个属性（`Id`、`Total`）映射到列，并在占位符下方插入相应的行。无需循环，也不需要手动定位单元格——只需声明式转换。

---

## 第六步 – 将工作簿保存为文件

最后，将填充好的工作簿持久化到磁盘。

```csharp
        // Step 6: Save the populated workbook to a physical file
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**将工作簿保存为文件** 是整个流程的最后一步。Aspose 在底层使用 Open XML 写入最终的 `.xlsx`，因此文件完全兼容 Excel、Google Sheets 和 LibreOffice。

---

## 完整示例（所有步骤合并）

下面是可以直接复制粘贴运行的完整程序。请确保已安装 Aspose.Cells NuGet 包（`dotnet add package Aspose.Cells`）。

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System;

class ExcelFromJsonDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Insert Smart Marker placeholder in cell A1
        workbook.Worksheets[0].Cells[0, 0].PutValue("${Orders:ArrayAsSingle}");

        // 3️⃣ Initialise SmartMarkerProcessor
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // 4️⃣ JSON data (could come from a file, API, etc.)
        string jsonData = "[{\"Id\":1,\"Total\":99.9},{\"Id\":2,\"Total\":45.0}]";

        // 5️⃣ Apply JSON – Smart Marker expands automatically
        processor.ApplyJson(jsonData);

        // 6️⃣ Save the workbook to disk
        string outputPath = @"C:\Temp\OrdersReport.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 预期输出

打开 `OrdersReport.xlsx` 后，你会看到：

| Id | Total |
|----|-------|
| 1  | 99.9  |
| 2  | 45.0  |

列标题会自动从 JSON 属性名生成，每个数组元素对应一行。无需手动定位单元格。

---

## 高级技巧 – 处理更大或嵌套的 JSON

如果你的 JSON 包含 **嵌套对象**（例如 `Order` 中的 `Customer` 子对象），Smart Markers 仍然可以使用，只是需要先将结构扁平化：

```csharp
// Example flattening using Newtonsoft.Json.Linq
var jArray = JArray.Parse(jsonData);
var flatList = jArray.Select(item => new {
    Id = (int)item["Id"],
    Total = (decimal)item["Total"],
    CustomerName = (string)item["Customer"]["Name"]
}).ToList();
string flatJson = JsonConvert.SerializeObject(flatList);
processor.ApplyJson(flatJson);
```

这种做法可以让 **将 JSON 加载到 Excel** 的流程保持顺畅，即使面对复杂数据也不例外。

---

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **缺少 Aspose.Cells 许可证** | 免费试用版会添加水印。 | 获取许可证文件并通过 `License license = new License(); license.SetLicense("Aspose.Cells.lic");` 注册。 |
| **占位符拼写错误** | Smart Marker 标签区分大小写。 | 仔细检查 `${Orders:ArrayAsSingle}` 的拼写及括号。 |
| **大尺寸 JSON 导致内存压力** | 整个 JSON 会一次性加载到内存。 | 使用流式读取或分批处理，然后合并工作表。 |
| **日期格式不匹配** | JSON 日期以原始时间戳形式出现。 | 使用 `JsonSerializerSettings` 格式化日期，或在处理后为相应列设置自定义格式。 |

---

## 为什么此方法优于手动循环

- **声明式**：你描述 *想要的表格*，而不是 *如何遍历行*。  
- **性能**：Smart Markers 使用内部优化缓冲区，通常比朴素的 `for` 循环更快。  
- **可维护性**：更换数据源（CSV、数据库、API）只需替换 JSON 字符串——Excel 逻辑代码无需改动。  
- **可扩展性**：同一模板可复用于 dozens of 报表，只需提供不同的数据结构。

---

## 结论

我们已经演示了如何在 C# 中 **从 JSON 生成 Excel**，通过 **将 JSON 加载到 Excel**、**以代码方式创建工作簿**，并最终 **将工作簿保存为文件**。整个流水线在内存中完成，仅需几行代码，即可生成整洁、可直接分享的电子表格。

想进一步探索？可以尝试添加条件格式、插入图表，或直接导出为 PDF——这些都可以使用同一个 `Workbook` 对象实现。关键点在于：Smart Markers 能以几乎零样板代码将 JSON 转换为 Excel 表格。

对特定 JSON 结构的处理或输出格式的微调有疑问？欢迎在下方评论或讨论区提问。祝编码愉快！

---

![Generate Excel from JSON using C# – screenshot of the resulting OrdersReport.xlsx](/images/generate-excel-from-json.png "generate excel from json")

*图片替代文字：* 使用 C# 从 JSON 生成 Excel – 教程的可视化结果。

## 相关教程

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Import JSON Data into Excel Using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}