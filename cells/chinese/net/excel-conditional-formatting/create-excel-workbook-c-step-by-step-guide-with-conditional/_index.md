---
category: general
date: 2026-03-27
description: 使用 C# 和 Aspose.Cells 创建 Excel 工作簿，应用条件格式，将 DataTable 导入 Excel 并将工作簿保存为
  xlsx——一篇完整教程。
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: zh
og_description: 使用 Aspose.Cells 在 C# 中创建 Excel 工作簿，应用条件格式，将 DataTable 导入 Excel，并在几分钟内将工作簿保存为
  xlsx。
og_title: 使用 C# 创建 Excel 工作簿 – 包含条件格式的完整指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 创建 Excel 工作簿 – 带条件格式的逐步指南
url: /zh/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 C# – 完整编程教程

是否曾经需要 **create excel workbook c#**，但不知从何入手？你并不孤单——许多开发者在首次实现报表自动化时都会遇到这个难题。在本指南中，我们将一步步演示如何使用 Aspose.Cells 创建 excel workbook c#，应用条件格式，将 datatable 导入 Excel，最后将工作簿保存为 xlsx。

通过本教程，你将获得一个可直接运行的控制台应用程序，它会生成一个彩色的 Excel 文件，并且每行代码都有清晰的解释，方便你在自己的项目中进行改造。无需查阅外部文档，只需复制、粘贴、运行即可。

### 前置条件

- 已安装 .NET 6+（或 .NET Framework 4.7.2+）  
- Visual Studio 2022 或任意你喜欢的 C# 编辑器  
- Aspose.Cells for .NET（可通过 NuGet 获取免费试用版）  

如果你已经具备上述条件，下面开始吧。

## Create Excel Workbook C# – 初始化工作簿

首先，你需要通过实例化 `Workbook` 类来 **create excel workbook c#**。该对象在内存中表示整个 Excel 文件。

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **为什么重要：** `Workbook` 类抽象了文件格式，你无需处理底层 XML 或 COM 互操作。它还直接提供了对样式、表格和智能标记的访问。

## 应用条件格式

工作簿创建完成后，接下来 **apply conditional formatting**，将数量大于 100 的行高亮显示。条件格式位于工作表层面，而不是单元格层面，这使得它可以复用。

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **小技巧：** 如果需要更复杂的规则（例如在两个值之间），只需再次调用 `AddCondition` 并使用 `OperatorType.Between`。

## 编写标题和智能标记

在 **import datatable to excel** 之前，需要先放置占位单元格——智能标记，库会用实际数据替换它们。可以把它们看作模板标签。

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **为什么使用智能标记？** 它们让你可以将 Excel 布局与代码分离。你只需设计一次工作表，然后提供一个 `DataTable`，库会自动完成其余工作。

## 将 DataTable 导入 Excel

下面是 **import datatable to excel** 的核心部分。我们构建一个与智能标记字段对应的 `DataTable`，并将其交给 `ImportDataTable`。

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **边缘情况：** 如果你的表格列数多于需要的列，只需在智能标记中省略多余的列；它们会被忽略。

## 将工作簿保存为 XLSX

最后，我们 **save workbook as xlsx** 到磁盘。`Save` 方法会根据文件扩展名自动确定保存格式。

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

这就是完整的程序。运行后，你会在输出文件夹中看到名为 `SmartMarkersConditional.xlsx` 的文件。

### 预期输出

| 产品   | 数量 | 状态 |
|--------|------|------|
| Apple  | 120  | 高   |
| Banana | 80   | 低   |
| Cherry | 150  | 高   |

数量 **> 100** 的行（Apple 和 Cherry）将因之前添加的条件格式而显示黄色背景红色文字。

## Create Excel File Programmatically – 完整源码列表

下面是完整的、可直接复制的源代码。它包含了我们讨论的所有部分，并附加了一些额外的注释以提升可读性。

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **提示：** 如果需要生成多个工作表，只需在通过 `workbook.Worksheets.Add()` 获取的新 `Worksheet` 实例上重复步骤 2‑6 即可。

## 为什么选择 Aspose.Cells 进行 C# Excel 自动化？

- **性能卓越：** 完全在内存中操作，无需 COM 互操作，即使面对大数据集也非常快速。  
- **功能丰富：** 支持智能标记、条件格式、图表、数据透视表等众多特性。  
- **跨平台：** 在 Windows、Linux、macOS 上均可运行，兼容 .NET Core/5/6+。  

如果在使用某个特性时卡住了——比如添加图表或保护工作表——只需搜索 “asp​ose.cells add chart c#”，即可找到相似的实现方式。

## 后续步骤与相关主题

- **导出为 PDF：** 在 **create excel workbook c#** 之后，你可以使用 `workbook.Save("output.pdf")` 立即导出为 PDF。  
- **读取已有 Excel 文件：** 使用 `new Workbook("ExistingFile.xlsx")` 来修改模板。  
- **批量导入：** 对于海量数据，考虑使用 `ImportArray` 或带 `ImportOptions` 的 `ImportDataTable` 以提升速度。  

欢迎尝试不同的条件规则、颜色，甚至使用公式添加合计行。只要 **create excel file programmatically**，你的想象力就是唯一的限制。

---

*准备好动手了吗？获取代码，运行它，然后打开生成的 `SmartMarkersConditional.xlsx`。如果遇到任何问题，欢迎在下方留言——祝编码愉快！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}