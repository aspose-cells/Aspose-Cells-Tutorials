---
category: general
date: 2026-02-14
description: Create master data object in C# and generate detail sheet effortlessly.
  Learn the full SmartMarker workflow with practical code examples.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: en
og_description: Create master data object in C# and generate detail sheet with SmartMarker.
  Follow our detailed tutorial for a ready‑to‑run solution.
og_title: Create Master Data Object – Complete Guide
tags:
- C#
- SmartMarker
- Excel Automation
title: Create Master Data Object – Step‑by‑Step Guide to Generate Detail Sheet
url: /net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Master Data Object – Complete Tutorial

Ever needed to **create master data object** for an Excel worksheet but weren’t sure how to hook it up to a SmartMarker detail sheet? You’re not alone. In many reporting scenarios the master object drives a dynamic detail sheet, and getting the wiring right can feel like assembling a puzzle without the picture.  

In this guide we’ll walk through the entire process—building the master data object, configuring the SmartMarker options to **generate detail sheet**, and finally firing the processor. By the end you’ll have a runnable snippet you can paste into any .NET project that uses the GrapeCity Documents for Excel (GcExcel) library.

## What You’ll Need

- .NET 6+ (or .NET Framework 4.7.2) with a reference to `GcExcel.dll`
- Basic C# familiarity (variables, anonymous types, object initializers)
- An Excel workbook that already contains SmartMarker tags like `{{OrderId}}` and a table for line items
- Visual Studio, Rider, or any editor you prefer

That’s it—no extra NuGet packages beyond the core GcExcel distribution.

## Step 1: Create the Master Data Object

The first thing you must do is **create master data object** that mirrors the structure expected by the SmartMarker tags. Think of it as a tiny in‑memory report model.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Why use an anonymous type here? Because it lets you define a lightweight container without declaring a full‑blown class—perfect for quick demos or when the shape is unlikely to change. If you need a reusable model later, just replace `var` with a proper POCO.

> **Pro tip:** Keep the property names (`OrderId`, `Product`, `Quantity`) identical to the placeholders in your worksheet; SmartMarker matches them case‑insensitively.

## Step 2: Configure SmartMarker Options to Generate a Detail Sheet

Now we tell SmartMarker that we want a separate worksheet for the line‑item table. This is where the **generate detail sheet** keyword comes into play.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

The `DetailSheetNewName` pattern uses curly‑brace placeholders that are replaced at runtime. In our example the sheet will be called `Order_1`. If you later loop over multiple orders, each gets its own tab—exactly what most accountants expect.

## Step 3: Run the SmartMarker Processor

With data and options ready, the final step is to invoke the processor on the target worksheet.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Behind the scenes, SmartMarker scans the worksheet for tags, injects the `orderData` values, and because `DetailSheet` is `true`, it clones the template into a new sheet named `Order_1`. All line items appear in the detail area, preserving any formatting you applied in the template.

### Full Working Example

Below is a self‑contained console program that opens a template workbook (`Template.xlsx`), runs the three steps, and saves the result as `Result.xlsx`. You can copy‑paste this into a new console project and hit **F5**.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Expected Output

- **Result.xlsx** contains a sheet called `Order_1`.
- Cell `A1` (or wherever you placed `{{OrderId}}`) now shows `1`.
- A table starting at the SmartMarker block lists two rows:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

If you open the file, you’ll see the formatting from the template preserved—borders, fonts, conditional formatting—all intact.

## Common Questions & Edge Cases

### What if I have multiple orders?

Wrap the master object in a collection and let SmartMarker iterate automatically:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Each order spawns its own sheet (`Order_1`, `Order_2`, …). The processor treats the outer array as the master collection.

### How do I control the sheet’s position?

Set `smartMarkerOptions.DetailSheetInsertIndex = 2;` to place the new sheet after the second tab, or use `DetailSheetInsertAfter = "Summary"` to insert after a named sheet.

### Can I disable the detail sheet for a particular run?

Simply toggle `DetailSheet = false;`. SmartMarker will then write the line items into the same sheet where the master tags reside.

### What about large data sets?

SmartMarker streams data efficiently, but if you exceed a few hundred thousand rows you might hit Excel’s 1,048,576‑row limit. In that case split the data into multiple master records or consider exporting to CSV.

## Visual Overview

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*The illustration shows the flow from the C# master object → SmartMarker options → worksheet processing → new detail sheet.*

## Conclusion

You now know how to **create master data object** in C# and configure SmartMarker to **generate detail sheet** automatically. The three‑step pattern—data, options, processor—covers the majority of Excel automation scenarios with GcExcel.  

From here you might explore:

- Adding header/footer data to each detail sheet
- Using conditional formatting based on order status
- Exporting the generated workbook to PDF with `workbook.SaveAsPdf(...)`

Feel free to experiment, break things, and then bring them back together. That’s the fastest way to master worksheet automation. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}