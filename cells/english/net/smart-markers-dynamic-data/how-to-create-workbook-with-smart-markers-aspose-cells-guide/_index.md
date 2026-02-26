---
category: general
date: 2026-02-23
description: How to create workbook using Aspose.Cells and add markers with a JSON
  array. Learn how to add markers, use JSON array, and smart markers Aspose.Cells
  in minutes.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: en
og_description: How to create workbook using Aspose.Cells, add markers, and use a
  JSON array. This step‑by‑step guide shows you everything you need.
og_title: How to Create Workbook with Smart Markers – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: How to Create Workbook with Smart Markers – Aspose.Cells Guide
url: /net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Workbook with Smart Markers – Aspose.Cells Guide

Ever wondered **how to create workbook** that automatically fills data from a JSON source? You’re not the only one—developers constantly ask how to add markers that pull values from arrays, especially when working with Aspose.Cells. The good news? It’s pretty straightforward once you grasp the smart‑marker concept. In this tutorial we’ll walk through creating a workbook, adding markers, using a JSON array, and configuring smart markers in Aspose.Cells so you can generate Excel files on the fly.

We’ll cover everything you need to know: initializing the workbook, building a `MarkerCollection`, feeding a JSON array, toggling the “ArrayAsSingle” flag, and finally applying the markers. By the end you’ll have a fully functional C# program that produces an Excel file with the values **A**, **B**, and **C** populated automatically. No external services, just pure Aspose.Cells magic.

## Prerequisites

- .NET 6.0 or later (the code also works with .NET Framework 4.6+)
- Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`)
- A basic understanding of C# syntax (if you’re brand new, the snippets are heavily commented)
- Visual Studio or any IDE you prefer

If you already have these, great—let’s dive in.

## Step 1: How to Create Workbook (Initialize the Excel File)

The first thing you need is an empty workbook object. Think of it as a blank canvas that Aspose.Cells will later paint with data.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Why this matters:** `Workbook` is the entry point for every Excel operation. Without it you can’t attach smart markers or save the file. Creating the workbook first also ensures you have a clean environment for the subsequent steps.

## Step 2: How to Add Markers – Initialise a Marker Collection

Smart markers live inside a `MarkerCollection`. This collection is where you define placeholders (the markers) and the data that will replace them.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Pro tip:** You can reuse the same `MarkerCollection` for multiple worksheets, but keeping one per sheet makes debugging easier.

## Step 3: Use JSON Array – Add a Marker with JSON Data

Now we actually add a marker. The placeholder `{SmartMarker}` will be replaced by the JSON array we supply. The JSON must be a stringified array, e.g., `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Explanation:** The `Add` method takes two arguments: the marker text and the data source. Here the data source is a JSON array, which Aspose.Cells can parse automatically. This is the core of **use json array** with smart markers.

## Step 4: Configure the Marker – Treat the Array as a Single Value

By default, Aspose.Cells expands a JSON array into separate rows. If you want the whole array to be treated as a single cell value (useful for dropdown lists or concatenated strings), set the `ArrayAsSingle` flag.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **When to use it:** If you need the array to appear in one cell (e.g., `"A,B,C"`), enable this flag. Otherwise, Aspose.Cells will write each element into its own row.

## Step 5: Attach Markers to the Worksheet and Apply Them

Finally, bind the marker collection to the worksheet and tell Aspose.Cells to replace the placeholders with actual data.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Result:** After running the program, `SmartMarkerResult.xlsx` contains the value **A** (or the whole array if `ArrayAsSingle` is true) in cell `A1`. Open the file to verify.

### Expected Output

| A |
|---|
| A |   *(if `ArrayAsSingle` is false, the first element fills the cell)*

If you set `ArrayAsSingle = true`, cell `A1` will contain the string `["A","B","C"]`.

## Step 6: How to Add Markers – Advanced Scenarios (Optional)

You might wonder, *what if I need more than one marker?* The answer is simple: just call `Add` again.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Why this works:** Each marker operates independently, so you can mix “array as single” and “expand into rows” within the same worksheet. This flexibility is a hallmark of **smart markers aspose.cells**.

## Common Pitfalls & How to Avoid Them

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| Marker not replaced | Placeholder text missing or typo | Ensure the cell contains the exact marker string (`{SmartMarker}`) |
| JSON not parsed | Invalid JSON syntax (missing quotes) | Use a JSON validator or double‑escape quotes in C# strings |
| Array expands unexpectedly | `ArrayAsSingle` left at default `false` | Set `["ArrayAsSingle"] = true` for the specific marker |
| Workbook saved empty | `Apply()` not called before `Save()` | Always call `worksheet.SmartMarkers.Apply()` before saving |

## Full Working Example (Copy‑Paste Ready)

Below is the complete program you can drop into a console app. No additional files are required.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Run the program, open `SmartMarkerResult.xlsx`, and you’ll see the JSON array (or its first element) neatly placed in cell **A1**.

## Next Steps: Extending the Solution

Now that you know **how to create workbook**, **how to add markers**, and **use json array** with Aspose.Cells, consider these follow‑up ideas:

1. **Multiple Worksheets** – Loop through a list of worksheets and attach different marker collections to each.
2. **Dynamic JSON** – Pull JSON from a web API (`HttpClient`) and feed it directly into `smartMarkerCollection.Add`.
3. **Styling Output** – After applying markers, format cells (fonts, colors) to make the report look polished.
4. **Export Formats** – Save the workbook as PDF, CSV, or HTML by changing `workbook.Save("file.pdf")`.

Each of these topics naturally involves **smart markers aspose.cells**, so you’ll be extending the same core concepts you just learned.

## Conclusion

We’ve walked through **how to create workbook** from scratch, **how to add markers**, and how to **use json array** with Aspose.Cells smart markers. The complete, runnable example demonstrates the entire workflow, from initializing the `Workbook` to saving the final file. By toggling the `ArrayAsSingle` flag you gain fine‑grained control over how JSON data appears in Excel, making the solution adaptable to a wide range of reporting scenarios.

Give the code a spin, tweak the JSON, and experiment with additional markers. When you master these building blocks, generating sophisticated Excel reports becomes a piece of cake. Got questions or want to share a cool use‑case? Drop a comment below—happy coding! 

![Diagram showing how to create workbook with smart markers in Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "how to create workbook with Aspose.Cells smart markers")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}