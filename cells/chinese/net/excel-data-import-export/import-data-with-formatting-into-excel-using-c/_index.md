---
category: general
date: 2026-03-01
description: 使用 C# 将带格式的数据导入 Excel。学习如何将 DataTable 导入 Excel，并在仅几步内为单元格添加背景颜色。
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: zh
og_description: 使用 C# 将带格式的数据导入 Excel。一步步指南，展示如何导入 DataTable 并为单元格添加背景颜色。
og_title: 将带格式的数据导入 Excel – C# 指南
tags:
- C#
- Excel
- DataTable
- Formatting
title: 使用 C# 将带格式的数据导入 Excel
url: /zh/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 将带格式的数据导入 Excel

是否曾经需要 **import data with formatting** 到 Excel 工作簿，但却只得到一张普通、乏味的表格？你并不孤单。当开发者发现默认导入会剥除他们在源数据中精心设置的所有颜色和样式时，往往会碰到这个问题。

在本教程中，我们将逐步演示一个完整、可直接运行的解决方案，能够 **imports a DataTable into Excel** 并 **adds background color to Excel cells**。无需额外的后处理——你的电子表格将直接以你想要的样子呈现。

## 你将学到

- 如何将数据检索到 `DataTable` 中。
- 如何定义一个携带背景颜色的 `Style` 对象数组。
- 如何使用这些样式调用 `ImportDataTable`，使导入保留格式。
- 一个完整、可运行的示例，你可以直接放入控制台应用并立即看到结果。
- 实际项目中的技巧、常见陷阱以及变体。

### 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）。
- **GemBox.Spreadsheet** 库（免费版已足够演示）。
- 对 C# 和 Excel 概念有基本了解。

如果你在想 *why GemBox?*，因为它提供了接受样式数组的单行 `ImportDataTable` 方法——正是我们在 **import data with formatting** 时无需编写循环所需要的。

---

## 第一步：设置项目并添加 GemBox.Spreadsheet

要开始，请创建一个新的控制台应用：

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** 免费版将工作表限制在 150 k 单元格，对于演示来说已经足够。如果遇到限制，可升级或切换到 EPPlus，但 API 会略有不同。

## 第二步：将源数据检索为 `DataTable`

我们首先需要一个模拟从数据库中通常获取的数据的 `DataTable`。下面是一个在内存中创建它的简易帮助方法：

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Why this matters:** 通过将数据检索封装在独立的方法中，你可以随意替换任何来源——SQL、CSV、Web 服务——而无需触及导入逻辑。这让代码保持整洁，也使本教程 **how to import datatable into excel** 具备可复用性。

## 第三步：定义要应用的样式

现在进入有趣的部分：我们将创建一个 `Style` 对象数组，每个对象拥有不同的 `ForegroundColor`。GemBox 允许你设置 `BackgroundPatternColor`（单元格填充）和 `ForegroundColor`（文字颜色）。本示例中我们将前两列分别着色。

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Explanation:**  
- `Style` 对象是轻量级容器；不需要为每个单元格都创建新实例。  
- 将数组顺序与列顺序对应，GemBox 会在导入时自动匹配相应的样式。  
- 这就是实现 **import data with formatting** 的关键——格式随数据一起传递，而不是事后再处理。

## 第四步：使用样式将 `DataTable` 导入工作表

准备好数据和样式后，我们可以创建工作簿、选取第一个工作表，并调用 `ImportDataTable`。方法签名如下：

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

下面是具体使用方式：

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**What’s happening under the hood?**  
- `true` 表示让 GemBox 将列名写入第一行。  
- `0, 0` 将导入定位在单元格 A1。  
- `importStyles` 将每列与前面定义的颜色关联起来。  

打开 *Report.xlsx* 时，你会看到 **ID** 列呈浅蓝色背景，**Name** 列呈浅绿色背景，而 **Score** 列保持默认白色背景。这就是一次调用完成的 **import data with formatting**。

## 第五步：验证结果（预期输出）

打开生成的 `Report.xlsx`，你应该会看到类似下面的内容：

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- **ID** 列的单元格拥有浅蓝色背景。  
- **Name** 列的单元格拥有浅绿色背景。  
- **Score** 列保持默认的白色背景。

这类视觉提示让报告一目了然，能够显著提升用户体验。

![Excel 表格显示 import data with formatting 示例 – ID 列浅蓝色，Name 列浅绿色](excel-screenshot.png "import data with formatting 示例")

*图片 alt 文本包含主要关键词，以提升 SEO 效果。*

---

## 常见问题与边缘情况

### 能否应用除背景色之外的其他样式？

当然可以。`Style` 还能设置字体、边框、数字格式，甚至条件格式。例如，将分数大于 90 的单元格设为粗体红色：

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### 如果我的 DataTable 列数多于样式数组怎么办？

GemBox 只会对数组中有对应条目的列应用样式。多余的列会使用默认样式——不会抛出错误。

### 这在处理大数据集时可行吗？

可以，但请留意免费版的单元格上限（150 k 单元格）。对于超大报表，建议购买付费许可证，或改用逐行写入 `worksheet.Cells[row, col].Value = …` 的方式——不过那样就失去了一行代码的便利。

### 如何从已有的 Excel 模板中导入带格式的数据？

可以先加载模板工作簿：

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

这样既能保留标题徽标、页脚以及预设样式，又能对动态部分执行 **import data with formatting**。

## 完整可运行示例（复制粘贴即用）

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

运行程序（`dotnet run`），打开生成的 *Report.xlsx*，即可立即看到颜色效果。

## 结论

You now have a solid, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}