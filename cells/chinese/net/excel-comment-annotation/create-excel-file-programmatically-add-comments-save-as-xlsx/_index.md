---
category: general
date: 2026-02-28
description: 以编程方式创建 Excel 文件，并学习如何向单元格添加批注、使用标记以及在几个简单步骤中将工作簿保存为 XLSX。
draft: false
keywords:
- create excel file programmatically
- add comment to cell
- save workbook as xlsx
- how to use markers
- how to add comment
language: zh
og_description: 使用 C# 编写清晰的逐步代码，编程创建 Excel 文件，向单元格添加批注，使用标记，并将工作簿保存为 XLSX。
og_title: 编程创建 Excel 文件 – 完整指南
tags:
- Excel
- C#
- Aspose.Cells
title: 以编程方式创建 Excel 文件 – 添加批注并保存为 XLSX
url: /zh/net/excel-comment-annotation/create-excel-file-programmatically-add-comments-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 编程创建 Excel 文件 – 完整指南

是否曾经需要**编程创建 Excel 文件**却不知从何入手？也许你盯着空白工作表发呆，心想，*“如何在不打开 Excel 的情况下在 B2 中添加评论？”* 你并不孤单。在本教程中，我们将逐步演示如何生成 `.xlsx` 文件，使用 Smart Markers 在单元格中添加评论，最后将结果保存到磁盘。

我们还会解答常见的后续问题：**如何使用标记**、**如何以可复用的方式添加评论**，以及在**将工作簿保存为 xlsx**时需要注意的事项。无需查阅外部文档——所有内容就在这里。

---

## 您需要的条件

在开始之前，请确保您已具备以下条件：

- **.NET 6+**（或 .NET Framework 4.6+）。代码兼容任何近期版本。
- **Aspose.Cells for .NET** – 为 Smart Marker 处理提供支持的库。您可以从 NuGet 获取（`Install-Package Aspose.Cells`）。
- 一个简单的 **input.xlsx**，其中包含类似 `${Comment}` 的 Smart Marker 占位符（本指南假设它位于单元格 B2）。

就这么简单——无需繁琐的设置，也不需要额外文件。准备好了吗？让我们开始吧。

---

## 步骤 1：加载 Excel 工作簿 — 编程创建 Excel 文件

当您**编程创建 Excel 文件**时，首先要做的就是打开一个模板或从头开始。在本例中，我们加载一个已经包含标记的现有工作簿。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the template that holds the ${Comment} marker
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

> **为何重要：** 加载模板可以保留样式、公式以及任何预定义的布局。如果从空工作簿开始，则需要手动重新创建所有这些内容。

---

## 步骤 2：准备数据对象 — 如何添加评论数据

Smart Markers 会用普通 C# 对象的值替换占位符。这里我们创建一个匿名类型来保存评论文本。

```csharp
        // Create the data that will fill the ${Comment} placeholder
        var commentData = new { Comment = "Reviewed by QA" };
```

> **专业提示：** 属性名（`Comment`）必须与标记名完全匹配，否则处理器将找不到可替换的内容。

---

## 步骤 3：运行 Smart Marker 处理器 — 如何使用标记

现在我们将工作簿和数据对象交给 `SmartMarkerProcessor`。这正是**如何使用标记**的核心部分。

```csharp
        // Process the marker – it will replace ${Comment} with our text
        new SmartMarkerProcessor().Process(workbook, commentData);
```

> **内部原理是什么？** 处理器会扫描每个单元格，查找 `${…}` 模式，并注入相应的属性值。它速度快、类型安全，并且同样支持集合。

---

## 步骤 4：添加真实的 Excel 评论（可选） — 向单元格添加评论

Smart Markers 只会将文本放入单元格。如果您还想要原生的 Excel 评论（悬停时出现的橙色小提示），可以在处理后手动设置。

```csharp
        // After processing, attach a true Excel comment to B2
        var commentCell = workbook.Worksheets[0].Cells["B2"];
        commentCell.Comment = commentCell.CreateComment(commentData.Comment, "QA Team");
```

> **为何添加评论？** 有些用户更喜欢评论的可视提示，同时仍然在单元格中看到纯文本。这对于审计追踪也很有用。

**边缘情况：** 如果单元格已经有评论，`CreateComment` 会覆盖它。若要保留已有备注，可检查 `if (commentCell.Comment != null)` 并进行追加。

---

## 步骤 5：将工作簿保存为 XLSX — 保存工作簿为 XLSX

最后，我们将更新后的工作簿写入新文件。这一步实际上完成了**将工作簿保存为 xlsx**。

```csharp
        // Persist the workbook to a new file
        workbook.Save(@"YOUR_DIRECTORY\Result.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created and saved successfully!");
    }
}
```

> **提示：** `SaveFormat.Xlsx` 枚举确保文件采用现代的 OpenXML 格式，可在所有近期版本的 Excel、Google Sheets 和 LibreOffice 中使用。

---

## 完整工作示例（所有步骤汇总）

下面是完整的、可直接复制粘贴的程序。将其放入任意 .NET 控制台应用运行，即可得到 `Result.xlsx`，其中 B2 单元格既包含文本 “Reviewed by QA”，又带有同样内容的 Excel 评论。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the template with a Smart Marker (${Comment})
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Prepare the data object that matches the marker name
        var commentData = new { Comment = "Reviewed by QA" };

        // 3️⃣ Process the marker – replaces ${Comment} with the actual text
        new SmartMarkerProcessor().Process(workbook, commentData);

        // 4️⃣ (Optional) Add a true Excel comment to the same cell
        var cell = workbook.Worksheets[0].Cells["B2"];
        cell.Comment = cell.CreateComment(commentData.Comment, "QA Team");

        // 5️⃣ Save the workbook as an XLSX file
        workbook.Save(@"YOUR_DIRECTORY\Result.xlsx", SaveFormat.Xlsx);

        Console.WriteLine("Excel file created and saved successfully!");
    }
}
```

**预期结果：** 打开 `Result.xlsx`。单元格 B2 显示 “Reviewed by QA”。将鼠标悬停在该单元格上，会看到一个黄橙色的评论框，内容相同，作者为 “QA Team”。

---

## 常见问题与注意事项

| Question | Answer |
|----------|--------|
| *我可以使用评论集合吗？* | 当然可以。将对象列表传递给处理器，并在范围内使用 `${Comments[i].Text}` 进行引用。 |
| *如果我的模板有多个标记怎么办？* | 只需在数据对象中添加更多属性（或使用复合对象），处理器会替换所有标记。 |
| *我需要 Aspose.Cells 的许可证吗？* | 免费评估版可用，但在生产环境中需要有效许可证以去除评估水印。 |
| *这种方式线程安全吗？* | 是的，只要每个线程使用各自的 `Workbook` 实例即可。 |
| *我可以针对旧的 .xls 格式吗？* | 将 `SaveFormat.Xlsx` 改为 `SaveFormat.Excel97To2003`。其余代码保持不变。 |

---

## 后续步骤与相关主题

既然您已经了解如何**编程创建 Excel 文件**，接下来可以探索以下内容：

- **使用 Smart Markers 与集合进行批量数据导入**。
- **在标记处理后以编程方式设置单元格样式**（字体、颜色）。
- **使用 Aspose.Cells 动态生成图表**。
- **读取已有评论并批量更新**。

所有这些都基于我们已经介绍的概念——加载工作簿、提供数据、并持久化结果。

---

## 总结

我们已经完整演示了**编程创建 Excel 文件**的整个生命周期，从加载模板、**向单元格添加评论**、使用**Smart Markers**，到最终**将工作簿保存为 XLSX**。代码简洁，概念清晰，您可以将其应用于任何自动化场景——无论是 QA 报告、财务汇总还是每日仪表盘。

动手试一试，修改评论文本，尝试使用多个标记，您会惊讶于无需打开 UI 就能快速生成精美的 Excel 文件。如果遇到问题，欢迎在下方留言；祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}