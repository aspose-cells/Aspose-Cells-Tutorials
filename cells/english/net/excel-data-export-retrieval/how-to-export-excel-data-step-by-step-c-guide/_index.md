---
category: general
date: 2026-03-29
description: Learn how to export Excel tables to plain text, write string to file,
  and convert Excel table to CSV or TXT using C#. Includes full code and tips.
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: en
og_description: How to export Excel tables to text files in C#. Get the full solution,
  code, and best practices for converting Excel tables and saving TXT files.
og_title: How to Export Excel Data – Complete C# Tutorial
tags:
- C#
- Excel
- File I/O
title: How to Export Excel Data – Step‑by‑Step C# Guide
url: /net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Export Excel Data – Complete C# Guide

Ever wondered **how to export Excel** data without opening the spreadsheet manually? Maybe you need to dump a table into a simple text file for a legacy system, or you want a quick CSV export for data‑analysis pipelines. In this tutorial we’ll walk through a practical, end‑to‑end solution that **writes a string to file** and shows you exactly how to **convert Excel table** data into a delimited text format using C#.

We’ll cover everything from loading the workbook, picking the right table, configuring export options, and finally saving the result as a `.txt` file. By the end you’ll be able to **export table as CSV** (or any delimiter you choose) and you’ll also see a few handy tricks for **saving txt file C#** projects. No external tools required—just a few NuGet packages and a bit of code.

---

## What You’ll Need

- **.NET 6.0+** (or .NET Framework 4.7.2 if you prefer classic)
- **Syncfusion.XlsIO** NuGet package (the `ExportTableOptions` class lives here)
- A basic C# IDE (Visual Studio, VS Code, Rider—any will do)
- An Excel workbook that contains at least one table (we’ll use `ws.Tables[0]` in the example)

> Pro tip: If you don’t already have the Syncfusion library, run  
> `dotnet add package Syncfusion.XlsIO.Net.Core` from the command line.

---

## Step 1 – Open the Workbook and Grab the First Table  

The first thing is to load the Excel file and get a reference to the worksheet that holds the table. This step is crucial because the **convert excel table** operation works on a `ITable` object, not on raw cell ranges.

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Why this matters:* Opening the workbook with `using` ensures all unmanaged resources are released, preventing file‑lock issues later when you try to **write string to file**.

---

## Step 2 – Configure Export Options (Plain Text, No Headers, Semicolon Delimiter)  

Now we tell Syncfusion how we want the table serialized. The `ExportTableOptions` lets you toggle header inclusion, choose a delimiter, and decide whether to get a string or a byte array.

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Why this matters:* Setting `IncludeHeaders = false` often matches the expectations of downstream systems that already know the column order. Changing the delimiter is how you **export table as CSV** with a custom separator.

---

## Step 3 – Export the Table to a String  

With the options ready, we call `ExportToString`. This method pulls the entire table (including all rows) and returns a single string ready for file output.

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Why this matters:* The `ExportToString` call does the heavy lifting of converting the Excel grid into a delimited format. It respects the `Delimiter` you set, so you get a clean **export table as csv** result without extra processing.

---

## Step 4 – Write the Exported Text to a File  

Finally, we persist the string to disk. `File.WriteAllText` is the simplest way to **save txt file C#**; it automatically creates the file if it doesn’t exist and overwrites it otherwise.

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Why this matters:* By writing the string directly, you avoid an extra conversion step. The file now contains rows like `Value1;Value2;Value3`, ready for any downstream parser.

---

## Full Working Example (All Steps in One Place)  

Below is the complete, copy‑paste‑ready program that combines everything we discussed. It includes error handling and comments for clarity.

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Expected output** (the content of `ExportedTable.txt`):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

Each line corresponds to a row from the original Excel table, with values separated by semicolons. If you change `Delimiter = ","` you’ll get a classic CSV file instead.

---

## Common Questions & Edge Cases  

### What if My Workbook Has Multiple Tables?  
You can simply change `ws.Tables[0]` to the appropriate index, or loop through `ws.Tables`:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### How Do I Include Column Headers?  
Set `IncludeHeaders = true` in `ExportTableOptions`. This is useful when the downstream system expects a header row.

### Can I Export to a Different Folder Dynamically?  
Absolutely. Use `Path.Combine` with `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` or any user‑provided path to make the solution more flexible.

### What About Large Files?  
For massive tables, consider streaming the output instead of loading the whole string into memory:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### Does This Work on .NET Core?  
Yes—Syncfusion.XlsIO supports .NET 5/6/7. Just reference the appropriate NuGet package and you’re good to go.

---

## Pro Tips for Reliable Exports  

- **Validate the file path** before writing. A missing directory will throw `DirectoryNotFoundException`.  
- **Check `ExportAsString`** only when the table fits comfortably in memory; otherwise, use `ExportToStream` for huge datasets.  
- **Mind the culture**: if your data contains commas as decimal separators, choose a semicolon (`;`) or tab (`\t`) delimiter to avoid CSV parsing errors.  
- **Version lock**: Syncfusion occasionally changes API signatures. Pin the NuGet version (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`) to keep your build reproducible.

---

## Conclusion  

In this guide we demonstrated **how to export Excel** tables to plain‑text files using C#. By loading the workbook, configuring `ExportTableOptions`, exporting the table to a string, and finally **writing the string to file**, you now have a robust pattern for **convert excel table** data, **export table as csv**, and **save txt file C#** tasks.  

Feel free to experiment—swap the delimiter, include headers, or loop over multiple tables. The same approach works for generating CSV reports, feeding data into legacy parsers, or simply archiving spreadsheet contents as lightweight text files.

Got more scenarios you’d like to tackle? Maybe you need to **write string to file** asynchronously, or you want to zip the output on the fly. Check out our next tutorials on *asynchronous file I/O in C#* and *zipping files with .NET* to keep the momentum going.

Happy coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}