---
category: general
date: 2026-10-01
description: C#로 Excel 워크북을 만들고 사용자 지정 숫자 형식을 적용하며 셀 소수점 자리수를 설정하고, 워크북을 XLSX 형식으로
  저장하는 방법을 단계별 완전 가이드에서 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: ko
lastmod: 2026-10-01
og_description: C#로 Excel 워크북을 만들고 사용자 지정 숫자 형식을 적용하며 셀 소수점 자리수를 설정한 뒤 워크북을 XLSX 형식으로
  저장합니다. 정확한 숫자 출력을 위해 이 완전한 가이드를 따라보세요.
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: C#로 Excel 워크북 만들기 – 사용자 지정 숫자 형식 및 XLSX 내보내기
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
title: C#에서 사용자 지정 숫자 서식을 사용하여 Excel 워크북 만들기
url: /ko/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook C# with custom number formatting

If you need to **create excel workbook c#** that displays numbers exactly the way you want, this guide shows you how to do it in a few clear steps. You’ll learn to apply a custom number format, set cell decimal places, and finally **save workbook as xlsx** for downstream consumption.

Working with numeric data often means balancing precision and readability. By the end of this tutorial you’ll have a reusable pattern that limits displayed digits to a specific number of significant figures while preserving the original value in the file. No external scripts are required—just C# and the Aspose.Cells library.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* Visual Studio 2022 (or any C# IDE)  
* The **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`) – this library provides the `Workbook`, `Worksheet`, and `ExportTableOptions` classes used in the examples.  

These requirements are minimal; the same code works in .NET Core, .NET Framework, and even in Azure Functions.

## Step 1: Create Excel workbook C# – initialize the file

The first operation is to instantiate a new `Workbook` object. This object represents the entire Excel file in memory and automatically contains a default worksheet.

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
Creating the workbook up front gives you a clean canvas. The default worksheet (`Worksheets[0]`) is ready for data entry, so you don’t need to add a new sheet unless your scenario calls for multiple tabs.

## Step 2: Write a numeric value to a cell

Now put a sample number into cell **A1**. The value we use (`123.456789`) contains more decimal places than we eventually want to display, which lets us demonstrate rounding later.

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` automatically detects the data type, so you don’t have to convert the number to a string.

## Step 3: Apply custom number format – limit visible decimals

To control how Excel shows the number, we create a `Style` with a **custom number format**. The pattern `"0.######"` tells Excel to display up to six decimal places but omit trailing zeros.

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**How this works:**  
The format string follows Excel’s custom‑format syntax. `0` forces a digit, while `#` displays a digit only if it’s significant. By combining them you get a flexible display that still respects the original precision.

## Step 4: Set cell decimal places – using ExportTableOptions

If you need to **set cell decimal places** for exported data (e.g., when converting to a DataTable), Aspose.Cells lets you specify the number of **significant digits**. This step ensures the exported CSV or DataTable respects the same rounding rules you applied in the workbook.

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Why use `SignificantDigits`?**  
Unlike a fixed decimal count, significant digits preserve the magnitude of the number while limiting precision, which is often what analysts expect when summarizing data.

## Step 5: Export the worksheet data and **save workbook as xlsx**

Finally, export the data (if you need a DataTable) and persist the workbook to disk. The `ExportDataTable` call respects the `ExportTableOptions` we configured, and `workbook.Save` writes a standard XLSX file.

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Expected result:**  
When you open *SigDigits.xlsx* in Excel, cell **A1** shows `123.5`. The underlying value remains `123.456789`, but the displayed number respects the 4‑significant‑digit rule. If you export the sheet to a DataTable, the value in the table will also be rounded to `123.5`.

---

## Apply custom number format to additional cells

If you need to format a range rather than a single cell, reuse the `Style` object:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** Re‑using a style object reduces memory overhead and guarantees consistent formatting across the sheet.

## How to format numbers Excel using C# – common variations

| Scenario | Format string | Result |
|----------|---------------|--------|
| 소수점 두 자리 고정 | `"0.00"` | `123.46` |
| 통화 (미국) | `"$#,##0.00"` | `$123.46` |
| 소수점 한 자리 퍼센트 | `"0.0%"` | `12,346.0%` |
| 과학적 표기법 | `"0.00E+00"` | `1.23E+02` |

Choose the pattern that matches your reporting requirements. All patterns are compatible with the `Style.Custom` property demonstrated earlier.

## Set cell decimal places dynamically based on user input

Sometimes the required precision isn’t known at compile time. You can build the format string at runtime:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Edge case:** If `decimals` is zero, the format becomes `"0"` (integer display). Always validate the user input to avoid malformed format strings.

## Save workbook as XLSX – best practices

* **Use absolute paths** when writing to a known directory (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`).  
* **Dispose** the `Workbook` if you wrap it in a `using` statement to free unmanaged resources promptly:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Version compatibility:** Aspose.Cells writes files compatible with Excel 2010‑2023, so downstream users won’t encounter format issues.

---

## Full working example

Below is the complete program you can copy, paste, and run immediately. It includes all necessary `using` directives, comments, and error handling.

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

1. Run the program (`dotnet run`).  
2. Open `SigDigits.xlsx`.  
3. Confirm that **A1** reads `123.5`.  
4. If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom format `"0.######"` stored in the `<c>` element’s `s` attribute.

---

## Conclusion

In this tutorial you learned how to **create excel workbook c#**, **apply custom number format**, **set cell decimal places**, and **save workbook as xlsx** using Aspose.Cells. The solution demonstrates both visual formatting inside Excel and data‑export rounding through `ExportTableOptions`.  

From here you can:

* Extend the approach to whole ranges or tables.  
* Combine multiple styles (fonts, borders) with `StyleFlag`.  
* Automate report generation by looping over data sources and applying the same formatting logic.  

Feel free to experiment with different format strings, decimal counts, or export options to match your specific reporting needs. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}