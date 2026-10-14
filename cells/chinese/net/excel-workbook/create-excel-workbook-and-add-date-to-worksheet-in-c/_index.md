---
category: general
date: 2026-10-13
description: 使用 C# 创建 Excel 工作簿，并使用 Aspose.Cells 将日期写入 Excel。学习如何将 Excel 文件保存为 xlsx
  并将日期添加到工作表，附完整代码。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: zh
lastmod: 2026-10-13
og_description: 在 C# 中创建 Excel 工作簿并写入日期。请按照本完整指南，将 Excel 文件保存为 xlsx，并使用 Aspose.Cells
  将日期添加到工作表中。
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: 创建 Excel 工作簿并在工作表中添加日期 – C# 步骤详解
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中创建 Excel 工作簿并向工作表添加日期
url: /zh/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 Excel 工作簿并向工作表添加日期

如果您需要以编程方式 **create excel workbook**，本指南将向您展示如何 **write date to excel** 并将 **save excel file** 为 *.xlsx* 工作簿。您将看到一个完整的可运行示例，该示例解析日本皇纪字符串并将生成的 `DateTime` 存储在单元格 A1 中。

使用 C# 操作 Excel 通常需要三个步骤：实例化工作簿、将数据放入工作表、最后持久化文件。本教程涵盖每个步骤，解释代码为何如此编写，并强调常见的陷阱，例如特定文化的解析和文件系统权限。完成后，您可以 **add date to worksheet**、**save workbook as xlsx**，并将此模式适用于任何数据类型。

> **Prerequisite** – 示例使用 **Aspose.Cells for .NET** 库（版本 23.10 或更高）。通过 NuGet 安装它：

```bash
dotnet add package Aspose.Cells
```

您还需要一个 .NET 6+ SDK 和一个可写入的输出目录。

---

## 创建 Excel 工作簿并配置工作表

第一步是实例化一个空工作簿并获取其默认工作表。Aspose.Cells 会自动创建一个名为 “Sheet1” 的工作表。

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**为什么重要** – `Workbook` 是所有 Excel 操作的入口点。通过不带参数创建它，您将得到一个干净的工作簿，随后可以 **save excel file** 为任意格式。

---

## 解析日本皇纪日期

日本皇纪日期使用时代符号（例如 “R” 代表 Reiwa）后跟两位数字的年份。当您提供自定义的 `DateTimeParseOptions` 对象并指示解析器使用日本皇帝日历时，.NET 的 `DateTime.ParseExact` 方法能够处理此格式。

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**说明** –  
* `gg` 读取时代标识符（`R` 代表 Reiwa）。  
* `yy` 读取该时代内的两位数年份。  
* `MM/dd` 读取月份和日期。  

如果省略 `parseOptions`，解析器会假设使用公历并抛出 `FormatException`。这在处理非公历时是常见的边缘情况。

---

## 将日期写入工作表

现在您已经拥有 `DateTime` 值，可以将其放入单元格。Aspose.Cells 会根据值的类型自动格式化单元格。

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**为什么要设置样式？** – 如果不设置样式，Excel 可能会使用系统默认格式显示日期，这在不同地区的用户之间可能会产生混淆。显式定义 `"yyyy-mm-dd"` 可确保外观一致。

---

## 将 Excel 文件保存为 xlsx

最后，将工作簿持久化到磁盘。`Save` 方法会根据文件扩展名确定输出格式，因此使用 “.xlsx” 会自动触发 Office Open XML 格式。

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**提示** – 如果目标目录不存在或没有写入权限，`Save` 会抛出 `IOException`。在调用 `Save` 前请务必验证路径。

---

## 完整可运行示例

下面是完整的程序代码，您可以复制、粘贴并运行。它包含所有 `using` 指令、错误处理以及阐明每一步操作的注释。

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**预期结果**

打开 `JapaneseDate.xlsx` 时，单元格 A1 将显示日期 **2021‑04‑01**（Reiwa 3 / 04 / 01 对应的公历日期），并采用 `yyyy‑mm‑dd` 格式。

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="Excel 工作簿的截图，显示单元格 A1 中的日本皇纪日期"}

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| *What if the era changes (e.g., Heisei to Reiwa)?* | `JapaneseEmperor` 日历会自动将时代符号（`H`、`R` 等）映射到正确的公历范围，您只需更新输入字符串即可。 |
| *Can I write multiple dates in a column?* | 可以。遍历数据并对每一行调用 `sheet.Cells[row, column].PutValue(dateValue)` 即可。 |
| *What if I need a different date format?* | 将 `dateStyle.Custom` 改为任意 Excel 日期格式字符串，例如 `"dd-mmm-yyyy"` 或 `"mm/dd/yyyy"`。 |
| *Is there a way to protect the sheet after writing the date?* | 在保存之前使用 `sheet.Protect(ProtectOptions.All, "password")` 即可。 |
| *How do I handle time zones?* | `DateTime` 存储 UTC 或本地时间。可在调用 `PutValue` 前使用 `DateTime.SpecifyKind` 或 `TimeZoneInfo.ConvertTime` 进行转换。 |

---

## 结论

您现在已经掌握了使用 Aspose.Cells 在 C# 中 **create excel workbook**、**write date to excel**、**add date to worksheet** 并 **save workbook as xlsx** 的完整流程。完整示例演示了如何解析日本皇纪字符串、应用统一样式以及处理文件系统相关问题。

从这里您可以

## 接下来应该学习什么？

以下教程涵盖了与本指南紧密相关的主题，帮助您在项目中进一步使用 API 功能并探索替代实现方式，每篇资源均提供完整的可运行代码示例和逐步解释。

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook – Wrap Columns and Save as XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}