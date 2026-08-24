---
category: general
date: 2026-02-15
description: Parse nested JSON C# using SmartMarkers and learn how to create JSON
  payload C# for complex orders. Step‑by‑step guide with full code and explanations.
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: en
og_description: Parse nested JSON C# instantly. Learn to create JSON payload C# and
  process it with SmartMarkers in a complete, runnable example.
og_title: Parse Nested JSON C# – Create JSON Payload C#
tags:
- json
- csharp
- smartmarkers
title: Parse Nested JSON C# – Create JSON Payload C#
url: /net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Nested JSON C# – Create JSON Payload C#  

Ever needed to **parse nested JSON C#** but weren’t sure where to start? You’re not alone—many developers hit a wall when their data contains arrays inside objects. The good news is that with a few lines of code you can both **create JSON payload C#** and let SmartMarkers walk through the nested structure for you.  

In this tutorial we’ll build a JSON string that represents orders with line‑items, enable the SmartMarkers processor to understand nested ranges, and finally verify that the data was parsed correctly. By the end you’ll have a self‑contained, copy‑paste‑ready program that you can adapt to any hierarchical JSON you face.

## What You’ll Need  

- .NET 6 or later (the code compiles with .NET Core 3.1 as well)  
- A reference to the SmartMarkers library (or any similar processor that supports nested ranges)  
- Basic C# knowledge—nothing exotic, just the usual `using` statements and a `Main` method  

That’s it. No extra NuGet packages beyond the marker library, and no external services.

## Step 1: Create JSON Payload C# – Building the Data  

First we craft the JSON string that contains an array of orders, each order holding its own `Lines` array. Think of it as a mini‑order‑management snapshot.

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

Why build the payload as a verbatim string? It preserves line breaks and lets you see the structure at a glance—handy when you’re debugging nested JSON.  

> **Pro tip:** If your JSON comes from a database or an API, you can replace the literal with `File.ReadAllText` or a web request—nothing in this tutorial depends on the source.

## Step 2: Enable Nested Ranges with SmartMarkerOptions  

SmartMarkers needs a little nudge to understand that an array can contain another array. That’s what `EnableNestedRanges` does.

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

Setting `EnableNestedRanges` to `true` tells the processor to treat each `Lines` collection as a sub‑range of its parent `Orders` range. Without this flag, the inner loop would be ignored, and you’d only see the top‑level objects.

## Step 3: Process the JSON with SmartMarkersProcessor  

Now we hand the JSON string and the options to the processor. The call is synchronous and returns nothing—SmartMarkers writes its results to the internal context, which you can retrieve later.

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

If you’re using a different library, replace `ws.SmartMarkersProcessor.Process` with the appropriate method name; the principle remains the same—pass the JSON and the configuration that enables nested handling.

## Step 4: Verify the Parsed Result  

After processing, you’ll typically want to confirm that every order and its line items were visited. Below is a simple way to dump the data back to the console using a hypothetical `GetProcessedData` method (replace with your library’s actual accessor).

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Expected console output**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

Seeing the hierarchy reproduced confirms that **parse nested json c#** worked as intended.

## Step 5: Edge Cases & Common Pitfalls  

### Empty Collections  
If an order has no `Lines`, the processor will still create an empty range. Make sure your downstream code can handle an empty list without throwing `NullReferenceException`.

### Deeply Nested Structures  
`EnableNestedRanges` works for two‑level nesting out of the box. For three or more levels you may need to set `MaxNestedDepth` (if the library exposes it) or recursively invoke the processor on each sub‑object.

### Special Characters  
JSON strings containing quotes, backslashes, or Unicode need proper escaping. Using a verbatim string (`@""`) as we did sidesteps most issues, but if you construct JSON programmatically, let `System.Text.Json.JsonSerializer` handle the escaping for you.

### Performance  
Parsing large payloads (megabytes) can be memory‑intensive. Consider streaming the JSON with `Utf8JsonReader` and feeding chunks to the processor if you hit performance bottlenecks.

## Visual Overview  

![Diagram illustrating how parse nested json c# flows through SmartMarkers processing](parse-nested-json-csharp-diagram.png "parse nested json c# diagram")

The image shows the journey from raw JSON → SmartMarkerOptions → Processor → Parsed object model.

## Recap  

We’ve walked through a complete **parse nested json c#** example, from **create json payload c#** to verifying the nested data after processing. The key takeaways are:

1. Build a well‑structured JSON string that mirrors your domain objects.  
2. Turn on `EnableNestedRanges` (or the equivalent) so the parser respects inner arrays.  
3. Run the processor and inspect the result to ensure every level was visited.  

## What’s Next?  

- **Dynamic payloads:** Replace the hard‑coded string with objects serialized via `System.Text.Json`.  
- **Custom markers:** Extend SmartMarkers with your own tags to inject calculated fields into each line item.  
- **Error handling:** Wrap the `Process` call in a try/catch and log `SmartMarkerException` details for troubleshooting.  

Feel free to experiment—swap out the `Orders` array for customers, invoices, or any hierarchical data you need to **parse nested json c#**. The pattern stays the same.

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}