---
category: general
date: 2026-10-01
description: 学习如何使用 C# 创建 Excel 工作簿、应用自定义数字格式、设置单元格小数位数，并将工作簿保存为 XLSX 的完整分步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: zh
lastmod: 2026-10-01
og_description: 使用 C# 创建 Excel 工作簿，设置自定义数字格式、单元格小数位数，并将工作簿保存为 XLSX。遵循本完整指南，以获得精确的数值输出。
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: 使用 C# 创建 Excel 工作簿 – 自定义数字格式与 XLSX 导出
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: 如何使用 C# 创建带自定义数字格式的 Excel 工作簿
url: /zh/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用自定义数字格式创建 Excel 工作簿

如果您需要 **create excel workbook c#**，让数字以您想要的方式显示，本指南将向您展示如何通过几个清晰的步骤完成。您将学习如何应用自定义数字格式、设置单元格小数位数，最后 **save workbook as xlsx** 以供下游使用。

处理数值数据时常常需要在精度和可读性之间取得平衡。完成本教程后，您将拥有一个可复用的模式，能够将显示的数字限制为特定的有效数字位数，同时在文件中保留原始值。无需外部脚本——只需 C# 和 Aspose.Cells 库。

## 前提条件

在开始之前，请确保您具备：

* .NET 6.0 SDK 或更高版本已安装  
* Visual Studio 2022（或任意 C# IDE）  
* **Aspose.Cells for .NET** NuGet 包 (`Install-Package Aspose.Cells`) – 该库提供本文示例中使用的 `Workbook`、`Worksheet` 和 `ExportTableOptions` 类  

这些要求非常低，相同的代码可在 .NET Core、.NET Framework，甚至 Azure Functions 中运行。

## 第一步：创建 Excel 工作簿 C# – 初始化文件

首先需要实例化一个新的 `Workbook` 对象。该对象在内存中表示整个 Excel 文件，并自动包含一个默认工作表。

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Why this matters:**  
创建工作簿后即可获得一块干净的画布。默认工作表 (`Worksheets[0]`) 已准备好进行数据输入，除非您的场景需要多个标签页，否则无需额外添加工作表。

## 第二步：向单元格写入数值

现在将示例数字写入 **A1** 单元格。我们使用的值 (`123.456789`) 小数位数多于最终想要显示的位数，这样可以演示后续的四舍五入。

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` 会自动检测数据类型，无需将数字转换为字符串。

## 第三步：应用自定义数字格式 – 限制可见小数位

为了控制 Excel 显示数字的方式，我们创建一个带有 **custom number format** 的 `Style`。模式 `"0.######"` 告诉 Excel 最多显示六位小数，但会省略末尾的零。

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**How this works:**  
格式字符串遵循 Excel 的自定义格式语法。`0` 强制显示一个数字位，而 `#` 仅在该位有意义时才显示。将两者组合即可实现既灵活又保留原始精度的显示效果。

## 第四步：设置单元格小数位 – 使用 ExportTableOptions

如果需要为导出数据（例如转换为 DataTable）**set cell decimal places**，Aspose.Cells 允许您指定 **significant digits** 的数量。此步骤可确保导出的 CSV 或 DataTable 遵循工作簿中设置的相同四舍五入规则。

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Why use `SignificantDigits`?**  
不同于固定的小数位数，显著数字在限制精度的同时保留数值的数量级，这正是分析师在汇总数据时常期待的行为。

## 第五步：导出工作表数据并 **save workbook as xlsx**

最后，导出数据（如果需要 DataTable），并将工作簿持久化到磁盘。`ExportDataTable` 调用会遵循我们配置的 `ExportTableOptions`，而 `workbook.Save` 则生成标准的 XLSX 文件。

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Expected result:**  
在 Excel 中打开 *SigDigits.xlsx* 时，单元格 **A1** 显示 `123.5`。底层数值仍为 `123.456789`，但显示的数字遵循 4 位有效数字规则。如果将工作表导出为 DataTable，表中的值同样会被四舍五入为 `123.5`。

---

## 将自定义数字格式应用于其他单元格

如果需要对一段范围而非单个单元格进行格式化，可复用 `Style` 对象：

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** 复用样式对象可降低内存开销，并确保整张工作表的格式保持一致。

## 如何使用 C# 在 Excel 中格式化数字 – 常见变体

| 场景 | 格式字符串 | 结果 |
|----------|---------------|--------|
| Fixed two decimal places | `"0.00"` | `123.46` |
| Currency (US) | `"$#,##0.00"` | `$123.46` |
| Percentage with one decimal | `"0.0%"` | `12,346.0%` |
| Scientific notation | `"0.00E+00"` | `1.23E+02` |

选择符合您报告需求的模式。所有模式均兼容前文演示的 `Style.Custom` 属性。

## 根据用户输入动态设置单元格小数位

有时所需的精度在编译时并不确定。您可以在运行时构建格式字符串：

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Edge case:** 如果 `decimals` 为零，格式会变为 `"0"`（整数显示）。务必验证用户输入，以避免生成无效的格式字符串。

## 将工作簿保存为 XLSX – 最佳实践

* **Use absolute paths** 在写入已知目录时使用绝对路径（例如 `Path.Combine(Environment.CurrentDirectory, "output.xlsx")`）。  
* **Dispose** 如果在 `using` 语句中使用 `Workbook`，请及时释放非托管资源：

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Version compatibility:** Aspose.Cells 生成的文件兼容 Excel 2010‑2023，因而下游用户不会遇到格式兼容性问题。

---

## 完整工作示例

下面是完整的程序代码，您可以直接复制、粘贴并立即运行。它包含所有必要的 `using` 指令、注释以及错误处理。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Verification steps**

1. 运行程序 (`dotnet run`)。  
2. 打开 `SigDigits.xlsx`。  
3. 确认 **A1** 显示 `123.5`。  
4. 若打开文件的 XML（`.xlsx` 实际是 zip 包），您会在 `<c>` 元素的 `s` 属性中看到自定义格式 `"0.######"`。

---

## 结论

在本教程中，您学习了如何 **create excel workbook c#**、**apply custom number format**、**set cell decimal places**，以及使用 Aspose.Cells **save workbook as xlsx**。该方案展示了 Excel 内部的可视化格式化以及通过 `ExportTableOptions` 实现的数据导出四舍五入。

接下来您可以：

* 将此方法扩展到整段范围或整张表。  
* 使用 `StyleFlag` 将多种样式（字体、边框）组合在一起。  
* 通过遍历数据源并应用相同的格式化逻辑，实现报告的自动化生成。  

欢迎尝试不同的格式字符串、小数位数或导出选项，以满足您的特定报告需求。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在项目中探索替代实现方式。每篇资源均提供完整的可运行代码示例和逐步解释。

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}