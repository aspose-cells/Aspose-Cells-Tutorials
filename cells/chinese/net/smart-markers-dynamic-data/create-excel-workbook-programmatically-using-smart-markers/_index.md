---
category: general
date: 2026-09-24
description: 使用编程方式创建 Excel 工作簿，学习如何创建多个明细工作表，然后使用清晰的 C# 示例将工作簿保存为 xlsx 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: zh
lastmod: 2026-09-24
og_description: 以编程方式创建 Excel 工作簿，查看如何在单个可运行示例中创建多个明细工作表并将工作簿保存为 xlsx 文件。
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: 通过编程创建 Excel 工作簿 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: 使用智能标记以编程方式创建 Excel 工作簿
url: /zh/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Smart Markers 编程创建 Excel 工作簿

如果您需要 **编程创建 Excel 工作簿**，本指南将手把手教您使用 Aspose.Cells .NET 完成此操作。您还将了解 **如何从单一数据源创建多个明细工作表**，以及最终 **将工作簿保存为 xlsx 文件**，全程无需手动步骤。

该方案是自包含的：我们逐行讲解代码，说明每个设置的意义，并覆盖常见的陷阱（如工作表名称重复）。完成后，您将拥有一个可直接运行的控制台应用程序，生成包含主工作表和一组明细工作表的工作簿。

## 您需要的准备

| 前置条件 | 原因 |
|--------------|--------|
| .NET 6.0 SDK 或更高版本 | 为 C# 控制台应用提供运行时 |
| Aspose.Cells for .NET（NuGet 包 `Aspose.Cells`） | 提供 `Workbook`、`SmartMarkerProcessor` 和 `SmartMarkerOptions` 类 |
| 简单的数据源（例如 `DataTable` 或对象列表） | 为 Smart Markers 提供待展开的数值 |
| Visual Studio 2022 或任何支持 .NET 的编辑器 | 方便编译和运行代码 |

> **专业提示：** 在开始之前通过 CLI 安装 Aspose.Cells 包：  
> `dotnet add package Aspose.Cells`

## 步骤 1：创建项目并导入命名空间

新建一个控制台项目，并将所需的命名空间引入作用域。

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*为什么重要*：`Aspose.Cells` 负责工作簿的生命周期，而 `Aspose.Cells.SmartMarkers` 则提供强大的 Smart Marker 引擎，能够从单一模板生成多个工作表。

## 步骤 2：以编程方式创建 Excel 工作簿

第一步是实例化一个 `Workbook`。该对象在内存中表示整个 Excel 文件。

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

如果您希望从已经包含标题行或格式的模板开始，只需将 `new Workbook()` 替换为 `new Workbook("Template.xlsx")`。后续流程保持不变。

## 步骤 3：准备 Smart Marker 模板

Smart Markers 作用于包含占位符的单元格内容，例如 `&=Employees.Name`。本教程将在代码中直接添加一个简单模板，您也可以在 Excel 中手动编辑工作表。

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*为什么重要*：占位符 `&=Employees.Name` 告诉 Smart Marker 处理器遍历 `Employees` 集合。每次遍历都会生成一个新工作表，因为我们将配置处理器为每行创建一个 **明细工作表**。

## 步骤 4：构建包含多行的数据源

这里使用 `DataTable` 快速模拟一组员工记录。

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

您也可以替换为任意 `IEnumerable`（例如 `List<Employee>`）——Smart Markers 接受实现了 `IEnumerable` 的任何数据源。

## 步骤 5：配置 Smart Marker 选项 —— 如何创建多个明细工作表

默认情况下，Smart Markers 将数据写回同一工作表。若要生成 **多个明细工作表**，必须设置 `DetailSheetNewName` 属性。这也演示了 **如何在不产生命名冲突的情况下创建多个明细工作表**。

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

如果数据源中出现重复名称，处理器会自动追加数字后缀（如 `Detail_1`、`Detail_2`），从而避免运行时错误并确保所有明细工作表均被保存。

## 步骤 6：处理 Smart Markers

现在调用处理器，传入数据源和刚才定义的选项。

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*为什么重要*：处理器读取占位符 `&=Employees.Name`，遍历 `employees` 的每一行，创建名为 “Detail” 的新工作表，并将行数据写入该工作表。原始工作表则保持为汇总或主工作表。

## 步骤 7：将工作簿保存为 xlsx 文件

最后，使用 **将工作簿保存为 xlsx 文件** 的模式将工作簿持久化到磁盘。

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`SaveFormat.Xlsx` 枚举确保文件以现代的 Office Open XML 格式存储，兼容 Excel 2007+ 以及大多数云服务。

## 完整可运行示例

将以下代码复制到 .NET 控制台项目的 `Program.cs` 中并运行。程序将在 `output` 文件夹生成 `detail.xlsx`，其中包含一个主工作表和三个明细工作表（每位员工各一张）。

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**预期输出**

- `output/detail.xlsx` 包含：
  - **Sheet1** – 原始模板，标题为 “Employee Report”。
  - **Detail** – 第一张明细工作表，记录 Alice。
  - **Detail_1** – 第二张明细工作表，记录 Bob。
  - **Detail_2** – 第三张明细工作表，记录 Carol。

在 Excel 中打开文件，您会看到每位员工都有自己的工作表，证明我们成功 **创建了多个明细工作表** 并 **将工作簿保存为 xlsx 文件**。

## 常见问题与边缘情况处理

| 问题 | 解答 |
|----------|--------|
| *如果我需要为每个明细工作表自定义名称怎么办？* | 将 `DetailSheetNewName = "Employee_"`，并在数据源中加入名为 `SheetName` 的列。处理器会将 `SheetName` 的值追加到基名称后。 |
| *我可以保留原始工作表作为所有明细的汇总吗？* | 可以。主工作表保持不变，您可以在其中添加引用生成的明细工作表的公式。 |
| *当数据源为空时会怎样？* | 不会创建明细工作表，但工作簿仍会保存。如果需要特殊处理，请在处理前检查 `employees.Rows.Count`。 |
| *能否使用已有的模板文件？* | 将 `new Workbook()` 替换为 `new Workbook("Template.xlsx")`。所有 Smart Marker 逻辑保持不变。 |

## 结论

您现在已经掌握了 **如何编程创建 Excel 工作簿**、**如何使用 Smart Markers 创建多个明细工作表**，以及 **如何使用 Aspose.Cells 将工作簿保存为 xlsx 文件**。完整示例可根据发票、报告或任何需要主‑明细 Excel 输出的场景进行改造。

### 后续步骤

- 探索其他 Smart Marker 功能，如 **分组标记** 和 **条件格式**。
- 将 `DataTable` 替换为真实的数据库查询，以生成大规模报告。
- 使用 `Workbook.Save("output.pdf", SaveFormat.Pdf)` 将相同数据导出为 PDF 进行分发。

欢迎尝试不同的命名方案、样式或额外工作表——您的编程 Excel 生成技能已经可以投入生产使用。祝编码愉快！

## 接下来您可以学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步说明。

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}