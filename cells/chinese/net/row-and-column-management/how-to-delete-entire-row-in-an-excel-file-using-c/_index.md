---
category: general
date: 2026-10-10
description: 学习如何使用 C# 删除 Excel 工作簿中的整行。本分步指南还涵盖了如何按索引删除行以及使用 Aspose.Cells 按索引删除行。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: zh
lastmod: 2026-10-10
og_description: 使用 C# 删除 Excel 工作簿中的整行。请按照本指南学习如何按索引删除行、按索引移除行以及安全保存文件。
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: 使用 C# 删除 Excel 中整行 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: 如何使用 C# 删除 Excel 文件中的整行
url: /zh/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 删除 Excel 文件中的整行

如果您需要在 Excel 工作簿中**删除整行**，本指南将向您展示如何使用 C# 完成此操作。无论是清理导入的数据还是构建报表工具，下面的步骤都可以让您按索引删除行并保存结果，而不会丢失其他数据。  
您还将看到相同的方法如何回答**如何按索引删除行**、**如何按索引移除行**的问题，以及为什么它适用于 C# 中的**delete row excel**场景。

## 前置条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）  
* **Aspose.Cells for .NET** 库（可通过 NuGet 获取：`Install-Package Aspose.Cells`）  
* 对 C# 控制台或桌面项目有基本了解  

无需额外的 Excel interop 或 COM 组件，这使得解决方案轻量且适合服务器端执行。

## 步骤 1：设置项目并导入命名空间

创建一个新的控制台应用程序（或将代码添加到现有项目），并添加所需的 `using` 指令：

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*为什么这很重要*：导入 `Aspose.Cells` 可让您访问 `Workbook`、`Worksheet` 以及执行实际行删除的 `DeleteRows` 方法。

## 步骤 2：加载工作簿并选择工作表

您必须加载源文件（`input.xlsx`）并获取要修改的工作表。第一张工作表可通过索引 `0` 访问。

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **提示**：如果需要处理特定工作表，请将索引替换为工作表名称：`workbook.Worksheets["Data"]`。

## 步骤 3：按零基索引删除整行

Aspose.Cells 使用零基索引，因此第一行是 `0`。要删除第 5 行（第六行可视行），请使用 `DeleteOptions.DeleteEntireRow` 调用 `DeleteRows`。

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*解释*：

* `ws.Cells[5, 0]` 指向您想删除的行的第一个单元格。  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` 告诉 Aspose.Cells 删除 **1** 行，且 `DeleteEntireRow` 标志确保**整行**消失，下面的行向上移动。

### 在其他场景中如何按索引删除行

* **删除多个连续行** – 将第一个参数改为您想删除的行数：

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **删除最后一行** – 使用 `ws.Cells.MaxDataRow` 获取最底部已填充行的索引：

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

这些代码片段满足 **remove row by index** 的需求，同时保持代码易读。

## 步骤 4：保存已删除行的工作簿

删除后，将修改后的工作簿写回磁盘。您可以覆盖原文件或创建新文件。

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

如果需要保持原文件不变，只需更改输出路径。`Save` 方法支持多种格式（`.xls`、`.csv`、`.pdf` 等）——只需更改文件扩展名。

## 完整工作示例

将所有内容组合在一起，下面是一个完整的、可直接运行的程序：

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**预期输出**：运行程序后，`output.xlsx` 将包含除第 6 行（可视行）之外的所有原始行。被删除行以下的所有数据会自动向上移动，保持公式和格式。

## 常见陷阱及避免方法

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **索引超出范围** | 尝试删除不存在的行索引（例如在 200 行的工作表中使用 `ws.Cells[1000,0]`） | 在调用 `DeleteRows` 前使用 `ws.Cells.MaxDataRow` 验证最高有效索引。 |
| **部分行删除** | 省略 `DeleteOptions.DeleteEntireRow` 会导致仅清除单元格内容，而不是整行。 | 在需要删除整行时，务必传入 `DeleteOptions.DeleteEntireRow`。 |
| **意外的公式更改** | 删除属于公式范围的行可能导致引用失效。 | 如果工作簿依赖动态范围，删除后请重新计算公式（`workbook.CalculateFormula()`）。 |
| **保存到只读位置** | 如果文件夹受保护，`Save` 调用会抛出异常。 | 确保目标目录可写，或以适当的权限运行程序。 |

解决这些问题可使解决方案在生产环境中更稳健，并满足 **delete row excel** 和 **delete row c#** 的查询需求。

## 高级：基于条件删除行

有时您需要删除满足特定条件的行（例如列 A 为空的行）。下面的循环演示了从底部向顶部扫描并安全删除匹配行的方法：

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

向上扫描可避免在前向遍历时删除行导致的索引偏移问题。

## 结论

现在您已经了解如何使用 C# 在 Excel 工作簿中**删除整行**。本指南涵盖了：

* 加载工作簿并选择工作表  
* 使用 `DeleteRows` 与 `DeleteOptions.DeleteEntireRow` 来**按索引删除行**  
* 安全保存修改后的文件  
* 边缘情况处理、性能提示以及条件删除示例  

有了这些知识，您可以自信地实现 **remove row by index** 功能，自动化数据清理，并将 Excel 操作集成到任何 C# 应用程序中。  

**下一步**：探索其他 Aspose.Cells 功能，如插入行、复制范围或将工作簿转换为 PDF——这些都基于您刚刚掌握的 `Workbook` 和 `Worksheet` 对象。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都包含完整的代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方法。

- [如何使用 Aspose.Cells .NET 删除 Excel 行：完整指南](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells 删除行 – 在 Excel 中保护标题行](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [使用 Aspose.Cells for Java 高效管理 Excel 行：插入和删除行](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}