---
category: general
date: 2026-02-14
description: 使用 SmartMarker 自动生成发票：学习如何重复工作表、动态命名工作表，并在几分钟内掌握动态工作表命名。
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: zh
og_description: 使用 SmartMarker 自动生成发票。本指南展示了如何重复工作表、动态命名工作表，以及掌握动态工作表命名。
og_title: 自动化发票生成 – 动态工作表命名与重复
tags:
- C#
- SmartMarker
- Excel Automation
title: 自动化发票生成——C# 中的动态工作表命名与重复
url: /zh/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自动化发票生成 – 动态工作表命名与重复（C#）

有没有想过如何 **自动化发票生成**，而不必为每个订单手动复制工作表？你并不孤单。许多开发者在需要为每张发票创建单独工作表且工作表名称要反映订单号时会遇到难题。在本教程中，我们将使用 SmartMarker 的 `SmartMarkerProcessor` 来解决该问题，并向你展示 **如何动态命名工作表**，同时讲解 **如何为每条记录重复工作表**。完成后，你将拥有一个可直接运行的 C# 示例，它会生成一个工作簿，每张发票都位于自己命名合理的标签页中。

我们将一步步演示——从从数据源获取订单到配置 `SmartMarkerOptions` 实现动态工作表命名。无需外部文档，所有内容都在这里。只需具备一点 C# 基础并引用 Aspose.Cells 库（或任何兼容 SmartMarker 的引擎）即可。

---

## 你将构建的内容

- 获取一组订单对象。
- 配置 SmartMarker 以 **为每个订单重复工作表**。
- 使用 `{OrderId}` 占位符实现 **动态工作表命名**。
- 生成的 Excel 文件中，每个标签页命名为 `Invoice_12345`、`Invoice_67890` 等。
- 通过打开工作簿来验证输出结果。

---

## 前提条件

- .NET 6.0 或更高版本（代码同样适用于 .NET 5+）。
- Aspose.Cells for .NET（或任何实现 SmartMarker 的库）。通过 NuGet 安装：

```bash
dotnet add package Aspose.Cells
```

- 一个基础的 `Order` 类（你可以用自己的 DTO 替代）。

---

## 步骤 1：设置项目和模型

首先，创建一个新的控制台应用程序，并定义表示订单的数据模型。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **专业提示：** 为演示保持模型轻量即可，后续可以随时添加明细行、税务信息等。

---

## 步骤 2：准备 Excel 模板

SmartMarker 需要基于模板工作簿。创建一个名为 `InvoiceTemplate.xlsx` 的文件，里面只有一个工作表，名称为 `InvoiceTemplate`。在单元格 **A1** 中放置 SmartMarker 占位符，例如：

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

你可以随意设置单元格格式——加粗标题、货币格式等。将文件保存到项目根目录。

> **为什么使用模板？** 它将布局与代码分离，设计师可以在不触及逻辑的情况下调整外观。

---

## 步骤 3：配置 SmartMarker 选项 – 重复并命名工作表

现在我们告诉 SmartMarker *为每个订单重复* 模板工作表，并为每个副本赋予包含订单 ID 的名称。这就是 **动态工作表命名** 的核心。

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### 工作原理

- **`RepeatWorksheet = true`** 告诉引擎为 `orders` 集合中的每个元素复制源工作表，满足 **如何重复工作表** 的需求。
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** 是一个模板字符串，其中 `{OrderId}` 是占位符，SmartMarker 会将其替换为当前订单的 ID。这就是 **如何命名工作表** 与 **动态工作表命名** 的实现方式。
- 处理器将每个订单的字段（`{{OrderId}}`、`{{Customer}}` 等）合并到复制后的工作表中，生成完整的发票。

---

## 步骤 4：运行应用并验证输出

编译并运行控制台应用：

```bash
dotnet run
```

控制台应显示成功信息。打开 `GeneratedInvoices.xlsx`，你会看到三个标签页：

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

每张工作表都已将订单数据替换到占位符中。模板中设计的布局保持不变，证明 **自动化发票生成** 已实现端到端。

### 预期截图（SEO 用 alt 文本）

![自动化发票生成示例，展示三个动态命名的工作表](/images/invoice-automation.png)

> *图片 alt 文本包含主要关键词，以满足 SEO 需求。*

---

## 步骤 5：边缘情况与常见变体

### 如果 OrderId 包含非法字符怎么办？

Excel 工作表名称不能包含 `\ / ? * [ ] :`。如果你的 ID 可能包含这些字符，请先进行清理：

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

在 `Order` 中添加计算属性：

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### 需要保留原始模板工作表吗？

设置 `smartMarkerOptions.RemoveTemplate = false;`（默认值为 `true`）。这样原始的 `InvoiceTemplate` 将保持不变，作为参考。

### 想按客户分组发票？

可以嵌套 **重复组**。先按客户重复，然后在每个客户的工作表中再按订单重复。语法会稍微复杂一些，但原理相同——使用 `RepeatWorksheet` 并提供反映层级结构的命名模式。

---

## 完整工作示例（所有代码集中在一起）

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

将此代码复制粘贴到 `Program.cs`，并将 `InvoiceTemplate.xlsx` 放在同目录下，即可运行。

---

## 常见问题

**问：这种方式能处理大数据集（成千上万张发票）吗？**  
答：可以。SmartMarker 会高效地流式处理数据，但仍需关注内存使用情况。如果出现限制，考虑分批处理并将每批写入单独的工作簿。

**问：能否自动在每张发票上添加 logo？**  
答：完全可以。只需将 logo 图片放在模板工作表上。由于工作表会被复制，logo 会出现在每张生成的发票中，无需额外代码。

**问：如果需要保护工作表该怎么办？**  
答：处理完后，遍历 `wb.Worksheets` 并调用 `ws.Protect(Password, ProtectionType.All)` 即可。

---

## 结论

我们已经通过 SmartMarker 的 **重复工作表** 功能和巧妙的命名模式，实现了 **自动化发票生成**。本教程涵盖了 **如何命名工作表**、演示了 **如何为每个订单重复工作表**，并展示了保持工作簿整洁可搜索的 **动态工作表命名**。从获取数据、搭建模板、配置 `SmartMarkerOptions` 到处理边缘情况，你现在拥有一个完整、可运行的解决方案。接下来，可以尝试添加明细表、应用条件格式，或将相同数据导出为 PDF，构建全自动的计费流水线。

准备好升级了吗？探索相关主题，如 “使用 Aspose.Cells 批量导出 Excel”、 “工作表的 PDF 转换”、 “从 C# 直接邮件发送生成的发票”。无限可能，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}