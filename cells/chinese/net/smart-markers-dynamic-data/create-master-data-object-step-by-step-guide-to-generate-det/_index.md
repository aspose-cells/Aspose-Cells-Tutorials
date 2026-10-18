---
category: general
date: 2026-02-14
description: 在 C# 中创建主数据对象，轻松生成明细表。通过实用代码示例学习完整的 SmartMarker 工作流。
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: zh
og_description: 在 C# 中创建主数据对象，并使用 SmartMarker 生成明细表。按照我们的详细教程，获取可直接运行的解决方案。
og_title: 创建主数据对象 – 完整指南
tags:
- C#
- SmartMarker
- Excel Automation
title: 创建主数据对象 – 生成明细表的分步指南
url: /zh/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建主数据对象 – 完整教程

是否曾经需要为 Excel 工作表 **创建主数据对象**，但不确定如何将其关联到 SmartMarker 明细表？你并不孤单。在许多报表场景中，主对象驱动动态的明细表，而正确的连接方式往往像在没有参考图的拼图。  

在本指南中，我们将完整演示整个过程——构建主数据对象、配置 SmartMarker 选项以 **生成明细表**，最后触发处理器。完成后，你将得到一个可直接粘贴到任何使用 GrapeCity Documents for Excel (GcExcel) 库的 .NET 项目中的可运行代码片段。

## 你需要准备的内容

- .NET 6+（或 .NET Framework 4.7.2），并引用 `GcExcel.dll`
- 基础的 C# 语法了解（变量、匿名类型、对象初始化器）
- 已经在工作簿中包含 `{{OrderId}}` 等 SmartMarker 标记以及用于明细行的表格
- Visual Studio、Rider 或任意你喜欢的编辑器

就这些——不需要额外的 NuGet 包，核心 GcExcel 发行版已足够。

## 第一步：创建主数据对象

首先必须 **创建主数据对象**，其结构要与 SmartMarker 标记期望的结构相匹配。可以把它看作一个小型的内存报表模型。

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

为什么这里使用匿名类型？因为它可以在不声明完整类的情况下定义轻量级容器——非常适合快速演示或当数据形状不太可能改变时。如果以后需要可复用的模型，只需将 `var` 替换为正式的 POCO 类即可。

> **小技巧：** 保持属性名（`OrderId`、`Product`、`Quantity`）与工作表中的占位符完全一致；SmartMarker 对大小写不敏感。

## 第二步：配置 SmartMarker 选项以生成明细表

接下来告诉 SmartMarker 我们希望为行项目表创建一个独立的工作表。这时 **generate detail sheet** 关键字就派上用场了。

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName` 模式使用大括号占位符，在运行时会被替换。在本例中，工作表将被命名为 `Order_1`。如果后续遍历多个订单，每个订单都会得到自己的标签页——这正是大多数会计人员的预期。

## 第三步：运行 SmartMarker 处理器

准备好数据和选项后，最后一步是对目标工作表调用处理器。

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

在幕后，SmartMarker 会扫描工作表中的标签，注入 `orderData` 的值，并且因为 `DetailSheet` 为 `true`，它会将模板克隆到一个名为 `Order_1` 的新工作表中。所有行项目会出现在明细区域，且保留模板中设置的任何格式。

### 完整可运行示例

下面是一个自包含的控制台程序，它打开模板工作簿 (`Template.xlsx`)，执行上述三步，并将结果保存为 `Result.xlsx`。你可以直接复制粘贴到新的控制台项目中，然后按 **F5** 运行。

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### 预期输出

- **Result.xlsx** 包含一个名为 `Order_1` 的工作表。
- 单元格 `A1`（或放置 `{{OrderId}}` 的位置）现在显示 `1`。
- 从 SmartMarker 块开始的表格列出两行数据：
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

打开文件后，你会看到模板中的格式仍然完整——边框、字体、条件格式等全部保留。

## 常见问题与边缘情况

### 如果有多个订单怎么办？

将主对象包装在集合中，SmartMarker 会自动迭代：

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

每个订单都会生成自己的工作表（`Order_1`、`Order_2`，……）。处理器会把外层数组视为主集合。

### 如何控制工作表的位置？

设置 `smartMarkerOptions.DetailSheetInsertIndex = 2;` 可以将新工作表插入到第二个标签页之后，或使用 `DetailSheetInsertAfter = "Summary"` 将其插入到指定名称的工作表之后。

### 能否在特定运行中禁用明细表？

只需将 `DetailSheet = false;`。此时 SmartMarker 会把行项目写入包含主标签的同一工作表。

### 大数据集怎么办？

SmartMarker 能够高效流式处理数据，但如果超过数十万行，可能会触及 Excel 的 1,048,576 行上限。此时可以将数据拆分为多个主记录，或考虑导出为 CSV。

## 可视化概览

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*该示意图展示了从 C# 主对象 → SmartMarker 选项 → 工作表处理 → 新建明细表的流程。*

## 结论

现在你已经掌握了如何在 C# 中 **创建主数据对象** 并配置 SmartMarker 自动 **生成明细表**。数据、选项、处理器这三步模式覆盖了大多数使用 GcExcel 的 Excel 自动化场景。  

接下来你可以进一步探索：

- 为每个明细表添加页眉/页脚数据
- 基于订单状态使用条件格式
- 使用 `workbook.SaveAsPdf(...)` 将生成的工作簿导出为 PDF

尽情实验、敢于出错，然后再把它们组合起来。这是掌握工作表自动化的最快途径。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}