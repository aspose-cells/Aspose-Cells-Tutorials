---
category: general
date: 2026-02-26
description: how to export excel to a tab‑delimited txt file using C#. Learn export
  excel as tab, convert excel to txt, and export excel with delimiter in three easy
  steps.
draft: false
keywords:
- how to export excel
- export excel as tab
- convert excel to txt
- export excel with delimiter
- export excel range
language: en
og_description: how to export excel to a tab‑delimited txt file using C#. This tutorial
  shows export excel as tab, convert excel to txt, and export excel with delimiter.
og_title: how to export excel – Tab‑Delimited Text Guide
tags:
- csharp
- excel
- file-conversion
title: how to export excel – Tab‑Delimited Text Guide
url: /net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to export excel – Complete C# Tutorial

Ever wondered **how to export excel** data into a plain‑text file without losing formatting? Maybe you need a quick TSV (tab‑separated values) for a data‑pipeline, or you’re feeding a legacy system that only reads `.txt`. Either way, you’re not alone—developers constantly hit this wall when moving data out of spreadsheets.

The good news? In just three straightforward steps you can **export excel as tab**‑delimited text, **convert excel to txt**, and even pick a custom delimiter if you change your mind later. Below you’ll see a fully runnable C# example, why each line matters, and a handful of tips to avoid the usual pitfalls.

> **Pro tip:** This approach works with the popular Aspose.Cells library, but the concepts translate to any .NET Excel API that offers an `ExportTable`‑style method.

## What You’ll Need

- **.NET 6+** (or .NET Framework 4.6+). The code compiles on any recent runtime.
- **Aspose.Cells for .NET** (free trial or licensed). Install via NuGet: `dotnet add package Aspose.Cells`.
- An input workbook named `input.xlsx` placed in a folder you control.
- A tiny bit of curiosity—no deep Excel internals required.

If you already have those, let’s jump straight into the solution.

## Step 1 – Load the Workbook You Want to Export

First we create a `Workbook` object that points to the source file. This object represents the entire Excel file, including all worksheets, named ranges, and formatting.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook that contains the data to export
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*Why this matters:*  
Loading the workbook gives you access to the worksheet collection (`workbook.Worksheets`). Without this object you can’t address cells, ranges, or export settings.  

> **Note:** If your file lives in a network share, prepend `\\` or use a UNC path—Aspose.Cells handles it just fine.

## Step 2 – Configure Export Options (String Values & Tab Delimiter)

Now we tell the library how we want the data written out. By setting `ExportAsString = true` we force every cell to be treated as a plain string, which eliminates Excel’s locale‑specific number formats. The `Delimiter = "\t"` part is the heart of **export excel as tab**.

```csharp
// Step 2: Configure the export options – export values as strings and use a tab delimiter
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,   // ensures numbers become plain text, not scientific notation
    Delimiter = "\t"         // tab character – perfect for TSV files
};
```

*Why this matters:*  
If you skip `ExportAsString`, a cell containing `12345` might become `12,345` in some locales, breaking downstream parsers. The delimiter can be swapped for commas, pipes, or any character if you later decide to **export excel with delimiter** other than a tab.

## Step 3 – Export a Specific Range to a Text File

Finally, we pick the range we care about (`A1:D10` in this example) and write it to `out.txt`. The method `ExportTable` does all the heavy lifting: it reads the cells, applies the options, and streams the result to disk.

```csharp
// Step 3: Export the range A1:D10 from the first worksheet to a text file
Worksheet sheet = workbook.Worksheets[0]; // first worksheet (index 0)
sheet.Cells.ExportTable("A1", "D10", @"C:\Data\out.txt", exportOptions);
```

After this runs, you’ll find `out.txt` with content that looks like:

```
Name    Age    City    Score
Alice   30     NY      85
Bob     25     LA      90
...
```

Each column is separated by a **tab**, making it ready for `awk`, `PowerShell`, or any CSV‑compatible tool that respects tabs.

### Quick Verification

Open the generated file in a plain‑text editor (Notepad, VS Code) and confirm:

1. Columns line up when you enable “Show whitespace”.
2. No extra quotes or commas appear.
3. All numeric cells appear exactly as they did in Excel (thanks to `ExportAsString`).

If anything looks off, double‑check that the source workbook isn’t hiding rows/columns, and ensure you referenced the correct worksheet index.

## Common Variations & Edge Cases

### Exporting an Entire Worksheet

If you want to **export excel range** that covers the whole sheet, you can use `sheet.Cells.MaxDisplayRange`:

```csharp
var maxRange = sheet.Cells.MaxDisplayRange;
sheet.Cells.ExportTable(maxRange.FirstRow, maxRange.FirstColumn,
                       maxRange.RowCount, maxRange.ColumnCount,
                       @"C:\Data\fullSheet.txt", exportOptions);
```

### Using a Different Delimiter

Switching from tab to pipe (`|`) is as easy as changing one line:

```csharp
exportOptions.Delimiter = "|"; // now we have a pipe‑delimited file
```

That satisfies the **export excel with delimiter** scenario without rewriting any other code.

### Handling Large Files (> 100 MB)

For massive workbooks, stream the export to avoid loading everything into memory:

```csharp
using (FileStream fs = new FileStream(@"C:\Data\largeOut.txt", FileMode.Create, FileAccess.Write))
{
    sheet.Cells.ExportTable("A1", "Z5000", fs, exportOptions);
}
```

### Converting Multiple Sheets in One Pass

If you need to **convert excel to txt** for several sheets, loop over them:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outPath = $@"C:\Data\Sheet{i + 1}.txt";
    workbook.Worksheets[i].Cells.ExportTable("A1", "D10", outPath, exportOptions);
}
```

Each sheet gets its own TSV file—handy for batch jobs.

## Full Working Example (Copy‑Paste Ready)

Below is the entire program, ready to compile. Just replace the file paths with your own.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            string inputPath = @"C:\Data\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set export options – strings + tab delimiter
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                Delimiter = "\t"
            };

            // 3️⃣ Export range A1:D10 from the first worksheet
            Worksheet sheet = workbook.Worksheets[0];
            string outputPath = @"C:\Data\out.txt";
            sheet.Cells.ExportTable("A1", "D10", outputPath, exportOptions);

            Console.WriteLine($"Export complete! Check {outputPath}");
        }
    }
}
```

**Expected output:** A file named `out.txt` where each column is separated by a tab character, and every cell value appears exactly as it does in Excel.

## Frequently Asked Questions

- **Does this work with .xls files?**  
  Yes. Aspose.Cells auto‑detects the format, so you can point `Workbook` at an older `.xls` and the same code applies.

- **What if my data contains tabs?**  
  Tabs inside a cell will be preserved, which can break TSV parsers. In that case, consider switching to a pipe (`|`) delimiter by updating `exportOptions.Delimiter`.

- **Can I export formulas instead of values?**  
  Set `exportOptions.ExportAsString = false` and use the `ExportTableOptions` overload that includes `ExportFormula = true`. The output will contain the raw formula text.

- **Is there a way to skip hidden rows?**  
  Yes. Set `exportOptions.ExportHiddenRows = false` (default is `true`). Hidden rows will be omitted from the final text file.

## Conclusion

You now have a solid, production‑ready recipe for **how to export excel** data as a tab‑delimited text file, how to **export excel as tab**, and how to **convert excel to txt** with full control over delimiters and range selection. By leveraging Aspose.Cells’ `ExportTable` method you avoid manual CSV construction, preserve data fidelity, and keep your codebase clean.

Ready for the next challenge? Try:

- Exporting directly to a `MemoryStream` for web APIs.  
- Adding a header row dynamically based on the first row’s content.  
- Integrating this routine into an Azure Function that watches a storage bucket for new Excel uploads.

Give it a spin, tweak the delimiter, and let the data flow wherever you need it. Happy coding!  

<img src="export-excel.png" alt="how to export excel example" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}