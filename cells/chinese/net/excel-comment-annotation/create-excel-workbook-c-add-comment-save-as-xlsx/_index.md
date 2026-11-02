---
category: general
date: 2026-03-18
description: 使用 C# 创建带有批注的 Excel 工作簿并将其保存为 XLSX。学习如何添加批注、生成 Excel 批注以及自动化 Excel 文件。
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: zh
og_description: 使用 C# 创建带批注的 Excel 工作簿并将其保存为 XLSX。请按照本分步指南添加 Excel 批注并以编程方式生成批注。
og_title: 创建 Excel 工作簿（C#）– 添加批注并保存为 XLSX
tags:
- C#
- Excel Automation
- Aspose.Cells
title: 使用 C# 创建 Excel 工作簿 – 添加批注并另存为 XLSX
url: /zh/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 C# – 添加批注并保存为 XLSX

是否曾需要 **create Excel workbook C#** 并在单元格中添加批注，却不知从何入手？你并非唯一的开发者——大家经常询问 *how to add comment*，而无需手动打开 Excel。

在本教程中，你将获得一个完整、可直接运行的示例，展示 **how to add excel comment**、使用 Smart Marker **generate excel comment**，以及 **save workbook as xlsx** 的完整流程。没有多余的引用，只需将代码粘贴到 Visual Studio 中即可运行。

## 你将学到的内容

- 使用 C# 从头初始化 Excel 工作簿。
- 插入一个会变成 Excel 批注的 Smart Marker。
- 提供 JSON 数据，将标记转换为真实批注。
- 将文件持久化为 `.xlsx` 工作簿。
- 可选的在不使用 Smart Marker 的情况下添加批注的方法。

### 前置条件

- .NET 6（或 .NET Framework 4.7+）。
- **Aspose.Cells for .NET** NuGet 包——提供 Smart Marker 功能的库。
- 基本的 C# 开发环境（Visual Studio、VS Code、Rider 等）。

> **专业提示：** 如果预算有限，Aspose 提供功能完整的免费试用，可用于开发和测试。

---

## 步骤 1：创建 Excel 工作簿 C# – 项目设置

首先，让我们创建一个新的控制台应用并引入 Aspose.Cells 包。

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

现在打开 `Program.cs`。我们首先要 **create a new workbook**。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

为什么要从全新的工作簿开始？它确保了干净的起点，消除隐藏的格式，并让你从头掌控所有内容——非常适合自动化报表生成。

---

## 步骤 2：如何添加批注 – 使用 Smart Marker

Smart Marker 是 Aspose 在运行时用数据替换的占位符。通过嵌入符合 **`${Comment:UserComment}`** 模式的标记，我们指示引擎将占位符转换为实际的批注。

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

注意到 `Comment:` 前缀了吗？这告诉处理器将该值视为批注而非普通文本。如果你在想 *“这能用于其他单元格类型吗？”*——答案是肯定的，你可以将相同的标记应用于任何单元格，甚至是合并的范围。

---

## 步骤 3：准备 JSON 数据 – 批注内容

下一步是数据源。这里我们使用一个简单的 JSON 字符串，但也可以提供 DataTable、List，甚至自定义对象。

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

可以随意将 `"Reviewed by QA"` 替换为任意动态值——例如时间戳、用户名，或指向问题跟踪器的链接。键名 (`UserComment`) 必须与标记的标识符匹配。

---

## 步骤 4：生成 Excel 批注 – 处理 Smart Marker

现在我们将 JSON 交给 Smart Marker 处理器。这就是 **generate excel comment** 实际发生的时刻。

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

在幕后，Aspose 解析 JSON，找到 `UserComment` 字段，并将其注入为附加在单元格 **B2** 的批注。单元格的可见值仍然是原始占位符文本，但在 Excel 中将鼠标悬停时会显示批注。

---

## 步骤 5：保存工作簿为 XLSX – 持久化结果

最后，我们将工作簿写入磁盘。这满足了 **save workbook as xlsx** 的需求。

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

在 Excel 中打开 `output.xlsx`，将鼠标悬停在单元格 **B2** 上，你会看到批注 *“Reviewed by QA”* 出现。就这样——无需手动操作、无需 COM 互操作，只需纯 C#。

---

## 替代方案：如何在不使用 Smart Marker 的情况下添加批注

如果你更喜欢直接的方式，可以自行创建批注对象：

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

当批注文本在编译时已知，或需要设置作者、宽度、高度等额外属性时，此方法非常方便。然而，在数据驱动、涉及大量行列的场景中，使用 Smart Marker **generate excel comment** 更为出色。

---

## 专业提示与常见陷阱

| 情况 | 需要注意的点 | 推荐解决方案 |
|-----------|-------------------|-----------------|
| 大型数据集（10k+ 行） | Smart Marker 处理可能占用大量内存 | 使用支持流式数据的 `SmartMarkerProcessor.Process` 重载，或将工作簿拆分为多个块 |
| 需要自定义作者名称 | 默认作者为空 | 在创建批注后设置 `comment.Author = "MyApp";` |
| 希望批注默认可见 | Excel 默认在悬停时才显示批注 | 设置 `comment.Visible = true;` |
| 使用旧版 Excel | 可能不支持 `.xlsx` | 改为保存为 `SaveFormat.Xls`，但需注意某些批注功能会有所不同 |

---

## 预期输出

- **工作簿文件：** `output.xlsx` 位于项目的 bin 文件夹中。  
- **单元格 B2：** 显示占位符文本 `${Comment:UserComment}`（可通过将单元格字体颜色设为白色来隐藏）。  
- **附加在 B2 的批注：** 鼠标悬停时显示 “Reviewed by QA”。

![创建 Excel 工作簿 C# 示例，显示单元格 B2 中的批注](https://example.com/placeholder-image.png "创建 Excel 工作簿 C# 示例，显示单元格 B2 中的批注")

*图片替代文字：* **创建 Excel 工作簿 C# 示例，显示单元格 B2 中的批注**

---

## 回顾 – 我们完成了什么

我们 **创建了 Excel 工作簿 C#**，插入了会转化为 **excel comment** 的 **Smart Marker**，提供 JSON 以 **generate excel comment**，最后 **saved workbook as xlsx**。整个流程仅用几十行简洁、独立的 C# 代码即可实现。

---

## 接下来？扩展方案

- **批量生成批注：**遍历 DataTable，对每行应用 Smart Marker 以添加特定行的备注。  
- **批注样式化：**使用 `Comment.RichText` 集合调整字体大小、颜色，甚至添加富文本。  
- **导出为 PDF：**使用 `workbook.Save("output.pdf", SaveFormat.Pdf);` 共享包含批注的报告。  

如果你想了解在其他环境下以编程方式 **add excel comment**——例如使用 OpenXML SDK 或 EPPlus——这些库同样支持批注创建，只是 API 形式不同。

---

### 最后思考

从 C# 向 Excel 文件添加批注并非繁琐任务。借助 Aspose.Cells 的 Smart Marker 引擎，你可以以简洁、数据驱动的方式 **add excel comment**、**generate excel comment**，并以最少的样板代码 **save workbook as xlsx**。

试一试，修改 JSON，看看如何快速将原始数据转化为精美、批注丰富的电子表格。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}