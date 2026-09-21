---
category: general
date: 2026-02-21
description: repeat data in excel quickly using SmartMarker—learn how to populate
  excel template and repeat rows effortlessly.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: en
og_description: repeat data in excel using SmartMarker. Learn how to populate excel
  template, repeat rows, and automate your spreadsheets.
og_title: repeat data in excel – Populate template with SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: repeat data in excel – Populate template with SmartMarker
url: /net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# repeat data in excel – Populate template with SmartMarker

Ever needed to **repeat data in Excel** but weren't sure how to avoid manual copy‑pasting? You're not alone. In many reporting scenarios you have a list of items that must expand into rows automatically, and doing it by hand is a recipe for errors.

Here's the thing—using the SmartMarkerProcessor from the **GemBox.Spreadsheet** library lets you **populate an Excel template** with a single line of C# and have rows repeat for each item in your collection. In this guide we'll walk through the exact steps, show you the complete code, and explain why each piece matters, so you can confidently repeat rows in Excel without breaking a sweat.

## What you'll learn

* How to define the data structure that drives the repeat operation.  
* How to hook a `SmartMarkerProcessor` to a workbook that contains a hidden template sheet.  
* How the `${Repeat:Item}` marker expands into multiple rows automatically.  
* Tips for handling edge cases like empty collections or custom formatting.  

By the end of this tutorial you’ll be able to **populate excel from data** in a way that scales, is easy to maintain, and works with any .NET project.

---

## Prerequisites

* .NET 6.0 or later (the code uses modern C# features).  
* The **GemBox.Spreadsheet** NuGet package (free version works for up‑to‑150 rows).  
* A basic Excel template file (`Template.xlsx`) with a hidden sheet named `HiddenTemplate`.  
* Familiarity with C# objects and LINQ is helpful but not required.

---

## Step 1 – Define the repeat data structure

First, you need a data source that the SmartMarker engine can iterate over. In most real‑world apps this will come from a database, an API, or a CSV file. For the sake of clarity we’ll use an anonymous type with a single property called `Item` that holds an array of strings.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Why this matters:** The `${Repeat:Item}` marker inside the Excel template looks for a property named `Item`. If you rename the property, update the marker accordingly. This tight coupling ensures that the template stays in sync with your code, making it easier to **populate excel template** without guessing column names.

### Common variations

* **Complex objects:** Instead of a simple string array you can supply a list of objects (`new[] { new { Name = "A", Qty = 10 } }`). The marker will repeat rows and you can reference `${Item.Name}` and `${Item.Qty}` in the sheet.  
* **Empty collections:** If `Item` is empty, SmartMarker simply removes the repeat block, leaving the template untouched—great for optional sections.

---

## Step 2 – Create the SmartMarkerProcessor for the hidden template sheet

Next, load your workbook and instantiate a `SmartMarkerProcessor`. Point it at the workbook that contains the hidden template sheet; SmartMarker will copy that sheet to a visible one and expand the repeat markers.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** If you have multiple templates in the same file, you can specify the source sheet name when calling `processor.Process`. This helps when you need to **repeat rows in excel** for different sections of a report.

### Edge case handling

* **Missing template sheet:** Wrap the load in a try/catch and log a clear error—this prevents silent failures when the file path is wrong.  
* **Large data sets:** For thousands of rows, consider streaming the output to a file (`processor.Save`) instead of keeping everything in memory.

---

## Step 3 – Apply the data and expand the `${Repeat:Item}` marker

Now comes the magic line that actually repeats the rows. Pass the object you created in Step 1 to `processor.Process`. SmartMarker will locate every `${Repeat:Item}` marker, duplicate the row for each element, and replace placeholders with the actual values.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### What you should see

When you open `Result.xlsx`, the hidden template sheet has been copied to a new visible sheet (by default named `Sheet1`). The row that contained `${Repeat:Item}` now appears three times, with the cells showing **A**, **B**, and **C** respectively.

| Item |
|------|
| A    |
| B    |
| C    |

If you added more columns like `${Item.Price}`, those would be filled in automatically from the data source.

---

## How to repeat rows in Excel without SmartMarker (quick comparison)

| Approach                | Code Complexity | Maintenance | Performance |
|-------------------------|-----------------|-------------|-------------|
| Manual copy‑paste       | High            | Low         | Poor        |
| VBA macro               | Medium          | Medium      | Good        |
| **SmartMarkerProcessor**| Low             | High        | Excellent   |

As you can see, using SmartMarker to **repeat data in excel** gives you the cleanest separation between template design and business logic. It’s also language‑agnostic—similar concepts exist in Java, Python, and JavaScript libraries.

---

## Advanced tips & common pitfalls

### 1. Formatting the repeated rows

SmartMarker copies the entire row—including cell styles, borders, and conditional formatting. If you need a different style for the first or last row, add extra markers like `${If:Item.IsFirst}` and use conditional formulas inside Excel.

### 2. Dealing with large datasets

When working with > 10 000 rows, disable Excel’s automatic calculation before processing:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Re‑enable it after saving to keep performance snappy.

### 3. Populating Excel from data in a real database

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Then use `${Repeat:Order}` in the template to list every order. This pattern shows how easy it is to **populate excel from data** directly from Entity Framework.

### 4. Using multiple repeat blocks

You can have several `${Repeat:...}` markers on the same sheet or on different sheets. SmartMarker processes them sequentially, so order matters only if one block depends on the output of another.

---

## Complete runnable example

Below is a self‑contained console application you can paste into Visual Studio and run immediately. It demonstrates all three steps plus saving the file.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Expected output:** `Result.xlsx` contains a sheet where the row with `${Repeat:Item}` appears three times, showing A, B, and C. No manual adjustments needed.

---

## Conclusion

You now know how to **repeat data in excel** efficiently by leveraging the SmartMarkerProcessor. By defining a simple data object, loading a template workbook, and calling `Process`, you can **populate excel template**, **repeat rows in excel**, and generally **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}