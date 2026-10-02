---
category: general
date: 2026-03-30
description: 使用 C# 创建带有货币格式的 Excel 工作簿。学习如何导入 DataTable、添加 Excel 数字格式，并在几分钟内为列应用货币格式。
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: zh
og_description: 使用 C# 创建 Excel 工作簿并立即将单元格格式设置为货币。本分步教程展示了如何将 DataTable 导入 Excel 并为列添加数字格式。
og_title: 使用 C# 创建 Excel 工作簿 – 货币格式化指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 创建 Excel 工作簿 – 应用货币格式并导入 DataTable
url: /zh/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 C# – 应用货币格式并导入 DataTable

是否曾需要 **create Excel workbook C#** 并且已经像精美报告一样？也许你正从数据库中提取销售数据，并希望价格列以美元显示，而无需手动在 Excel 中调整。听起来很熟悉吗？你并不孤单——大多数开发者在首次自动化 Excel 导出时都会遇到这个问题。

在本指南中，我们将逐步演示一个完整、可直接运行的解决方案，该方案 **creates an Excel workbook C#**，导入 `DataTable`，并 **formats the Price column as currency**。完成后，你将得到一个名为 `StyledTable.xlsx` 的文件，打开后即可看到格式良好的数字。无需额外的后处理。

> **你将学到的内容**
> - 如何在 .NET 项目中设置 Aspose.Cells  
> - 如何 **import datatable to excel** 使用样式数组  
> - 如何 **add number format excel** 为特定列设置数字格式  
> - 处理更多列或不同地区设置的技巧  

> **先决条件**  
> - 已安装 .NET 6+（或 .NET Framework 4.6+）  
> - Aspose.Cells for .NET NuGet 包 (`Install-Package Aspose.Cells`)  
> - 对 C# 和 DataTables 有基本了解  

## Step 1: Prepare the DataTable (import datatable to excel)

首先，我们需要一些示例数据。在真实的应用中，你可能会通过数据库查询填充此表，但硬编码示例可以保持简单。

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*为什么这很重要*：`DataTable` 是业务数据与 Excel 文件之间的桥梁。Aspose.Cells 可以直接导入它，保留列名和数据类型。

## Step 2: Spin Up a New Workbook (create excel workbook c#)

现在我们创建实际的 Excel 文件对象。可以把它看作是你将要绘制的空白画布。

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **专业提示**：如果需要多个工作表，请调用 `workbook.Worksheets.Add()` 并为每个工作表提供有意义的名称。

## Step 3: Define a Currency Style (format cells currency)

Aspose.Cells 允许你创建一个描述单元格外观的 `Style` 对象。对于货币，我们使用内置的数字格式 ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*为什么不直接设置格式字符串？* 使用内置 ID 可确保在不同 Excel 版本之间的兼容性，并避免地区特定的怪异行为。

## Step 4: Build the Style Array (apply currency format column)

在导入 `DataTable` 时，你可以传入一个 `Style` 对象数组——每列一个。`null` 表示“使用默认样式”。这里我们仅对第二列应用 `priceStyle`。

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

如果以后添加更多列，只需相应地扩展数组。`columnStyles` 的长度必须与导入的列数匹配，否则 Aspose 会抛出异常。

## Step 5: Import the DataTable with Styles (import datatable to excel)

现在魔法发生了——我们的 `DataTable` 被放入工作表，且价格列立即显示为货币格式。

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*如果有超过两列怎么办？* 只需扩展 `columnStyles`，让每列获得相应的样式（或 `null` 使用默认）。这是有选择地 **add number format excel** 的最简洁方式。

## Step 6: Save the Workbook (create excel workbook c#)

最后，我们将文件写入磁盘。选择任意你有写入权限的文件夹。

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

在 Excel 中打开 `StyledTable.xlsx`，你应该看到：

| 产品 | 价格 |
|------|------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

**Price** 列已经格式化为货币——无需额外步骤。

## Edge Cases & Variations

### More Columns, Different Formats

如果需要为多个列（例如 Cost、Tax、Total） **format cells currency**，请为每个列创建单独的 `Style` 并相应填充 `columnStyles`：

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑Specific Currency

对于欧元或英镑，使用不同的内置 ID（例如，165 对应 `€#,##0.00`）。或者，设置自定义格式字符串：

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Large Data Sets

Aspose.Cells 能处理数百万行，但内存消耗会随样式对象增加。对所有货币列复用同一个 `Style` 实例，以保持占用低。

### Missing Styles

如果 `columnStyles` 的长度小于列数，Aspose 会对其余列使用默认样式。当你只关心少数列时，这很方便。

## Full Working Example (All Steps Combined)

下面是完整的程序，你可以复制粘贴到控制台应用中。它包含了我们讨论的所有部分，并附带一些有用的注释。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**预期结果**：打开 `StyledTable.xlsx` 时，`Price` 列显示美元符号和两位小数，正好符合 `format cells currency` 指令的要求。

## Frequently Asked Questions

**Q: 这在 .NET Core 上能工作吗？**  
A: 当然可以。Aspose.Cells 符合 .NET‑standard 标准，因此你可以针对 .NET 5、.NET 6 或更高版本而无需更改。

**Q: 如果我的 DataTable 有 10 列，但我只想格式化第 5 列怎么办？**  
A: 创建长度为 10 的 `Style[]`，将位置 0‑4 和 6‑9 填入 `null`，并在索引 4（从零开始）处放置自定义样式。Aspose 会遵循每个条目。

**Q: 我可以隐藏标题行吗？**  
A: 导入后，设置 `worksheet.Cells.Rows[0].Hidden = true;`，或者在 `ImportDataTable` 中将 `includeColumnNames` 参数设为 `false`。

## Conclusion

我们刚刚 **created an Excel workbook C#**，导入了 `DataTable`，并使用 Aspose.Cells **applied a currency format column**。主要步骤——准备数据、定义样式、构建样式数组、使用 `ImportDataTable` 导入以及保存——涵盖了大多数 Excel 自动化任务的核心。

从这里你可以进一步探索：

- 为日期或百分比 **add number format excel**  
- 在单个文件中导出多个工作表  
- 使用 **format cells currency** 与地区特定符号  
- 基于相同数据自动生成图表  

尝试一下，你很快就会成为团队中 Excel 报告的首选专家。有什么独特的做法想分享？在下方留言——祝编码愉快！  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}