---
category: general
date: 2026-11-25
description: Learn how to create multiple sheets in an Excel file using C#. This guide
  covers saving the workbook as XLSX and handling duplicate sheet names.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create multiple sheets
- create excel file c#
- duplicate sheet names
- save workbook xlsx
language: en
lastmod: 2026-11-25
og_description: Create multiple sheets in an Excel file using C#. Follow this complete
  tutorial to save the workbook as XLSX and manage duplicate sheet names.
og_image_alt: Code editor showing C# sample that generates an Excel workbook with
  several detail sheets
og_title: Create multiple sheets in an Excel file with C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  headline: How to create multiple sheets in an Excel file using C#
  type: TechArticle
- description: Learn how to create multiple sheets in an Excel file using C#. This
    guide covers saving the workbook as XLSX and handling duplicate sheet names.
  name: How to create multiple sheets in an Excel file using C#
  steps:
  - name: '**Create a new workbook** and name the first worksheet *Master*.'
    text: '**Create a new workbook** and name the first worksheet *Master*.'
  - name: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
    text: '**Insert a smart marker** that tells Aspose.Cells how to name the detail
      worksheets.'
  - name: '**Process the smart marker** with a data source that may contain duplicate
      names.'
    text: '**Process the smart marker** with a data source that may contain duplicate
      names.'
  - name: '**Save the workbook** as an XLSX file.'
    text: '**Save the workbook** as an XLSX file.'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Create multiple sheets in an Excel file using Aspose.Cells for C#
url: /net/worksheet-management/how-to-create-multiple-sheets-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create multiple sheets in an Excel file using C#

If you need to **create multiple sheets** in an Excel workbook from C#, this tutorial gives you a ready‑to‑run solution. By the end of the guide you will have a program that generates a master sheet, creates detail sheets via smart markers, and saves the result as an **XLSX** file—while safely handling **duplicate sheet names**.

You’ll also see how to **create excel file c#** projects with the Aspose.Cells library, a popular choice for server‑side spreadsheet automation.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* Visual Studio 2022 (or any IDE that supports .NET)  
* The **Aspose.Cells for .NET** NuGet package (`Aspose.Cells`) – it provides `Workbook`, `Worksheet`, and `SmartMarkersFactory` classes used in the code.  

You can add the package with the following CLI command:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Use a private NuGet feed or the free community edition if you only need basic features.

## Overview of the solution

The approach consists of four logical steps:

1. **Create a new workbook** and name the first worksheet *Master*.  
2. **Insert a smart marker** that tells Aspose.Cells how to name the detail worksheets.  
3. **Process the smart marker** with a data source that may contain duplicate names.  
4. **Save the workbook** as an XLSX file.

Each step is explained in detail below, and the complete source file is provided at the end of the article.

## Step 1: Create a new workbook and add a master sheet

The `Workbook` class represents an entire Excel file. When you instantiate it without parameters, Aspose.Cells creates a default workbook that already contains a single worksheet. Renaming that sheet to *Master* makes the purpose of the sheet clear.

```csharp
using Aspose.Cells;
using System;
using System.Data;   // For DataTable used as a data source

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 1️⃣ Retrieve the first worksheet (index 0) and give it a friendly name
Worksheet masterSheet = workbook.Worksheets[0];
masterSheet.Name = "Master";
```

**Why this matters:**  
Starting with a clean workbook avoids leftover formatting or hidden sheets from previous runs. Naming the sheet *Master* helps you locate the smart marker later and keeps the file readable for non‑technical users.

## Step 2: Insert a smart marker that defines detail sheet names

Smart markers are placeholders that Aspose.Cells replaces with data at runtime. The syntax `&=DetailSheetNewName=Detail` tells the engine to create a new worksheet for each row in the data source, using the value of the `Detail` column as the sheet name.

```csharp
// 2️⃣ Place a smart marker in cell A1 of the master sheet
masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");
```

**Why this matters:**  
The smart marker eliminates the need to write a loop that manually adds worksheets. It also automatically copies the master sheet’s layout to each newly generated sheet, ensuring consistent styling.

## Step 3: Process the smart marker with a data source that may contain duplicates

Below we build a `DataTable` that simulates a data source. Notice that the *Detail* column contains duplicate values (`"Report"` appears twice). The `SmartMarkersFactory.Process` method respects the `AllowDuplicateSheetNames` setting, which is **true** by default for this example.

```csharp
// 3️⃣ Build a sample data source (DataTable) with duplicate sheet names
DataTable dataSource = new DataTable();
dataSource.Columns.Add("Detail", typeof(string));
dataSource.Columns.Add("Value", typeof(double));

// Add rows – "Report" appears twice to demonstrate duplicate handling
dataSource.Rows.Add("Report", 123.45);
dataSource.Rows.Add("Summary", 67.89);
dataSource.Rows.Add("Report", 101.12);   // Duplicate sheet name

// Register the data source in the workbook's data collection
workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });
```

> **Important:** If you need to guarantee unique sheet names, set `workbook.Settings.CheckDuplicateSheetNames = true;` before processing. The default behavior creates sheets with the same name, which Excel allows but can be confusing when navigating the file.

## Step 4: Save the workbook as an XLSX file

Finally, persist the generated workbook to disk. The `Save` method automatically chooses the appropriate writer based on the file extension.

```csharp
// 4️⃣ Save the workbook – the file will contain the master sheet and two "Report" sheets plus a "Summary" sheet
string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

**Expected result**

When you open `duplicate_detail_sheets.xlsx` you will see:

| Sheet Name | Content (first row) |
|------------|---------------------|
| Master     | Smart marker placeholder (no data) |
| Report     | Data row 1 (`123.45`) |
| Summary    | Data row 2 (`67.89`) |
| Report (2) | Data row 3 (`101.12`) |

The second *Report* sheet is automatically renamed to *Report (2)* by Aspose.Cells to avoid a hard error while still reflecting the original duplicate intent.

## Full source code

Copy the following file into a console project (`dotnet new console`) and run it. The program demonstrates the complete workflow for **create multiple sheets** and **save workbook xlsx** while handling **duplicate sheet names**.

```csharp
// Program.cs
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelMultipleSheetsDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and name the first sheet "Master"
            Workbook workbook = new Workbook();
            Worksheet masterSheet = workbook.Worksheets[0];
            masterSheet.Name = "Master";

            // Step 2: Add a smart marker that will generate detail sheets
            masterSheet.Cells["A1"].PutValue("&=DetailSheetNewName=Detail");

            // Step 3: Prepare a data source with duplicate sheet names
            DataTable dataSource = new DataTable();
            dataSource.Columns.Add("Detail", typeof(string));
            dataSource.Columns.Add("Value", typeof(double));

            dataSource.Rows.Add("Report", 123.45);
            dataSource.Rows.Add("Summary", 67.89);
            dataSource.Rows.Add("Report", 101.12); // duplicate name

            // Bind the data source to the workbook
            workbook.Worksheets[0].SmartMarkersFactory.Process(new[] { "dataSource" });

            // Step 4: Save the workbook as an XLSX file
            string outputPath = @"C:\Temp\duplicate_detail_sheets.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Run `dotnet run` from the project folder. After execution, open the generated file to verify that three detail sheets were created, two of them sharing the base name **Report**.

## Handling edge cases and best practices

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large data sets** ( > 10 000 rows) | Use `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;` to reduce memory pressure. |
| **Custom sheet naming rules** | Pre‑process the `Detail` column to replace illegal characters (`/ \ ? * [ ] :`) before calling `Process`. |
| **Need truly unique names** | Set `workbook.Settings.CheckDuplicateSheetNames = true;` and provide a fallback naming scheme (e.g., append a GUID). |
| **Generating PDFs instead of XLSX** | After saving, call `workbook.Save("output.pdf", SaveFormat.Pdf);` – Aspose.Cells can export directly to PDF. |
| **Running in a web service** | Write the workbook to a `MemoryStream` and return it as a file download to avoid disk I/O. |

### Pro tip: reuse the same `Workbook` instance for multiple exports

If your application creates several reports per request, keep a single `Workbook` object in memory, clear its worksheets (`workbook.Worksheets.Clear();`), and repeat the steps. This avoids the overhead of repeatedly loading the Aspose.Cells runtime.

## Conclusion

You now know how to **create multiple sheets** in an Excel workbook using C#, how to **create excel file c#** with Aspose.Cells, how to manage **duplicate sheet names**, and how to **save workbook xlsx** reliably. The complete example demonstrates a clean, maintainable pattern that scales from quick scripts to production‑grade services.

### What’s next?

* Explore **conditional formatting** on the generated sheets to highlight key values.  
* Use **Smart Markers** to populate tables, charts, or pivot tables automatically.  
* Integrate the code into an ASP.NET Core API and return the XLSX file as a download stream.

Feel free to experiment with different data sources (JSON, XML, or a database) and adapt the smart marker syntax to suit your reporting needs. Happy coding!


## What should you learn next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook C# – Step‑by‑Step Guide to Write Dates & Save as XLSX]({{< relref "/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide-to-write-dates-sa/" >}})
- [Create New Workbook in C# – Add Formula and Save Excel File]({{< relref "/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/" >}})
- [Create excel workbook and save it to file in C#]({{< relref "/cells/english/net/excel-workbook/create-excel-workbook-and-save-it-to-file-in-c/" >}})

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}