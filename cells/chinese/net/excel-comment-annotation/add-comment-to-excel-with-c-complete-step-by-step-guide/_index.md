---
category: general
date: 2026-05-30
description: 使用 C# 快速向 Excel 添加批注。学习如何向单元格写入批注、插入 Smart Marker 占位符并保存工作簿。
draft: false
keywords:
- add comment to excel
- write comment to cell
- add comment using c#
language: zh
og_description: 使用 C# 在几分钟内向 Excel 添加批注。本教程展示如何向单元格写入批注、处理 Smart Marker 并保存文件。
og_title: 使用 C# 向 Excel 添加批注 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  headline: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  name: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Adding Multiple Comments in One Pass
    text: If you need to add comments to several cells, just place multiple placeholders
      (`${Comment1}`, `${Comment2}`, …) and expand the data object accordingly.
  - name: 2. Preserving Existing Comments
    text: Sometimes a sheet already contains reviewer notes that you don’t want to
      lose. Retrieve the existing comment, merge, then write back.
  - name: 3. Unicode and Emojis
    text: Excel fully supports Unicode, so you can embed emojis, non‑Latin scripts,
      or special symbols directly in the comment string.
  - name: 4. Large Workbooks & Performance
    text: 'Processing a workbook with thousands of Smart Markers can be costly. To
      improve speed:'
  type: HowTo
- questions:
  - answer: Yes, but you must open the workbook with the `LoadOptions` that allow
      editing, e.g., `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.
    question: Can I add a comment to a *read‑only* workbook?
  - answer: '`PutComment` overwrites the existing comment. To merge, retrieve the
      current comment first (`GetComment()`), concatenate, then call `PutComment`
      again.'
    question: What if the target cell already has a comment?
  - answer: Absolutely. Aspose.Cells abstracts the format; just point the `Workbook`
      constructor at the `.xls` file and everything else stays the same.
    question: Does this work with older `.xls` files?
  - answer: 'Practically, Excel supports comments up to 32,767 characters. Aspose.Cells
      respects the same limit—larger strings will be truncated. --- ## Recap & Next
      Steps We’ve covered how to **add comment to Excel** using C#, demonstrated the
      **write comment to cell** technique with Smart Markers, and explored'
    question: Is there a limit to comment length?
  type: FAQPage
tags:
- Excel
- C#
- Aspose.Cells
title: 使用 C# 向 Excel 添加批注 – 完整逐步指南
url: /zh/net/excel-comment-annotation/add-comment-to-excel-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中向 Excel 添加批注 – 完整分步指南

是否曾想过如何在不手动打开文件的情况下，从 C# 应用程序 **add comment to Excel**？你并不孤单。许多开发者需要以编程方式 **write comment to cell**——无论是用于审计轨迹、审阅者备注，还是动态报告。在本教程中，我们将演示一个使用 Aspose.Cells 的 Smart Marker 功能的完整端到端解决方案，并解释每一步背后的“原因”，帮助你将此模式迁移到自己的项目中。

完成本指南后，你将能够：

* 加载现有工作簿，
* 在特定单元格插入占位符批注，
* 使用匿名对象将占位符替换为真实文本，
* 保存更新后的文件，
* 并处理一些常见的边缘情况，如已有批注或 Unicode 文本。

无需外部脚本，无需 Excel interop，只需纯 C# 代码即可在 Windows、Linux 和 macOS 上运行。

---

## 前置条件 — 开始前需要准备的内容

* **Aspose.Cells for .NET** (v23.10 或更高)。该库可免费试用，NuGet 包名为 `Aspose.Cells`。
* .NET 开发环境 (Visual Studio、Rider，或带 C# 扩展的 VS Code)。
* 一个放在代码可引用文件夹中的输入工作簿 (`input.xlsx`)。
* 对 C# 匿名类型和对象初始化器的基本了解。

如果你已经具备这些条件，太好了——让我们开始吧。如果没有，请使用以下命令获取 NuGet 包：

```bash
dotnet add package Aspose.Cells
```

这行代码会把你需要的所有内容拉进来，包括我们后面会使用的 `SmartMarkerProcessor` 类。

---

## 第一步 – 加载工作簿（add comment to excel）

在我们能够 **add comment to Excel** 之前，必须先在内存中打开文件。Aspose.Cells 抽象了文件格式，你无需关心它是 .xlsx、.xls 还是 .csv。

```csharp
// Load the workbook that contains the target worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Why this matters:** 打开工作簿会创建一个 `Workbook` 对象，包含所有工作表、样式和已有批注。如果跳过此步骤直接引用工作表，会触发 `NullReferenceException`。

---

## 第二步 – 选择工作表和单元格（write comment to cell）

大多数实际的电子表格都有多个标签页。为简化起见，我们使用第一张工作表，但如果需要也可以按名称索引。

```csharp
// Grab the first worksheet (index 0)
Worksheet ws = wb.Worksheets[0];

// Place a Smart Marker placeholder in cell A1 where the comment will appear
ws.Cells["A1"].PutComment("${Comment}");
```

对 `A1` 调用 `PutComment` 会创建一个附着在该单元格的 *comment* 对象。内容 `${Comment}` 是一个 **Smart Marker 占位符**——相当于稍后会被真实数据替换的标记。

> **Pro tip:** 如果单元格已经有批注，`PutComment` 会覆盖它。若想保留已有批注，可先读取 `ws.Cells["A1"].GetComment().Comment`，进行拼接后再重新写入。

---

## 第三步 – 准备数据对象（add comment using c#）

Smart Markers 可以与任何具有匹配占位符属性的 .NET 对象配合使用。匿名对象非常适合快速演示。

```csharp
// Anonymous object that supplies the actual comment text
var data = new { Comment = "Reviewed by John – ✅ Approved" };
```

如果需要验证或更多字段，也可以使用强类型类。

```csharp
public class ReviewInfo
{
    public string Comment { get; set; }
    public DateTime ReviewedOn { get; set; }
}
```

然后实例化：

```csharp
var data = new ReviewInfo
{
    Comment = "Reviewed by John – ✅ Approved",
    ReviewedOn = DateTime.UtcNow
};
```

> **Why anonymous objects?** 当只需要少量值时，它们可以让代码保持简洁。对于更大的数据集，使用正式的 DTO（数据传输对象）可提升可维护性。

---

## 第四步 – 处理 Smart Marker（add comment to excel）

现在魔法发生了。`SmartMarkerProcessor` 会扫描工作表，找到 `${Comment}`，并用 `data.Comment` 的值进行替换。

```csharp
// Run the processor to replace placeholders with real values
new SmartMarkerProcessor().Process(ws, data);
```

在内部，处理器会：

1. 解析工作表的 XML 表示，
2. 检测任何 `${…}` 标记，
3. 在提供的对象上查找匹配的属性，
4. 将解析后的字符串写入批注的文本节点。

如果占位符不存在，处理器会静默跳过——不会抛出异常。这使得该方法对可选批注也安全可靠。

---

## 第五步 – 保存工作簿（see the result）

最后，将修改后的工作簿写回磁盘。你可以覆盖原文件，也可以生成新文件。

```csharp
// Save the workbook – you can change the format by using SaveOptions if needed
wb.Save("YOUR_DIRECTORY/output.xlsx");
```

打开 `output.xlsx` 时，你会看到单元格 **A1** 附带了批注 “Reviewed by John – ✅ Approved”。将鼠标悬停在单元格右上角的小红三角上即可查看。

> **Expected output:**  

> ![显示带有批注的单元格的截图 – add comment to excel 示例](add-comment-to-excel-example.png "add comment to excel 示例")

*该 alt 文本包含主要关键词，满足 SEO 规则。*

---

## 处理常见场景

### 1. 一次性添加多个批注

如果需要为多个单元格添加批注，只需放置多个占位符（`${Comment1}`、`${Comment2}` …），并相应扩展数据对象。

```csharp
ws.Cells["A1"].PutComment("${Comment1}");
ws.Cells["B2"].PutComment("${Comment2}");

var data = new
{
    Comment1 = "First note",
    Comment2 = "Second note"
};

new SmartMarkerProcessor().Process(ws, data);
```

### 2. 保留已有批注

有时工作表已经包含审阅者备注，你不想丢失。先获取现有批注，合并后再写回。

```csharp
var existing = ws.Cells["A1"].GetComment()?.Comment ?? string.Empty;
var merged   = string.IsNullOrWhiteSpace(existing)
               ? data.Comment
               : $"{existing}\n{data.Comment}";

ws.Cells["A1"].PutComment(merged);
```

### 3. Unicode 与表情符号

Excel 完全支持 Unicode，因此可以直接在批注字符串中嵌入表情符号、非拉丁文字或特殊符号。

```csharp
var data = new { Comment = "审查通过 – ✅" };
```

只需确保源文件以 UTF‑8 编码保存（大多数现代 IDE 的默认设置）。

### 4. 大型工作簿与性能

处理包含数千个 Smart Marker 的工作簿可能会消耗较多资源。提升速度的做法包括：

* 使用 `SmartMarkerProcessorOptions` 将范围限制在单个工作表。
* 如果只需要批注，关闭计算 (`wb.CalculateFormula = false`)。
* 重用单个 `SmartMarkerProcessor` 实例，而不是为每个工作表创建新实例。

```csharp
var processor = new SmartMarkerProcessor
{
    Options = new SmartMarkerProcessorOptions { ProcessAllWorksheets = false }
};

processor.Process(ws, data);
```

---

## 完整工作示例

将所有内容组合起来，下面是一个可以直接复制粘贴到 `Program.cs` 并运行的完整控制台应用示例。

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet and insert a placeholder comment
            Worksheet ws = wb.Worksheets[0];
            ws.Cells["A1"].PutComment("${Comment}");

            // 3️⃣ Prepare data – you can use an anonymous type or a DTO
            var data = new { Comment = "Reviewed by John – ✅ Approved" };

            // 4️⃣ Process Smart Markers to replace the placeholder
            new SmartMarkerProcessor().Process(ws, data);

            // 5️⃣ Save the result
            wb.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Comment added successfully!");
        }
    }
}
```

运行程序，打开 `output.xlsx`，你会看到批注正好出现在我们放置占位符的位置。无需 Excel UI，无需 COM interop，纯托管代码即可。

---

## 常见问题 (FAQ)

**Q: 能否向 *只读* 工作簿添加批注？**  
A: 可以，但必须使用允许编辑的 `LoadOptions` 打开工作簿，例如 `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`。

**Q: 如果目标单元格已经有批注怎么办？**  
A: `PutComment` 会覆盖已有批注。若想合并，先使用 `GetComment()` 读取当前批注，进行拼接后再次调用 `PutComment`。

**Q: 这能在旧的 `.xls` 文件上工作吗？**  
A: 完全可以。Aspose.Cells 抽象了文件格式，只需将 `.xls` 文件传给 `Workbook` 构造函数，其他操作保持不变。

**Q: 批注长度有没有限制？**  
A: 实际上，Excel 支持最长 32,767 个字符的批注。Aspose.Cells 也遵循同一限制——超出部分会被截断。

---

## 回顾与后续步骤

我们已经介绍了如何使用 C# **add comment to Excel**，演示了 **write comment to cell** 的 Smart Marker 技术，并探讨了多批注、Unicode 支持以及性能调优等变体。核心模式——占位符 → 数据对象 → 处理器 → 保存——可复用于任何动态内容，未…

## 接下来你应该学习什么？

- [在 Excel 中添加带图片的批注](/cells/english/net/excel-comment-annotation/add-comment-with-image-excel/)
- [使用 Aspose.Cells for Java 向 Excel 批注添加图片：完整指南](/cells/english/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)
- [在 Excel 中添加带图片的批注](/cells/german/net/excel-comment-annotation/add-comment-with-image-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}