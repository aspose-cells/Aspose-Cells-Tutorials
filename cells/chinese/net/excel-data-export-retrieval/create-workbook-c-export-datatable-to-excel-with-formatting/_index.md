---
category: general
date: 2026-02-15
description: 使用 C# 创建工作簿并将 DataTable 导出到 Excel，进行行格式设置、设置行背景，并在几分钟内实现 Excel 任务自动化。
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: zh
og_description: 快速使用 C# 创建工作簿，应用行样式，并通过完整代码示例和最佳实践技巧实现 Excel 导出自动化。
og_title: 创建工作簿 C# – 将 DataTable 导出为带格式的 Excel
tags:
- C#
- Excel
- DataExport
title: 创建工作簿 C# – 将 DataTable 导出为带格式的 Excel
url: /zh/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建工作簿 C# – 将 DataTable 导出到 Excel 并进行格式化

是否曾经需要 **create workbook C#** 并将 `DataTable` 导入到 Excel 并进行自定义样式设置？你并不孤单。在许多行业应用中，需求是导出一个格式良好的电子表格，让非技术用户能够立即打开并理解。

在本指南中，我们将逐步演示一个完整、可直接运行的解决方案，向您展示 **how to create workbook C#**、应用 **excel export formatting**、设置 **row background**，以及利用 **excel automation c#** 生成精美文件。没有模糊的“查看文档”快捷方式——只有完整代码、每行代码意义的解释，以及您明天就能使用的技巧。

---

## 先决条件

- .NET 6（或 .NET Framework 4.6+）。  
- Visual Studio 2022 或任何兼容 C# 的 IDE。  
- **Aspose.Cells for .NET** NuGet 包（或任何提供 `Workbook`、`Worksheet`、`Style` 的库）。  
- 对 `DataTable` 的基本了解。

如果您还没有 Aspose.Cells，请运行：

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** 免费试用适用于大多数开发场景；只需记得在发布前替换许可证密钥。

![创建工作簿 C# 示例，展示 Excel 中带样式的行]( "创建工作簿 C# 示例，带行背景颜色")

---

## 步骤 1：初始化工作簿和工作表（Create Workbook C#）

您首先需要实例化一个 `Workbook`。可以把它想象成在内存中打开一个全新的 Excel 文件。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**为什么？**  
`Workbook` 包含整个 Excel 文档，而 `Worksheet` 代表单个标签页。使用全新的工作簿可以确保您掌控输出的每个细节——不会出现隐藏的默认样式。

---

## 步骤 2：准备示例 DataTable（Export DataTable Excel）

在实际项目中，您会从数据库中获取数据，但为了演示，我们将在运行时构建一个小型 `DataTable`。

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**为什么这很重要：**  
导出 `DataTable` 是将应用程序中的表格数据移动到 Excel 的最常见方式。上述方法是完全自包含的，您可以复制粘贴到任何项目中即可运行。

---

## 步骤 3：为每行创建样式（Excel Export Formatting）

为了给每行设置独立的背景颜色，我们为 `DataTable` 中的每一行生成一个 `Style` 对象。这正是 **excel export formatting** 发挥作用的地方。

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**为什么要按行样式化？** 如果需要突出显示特定记录（例如逾期发票），可以用条件逻辑替代简单的颜色循环——只需根据行数据设置 `style.ForegroundColor`。

---

## 步骤 4：使用行样式导入 DataTable（Set Row Background）

现在我们将所有内容整合起来：数据、工作簿和样式。

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**您将看到的结果：** 打开 `EmployeesReport.xlsx`，会看到标题行使用默认格式，随后四行数据各自带有淡背景色。结果看起来像是手工制作的报告，而非枯燥的导出。

---

## 步骤 5：高级 Excel Automation C# 提示（Excel Automation C#）

下面列出几个可以在基础示例之上叠加的快速技巧：

| 技巧 | 代码片段 | 使用时机 |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | 导入数据后，以避免文本被截断。 |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | 当表格可能滚动超出屏幕时。 |
| **Conditional Formatting** | <details><summary>显示</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | 突出显示超过阈值的薪资。 |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | 当您需要只读报告时。 |

这些代码片段展示了 **excel automation c#** 的广度——您可以在不重写核心导入逻辑的情况下不断扩展工作簿。

---

## 常见问题与边缘情况

**如果 DataTable 有成千上万行怎么办？** Aspose.Cells 能高效流式处理数据，但您可能想关闭对每行的样式创建以节省内存。相反，可对一个范围应用单一样式：

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**我可以导出为 .csv 而不是 .xlsx 吗？** 当然——只需更改保存格式：

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

样式将会丢失（CSV 不支持样式），但数据导出保持不变。

**这在 .NET Core 上能工作吗？** 可以。Aspose.Cells 支持 .NET Standard 2.0 及更高版本，因此相同代码可在 .NET 6、.NET 7 或 .NET Framework 上运行。

---

## 完整可运行示例（复制粘贴即可）

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}