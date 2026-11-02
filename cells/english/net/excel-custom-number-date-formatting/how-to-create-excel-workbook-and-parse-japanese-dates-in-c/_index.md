---
category: general
date: 2026-10-10
description: Create Excel workbook in C# and set cell value with a Japanese era date,
  then apply custom format and read date cell using Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell value
- apply custom format
- read date cell
- excel date parsing
language: en
lastmod: 2026-10-10
og_description: Create Excel workbook in C# and parse Japanese era dates. Learn to
  set cell value, apply custom format, and read date cell with Aspose.Cells.
og_image_alt: Screenshot showing a C# program that creates an Excel workbook and parses
  a Japanese era date
og_title: Create Excel workbook in C# – full guide to date parsing
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and set cell value with a Japanese era
    date, then apply custom format and read date cell using Aspose.Cells.
  headline: How to create Excel workbook and parse Japanese dates in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: How to create Excel workbook and parse Japanese dates in C#
url: /net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook and parse Japanese dates in C#

If you need to **create Excel workbook** from scratch, this guide shows you exactly how. You’ll learn to **set cell value** with a Japanese era date string, **apply custom format** that understands the era, and finally **read date cell** to obtain a .NET `DateTime`. The complete example works with the latest Aspose.Cells for .NET, so you can copy‑paste the code into any C# project.

Working with dates that include Japanese eras can be tricky because the default Excel parser does not recognize the era symbols. By using a custom number format (`[ja-JP-Era]`) you tell Excel how to interpret the string, enabling reliable **excel date parsing**. The steps below cover the whole workflow, from workbook creation to date extraction.

## Prerequisites

- .NET 6.0 or later (the code also runs on .NET Framework 4.7+)
- Aspose.Cells for .NET (NuGet package `Aspose.Cells`)
- Basic familiarity with C# and Visual Studio or any IDE of your choice

## Step 1: Create Excel workbook and add a worksheet

The first operation is to **create Excel workbook** in memory. Aspose.Cells creates a default worksheet automatically, but you can add more if needed.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // Optional: rename the default worksheet for clarity
        workbook.Worksheets[0].Name = "Dates";
```

Creating the workbook allocates the internal structures that later hold cells, styles, and formulas. No file is written at this point, which keeps the operation fast and testable.

## Step 2: Set cell value with a Japanese era date string

Next, **set cell value** to the Japanese era representation `"R5-04-01"` (Reiwa 5, April 1). The string follows the pattern `EraYear-MM-DD`.

```csharp
        // Step 2: Reference cell A1 on the first worksheet
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Put the Japanese era date string into the cell
        dateCell.PutValue("R5-04-01");
```

Using `PutValue` stores the raw text. Excel will treat it as a string until a number format tells it otherwise. This approach works for any custom calendar representation, not only Japanese eras.

## Step 3: Apply a custom number format that understands the Japanese era

Now **apply custom format** so Excel can translate the era string into an actual serial date. The format `[ja-JP-Era]yyyy/MM/dd` tells the engine to interpret the leading era character (`R` for Reiwa) and calculate the Gregorian date.

```csharp
        // Step 3: Apply a custom number format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";
```

The custom format is stored in the cell’s style object. Aspose.Cells respects this format during both rendering and value conversion, enabling reliable **excel date parsing** later in the pipeline.

## Step 4: Retrieve the parsed DateTime value from the cell

Finally, **read date cell** to obtain a .NET `DateTime`. The `DateTimeValue` property returns the converted value based on the custom format applied earlier.

```csharp
        // Step 4: Retrieve the parsed DateTime value
        DateTime parsedDate = dateCell.DateTimeValue;

        // Output the result to the console for verification
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
```

When the program runs, the console prints:

```
Parsed Gregorian date: 2023-04-01
```

The output confirms that the Japanese era string `"R5-04-01"` was correctly interpreted as April 1 2023.

## Full, runnable example

Putting the pieces together yields a self‑contained program you can compile and run immediately.

```csharp
using Aspose.Cells;
using System;

class JapaneseDateExample
{
    static void Main()
    {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Reference cell A1
        Cell dateCell = workbook.Worksheets[0].Cells["A1"];

        // Insert Japanese era date string
        dateCell.PutValue("R5-04-01");

        // Apply custom format for Japanese era parsing
        dateCell.Style.Custom = "[ja-JP-Era]yyyy/MM/dd";

        // Retrieve the parsed DateTime
        DateTime parsedDate = dateCell.DateTimeValue;

        // Show the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");

        // (Optional) Save the workbook to verify the visual format
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

Running the program creates `JapaneseEraDate.xlsx` with cell A1 displaying `2023/04/01` while the console shows the same Gregorian date. The file can be opened in Excel to see the formatted value.

## Why this approach works

- **create excel workbook** – Instantiating `Workbook` builds the full Excel file structure in memory without touching the disk.
- **set cell value** – `PutValue` stores raw text, which is necessary before applying a culture‑specific format.
- **apply custom format** – The `[ja-JP-Era]` token bridges the gap between era notation and Excel’s internal serial date system.
- **read date cell** – `DateTimeValue` automatically uses the cell’s style to perform the conversion, giving you a native `DateTime`.
- **excel date parsing** – By delegating parsing to the cell’s style, you avoid manual string manipulation, reducing bugs and improving locale support.

## Edge cases and practical tips

- **Different eras** – Use `S` for Showa, `H` for Heisei, `R` for Reiwa. The same format string works for all eras.
- **Invalid strings** – If the cell contains a malformed era date, `DateTimeValue` returns `DateTime.MinValue`. Check `dateCell.IsDate` before reading.
- **Multiple cells** – Apply the custom format to a whole range (`range.ApplyStyle(style)`) when you need to parse many dates.
- **Performance** – Setting the style once per column is faster than per‑cell for large sheets.
- **Saving options** – Aspose.Cells can output to XLSX, XLS, CSV, or PDF. Choose the format that matches downstream processing.

## Frequently asked questions

**Can I use the built‑in .NET culture instead of a custom format?**  
The .NET `CultureInfo` class does not understand Japanese era symbols in the same way Excel does. Using a custom number format is the most reliable method for **excel date parsing** of era strings.

**What if I need to write the date back to Excel in era format?**  
Set the cell’s value to a `DateTime` and apply the same custom format. Excel will display the era automatically.

**Does this work on older versions of Excel?**  
The `[ja-JP-Era]` token is supported by Excel 2010 and later. Aspose.Cells emulates the behavior, so the workbook displays correctly even when opened in older Excel versions that lack native era support.

## Conclusion

You now know how to **create Excel workbook**, **set cell value** with a Japanese era string, **apply custom format**, and **read date cell** to get a `DateTime`. This pattern provides robust **excel date parsing** without manual string handling, making your C# automation code both concise and reliable.

Next, explore related topics such as **formatting multiple date columns**, **working with other cultural calendars**, or **exporting the workbook to PDF**. Each extension builds on the same principles covered here, so you can adapt the solution to a wide range of localization scenarios. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook in C# – Apply Custom Number Format](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/)
- [Create Excel Workbook with Custom Format – C# Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-custom-format-c-guide/)
- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}