---
category: general
date: 2026-08-11
description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
  xlsx to plain text using Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: en
lastmod: 2026-08-11
og_description: Export excel to txt in C# quickly. This tutorial shows how to convert
  xlsx to plain text, configure formats, and handle large worksheets.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: Export excel to txt in C# – step‑by‑step guide for developers
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: Export excel to txt in C# – complete programming guide
url: /net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export excel to txt in C# – complete programming guide

If you need to **export excel to txt** you can achieve the result with a few lines of C# code. This guide shows how to convert an `.xlsx` workbook into a plain‑text file while preserving the data format you define.

Exporting worksheets as text files is a common requirement when downstream systems only accept delimited data or when you need to audit raw cell values. In the following sections you will learn how to configure date and number formats, handle large sheets, and avoid typical pitfalls.

## Prerequisites for converting xlsx to plain text

Before you start, make sure you have:

* .NET 6.0 (or later) installed – the code targets .NET Standard 2.0, so it works with .NET Framework 4.6+ as well.
* A license for **Aspose.Cells** (the free evaluation works for testing).
* An IDE such as Visual Studio 2022 or Visual Studio Code.
* An Excel file named `input.xlsx` placed in a folder you can reference from your project.

These items are the only external requirements; the tutorial does not depend on additional NuGet packages.

## How to export excel to txt using Aspose.Cells

Aspose.Cells provides the `ExportTableOptions` class that lets you control how cell values are rendered as strings. By setting `ExportAsString` to `true` you force every cell to be written as text, which is essential when you want a deterministic plain‑text output.

### Step 1 – load the workbook

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*The `Workbook` constructor reads the Excel file into memory. If the file does not exist, an exception is thrown, so you may want to wrap this call in a try‑catch block for production code.*

### Step 2 – get the first worksheet

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Worksheets are zero‑based, so index 0 refers to the first tab. You can replace the index with a sheet name (`workbook.Worksheets["Sheet1"]`) when you need to target a specific tab.*

### Step 3 – define export options for text conversion

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` guarantees that every cell, regardless of its original type, becomes a string in the output file. The `DateTimeFormat` and `NumberFormat` properties let you control how dates and numbers appear, which is crucial when you **convert xlsx to plain text** for systems that expect a specific pattern.*

### Step 4 – export worksheet as text file

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` writes the worksheet content to a plain‑text file using the options you supplied. The default delimiter is a tab character (`\t`). If you need a different delimiter, you can use the overload that accepts a `ExportTableOptions` instance and specify `ExportTableOptions.Separator`. The resulting file can be opened in any text editor or imported into a database.*

#### Expected output

Assume `input.xlsx` contains:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

With the options above the `Exported.txt` file will contain:

```
2023-05-01	1,234.50	Sample text
```

Each column is separated by a tab, dates follow `yyyy‑MM‑dd`, and numbers use a comma as a thousands separator and two decimal places.

## Common pitfalls when you export worksheet as text file

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| Locale‑dependent number formatting | The default format respects the OS culture, which may produce commas or periods inconsistently. | Explicitly set `NumberFormat` in `ExportTableOptions`. |
| Hidden rows or columns appear in the output | Aspose.Cells exports the entire used range, including hidden rows. | Set `ExportTableOptions.ExportHiddenRows = false` and `ExportHiddenColumns = false` if you want to skip them. |
| Large worksheets cause memory pressure | The whole workbook is loaded into memory before export. | Use `Workbook.LoadOptions` with `LoadDataOnly = true` to reduce memory usage, or process the file in chunks. |
| Date cells stored as text in the source file | If a cell already contains a formatted string, the exporter treats it as text and ignores `DateTimeFormat`. | Ensure the source workbook stores dates as proper Excel date types. |

Addressing these issues makes the **how to export excel worksheet as text** process reliable across different environments.

## Extending the solution – custom delimiters and streaming export

If you need a comma‑separated values (CSV) file instead of a tab‑delimited file, modify the options:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

For files larger than 500 MB, streaming the output prevents the application from exhausting RAM:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

The overload that accepts a `Stream` writes rows incrementally, which is ideal for batch jobs or web services that return the text file directly to a client.

## Verify the result programmatically

After the export finishes you can read the first line back into memory to confirm the format:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Running this snippet should print the same line shown in the *Expected output* section, giving you confidence that the conversion succeeded.

## Recap of the complete code

Putting all pieces together yields a self‑contained program you can copy into a console application:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Compile and run the program; the `Exported.txt` file appears in the same directory as the source workbook.

## Next steps and related topics

* **Export worksheet as text file** – experiment with different delimiters, encodings (UTF‑8 vs. ASCII), and line‑ending styles for cross‑platform compatibility.
* **Bulk conversion** – loop through `workbook.Worksheets` to generate a separate text file for each tab.
* **Integration with databases** – pipe the generated text directly into a bulk‑insert operation for SQL Server or PostgreSQL.
* **


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}