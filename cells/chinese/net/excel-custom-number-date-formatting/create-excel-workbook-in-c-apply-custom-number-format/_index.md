---
category: general
date: 2026-05-23
description: 在 C# 中创建 Excel 工作簿，学习如何应用自定义数字格式、以编程方式设置单元格样式、将单元格格式化为科学计数法，然后将工作簿保存为
  xlsx。
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: zh
og_description: 快速使用 C# 创建 Excel 工作簿。学习如何以编程方式应用自定义数字格式、设置单元格样式、格式化科学计数法，并保存为 xlsx。
og_title: 在 C# 中创建 Excel 工作簿 – 应用自定义数字格式
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: 在 C# 中创建 Excel 工作簿 – 应用自定义数字格式
url: /zh/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 Excel 工作簿 – 应用自定义数字格式

在 C# 中创建 Excel 工作簿比你想象的更简单。在本指南中，我们将逐步演示如何应用自定义数字格式、将单元格格式化为科学计数法、以编程方式设置单元格样式，最后将工作簿保存为 xlsx 文件。

如果你曾盯着空白的电子表格发呆，想要自动化整个过程——从填充数据到让数字呈现出你需要的样子——本教程正适合你。完成后，你将拥有一个可在任何电子表格程序中打开的完整功能的 Excel 文件，并且你会理解 **为什么** 每一步都很重要，而不仅仅是 **如何** 编写代码。

## 所需条件

- **.NET 6+**（或任何支持该库的近期 .NET Framework）  
- **Aspose.Cells for .NET**（或其他提供 `Workbook`、`Cell` 和 `CellFormat` 类的 API）  
- 适量的 C# 经验——只要会写 `Console.WriteLine`，就可以开始了。  

无需额外的配置文件、COM 互操作，也绝对不需要手动安装 Excel。

---

## 创建 Excel 工作簿 – 初始化 Workbook 对象

我们首先要做的是创建一个空的工作簿。把 `Workbook` 类想象成一块空白画布，你将在其上绘制行、列和样式。

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

就是这么简单——一行代码即可在内存中得到一个全新的 Excel 文件。`Workbook` 构造函数会创建默认的工作表集合，因此你可以立即开始添加数据。

> **专业提示：** 如果需要多个工作表，可以在填充单元格之前调用 `workbook.Worksheets.Add()`。

![创建 Excel 工作簿示例](image-placeholder.png "创建 Excel 工作簿截图")

*图片替代文字：在 IDE 中显示空白 Excel 工作表的创建 Excel 工作簿示例。*

## 为单元格应用自定义数字格式

工作簿已经创建好后，让我们在 **A1** 单元格中写入一个数字并为其设置自定义格式。自定义数字格式可以让你控制数字的显示方式——货币、百分比、日期，或者在本例中的科学计数法。

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

为什么要先获取样式？因为 `Cell` 对象内部保存了一个 **Style** 对象，里面包含字体、边框、对齐方式以及数字格式等所有属性。通过编辑 `Custom` 属性，我们告诉 Excel “使用带两位小数的科学计数法来显示此值”。

> **常见问题：** *我可以使用内置格式而不是自定义格式吗？*  
> 是的——将 `style.Number = 10` 设置为内置的科学计数法格式，但自定义字符串可以让你精确控制小数位数。

## 以编程方式设置单元格样式（超越数字格式）

通常你会想要的不止数字格式。我们给单元格添加粗体字体和浅灰色背景，使其更加突出。

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

请注意我们复用了之前调整过的同一个 `style` 对象。这正是 **以编程方式设置单元格样式** 的优势——只需获取一次样式，修改所需属性后写回。无需重新创建对象，也不会丢失已经设置好的数字格式。

## 科学计数法格式化单元格（边缘情况处理）

当处理非常大或非常小的数字时，科学计数法是救星。我们使用的自定义格式 (`0.00E+00`) 保证小数点后两位，并强制在指数前显示正号。下面是一个快速的验证示例：

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

打开生成的文件后，B2 将显示为 `1.23E-05`，从而确认 **科学计数法格式化单元格** 的指令对大数和小数都有效。

## 将工作簿保存为 XLSX

所有有趣的操作都在将文件写入磁盘时结束。`Save` 方法负责将内存中的表示转换为正式的 `.xlsx` 包。

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

这行代码实现了 **将工作簿保存为 xlsx** 的目标。如果目录不存在，`Save` 会抛出异常——因此请提前创建文件夹，或在调用时使用 try/catch 包裹。

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

现在你已经拥有一个可共享的 Excel 文件，里面包含格式良好的科学计数、粗体样式和浅灰色背景。

## 完整工作示例

下面是完整的、可直接复制粘贴的程序示例，展示了如何将所有部分组合在一起。它可以编译为控制台应用，也可以将逻辑嵌入任何 C# 项目中。

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**预期结果：** 打开 `CustomFormatted.xlsx`，你会看到：

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

两个单元格均为粗体、填充浅灰色，并以两位小数的科学计数法显示数字。

---

## 小结

我们已经从零 **创建 Excel 工作簿**、**应用自定义数字格式**、**科学计数法格式化单元格**、**以编程方式设置单元格样式**，并 **将工作簿保存为 xlsx**——全部只用了几行 C# 代码。该方法具备可扩展性：只需遍历行、克隆 `style` 对象，即可在几秒钟内生成完整样式的报表。

### 接下来可以做什么？

- **动态格式化：** 根据数值大小切换格式（例如货币 vs. 百分比）。  
- **多工作表：** 使用 `workbook.Worksheets.Add("Summary")` 构建仪表盘。  
- **高级样式：** 边框、条件格式和数据验证

## 相关教程

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}