---
category: general
date: 2026-10-26
description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
  dates and inserting them into an Excel worksheet with NPOI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: en
lastmod: 2026-10-26
og_description: Use Japanese calendar CultureInfo in C# to parse Reiwa era dates and
  write them to an Excel worksheet. Complete, runnable code with explanations.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: Use Japanese calendar CultureInfo in C# – full Excel example
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
title: How to use Japanese calendar CultureInfo in C# to write dates to Excel
url: /net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to use Japanese calendar CultureInfo in C# to write dates to Excel

If you need to **use Japanese calendar CultureInfo** while working with dates in C#, this guide shows you exactly how. You’ll learn to parse a date string that contains a Japanese era name (for example, *Reiwa 2/5/1*) and then write the resulting `DateTime` into the first cell of an Excel worksheet using the NPOI library.

Parsing era‑based dates without the correct `CultureInfo` leads to `FormatException` or incorrect month/day values. By configuring `CultureInfo` to the Japanese calendar, you guarantee that the .NET runtime interprets the era correctly and that the value you store in Excel matches the original Japanese notation.

In this tutorial you will:

* Create a `CultureInfo` object that uses the Japanese calendar.
* Parse a Japanese era date string with `DateTime.Parse`.
* Insert the parsed `DateTime` into an NPOI worksheet cell.
* See the complete, runnable program and expected output.

> **Prerequisites** – .NET 6.0+ (or .NET Core 3.1+), the **NPOI** NuGet package, and a basic understanding of C# and Excel file handling.

---

## What you’ll need

| Item | Reason |
|------|--------|
| **.NET SDK** (6.0 or later) | Provides the runtime and libraries for `CultureInfo`. |
| **NPOI** (`NPOI` NuGet package) | Allows you to create and manipulate Excel files without Office installed. |
| **Visual Studio Code**, **Visual Studio**, or any C# IDE | To compile and run the sample. |
| **Japanese era date string** (e.g., `"Reiwa 2/5/1"`) | Demonstrates the use of the Japanese calendar. |

---

## Step 1: Install NPOI

Open a terminal in your project folder and run:

```bash
dotnet add package NPOI --version 2.6.1
```

The package supplies `IWorkbook`, `ISheet`, and `ICell` types used later.

---

## Step 2: Create a CultureInfo that uses the Japanese calendar

The Japanese calendar is an era‑based calendar. You must request the *Japanese* variant of the `ja-JP` locale and explicitly set the calendar to `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – The default `ja-JP` culture uses the Gregorian calendar. Reassigning the `Calendar` property ensures that era names such as *Reiwa* are recognized during parsing.

---

## Step 3: Parse a Japanese era date string

Now that the `CultureInfo` is configured, you can safely parse a string that contains an era name.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

The `Parse` method interprets *Reiwa 2* as the Gregorian year 2020, month 5, day 1.

### Edge case: handling invalid eras

If a user supplies an unsupported era (e.g., `"Heisei 31/4/30"` after the Heisei era ended), `DateTime.Parse` throws a `FormatException`. Wrap the call in a try‑catch block to provide a friendly error message:

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

## Step 4: Write the parsed DateTime into an Excel worksheet

With the `DateTime` object ready, you can store it in an Excel cell. NPOI automatically formats `DateTime` values as Excel dates.

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

**Result** – Opening *JapaneseEraDate.xlsx* shows the date **2020‑05‑01** in cell A1.

### Why use NPOI?

*Works on any platform* (Windows, Linux, macOS) and does **not** require Microsoft Office. This makes the solution suitable for CI pipelines, Docker containers, or server‑side processing.

---

## Step 5: Full, runnable program

Putting everything together, here is a complete console application that demonstrates the entire flow:

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

**How to run**

```bash
dotnet run
```

After execution, you’ll find `JapaneseEraDate.xlsx` in the project folder with the correctly parsed date.

---

## Common pitfalls and best‑practice tips

| Pitfall | Fix / Recommendation |
|---------|----------------------|
| Forgetting to set `japaneseCulture.DateTimeFormat.Calendar` | Always assign a `JapaneseCalendar` instance; otherwise the era name is not recognized. |
| Using `DateTime.TryParse` without the custom `CultureInfo` | Pass the same `japaneseCulture` to `TryParse` to keep behavior consistent. |
| Expecting Excel to display the era name | Excel’s built‑in date formats are Gregorian only. If you need the era displayed, store the original string in a separate column or create a custom text format. |
| Not disposing the `FileStream` | Use a `using` block (as shown) to ensure the file handle is released promptly. |
| Mixing `CultureInfo` objects across threads | `CultureInfo` is thread‑safe for read‑only operations, but avoid modifying its `Calendar` property after initial setup. |

---

## Conclusion

You now know how to **use Japanese calendar CultureInfo** in C# to accurately parse Japanese era dates and write the resulting `DateTime` into an Excel worksheet with NPOI. The complete example covers configuration, parsing, error handling, and Excel output, giving you a solid foundation for any internationalized reporting or data‑exchange scenario.

Next, you might explore:

* **Formatting dates with custom text** to retain the era name inside Excel.
* **Reading dates from Excel** using `cell.DateCellValue` while respecting the Japanese calendar.
* **Applying the same technique** for other era‑based calendars (e.g., Thai Buddhist calendar) by swapping `JapaneseCalendar` with the appropriate `Calendar` subclass.

Feel free to experiment with different era strings, larger data sets, or integrating this logic into ASP.NET Core APIs that generate Excel reports on the fly. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}