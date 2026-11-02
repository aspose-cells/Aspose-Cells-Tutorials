---
category: general
date: 2026-02-28
description: 在 C# 中创建主从报表，并学习如何填充 Excel 模板、将数据合并到 Excel，以及仅需几步即可加载 Excel 工作簿。
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: zh
og_description: 使用 Aspose.Cells SmartMarker 在 C# 中创建主从报表。学习如何在 C# 中加载 Excel 工作簿、将数据合并到
  Excel，并填充 Excel 模板。
og_title: 在 C# 中创建主从报表 – 填充 Excel 模板
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: 在 C# 中创建主从报表 – 使用 SmartMarker 填充 Excel 模板
url: /zh/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建主从报表 – 使用 SmartMarker 填充 Excel 模板

是否曾经想要 **在 C# 中创建主从报表**，但不确定如何将数据写入 Excel 文件？你并不孤单。在本指南中，我们将逐步演示如何 **填充 Excel 模板**、**将数据合并到 Excel**，以及 **以 C# 方式加载 Excel 工作簿**，从而得到一份可直接分发的精美主从报表。

我们将使用 Aspose.Cells SmartMarker，这是一款开箱即支持主从关系的强大引擎。教程结束时，你将拥有一个完整、可运行的示例，能够直接放入任何 .NET 项目中。没有模糊的 “参考文档” 之类的捷径——只有可以复制粘贴并运行的自包含解决方案。

## 你将学到的内容

- 如何在 C# 中 **创建主从** 数据结构，并直接映射到 Excel 模板。
- **以 C# 方式加载 Excel 工作簿** 的完整代码，打开包含 SmartMarker 标记的 `.xlsx` 文件。
- 通过运行 `SmartMarkerProcessor` **填充 Excel 模板** 的过程。
- 处理边缘情况的技巧，例如缺失标签或大数据集。
- 如何验证结果以及最终的 **主从报表** 长什么样。

### 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.8）。
- Aspose.Cells for .NET（可通过 NuGet 获取免费试用包：`Install-Package Aspose.Cells`）。
- 一个基本的 Excel 文件（`template.xlsx`），其中包含 SmartMarker 标记（我们会展示最小化的标记示例）。

如果你已经准备好这些，下面开始吧。

## 第 1 步 – 创建主从数据源 *(如何创建主从)*

首先需要一个 C# 对象来表示主行（订单）及其子行（订单项）。当 `MasterDetail` 设置为 `true` 时，SmartMarker 会自动读取此层次结构。

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**为什么重要：**  
SmartMarker 会查找名为 `Orders` 的属性（主表），随后对每个订单搜索名为 `Items` 的集合。只要名称匹配，你就能在无需手写循环的情况下得到 **主从报表**。

> **小贴士：** 保持属性名称简短且有意义；它们会成为 Excel 模板中的占位符。

## 第 2 步 – 为主从处理配置 SmartMarker 选项

告诉引擎你正在处理主从场景，并提供将接收子行的明细工作表名称。

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**为什么重要：**  
如果省略 `MasterDetail = true`，SmartMarker 会把数据当作平面列表处理，明细行将永远不会出现。`DetailSheetName` 必须与模板中创建的工作表名称完全匹配（区分大小写）。

## 第 3 步 – 以 C# 方式加载 Excel 工作簿

现在打开包含 SmartMarker 标记的模板。这一步就是 **以 C# 方式加载 Excel 工作簿**，许多开发者常因忘记使用正确的文件路径或未正确释放工作簿而卡住。

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**为什么重要：**  
Aspose.Cells 会将整个工作簿读取到内存中，因此文件可以位于磁盘、作为资源嵌入，甚至从 Web 服务流式获取。只需确保路径指向包含我们后面要讨论的标签的有效 `.xlsx` 文件即可。

## 第 4 步 – 向模板插入 SmartMarker 标记（填充 Excel 模板）

如果此时打开 `template.xlsx`，你会看到两个工作表：

- **Orders** – 主工作表，包含类似 `&=Orders.Id` 的行。
- **OrderDetail** – 明细工作表，包含类似 `&=Items.Sku` 和 `&=Items.Qty` 的行。

下面是最小化的标记视图：

| 工作表 | 单元格 A1 | 单元格 B1 |
|-------|----------|----------|
| Orders | `&=Orders.Id` | *(空)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

这些标签不需要任何代码，它们直接写在 Excel 文件中。**填充 Excel 模板** 的步骤仅仅是调用处理器：

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**为什么重要：**  
处理器会扫描每个工作表，用实际值替换 `&=` 占位符，并为每条主记录和对应的明细记录展开行。因为已开启 `MasterDetail`，它会自动在相应订单下为每个明细项创建新行。

## 第 5 步 – 保存主从报表

最后，将填充后的工作簿写入磁盘。这一步就会得到一份可直接分享的 **主从报表**。

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**预期输出：**  

- **Orders** 工作表显示两行：`1` 和 `2`（订单 ID）。  
- **OrderDetail** 工作表显示三行：  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

这就是一个完整可用的 **创建主从报表** 示例，你可以通过邮件发送、打印或导入其他系统。

## 边缘情况与常见问题

### 模板缺少标签怎么办？
SmartMarker 会静默忽略未知标签，但相应单元格会为空。请检查标签拼写，并确保 C# 对象中的属性名称完全匹配。

### 大数据集如何处理？
处理器采用流式写入行的方式，即使是数千条明细记录也不会导致内存爆炸。不过，对于极大文件，可能需要在 `LoadOptions` 中提升 `MemorySetting`。

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### 可以为主表使用不同的工作表名称吗？
可以——只需在模板中重命名工作表，并在需要时调整 `DetailSheetName`（如果你有明细工作表的话）。主工作表名称是从占位符（`&=Orders.Id`）中推断出来的。

### 如果需要添加合计行怎么办？
在模板中直接添加普通的 Excel 公式（例如 `=SUM(B2:B{#})`）。SmartMarker 在填充数据后会保留该公式。

## 完整可运行示例

下面是可以直接复制粘贴到控制台应用中的完整程序。它包含所有 `using` 指令、数据模型、选项以及文件处理代码。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

运行程序，打开 `output.xlsx`，即可看到美观的主从数据已成功填充。

## 可视化参考

![Create master detail report output screenshot](https://example.com/images/master-detail-report.png "Create master detail report example")

*该图片展示了 Orders 工作表中的 ID 为 1 和 2，以及 OrderDetail 工作表中的三行 SKU‑Qty 数据。*

## 结论

现在，你已经掌握了 **如何在 C# 中使用 Aspose.Cells SmartMarker 创建主从报表**，从构建数据源到 **以 C# 方式加载 Excel 工作簿**、**填充 Excel 模板**，直至最终生成报表的完整流程。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}