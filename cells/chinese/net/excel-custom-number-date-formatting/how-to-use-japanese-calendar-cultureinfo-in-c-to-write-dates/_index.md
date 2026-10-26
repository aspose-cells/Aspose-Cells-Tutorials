---
category: general
date: 2026-10-26
description: 学习如何在 C# 中使用日本日历 CultureInfo 解析纪元日期并将其插入到使用 NPOI 的 Excel 工作表中。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: zh
lastmod: 2026-10-26
og_description: 在 C# 中使用日本日历 CultureInfo 解析令和时代的日期并将其写入 Excel 工作表。提供完整、可运行的代码以及解释。
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: 在 C# 中使用日本日历 CultureInfo – 完整的 Excel 示例
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: 如何在 C# 中使用日本历法 CultureInfo 将日期写入 Excel
url: /zh/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用日本历法 CultureInfo 将日期写入 Excel

如果您在 C# 中处理日期时需要 **使用日本历法 CultureInfo**，本指南将手把手教您实现。您将学习如何解析包含日本元号的日期字符串（例如 *Reiwa 2/5/1*），并使用 NPOI 库将得到的 `DateTime` 写入 Excel 工作表的第一个单元格。

在未使用正确的 `CultureInfo` 解析基于元号的日期时，会导致 `FormatException` 或月份/日期值错误。通过将 `CultureInfo` 配置为日本历法，您可以确保 .NET 运行时正确解释元号，并且写入 Excel 的值与原始的日本表示保持一致。

在本教程中，您将：

* 创建使用日本历法的 `CultureInfo` 对象。
* 使用 `DateTime.Parse` 解析日本元号日期字符串。
* 将解析后的 `DateTime` 插入到 NPOI 工作表单元格中。
* 查看完整的可运行程序以及预期输出。

> **先决条件** – .NET 6.0+（或 .NET Core 3.1+）、**NPOI** NuGet 包，以及对 C# 和 Excel 文件处理的基本了解。

---

## 您需要的内容

| 项目 | 原因 |
|------|------|
| **.NET SDK**（6.0 或更高） | 提供 `CultureInfo` 所需的运行时和库。 |
| **NPOI**（`NPOI` NuGet 包） | 让您在未安装 Office 的情况下创建和操作 Excel 文件。 |
| **Visual Studio Code**、**Visual Studio** 或任意 C# IDE | 用于编译和运行示例。 |
| **日本元号日期字符串**（例如 `"Reiwa 2/5/1"`） | 演示日本历法的使用。 |

---

## 第 1 步：安装 NPOI

在项目文件夹的终端中运行：

```bash
dotnet add package NPOI --version 2.6.1
```

该包提供后续使用的 `IWorkbook`、`ISheet` 和 `ICell` 类型。

---

## 第 2 步：创建使用日本历法的 CultureInfo

日本历法是基于元号的历法。您必须请求 `ja-JP` 区域设置的 *Japanese* 变体，并显式将日历设置为 `JapaneseCalendar`。

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **为什么重要** – 默认的 `ja-JP` 文化使用公历。重新分配 `Calendar` 属性可确保在解析时识别诸如 *Reiwa* 的元号名称。

---

## 第 3 步：解析日本元号日期字符串

现在 `CultureInfo` 已配置好，您可以安全地解析包含元号的字符串。

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**输出**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse` 方法将 *Reiwa 2* 解释为公历 2020 年 5 月 1 日。

### 边缘情况：处理无效元号

如果用户提供了不受支持的元号（例如在平成时代结束后仍使用 `"Heisei 31/4/30"`），`DateTime.Parse` 会抛出 `FormatException`。请使用 try‑catch 块提供友好的错误信息：

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## 第 4 步：将解析后的 DateTime 写入 Excel 工作表

准备好 `DateTime` 对象后，您可以将其存入 Excel 单元格。NPOI 会自动将 `DateTime` 值格式化为 Excel 日期。

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**结果** – 打开 *JapaneseEraDate.xlsx*，在单元格 A1 中会显示日期 **2020‑05‑01**。

### 为什么使用 NPOI？

*跨平台运行*（Windows、Linux、macOS），且 **不需要** Microsoft Office。这使得该方案适用于 CI 流水线、Docker 容器或服务器端处理。

---

## 第 5 步：完整、可运行的程序

将所有内容整合在一起，以下是演示完整流程的控制台应用程序代码：

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**运行方式**

```bash
dotnet run
```

执行后，您将在项目文件夹中找到 `JapaneseEraDate.xlsx`，其中包含正确解析的日期。

---

## 常见陷阱与最佳实践提示

| 陷阱 | 修复 / 建议 |
|------|------------|
| 忘记设置 `japaneseCulture.DateTimeFormat.Calendar` | 始终分配 `JapaneseCalendar` 实例；否则元号名称无法识别。 |
| 在未使用自定义 `CultureInfo` 的情况下使用 `DateTime.TryParse` | 将相同的 `japaneseCulture` 传递给 `TryParse`，以保持行为一致。 |
| 期望 Excel 显示元号 | Excel 内置的日期格式仅支持公历。如果需要显示元号，请将原始字符串存入其他列或使用自定义文本格式。 |
| 未释放 `FileStream` | 使用 `using` 块（如示例所示）确保及时释放文件句柄。 |
| 在多个线程间混用 `CultureInfo` 对象 | `CultureInfo` 对只读操作是线程安全的，但在初始设置后避免修改其 `Calendar` 属性。 |

---

## 结论

现在，您已经掌握了在 C# 中 **使用日本历法 CultureInfo**，准确解析日本元号日期并使用 NPOI 将得到的 `DateTime` 写入 Excel 工作表的完整方法。完整示例涵盖了配置、解析、错误处理以及 Excel 输出，为任何国际化报表或数据交换场景提供了坚实基础。

接下来，您可以进一步探索：

* **使用自定义文本格式化日期**，在 Excel 中保留元号显示。
* **从 Excel 中读取日期**，使用 `cell.DateCellValue` 并尊重日本历法。
* **将相同技术应用于其他基于元号的历法**（例如泰国佛历），只需将 `JapaneseCalendar` 替换为相应的 `Calendar` 子类。

欢迎尝试不同的元号字符串、更大的数据集，或将此逻辑集成到生成 Excel 报表的 ASP.NET Core API 中。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}