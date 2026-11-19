---
category: general
date: 2026-11-19
description: 学习如何在 C# 中删除 Excel 表格。本教程还展示了如何使用 C# 读取 Excel 文件以及加载 Excel 工作簿，并提供完整的代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete table from excel
- read excel file c#
- how to remove table excel
- load excel workbook c#
- how to delete excel table
language: zh
lastmod: 2026-11-19
og_description: 在 C# 中快速删除 Excel 表格。请按照本指南阅读 Excel 文件（C#）并加载 Excel 工作簿（C#），并附带可运行示例。
og_image_alt: Screenshot of C# code that deletes a table from an Excel worksheet
og_title: 在 C# 中从 Excel 删除表格 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to delete table from Excel in C#. This tutorial also shows
    how to read Excel file C# and load Excel workbook C# with a complete code example.
  headline: How to delete table from Excel using C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: 如何使用 C# 从 Excel 中删除表格 – 步骤指南
url: /zh/net/tables-and-lists/how-to-delete-table-from-excel-using-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 删除 Excel 表格 – 步骤指南

如果您需要以编程方式 **delete table from Excel**，本指南将向您展示如何使用 C# 完成此操作。您将看到一个完整的、可运行的示例，加载 Excel 工作簿，删除第一个表格，并保存结果。同样的模式也涵盖 **read excel file c#** 和 **load excel workbook c#**，因此您可以将其适配到任何自动化场景。

在 .NET 中处理 Excel 文件通常需要可靠的库。在本教程中，我们使用 **Aspose.Cells**，这是一套完全托管的 API，支持表格、公式和丰富的格式化，且无需在服务器上安装 Microsoft Office。步骤简洁，代码自包含，您将了解每一行代码的意义。

## 您将实现的目标

* 将现有的 `.xlsx` 文件加载到内存中。
* 在工作表中定位并删除表格（也称为 ListObject）。
* 将修改后的工作簿保存为新文件。
* 扩展此方法以处理多个表格或表格缺失的情况。

无需事先了解 Aspose.Cells——只需具备基本的 C# 知识。

## 前提条件

* .NET 6.0 SDK 或更高版本（代码同样适用于 .NET Core 3.1 和 .NET Framework 4.6+）。
* Visual Studio 2022（或任何支持 .NET 项目的编辑器）。
* **Aspose.Cells** NuGet 包。使用以下方式安装：

```bash
dotnet add package Aspose.Cells
```

* 一个包含至少一个表格的 Excel 文件（`input.xlsx`）。如果没有，可在 Excel 中创建一个简单的表格并保存到项目同一文件夹中。

---

## 步骤 1：在 C# 中加载 Excel 工作簿

第一步是从磁盘读取工作簿。这是 **load excel workbook c#** 的核心。

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Define file paths
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Step 1: Load the workbook
        Workbook workbook = new Workbook(inputPath);
```

**为什么这很重要：**  
`Workbook` 表示内存中的整个 Excel 文件。一次加载后，您可以执行多项操作——读取单元格、修改表格或更改格式，而无需反复打开文件。

---

## 步骤 2：访问第一个工作表（read excel file c#）

工作簿加载后，您需要获取包含表格的工作表的引用。

```csharp
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

`Worksheets` 是零基集合，因此 `[0]` 返回第一张工作表。如果您的文件布局不同，请更改索引或使用 `workbook.Worksheets["SheetName"]`。

---

## 步骤 3：从工作表中删除表格

现在我们执行核心的 **delete table from excel** 操作。示例删除第一个表格，但相同的逻辑适用于任何表格索引。

```csharp
        // Step 3: Delete the first table in the worksheet
        if (worksheet.Tables.Count > 0)
        {
            // Table[0] is the first ListObject on the sheet
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }
```

**为什么这样有效：**  
`Tables` 是 `ListObject` 对象的集合。调用 `Delete()` 会删除表格定义 *以及* 底层的数据范围，留下普通单元格。`if` 条件实现了 **how to remove table excel** 的安全删除，防止在工作表不含表格时抛出异常。

**技巧提示：**  
如果需要按名称而非位置删除表格，请使用 `worksheet.Tables["TableName"].Delete();`。当工作簿包含多个表格且只想针对特定表格时，这非常有用。

---

## 步骤 4：保存修改后的工作簿（how to delete excel table）

最后，将更改写回磁盘。这完成了 **how to delete excel table** 工作流。

```csharp
        // Step 4: Save the modified workbook
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**内部发生了什么：**  
`Save` 会创建一个新的 `.xlsx` 文件，反映所有内存中的更改。原始的 `input.xlsx` 保持不变，这在生产脚本中是一种安全的做法。

---

## 完整、可运行的示例

将所有部分组合在一起，下面是完整的程序，您可以复制、粘贴并运行：

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Load the workbook (load excel workbook c#)
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet (read excel file c#)
        Worksheet worksheet = workbook.Worksheets[0];

        // Delete the first table (delete table from excel)
        if (worksheet.Tables.Count > 0)
        {
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }

        // Save the changes (how to delete excel table)
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**预期输出**

```
Table deleted successfully.
Modified workbook saved to YOUR_DIRECTORY\output.xlsx
```

在 Excel 中打开 `output.xlsx`；您删除的表格现在会显示为包含原始数据的普通单元格。

---

## 处理常见的边缘情况

| 情况 | 推荐做法 |
|-----------|----------------------|
| **Multiple tables** | 遍历 `worksheet.Tables` 并删除每个表格，或使用 `worksheet.Tables["MyTable"].Delete();` 按名称删除。 |
| **Table does not exist** | `if (worksheet.Tables.Count > 0)` 条件已经防止了 `NullReferenceException`。您也可以记录警告以供审计。 |
| **Large files** | 使用 `Workbook.LoadOptions` 以 **memory‑efficient** 模式打开文件（例如 `LoadOptions { MemorySetting = MemorySetting.MemoryPreference };`）。 |
| **Preserve formatting** | 删除表格会移除其样式。如果需要保留视觉样式，请在调用 `Delete()` 前将样式复制到目标范围。 |

---

## 性能提示：批量操作

如果需要在多个工作表中删除大量表格，请在同一个 `Workbook` 实例中进行所有更改，并在全部删除完成后仅调用一次 `workbook.CalculateFormula()`。这比在每次删除后重新计算公式能减少 CPU 开销。

---

## 下一步

既然您已经了解 **how to remove table excel** 和 **delete table from excel**，接下来可能想要：

* **Read Excel file C#** 用于在表格删除后提取数据。`Cells` 集合允许您遍历行和列。
* 使用 `worksheet.Tables.Add()` 以编程方式生成新表格——在报表场景中非常有用。
* 探索 Aspose.Cells 的其他功能，如图表操作、数据透视表或条件格式化。

这些主题都基于您刚才使用的相同 `Workbook` 和 `Worksheet` 对象，因此代码的适配非常直接。

---

## 结论

您已经学习了如何使用 C# **delete table from Excel**。本指南涵盖了加载工作簿、访问工作表、安全删除表格以及保存更新后的文件——全部通过完整的可运行示例实现。凭借此基础，您可以自动化任何基于 Excel 的工作流，无论是 **read excel file c#**、**load excel workbook c#**，还是在更复杂的场景中 **how to delete excel table**。

欢迎尝试多个表格、不同工作表，或使用诸如 EPPlus 等开源库来实现相同功能。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行深入。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [读取 Excel 文件 C# – 如何高效加载 Excel 工作簿 C#](/cells/english/net/loading-and-saving-excel-files-with-options/read-excel-file-c-how-to-load-excel-workbook-c-efficiently/)
- [如何在 C# 中删除 Excel 表格中的行并更改其名称](/cells/english/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/)
- [如何使用 C# 重命名 Excel 表格 – 步骤指南](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}