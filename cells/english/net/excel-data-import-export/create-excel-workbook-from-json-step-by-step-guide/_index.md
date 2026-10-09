---
category: general
date: 2026-03-25
description: Create excel workbook from JSON and save workbook as xlsx. Learn how
  to export json to xlsx, generate excel from json, and populate excel from json in
  minutes.
draft: false
keywords:
- create excel workbook
- export json to xlsx
- generate excel from json
- populate excel from json
- save workbook as xlsx
language: en
og_description: Create excel workbook from JSON instantly. This guide shows how to
  export json to xlsx, generate excel from json, and populate excel from json with
  Aspose.Cells.
og_title: Create Excel Workbook from JSON – Complete C# Tutorial
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: Create Excel Workbook from JSON – Step‑by‑Step Guide
url: /net/excel-data-import-export/create-excel-workbook-from-json-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook from JSON – Complete C# Tutorial

Ever needed to **create excel workbook** from a JSON payload but weren’t sure where to start? You’re not alone; many developers hit that wall when they try to turn API data into a tidy spreadsheet. The good news? With a few lines of C# and Aspose.Cells you can **export json to xlsx**, **generate excel from json**, and **populate excel from json** without juggling third‑party converters.

In this guide we’ll walk through the entire process—starting from a raw JSON string, dropping it into a SmartMarker, and finally **save workbook as xlsx** on disk. By the end you’ll have a ready‑to‑use Excel file that looks like this:

| Name | Score |
|------|-------|
| John | 90    |
| Anna | 85    |

> **Pro tip:** If you’re already using Aspose.Cells elsewhere in your project, you can reuse the same `Workbook` instance for multiple JSON imports—great for batch processing.

---

## What You’ll Need

- **.NET 6+** (or any recent .NET Framework that supports C# 10)
- **Aspose.Cells for .NET** – install via NuGet: `dotnet add package Aspose.Cells`
- A basic understanding of C# syntax (no deep Excel knowledge required)

That’s it. No external services, no COM interop, just pure managed code.

---

## Step 1: Initialize a New Excel Workbook

The first thing we do is create a fresh workbook object. Think of it as opening a blank Excel file where we’ll later drop our data.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and grab the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];
```

Why start with a new workbook? It guarantees a clean slate, prevents leftover styles from previous runs, and keeps the file size minimal—perfect for automated pipelines.

---

## Step 2: Prepare the JSON Data You Want to Import

For demonstration we’ll use a tiny JSON array, but you can swap this out with any valid JSON you receive from a web service, a file, or a database query.

```csharp
// Step 2: JSON string representing a simple collection of records
string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";
```

Notice the double‑escaped quotes (`\"`)—that’s just C# string literal syntax. In a real‑world scenario you’d probably read this from a file:

```csharp
// string jsonData = File.ReadAllText("data.json");
```

---

## Step 3: Tell SmartMarker to Treat the Whole Array as One Record

Aspose.Cells’ SmartMarker engine can iterate over collections automatically. By enabling **ArrayAsSingle**, we treat the entire JSON array as a single record, which is exactly what we need for a flat table.

```csharp
// Step 3: Configure SmartMarker options – array‑as‑single mode
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // This makes the whole JSON array behave like one record
};
```

If you forget this flag, SmartMarker would try to create a separate sheet for each element—definitely not what you want when generating a simple table.

---

## Step 4: Place a SmartMarker Token in the Worksheet

SmartMarker tokens look like `${jsonArray}`. When the processor runs, it replaces the token with the data from the JSON source. We’ll put the token in cell **A1** so the output starts at the top‑left corner.

```csharp
// Step 4: Insert the SmartMarker token into cell A1
worksheet.Cells["A1"].PutValue("${jsonArray}");
```

You can also pre‑format the header row before processing. For example, set bold font on the first row:

```csharp
Cell headerCell = worksheet.Cells["A1"];
headerCell.Style.Font.IsBold = true;
```

---

## Step 5: Run the SmartMarker Processor

Now the magic happens. The processor reads the JSON, maps each property to a column, and writes the rows beneath the token.

```csharp
// Step 5: Process the SmartMarker with our JSON data and options
worksheet.SmartMarkerProcessor.Process(jsonData, options);
```

Behind the scenes, Aspose.Cells:

1. Parses the JSON into a .NET object.
2. Matches property names (`Name`, `Score`) to column headers.
3. Writes each array element as a new row.

If your JSON contains nested objects, you can reference them with dot notation (`${parent.child}`) – a handy feature for more complex reports.

---

## Step 6: Save the Workbook as an XLSX File

Finally, persist the workbook to disk. The file extension `.xlsx` tells Excel (and most other spreadsheet apps) that this is an OpenXML workbook.

```csharp
// Step 6: Save the workbook to a file
string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

You can, of course, stream the workbook directly to an HTTP response if you’re building a web API:

```csharp
// Example for ASP.NET Core
using (var stream = new MemoryStream())
{
    workbook.Save(stream, SaveFormat.Xlsx);
    stream.Position = 0;
    return File(stream, "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "data.xlsx");
}
```

---

## Full Working Example

Below is the complete, ready‑to‑run program that incorporates every step above. Copy‑paste it into a new console project and hit **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ JSON data to be merged into the sheet
        string jsonData = "[{\"Name\":\"John\",\"Score\":90},{\"Name\":\"Anna\",\"Score\":85}]";

        // 3️⃣ Enable array‑as‑single mode so the whole array is one record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Put a SmartMarker token in A1 that points to the JSON array
        worksheet.Cells["A1"].PutValue("${jsonArray}");

        // Optional: make the header bold for better readability
        worksheet.Cells["A1"].Style.Font.IsBold = true;

        // 5️⃣ Process the SmartMarker with the JSON payload
        worksheet.SmartMarkerProcessor.Process(jsonData, options);

        // 6️⃣ Save the result as an XLSX file
        string outputPath = Path.Combine(Environment.CurrentDirectory, "json-single.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"✅ Workbook created and saved to: {outputPath}");
    }
}
```

**Expected result:** Opening `json-single.xlsx` shows two rows under the bold header—`John` with a score of `90` and `Anna` with `85`. The column names are automatically inferred from the JSON property names.

---

## Common Questions & Edge Cases

### What if my JSON keys contain spaces or special characters?

SmartMarker expects valid identifier names. Replace spaces with underscores or use a custom mapping:

```csharp
// Example JSON: {"First Name":"John"}
string jsonData = "[{\"First_Name\":\"John\",\"Score\":90}]";
// Token stays the same – Aspose.Cells will map "First_Name" to column header "First_Name"
```

### How do I export a large JSON array (thousands of rows)?

The processor streams data internally, so memory usage stays modest. However, you might want to:

- Increase the worksheet’s `MaxRows` limit (`worksheet.Cells.MaxRow = 1_048_576;` – the Excel maximum).
- Turn off gridlines for performance (`worksheet.IsGridlinesVisible = false;`).

### Can I add multiple JSON tables to the same workbook?

Sure. Just place different SmartMarker tokens in separate ranges (e.g., `${orders}` in `A10`, `${customers}` in `D1`) and call `Process` once per token or once with a composite JSON object containing both arrays.

---

## Bonus: Adding a Simple Chart (Optional)

If you want to visualise the scores, add a quick column chart after the data is populated:

```csharp
// Insert a column chart starting at cell E1
int chartIndex = worksheet.Charts.Add(ChartType.Column, 0, 4, 15, 10);
Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("B2:B3", true);
chart.NSeries[0].Name = "Score";
chart.Title.Text = "Scores by Name";
```

The chart will automatically reference the newly added rows, giving you a polished report in one go.

---

## Conclusion

You now know **how to create excel workbook** from a JSON string, **export json to xlsx**, **generate excel from json**, and **populate excel from json** using Aspose.Cells’ SmartMarker feature. The complete solution—initializing a workbook, configuring SmartMarker, processing JSON, and saving the file—fits into a handful of lines, yet scales to massive data sets.

Next steps? Try swapping the static JSON with an API call, add conditional formatting based on scores, or generate multiple sheets for different data domains. The same pattern works for CSV, XML, or even database result sets—just change the source string and adjust the SmartMarker token.

Happy coding, and may your spreadsheets always be tidy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}