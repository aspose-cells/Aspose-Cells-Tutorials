---
category: general
date: 2026-10-26
description: disable autofilter in Excel using C#. This tutorial shows how to remove
  autofilter from Excel table programmatically and includes a full working example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: en
lastmod: 2026-10-26
og_description: disable autofilter in Excel quickly. Follow this guide to remove autofilter
  from Excel table using C# and Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Disable autofilter in Excel with C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: How to disable autofilter in Excel with C# – complete guide
url: /net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to disable autofilter in Excel with C# – complete guide

If you need to **disable autofilter in Excel**, this guide shows you exactly how to do it from C#. Whether you’re cleaning up a report before publishing or automating a data‑export pipeline, removing the filter ensures the worksheet displays every row. You’ll also learn how to **remove autofilter from Excel table** in a single, reliable call.

We’ll use the popular **Aspose.Cells for .NET** library because it works without requiring Excel to be installed on the server. By the end of this tutorial you will have a self‑contained console application that loads a workbook, finds the first table, and disables its autofilter. The solution works with .xlsx files created by Excel 2007 or newer.

## What you’ll need

| Prerequisite | Why it matters |
|--------------|----------------|
| .NET 6.0 or later | Provides the runtime for the C# code. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Gives programmatic access to worksheets, tables, and autofilters. |
| A sample Excel file (`Sample.xlsx`) that contains at least one table with an autofilter applied | The code operates on the first table; having a table lets us demonstrate disabling the filter. |
| Visual Studio 2022 (or any C# IDE) | Makes building and debugging the console app straightforward. |

> **Pro tip:** If you prefer a free alternative, you can adapt the code to use **ClosedXML** or **EPPlus**; the core idea—setting the table’s `AutoFilter` property to `null`—remains the same.

## Step 1: Create a new console project

Open a terminal or the Visual Studio command prompt and run:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

This creates a fresh project named `ExcelFilterDemo` and pulls in the Aspose.Cells library.

## Step 2: Load the workbook and locate the first worksheet

The first logical operation is to open the workbook file. Aspose.Cells reads the file into a `Workbook` object that gives you direct access to worksheets and tables.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Why this step?** Loading the workbook is required before you can manipulate any Excel objects. Using the first worksheet (`Worksheets[0]`) mirrors the typical scenario where the primary data lives on the first sheet.

## Step 3: Retrieve the first table defined on the worksheet

Excel tables (also called ListObjects) are the containers that hold structured data. Each table can have its own autofilter. To remove the filter we first need a reference to the table object.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Edge case:** If the workbook might contain worksheets without tables, wrap the access in a `if (worksheet.Tables.Count > 0)` check. This prevents runtime errors and makes the solution robust.

## Step 4: Disable the autofilter for the table

The actual disabling is a single line: assign `null` to the `AutoFilter` property of the `Table` object. This clears any filter criteria and removes the dropdown arrows from the header row.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

After this line runs, the table behaves like a regular range with no filter UI.

## Step 5: Save the modified workbook

Finally, write the changes back to disk. You can overwrite the original file or create a new one to keep the source intact.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Full source code

Putting all the pieces together, the complete program looks like this:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Run the program with `dotnet run`. After execution, open `Sample_NoFilter.xlsx` in Excel; you’ll see that the filter arrows have disappeared and all rows are visible.

## Verify that the autofilter is really gone

1. Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.  
2. Click any column header – you should **not** see the drop‑down filter arrow.  
3. If you still see arrows, double‑check that the table you targeted is indeed the one with the filter. You can list all tables with:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

The console output should report `Has AutoFilter: False` for the table you modified.

## Common pitfalls and how to avoid them

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | The worksheet has no tables. | Add a guard `if (worksheet.Tables.Count == 0)` before accessing. |
| Saved file still shows filters | You edited the wrong worksheet or table. | Use `wb.Worksheets["SheetName"]` or iterate through `wb.Worksheets` to locate the correct table. |
| The program crashes on older .NET versions | Aspose.Cells requires .NET 6.0+ for the latest package. | Upgrade the target framework in the `.csproj` file. |
| NullReferenceException when `table.AutoFilter` is already null | You called the code twice on the same file without re‑loading. | Reload the workbook or check `if (table.AutoFilter != null)` before assigning. |

## Extending the solution

Now that you know how to **disable autofilter in Excel**, you might want to:

* **Remove autofilter from Excel table** only when a specific condition is met (e.g., when a user flag is set). Add an `if` statement around `table.AutoFilter = null;`.
* **Apply a new filter** programmatically after clearing the old one, using `table.AutoFilter.Range` and `table.AutoFilter.AddFilterColumn(...)`.
* **Process multiple tables** in the same workbook by looping through `worksheet.Tables` and disabling each filter.

These extensions follow the same pattern demonstrated above and keep the codebase clean.

## Conclusion

You now have a concise, production‑ready method to **disable autofilter in Excel** using C#. By loading the workbook, accessing the first table, and setting `table.AutoFilter = null`, you effectively **remove autofilter from Excel table** without manual interaction. The complete example compiles, runs, and produces a clean file ready for further automation or distribution.

Feel free to experiment with additional tables, conditional logic, or alternative libraries. If you encounter any edge cases, refer back to the troubleshooting section or explore Aspose.Cells’ extensive documentation for advanced filter handling. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to remove autofilter from Excel tables using C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}