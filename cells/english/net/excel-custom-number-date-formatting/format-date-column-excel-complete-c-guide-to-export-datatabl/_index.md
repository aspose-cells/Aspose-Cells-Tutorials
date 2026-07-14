---
category: general
date: 2026-07-13
description: Format date column Excel while exporting a DataTable from C#. Learn excel
  export datatable c# and import datatable to excel with styling in minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: en
lastmod: 2026-07-13
og_description: Format date column Excel effortlessly. This guide shows you how to
  excel export datatable c# and import datatable to excel with custom styles.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Format Date Column Excel – Step‑by‑Step C# Export Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Format Date Column Excel – Complete C# Guide to Export DataTable
url: /net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Format Date Column Excel – Complete C# Guide to Export DataTable

Ever needed to **format date column Excel** when pulling data from a database, but the cells kept showing raw timestamps? You're not the only one. In many business apps the default export dumps a `DateTime` value like `2024‑03‑15 00:00:00` and nobody wants that clutter.  

The good news is that you can control the exact look of each column straight from C#. In this tutorial we’ll walk through an end‑to‑end solution that **excel export datatable c#**, applies a date style to the first column, a currency style to the second, and finally **import datatable to excel** with zero‑pain styling.

By the end you’ll have a reusable method you can drop into any .NET project, no matter whether you’re using .NET 6, .NET Framework 4.8, or a later version.

---

## What You’ll Need

- **Aspose.Cells for .NET** (or any library that offers `CreateStyle` and `ImportDataTable`). The code snippets use Aspose because its API is clean and widely adopted.
- A **DataTable** that you already populate from SQL, CSV, or any other source.
- Visual Studio (or your favorite IDE).  
- .NET runtime 5.0+ (the sample targets .NET 6, but older frameworks work the same).

If you don’t have Aspose.Cells yet, grab a free trial from the official site—no credit‑card required.

---

## Step 1: Retrieve the Source Data as a DataTable

First things first, you need a `DataTable`. In real‑world scenarios this usually comes from `SqlDataAdapter.Fill`, but for the sake of clarity we’ll mock a simple table:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro tip:** When you pull data directly from a stored procedure, make sure the column types match the intended Excel formats. A `datetime` column will later be the target for our **format date column excel** style.

---

## Step 2: Create an Excel Workbook and Define Column Styles

Now we spin up a new workbook. The trick to **format date column excel** lies in creating a `Style` object, setting its `Number` property to the built‑in Excel date format (code 14), and assigning that style to the appropriate column index.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Why `Number = 14`? Excel stores dates as serial numbers; format 14 tells the program to render those numbers using the locale’s short‑date pattern. If you need a custom pattern (like `dd‑MMM‑yyyy`), you could set `columnStyles[0].Custom = "dd-MMM-yyyy"` instead.

---

## Step 3: Import the DataTable into the Worksheet with Styles

With the style array ready, the import call is a single line. This is the heart of **excel export datatable c#** and also the place where we **import datatable to excel** while preserving our formatting.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

The `ImportDataTable` overload we’re using accepts the style array, applying each style to the matching column as the data is written. No post‑processing loop required—your date column is already prettily formatted.

---

## Step 4: Save the Workbook (or Stream It Directly to the Browser)

Depending on your scenario you might save to disk, a memory stream, or return the file as an HTTP response. Here are three common patterns:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Watch out for:** If you’re using `FileResult` in ASP.NET Core, make sure to set `Response.Headers["Cache-Control"] = "no-cache"` when the file is generated on the fly. It prevents the browser from serving a stale version.

---

## Step 5: Verify the Result – What the Excel Sheet Looks Like

After running the code, open `ExportedReport.xlsx`. You should see:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

Notice how the **format date column excel** shows a clean short date, while the currency column automatically aligns with your regional settings. No manual cell‑by‑cell formatting needed.

![format date column excel example](/images/format-date-column-excel.png)

*Image alt text: format date column excel – a screenshot of the Excel sheet with a properly formatted date column.*

---

## Common Questions & Edge Cases

### What if My DataTable Has More Than Three Columns?

Just extend the `columnStyles` array. For any column you don’t explicitly style, leave the entry `null`; Excel will apply the default General format.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?

Replace the built‑in number with a custom string:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Can I Use This Approach with EPPlus or ClosedXML?

Yes, the concept is identical: create a style object, assign it to a column, then load the `DataTable`. The API differs, but the **excel export datatable c#** pattern remains the same.

### What About Large DataSets (100k+ rows)?

`ImportDataTable` is optimized for bulk writes, but you might hit memory limits. In that case, consider streaming rows with `Cells.ImportDataTable` in chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the style objects.

---

## Full Working Example (All Steps in One Method)

Below is a self‑contained method you can copy‑paste into any console app or ASP.NET controller. It demonstrates the entire flow—from data retrieval to styled Excel export.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Run the program, open `StyledExport.xlsx`, and you’ll see the **format date column excel** applied perfectly.

---

## Recap & Next Steps

We’ve just covered how to **format date column excel** when performing an **excel export datatable c#**, and how to **import datatable to excel** with per‑column styling in a single call. The key takeaways:

1. Create a `Style` per column you want to format.  
2. Use `Number = 14` for dates, `Number = 2` for currency, or any custom format you need.  
3. Pass the style array to `ImportDataTable`—the library does the heavy lifting.

What could you explore next?

- **Conditional formatting** to highlight overdue dates.  
- **


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}