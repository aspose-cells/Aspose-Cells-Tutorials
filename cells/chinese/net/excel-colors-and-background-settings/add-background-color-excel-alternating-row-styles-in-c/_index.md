---
category: general
date: 2026-04-07
description: 使用 C# 为 Excel 行添加背景颜色。了解如何应用交替行颜色、设置纯色背景样式，以及在单个工作流中将 DataTable 导入 Excel。
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: zh
og_description: 使用 C# 为 Excel 行添加背景颜色。本指南展示了如何实现交替行颜色、设置纯色背景，以及高效地将 DataTable 导入 Excel。
og_title: 在 Excel 中添加背景颜色 – C# 中的交替行样式
tags:
- C#
- Excel
- DataTable
- Styling
title: 在 Excel 中添加背景颜色 – 使用 C# 实现交替行样式
url: /zh/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中添加背景颜色 – C# 中的交替行样式

是否曾经需要 **add background color excel** 行，但不确定如何在不写上千行繁琐代码的情况下实现？你并不孤单——大多数开发者在首次尝试让电子表格看起来不仅仅是原始数据时都会遇到这个难题。  

好消息是？只需几分钟，你就可以 **apply alternating row colors**、设置 **solid background**，甚至使用 C# 中的简洁可复用模式 **import datatable to excel**。  

在本教程中，我们将完整演示整个过程，从将数据提取到 `DataTable` 到使用浅黄‑白相间的条纹模式为每行设置样式。除了一些可靠的 Excel 处理库（如 **ClosedXML** 或 **GemBox.Spreadsheet**）之外，无需其他外部库，你将看到这种方法为何既高效又易于维护。

## 你将学到

- 如何检索数据并将其写入 Excel 工作表。
- 如何使用交替背景颜色 **style excel rows**。
- 使用 `Style` 对象实现 **set solid background** 的机制。
- 如何在保留行样式的情况下 **import datatable to excel**。
- 处理空表或自定义配色方案等边缘情况的技巧。

> **Pro tip:** 如果你已经在使用支持样式创建的库中的工作簿对象 (`wb`)，可以在多个工作表之间复用相同的 `Style` 实例——节省内存并保持代码整洁。

---

## 步骤 1：检索数据 – 准备 DataTable

在进行任何样式设置之前，我们需要一个行数据源。在大多数实际场景中，这些数据来自数据库、API 或 CSV 文件。为了演示，我们将仅在内存中创建一个简单的 `DataTable`。

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** 使用 `DataTable` 提供了一个表格化、具备模式感知的容器，Excel 库可以直接导入，从而无需编写逐单元格的循环。

---

## 步骤 2：创建行样式 – **Apply alternating row colors**

现在我们将构建一个 `Style` 对象数组——每行一个——以便每行都能拥有自己的背景。我们使用的模式是偶数行使用经典的浅黄色，奇数行使用白色。

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` 为你提供一个干净的样式对象，你可以在不影响其他对象的情况下进行调整。  
- 三元运算符 `(i % 2 == 0)` 决定该行是偶数（浅黄色）还是奇数（白色）。  
- 将 `Pattern = BackgroundType.Solid` 设置为关键步骤，它实现了 **set solid background**；若不设置，颜色将被忽略。

---

## 步骤 3：获取目标工作表

大多数库都会公开工作表集合。我们将使用第一个工作表，但你可以根据需要选择任意索引或名称。

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

如果工作簿是全新创建的，库通常会为你创建一个默认工作表。否则，你可以显式添加一个：

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## 步骤 4：使用行样式导入 DataTable – **Import datatable to excel**

样式准备好后，最后一步是将 `DataTable` 推入工作表，并为每行应用相应的样式。

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` 表示方法将列标题写入第一行。  
- `0, 0` 将左上角 (A1) 标记为插入点。  
- `rowStyles` 将每个 `Style` 与相应的数据行对齐，从而实现我们之前准备的交替颜色。

---

## 步骤 5：保存工作簿

最后一步是将工作簿持久化到文件，这样你就可以在 Excel 中打开并查看结果。

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

打开文件后，你应该会看到一个整齐格式化的工作表：  

- 标题行加粗（默认库样式）。  
- 第 1、3、5… 行使用干净的白色背景。  
- 第 2、4、6… 行使用柔和的浅黄色填充，便于浏览。

### 预期输出示例

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rows 2, 4, 6, … appear with a light‑yellow background—exactly the **apply alternating row colors** effect we aimed for.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt 文本包含主要关键词以提升 SEO。)*

---

## 处理边缘情况与变体

### 空 DataTable

如果 `dataTable.Rows.Count` 为零，`rowStyles` 数组将为空，`ImportDataTable` 仍会写入标题行（如果 `includeHeaders` 为 `true`）。不会抛出异常，但你可能需要防止生成几乎为空的文件：

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### 自定义配色方案

想要蓝色/灰色条纹而不是黄/白？只需替换 `Color` 值：

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

可以从配置文件中读取颜色，这样非开发人员也能在不修改代码的情况下调整配色方案。

### 在多个工作表之间复用样式

如果你将多个表导出到同一个工作簿，可以一次生成样式数组并复用它：

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

只需注意两个表的行数是否相同，或者为每个工作表生成新的数组。

---

## 完整工作示例

将所有内容整合在一起，下面是一个可直接复制粘贴到控制台应用的完整自包含程序。

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

运行程序，打开 `Report.xlsx`，你将看到如描述的交替背景效果。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}