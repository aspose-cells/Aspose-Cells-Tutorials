---
category: general
date: 2026-08-11
description: 在 C# 中从 DataTable 创建 Excel 工作表，并将 DataTable 导出为 Excel，自动命名工作表。学习如何向 DataTable
  添加行并将工作簿保存为 xlsx。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: zh
lastmod: 2026-08-11
og_description: 在 C# 中从 DataTable 创建 Excel 工作表。本教程展示如何将 DataTable 导出为 Excel、向 DataTable
  添加行、生成多个 Excel 工作表以及将工作簿保存为 xlsx。
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: 在 C# 中从 DataTable 创建 Excel 工作表 – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: 在 C# 中从 DataTable 创建 Excel 工作表 – 步骤指南
url: /zh/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 C# 中的 DataTable 创建 Excel 工作表 – 步骤指南

如果你需要 **create excel sheet**（创建 Excel 工作表）从 `DataTable`，本指南将手把手教你如何实现。你将看到如何 **export datatable to excel**（将 DataTable 导出为 Excel）、添加行、处理重复的工作表名称，最后 **save workbook as xlsx**（将工作簿保存为 xlsx）。

示例使用 Aspose.Cells，这是一款广泛使用的 .NET Excel 自动化库。相同的概念同样适用于其他支持 SmartMarker 风格处理的库，但下面的代码在 Aspose.Cells 22.12 或更高版本中可直接使用。

## 前置条件

在开始之前，请确保你已经具备：

* 已安装 .NET 6.0 SDK 或更高版本  
* 已引用 **Aspose.Cells** NuGet 包（`Install-Package Aspose.Cells`）  
* 对 `DataTable` 和 C# 控制台应用有基本了解  

这些要求保证本教程自成一体，且无需外部工具。

## 第一步：创建将要导出到 Excel 的 DataTable

第一步是构建一个与工作表数据相匹配的 `DataTable`。这里我们创建一个名为 **Sheet1** 的表，添加 `Id` 列，并插入两行数据。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**为什么重要：**  
`DataTable` 是一种便捷的内存表格数据表示方式。将表命名为 `"Sheet1"` 可让 Aspose.Cells 在处理 SmartMarkers 时定位到对应的工作表。

## 第二步：向 DataTable 添加行（可选扩展）

如果源数据是动态的，通常需要在循环中添加行。下面的代码片段演示了常见的做法：

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**提示：** 当添加大量行时，考虑先禁用约束（`dataTable.Constraints.Clear()`）以提升性能。

## 第三步：配置 SmartMarker 选项以自动创建多个 Excel 工作表

SmartMarker 选项让你能够控制重复工作表名称的处理方式。将 `DetailSheetNewName` 设置为 `"Sheet1_{0}"`，即可让 Aspose.Cells 将后续工作表重命名为 `Sheet1_1`、`Sheet1_2` 等。

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**为什么重要：**  
当你处理多个同名 `DataTable` 时，Excel 通常会因工作表名称必须唯一而报错。`DetailSheetNewName` 模式会自动消除这种冲突。

## 第四步：处理 SmartMarkers 并将 datatable 导出到 Excel

现在我们创建一个全新的 `Workbook`，运行 `ProcessSmartMarkers`，让 Aspose.Cells 根据 `DataTable` 填充工作表。

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**说明：**  
`ProcessSmartMarkers` 会扫描工作簿中的标记（如 `&=Sheet1!A1`，此处未展示），并用 `dataTable` 中的数据替换它们。因为我们从空工作簿开始，Aspose.Cells 会创建一个与表名相同的新工作表并填充我们添加的行。

## 第五步：将工作簿保存为 xlsx

最后，将工作簿以现代的 OpenXML 格式（`.xlsx`）写入磁盘。你可以根据实际环境修改路径。

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**结果：**  
运行程序后会生成一个 Excel 文件，内容如下：

| 工作表名称 | 行数 |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | （如果处理了另一个同名 DataTable） |

工作表重命名逻辑确保 **create multiple excel sheets**（创建多个 Excel 工作表）时无需手动管理名称。

## 常见变体与边缘情况

| 场景 | 处理方式 |
|-----------|------------------|
| **非常大的表**（≥ 100 000 行） | 在处理前使用 `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` 以降低内存占用。 |
| **自定义列顺序** | 在调用 `ProcessSmartMarkers` 前重新排列 `DataTable` 中的 `DataColumn` 对象。 |
| **多个不同名称的 DataTable** | 为每个表分别调用 `ProcessSmartMarkers`；Aspose.Cells 会自动为每个名称创建独立工作表。 |
| **需要带样式的标题行** | 处理完后访问 `Worksheet.Cells["A1"]` 并设置 `Style` 属性（字体、背景等）。 |
| **保存到流而非文件** | 将 `workbook.Save(outputPath, SaveFormat.Xlsx)` 替换为 `workbook.Save(stream, SaveFormat.Xlsx)`。 |

**专业提示：** 始终将文件系统操作包装在 `try…catch` 块中，以便及早捕获权限问题。

## 完整源码（可直接复制）

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 预期输出

运行程序后会在控制台打印：

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

打开 `DuplicateSheets.xlsx` 可看到一个名为 **Sheet1** 的工作表，`Id` 列包含值 `1, 2, 3, 4, 5`。如果随后在同一工作簿中再处理一个名为 `"Sheet1"` 的 `DataTable`，Aspose.Cells 将自动创建 **Sheet1_1**、**Sheet1_2** 等工作表。

## 结论

现在你已经掌握了如何 **create excel sheet**（创建 Excel 工作表）从 C# 中的 `DataTable`，以及 **export datatable to excel**（将 DataTable 导出为 Excel）、**add rows to datatable**（向 DataTable 添加行）、生成 **create multiple excel sheets**（创建多个 Excel 工作表）并自动命名，最后 **save workbook as xlsx**（将工作簿保存为 xlsx）。完整、可运行的示例展示了端到端的工作流，并提供了处理大数据集和自定义样式的实用技巧。

### 接下来该做什么？

* 通过访问 `Worksheet.Cells` 在 `ProcessSmartMarkers` 之后探索 **cell formatting**（单元格格式化），如字体、颜色、边框等。  
* 使用 **SmartMarker loops**（SmartMarker 循环）在同一工作簿中生成主从报表。  
* 如需纯文本表示，可将 `SaveFormat.Csv` 替换为 **CSV export**（CSV 导出）。  

欢迎将代码适配到自己的数据源——无论是数据库查询、API 响应，还是内存集合。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索项目中的其他实现方式。每篇资源都提供完整可运行的代码示例和逐步解释。

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java \| Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}