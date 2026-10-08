---
category: general
date: 2026-02-09
description: 如何在 C# 中创建工作簿并设置淡蓝色背景以及导入带标题的数据。学习如何添加淡蓝色背景，使用 Excel 默认样式并导入数据表。
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: zh
og_description: 如何在 C# 中创建带浅蓝色背景的工作簿，导入带标题的数据，并应用默认的 Excel 样式——一份简明指南。
og_title: 如何创建工作簿 – 浅蓝背景，数据导入
tags:
- C#
- Excel
- Aspose.Cells
title: 如何创建工作簿 – 浅蓝色背景，数据导入
url: /zh/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何创建工作簿 – 浅蓝背景，导入数据

是否曾想过 **如何创建工作簿**（Workbook）在 C# 中看起来更美观一点？也许你已经从数据库中取出了 `DataTable`，但对单调的默认白色单元格感到厌倦。在本教程中，我们将演示如何创建一个新工作簿、为某列添加浅蓝背景，并在使用 Excel 默认样式的同时导入带标题的数据。

我们还会穿插一些 “如果…” 场景，例如处理空值或为多列自定义样式。完成后，你将拥有一个完全美化的 Excel 文件，能够直接交付给相关方，无需后期处理。

## 前置条件

在开始之前，请确保你已经具备：

* **.NET 6+**（代码同样适用于 .NET Framework 4.6+）  
* **Aspose.Cells for .NET** – 提供 `Workbook`、`Style` 与 `ImportDataTable` 等调用的库。通过 NuGet 安装：

  ```bash
  dotnet add package Aspose.Cells
  ```

* 一个 `DataTable` 数据源 – 示例中我们会自行构造，但你可以替换为任何 ADO.NET 查询。

准备好了吗？那我们开始吧。

## 步骤 1：初始化新工作簿（主要关键词）

首先要做的就是 **如何创建工作簿**——字面意思。`Workbook` 类代表整个 Excel 文件，其构造函数会为你提供一张全新的空白页。

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **为什么这很重要：** 从全新的 `Workbook` 开始，能够让你从一开始就掌控所有样式。如果直接打开已有文件，你将继承原作者留下的样式，可能导致格式不统一。

## 步骤 2：准备要导入的 DataTable

为了演示，我们先创建一个简单的 `DataTable`。在实际项目中，你可能会调用存储过程或 ORM 方法来获取数据。

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **小贴士：** 如果需要严格保持列顺序与数据库中的一致，请将 `ImportDataTable` 的 `importColumnNames` 参数设为 `true`。这会让 Aspose.Cells 自动为你写入列标题。

## 步骤 3：定义列样式 – 默认 + 浅蓝背景

现在我们来实现 **添加浅蓝背景** 的需求。Aspose.Cells 允许你传入一个 `Style` 对象数组，数组中的每个元素对应要导入的列。第一个元素对应第 0 列，第二个对应第 1 列，以此类推。如果样式数量少于列数，剩余列会使用工作簿的默认样式。

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **为什么只有两种样式？** 在示例中我们有四列，但只想让第二列（Name）突出显示。数组长度不必与列数完全匹配，缺失的条目会自动继承工作簿的默认样式。

## 步骤 4：使用标题和样式导入 DataTable

这里我们把 **excel import datatable c#** 与 **import data with headers** 结合起来。`ImportDataTable` 方法负责核心工作：写入列名、行数据，并应用我们刚才构建的样式数组。

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### 预期结果

运行程序后，`workbook` 将包含一个工作表，效果如下：

| **ID** | **Name**（浅蓝色） | **HireDate** | **Salary** |
|-------|-------------------|--------------|------------|
| 1     | Alice Johnson     | 5/12/2020    | 72000      |
| 2     | Bob Smith         | 3/4/2019     | 68000      |
| 3     | Carol White       | *(blank)*   | 75000      |

* **Name** 列拥有浅蓝背景，证明样式数组生效。  
* 由于我们传入了 `true` 的 `importColumnNames`，列标题会自动生成。  
* 空值会显示为空单元格，这是 Aspose.Cells 的默认行为。

## 步骤 5：保存工作簿（可选但实用）

你可能需要将文件写入磁盘或返回给 Web 客户端。保存非常简单：

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **专业提示：** 如果目标是旧版 Excel， 将 `SaveFormat.Xlsx` 改为 `SaveFormat.Xls` 即可。API 会自动完成转换。

## 边缘情况与变体

### 多列样式化

如果需要为多列设置样式，只需扩展 `columnStyles` 数组：

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

这样 **Name** 与 **Salary** 两列都会呈现浅蓝背景。

### 使用条件格式代替固定样式

有时希望当数值超过阈值时将列变为红色。这时 **使用默认样式 excel** 与条件格式相结合：

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### 不导入标题

如果下游系统已经提供了自己的标题，只需将 `importColumnNames` 参数设为 `false`。数据将从 `A1` 开始，你可以随后自行写入自定义标题。

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## 完整示例（全部代码）

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}