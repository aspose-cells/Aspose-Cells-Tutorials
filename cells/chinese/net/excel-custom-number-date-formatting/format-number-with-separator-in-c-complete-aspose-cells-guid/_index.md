---
category: general
date: 2026-03-30
description: 学习如何在 C# 中使用 Aspose.Cells 对数字进行分隔符格式化。包括设置自定义数字格式、添加千位分隔符、格式化小数位以及如何格式化单元格。
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: zh
og_description: 在 C# 中使用分隔符格式化数字。本指南展示了如何设置自定义数字格式、添加千位分隔符、格式化小数位，以及如何使用 Aspose.Cells
  格式化单元格。
og_title: 在 C# 中使用分隔符格式化数字 – Aspose.Cells 教程
tags:
- C#
- Aspose.Cells
- Number Formatting
title: 在 C# 中使用分隔符格式化数字 – 完整的 Aspose.Cells 指南
url: /zh/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 为数字添加分隔符 – 完整 Aspose.Cells 指南

是否曾经需要在电子表格中**为数字添加分隔符**但不确定使用哪个 API 调用？你并不是唯一的——开发者在导出数据时经常要处理千位分隔符、小数位数和自定义模式。

好消息：Aspose.Cells 让这件事轻而易举。在本教程中，我们将通过一个真实案例演示**设置自定义数字格式**、**添加千位分隔符**、**格式化小数位数**，并展示**如何将单元格格式化为字符串**。完成后，你将拥有一个可直接在任何 .NET 项目中使用的完整代码片段。

## 本指南涵盖内容

* 需要的 NuGet 包以及如何安装。  
* 步骤清晰的代码，创建工作簿、写入数值并应用自定义格式。  
* 为什么 `ExportTableOptions.ExportAsString` 是获取格式化值的首选方式。  
* 常见陷阱——例如忘记启用 `ExportAsString` 或使用错误的格式掩码。  
* 如需不同的小数位数或不同的分隔符样式，如何调整格式掩码。

无需外部文档链接，所有内容都在这里。让我们开始吧。

---

## 前置条件

| 需求 | 原因 |
|------|------|
| .NET 6.0 或更高版本 | Aspose.Cells 23.10+ 目标 .NET Standard 2.0+，因此 .NET 6 安全且是当前主流。 |
| Visual Studio 2022（或任意 C# IDE） | 便于调试和包管理。 |
| Aspose.Cells for .NET NuGet 包 | 提供我们将使用的 `Workbook`、`Worksheet` 和 `ExportTableOptions` 类。 |

你可以通过包管理控制台安装该包：

```powershell
Install-Package Aspose.Cells
```

就这么简单——无需额外 DLL、无需 COM 互操作，只需一个 NuGet 引用。

---

## 第 1 步：初始化新工作簿（如何格式化单元格）

首先创建一个全新的 `Workbook` 实例。它相当于一个空的 Excel 文件，准备接受数据。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **为什么这很重要：**`Workbook` 是 Aspose.Cells 中所有操作的入口。通过获取第一个工作表 (`Worksheets[0]`)，我们得到一个干净的画布，无需额外命名工作表。

---

## 第 2 步：将数值写入目标单元格

接下来，将原始数字写入 **A1** 单元格。此时数值尚未格式化，仅是一个 double。

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **小技巧：**当你计划后续应用数字格式时，请使用 `PutValue` 而不是 `PutString`。这会保留底层数据类型，便于 Excel 兼容的计算。

---

## 第 3 步：设置自定义数字格式（添加千位分隔符并格式化小数位数）

现在进入教程核心：定义一个格式掩码，告诉 Aspose.Cells 如何显示数字。掩码 `#,##0.00` 实现了三件事：

1. **`#,##0`** – 默认使用逗号作为千位分隔符。  
2. **`.00`** – 强制显示两位小数。  

如果需要不同的小数位数，只需更改小数点后 `0` 的数量。

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **为什么使用 `ExportAsString`：**默认情况下，`ExportString` 返回原始值。将 `ExportAsString = true` 设置为 true 会在转换为文本之前先应用 `NumberFormat` 掩码。这在需要将精确的字符串表示用于报表、JSON 或 UI 显示时至关重要。

---

## 第 4 步：导出格式化文本（如何格式化单元格）

准备好选项后，我们在同一个单元格上调用 `ExportString`。该方法会遵循我们刚定义的掩码，并返回一个格式化好的字符串。

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

运行程序后，控制台会打印 **`12,345.68`**，正是我们期望的格式。

> **边缘情况：**如果源数字的小数位超过两位，掩码会进行四舍五入。如果需要截断而非四舍五入，必须在调用 `PutValue` 前使用 `Math.Truncate` 预处理数值。

---

## 第 5 步：微调格式 – 常见变体

### 5.1 更改小数精度

想要三位小数吗？只需替换掩码：

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 使用不同的千位分隔符

某些地区更喜欢空格或句点。可以直接在掩码中嵌入该字符：

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

或者依赖工作簿的区域设置：

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 前缀或后缀（货币、百分比）

在掩码中直接加入美元符号或百分号：

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **注意：**掩码区分大小写。`$` 和 `%` 是字面符号，不会影响底层数值。

---

## 第 6 步：完整可运行示例（复制粘贴即用）

下面是可以直接复制到新控制台应用中的完整程序。它包含所有步骤、注释以及最终输出验证。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

运行程序（在终端执行 `dotnet run` 或在 Visual Studio 中按 F5），即可看到如上所示的格式化数字。

---

## 常见问题解答 (FAQ)

**问：这在旧版本的 Excel 中也能工作吗？**  
答：可以。格式掩码遵循 Excel 原生的数字格式语法，任何能够识别 `#,##0.00` 的 Excel 版本都会呈现相同的字符串。

**问：如果需要格式化一整块单元格怎么办？**  
答：遍历目标范围，对每个单元格应用相同的 `ExportTableOptions`，或者在该范围上设置 `Style.Custom` 属性，然后在任意单元格上调用 `ExportString`。

**问：能直接导出为 CSV 并保留这些格式吗？**  
答：完全可以。在为每个单元格设置格式后，使用 `Workbook.Save("output.csv", SaveFormat.CSV);`。Aspose.Cells 在生成 CSV 时会尊重单元格的 `Style`。

---

## 结论

我们已经展示了如何在 C# 中使用 Aspose.Cells **为数字添加分隔符**，涵盖了从**设置自定义数字格式**、**添加千位分隔符**、**格式化小数位数**到**如何将单元格格式化为字符串**的完整过程。代码完全自包含，适用于 .NET 6+，并可根据任何地区或精度需求进行调整。

接下来，你可以尝试：

* 将相同技术应用于日期和时间（`NumberFormat = "dd‑MMM‑yyyy"`）。  
* 自动化批量导出，为每列设置不同的掩码。  
* 将格式化后的字符串集成到使用 Aspose.Words 的 PDF 报表中。

试一试这些技巧，你很快就会成为团队中电子表格格式化的首选专家。祝编码愉快！   (Image: ![显示在 Aspose.Cells 输出中的带分隔符的格式化数字的截图](image-placeholder.png){alt="在 Aspose.Cells 输出中显示的带分隔符的格式化数字"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}