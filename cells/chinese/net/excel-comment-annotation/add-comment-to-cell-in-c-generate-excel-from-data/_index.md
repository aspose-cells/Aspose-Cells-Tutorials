---
category: general
date: 2026-06-24
description: 在 C# 中向单元格添加批注，并在从数据生成 Excel 时将工作簿保存为 xlsx。一步一步的指南，教你使用智能标记创建工作簿工作表。
draft: false
keywords:
- add comment to cell
- save workbook as xlsx
- generate excel from data
- create workbook worksheet
language: zh
og_description: 在 C# 中向单元格添加批注并将工作簿保存为 xlsx。了解如何从数据生成 Excel 并使用智能标记创建工作簿工作表。
og_title: 在 C# 中向单元格添加注释 – 从数据生成 Excel
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Add comment to cell in C# and save workbook as xlsx while generating
    Excel from data. Step‑by‑step guide to create workbook worksheet with smart markers.
  headline: Add comment to cell in C# – Generate Excel from data
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: 在 C# 中向单元格添加注释 – 从数据生成 Excel
url: /zh/net/excel-comment-annotation/add-comment-to-cell-in-c-generate-excel-from-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中向单元格添加注释 – 从数据生成 Excel

是否曾经需要在 C# 自动生成 Excel 文件的同时 **向单元格添加注释**？如果你也在处理数据驱动的报表并希望这些小备注恰好出现在对应位置，那么好消息来了：只需几行代码，就能 **从数据生成 Excel** 并 **将工作簿保存为 xlsx**，轻松搞定。

本教程将演示一个完整、可运行的示例，展示如何 **创建工作簿工作表**、在单元格中放置 smart‑marker、附加注释、运行 smart‑marker 引擎，最后将文件写入磁盘。完成后，你将拥有一个可以在任何数据导出场景中复用的可靠模式。

## 你需要的环境

- .NET 6 或更高版本（代码同样适用于 .NET Framework 4.7+）  
- Aspose.Cells for .NET 库（免费试用版足以进行测试）  
- 对 C# 对象和匿名类型的基本了解——无需任何高级技巧  

如果这些都已经准备好，下面开始吧。

## 第一步 – 向单元格添加注释：设置数据源

首先需要定义用于填充 smart markers 的数据。使用匿名对象可以让示例保持简洁，但你同样可以传入强类型类或 `DataTable`。

```csharp
// Step 1: Define the data source that will fill the smart markers
var data = new { Value = "Hello, world!", Comment = "This is a note" };
```

**为什么这样做很重要：**  
Smart markers 会在工作表中查找 `${Value}` 之类的占位符。将 `data` 对象传递给处理器后，每个占位符都会被对应的属性值替换。`Comment` 属性稍后将成为实际的单元格注释。

> **小技巧：** 如果需要多行数据，请传入集合 (`IEnumerable<T>`) 而不是单个对象。引擎会自动为每个项目创建行。

## 第二步 – 创建工作簿工作表：实例化工作簿

接下来我们创建一个全新的工作簿并获取第一张工作表。Aspose.Cells 会自动为你创建一张工作表，所以可以通过索引直接引用。

```csharp
// Step 2: Create a new workbook and obtain the first worksheet
var workbook = new Workbook();               // creates an empty .xlsx workbook
var worksheet = workbook.Worksheets[0];      // the default first sheet
```

**这样做的原因：**  
先创建工作簿可以让你在插入数据之前完全控制其属性（如默认字体、页面设置等）。这也使后面的 **将工作簿保存为 xlsx** 步骤更加直接，因为工作簿对象已经知道自己的格式。

## 第三步 – 放置 smart‑marker 占位符并向单元格添加注释

现在进入教程的核心：我们在单元格 **A1** 中放置 smart‑marker，并附加一个稍后会被 `${Comment}` 替换的注释。

```csharp
// Step 3: Place smart‑marker placeholders in the target cell
worksheet.Cells["A1"].PutValue("${Value}");          // placeholder for the value
worksheet.Cells["A1"].PutComment("${Comment}");     // placeholder for the comment
```

**说明：**  
- `PutValue` 将字面字符串 `${Value}` 写入单元格。处理器运行时会将其替换为 `data.Value`。  
- `PutComment` 为同一单元格附加一个包含占位符 `${Comment}` 的注释对象。处理器会替换注释的文本，而不是单元格的值。

> **边缘情况：** 如果目标单元格已经存在注释，`PutComment` 会覆盖它。若想保留已有注释，请先获取该注释，修改其 `Note` 属性后再重新赋值。

## 第四步 – 处理工作表：从数据生成 Excel

占位符就位后，我们让 Aspose.Cells 运行 smart‑marker 引擎。此步骤会一次性替换单元格值和注释文本。

```csharp
// Step 4: Process the worksheet, substituting the placeholders with actual data
worksheet.SmartMarkerProcessing(data);
```

**内部工作原理：**  
引擎扫描工作表中 `${…}` 模式，将其与 `data` 的属性匹配并完成替换。由于我们传入的是匿名对象，匹配是大小写不敏感且速度快。

如果需要更复杂的场景——例如遍历列表或条件格式化——只需相应地扩展数据源。处理器能够处理集合、嵌套对象，甚至字典。

## 第五步 – 将工作簿保存为 xlsx：写入磁盘

最后，我们将工作簿持久化为 **.xlsx** 文件。`Save` 方法会根据文件扩展名自动选择正确的格式。

```csharp
// Step 5: Save the workbook to see the result
workbook.Save("output.xlsx");   // saves in the current directory
```

**为什么使用 `.xlsx`？**  
现代的 Open XML 格式体积更小、打开更快，并且被 Office 365、Google Sheets 和 LibreOffice 完全支持。如果需要传统的 `.xls` 格式，只需将扩展名改为 `.xls`，Aspose 会自动完成转换。

> **常见问题：** *“我可以直接将工作簿流式输出到 Web 响应吗？”*  
> 完全可以——使用 `workbook.Save(Stream, SaveFormat.Xlsx)` 将流推送到 HTTP 响应中，这样就避免在服务器上生成临时文件。

### 完整可运行示例

将所有步骤组合在一起，下面是一个可以直接复制粘贴并运行的控制台程序：

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define data source
        var data = new { Value = "Hello, world!", Comment = "This is a note" };

        // 2️⃣ Create workbook and get first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Insert smart‑marker placeholders and a comment
        worksheet.Cells["A1"].PutValue("${Value}");
        worksheet.Cells["A1"].PutComment("${Comment}");

        // 4️⃣ Run smart‑marker processing (generate Excel from data)
        worksheet.SmartMarkerProcessing(data);

        // 5️⃣ Save workbook as xlsx
        workbook.Save("output.xlsx");

        System.Console.WriteLine("Excel file created successfully!");
    }
}
```

**预期结果：**  
- 单元格 **A1** 将显示 `Hello, world!`。  
- 在 Excel 中将鼠标悬停在 **A1** 上会看到注释 “This is a note”。  
- 文件 `output.xlsx` 位于可执行文件所在文件夹，随时可打开。

## 进阶技巧与常见坑点

- **多个注释：** 若需要在多个单元格上添加注释，只需对每个地址重复调用 `PutComment`。  
- **Unicode 支持：** Aspose.Cells 天生支持 UTF‑8，完全可以在注释中插入表情或非拉丁文字。  
- **性能考虑：** 对于大数据集，建议传入 `DataTable` 或 `IEnumerable<T>`；引擎会批量写入，效率更高。  
- **测试建议：** 第一次运行后务必在 Excel 中打开生成的文件，快速验证注释是否出现在预期位置。

## 结论

我们已经演示了如何在 C# 中 **向单元格添加注释**、**将工作簿保存为 xlsx**，以及通过 **创建工作簿工作表** 并使用 smart markers **从数据生成 Excel**。这一模式简洁可靠，能够从单个单元格的备注扩展到大型多工作表报表。

接下来可以尝试将数据源扩展为订单列表，自动生成表格，或直接将工作簿流式输出到 Web API 端点。你还可以探索条件格式或图表创建——只需几行 Aspose.Cells 方法调用即可实现。

祝编码愉快，愿你的 Excel 导出始终像注释一样整洁有序！

## 接下来该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并在项目中探索替代实现方式，每篇都提供完整可运行的代码示例和逐步解释。

- [Add Excel Worksheet To Existing Workbook Csharp Tutorial](/cells/english/net/excel-worksheet-csharp-tutorials/add-excel-worksheet-to-existing-workbook-csharp-tutorial/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step-by-Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}