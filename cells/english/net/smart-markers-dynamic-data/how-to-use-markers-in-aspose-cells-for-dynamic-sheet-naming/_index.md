---
category: general
date: 2026-05-23
description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
  Excel automation. Learn smart markers, JSON data binding, and sheet creation in
  minutes.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: en
og_description: How to use markers in Aspose.Cells to generate Excel files with dynamic
  sheet naming. Complete step‑by‑step guide with full C# example.
og_title: How to Use Markers – Dynamic Sheet Naming in Excel with Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
url: /net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel

Ever wondered **how to use markers** to turn a static Excel template into a fully‑fledged master‑detail workbook? You’re not alone. Many developers hit a wall when they need *dynamic sheet naming excel* capabilities, especially when the sheet names must reflect data values coming from JSON or a database.  

In this tutorial we’ll walk through a complete, ready‑to‑run C# example that shows **how to use markers** with **Aspose.Cells** smart markers, bind JSON data, and let the processor create sheets whose names change on the fly. No fluff, just the exact code you can drop into Visual Studio and see results instantly.

## What You’ll Learn

- The concept of **smart markers** and why they’re perfect for master‑detail scenarios.  
- How to embed marker tags in a workbook that will later be replaced with actual sheet names.  
- Setting up **dynamic sheet naming excel** using the `DetailSheetNewName` option.  
- Running the `SmartMarkerProcessor` against JSON data to generate multiple sheets automatically.  
- Verifying the output and a few handy tips to avoid common pitfalls.

> **Prerequisites** – You need a recent .NET runtime (≥ .NET 6 is fine), the Aspose.Cells for .NET library (you can grab a free trial from Aspose), and a basic familiarity with C#.  

---

![how to use markers example in Aspose.Cells](example.png "how to use markers example in Aspose.Cells")

## How to Use Markers to Create Dynamic Sheet Naming (Step 1)

The first thing we need is a blank workbook that will act as our template. In a real project you’d probably start from an existing `.xlsx` file that already contains layout, formatting, and placeholder cells. For the sake of clarity we’ll create everything programmatically.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Why this matters*: The `Worksheet` object is where we’ll drop our **smart marker** tags. Think of the tags as tiny placeholders that the processor will later replace with actual values from JSON.  

## Insert Smart Marker Tags (Step 2)

Now we place the marker tags directly into cells. The syntax `${...}` tells Aspose.Cells “this is a marker”. In our example we need two markers: one for the master sheet name and another for the detail sheet name.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – Keep marker names short and meaningful; they become the keys you’ll use in your JSON payload.

## Prepare the JSON Data (Step 3)

The processor works with any data source that can be represented as JSON, a `DataSet`, or even a plain object. Here’s a minimal JSON string that contains a master‑detail collection. Notice that each order carries both a `MasterSheetName` and a `DetailSheetName`.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Why JSON?* It’s lightweight, human‑readable, and works great with web APIs. You could just as easily pull this data from a SQL query and serialize it with `Newtonsoft.Json`.

## Initialise the SmartMarkerProcessor (Step 4)

The `SmartMarkerProcessor` is the engine that scans the workbook, finds markers, and performs the data binding. Instantiating it is a one‑liner.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Define Dynamic Sheet Naming (Step 5)

Here’s where **dynamic sheet naming excel** truly shines. By setting `DetailSheetNewName`, we tell the processor to create a new detail sheet for each order and name it based on the `OrderId`. The `${OrderId}` placeholder is resolved from the current record during processing.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Watch out** – If you forget to include the `${}` syntax, the sheet will literally be named “Detail_${OrderId}” instead of “Detail_1”, “Detail_2”, etc.

## Apply JSON and Generate Sheets (Step 6)

Now we let the processor do the heavy lifting. It will read the JSON, replace the markers, and create new worksheets as needed.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### What Happens Under the Hood?

1. The processor reads the `Orders` array.  
2. For each order it creates a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet** (using the `DetailSheetNewName` pattern).  
3. Cell values are replaced with the corresponding JSON fields, so the master sheet’s first cell ends up containing “Master_1”, “Master_2”, etc.  

## Save and Verify the Result (Optional)

Finally, write the workbook to disk. Open the file in Excel and you should see two master sheets (`Master_1`, `Master_2`) and two dynamically named detail sheets (`Detail_1`, `Detail_2`).  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Expected output** – After opening `output.xlsx` you’ll see:

- Sheet **Master_1** with cell A1 = “Master_1”.  
- Sheet **Detail_1** with cell A1 = “Detail_1”.  
- Sheet **Master_2** with cell A1 = “Master_2”.  
- Sheet **Detail_2** with cell A1 = “Detail_2”.  

That’s the full cycle of **how to use markers** to achieve **dynamic sheet naming excel** with **Aspose.Cells smart markers**.

---

## Common Questions & Edge Cases

### What if I need more than two levels of hierarchy?

You can nest markers inside the newly created detail sheets. Just place additional `${...}` tags in the template sheet before processing. The processor will cascade through each level automatically.

### Can I use a DataTable instead of JSON?

Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`, and even custom objects. The only change is the call to `ApplyJson` – you’d use `ApplyDataSet(myDataSet)` instead.

### How do I control the order of sheet creation?

The order follows the sequence of the source collection. If you need a custom sort, simply sort the JSON array (or DataTable) before passing it to the processor.

### Is there a way to hide the template sheet after processing?

Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`. The original sheet (index 0) will be removed from the final workbook.

---

## Full Working Example (All Steps Combined)

Below is the complete program you can copy‑paste into a new C# console project. Make sure you’ve referenced the `Aspose.Cells` NuGet package.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Run the program, open `output.xlsx`, and you’ll see the dynamic sheets exactly as described earlier.

---

## Wrapping Up

We’ve just covered **how to use markers** in Aspose.Cells to turn a plain workbook into a master‑detail solution with **dynamic sheet naming excel**. The key takeaways are:

1. Place `${...}` smart markers where you want data to appear.  
2. Feed JSON (or any supported data source) to the `SmartMarkerProcessor`.  
3. Use `DetailSheetNewName` to let the processor name new sheets on the fly.  

From here you can explore more advanced scenarios—adding tables, styling cells, or even embedding charts—all driven


## Related Tutorials

- [How to Implement Aspose.Cells Smart Markers in C# for Dynamic Excel Reporting](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Generate Dynamic Excel Reports Using Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Mastering Aspose.Cells .NET: Implement Smart Markers and Custom Labels for Dynamic Excel Reports](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}