---
category: general
date: 2026-03-25
description: Learn how to repeat items in Excel using C#. This guide shows how to
  generate Excel rows dynamically and populate an Excel template C# for any collection.
draft: false
keywords:
- how to repeat items in excel
- generate excel rows dynamically
- populate excel template c#
language: en
og_description: How to repeat items in Excel with C#? Follow this complete tutorial
  to generate Excel rows dynamically and populate an Excel template C# effortlessly.
og_title: How to Repeat Items in Excel – Step‑by‑Step C# Guide
tags:
- C#
- Excel automation
- Aspose.Cells
title: How to Repeat Items in Excel – Dynamic Row Generation with C#
url: /net/row-and-column-management/how-to-repeat-items-in-excel-dynamic-row-generation-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Repeat Items in Excel – Dynamic Row Generation with C#

Ever wondered **how to repeat items in Excel** without manually copying rows? Maybe you’ve got a list of orders, each with several line items, and you need a neat worksheet that expands automatically. In this tutorial you’ll see exactly that: we’ll generate Excel rows dynamically and **populate an Excel template C#** using the powerful Smart Marker feature of Aspose.Cells.

We’ll walk through a real‑world scenario, build a tiny data model, and watch the library turn our template into a fully‑filled sheet. By the end you’ll be able to repeat items in Excel for any collection, whether it’s a single order or a massive catalog. No fluff—just a working solution you can copy‑paste into your project.

## Prerequisites

- .NET 6.0 or later (the code also works on .NET Framework 4.7+)
- Visual Studio 2022 (or any IDE you prefer)
- **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`)
- A basic understanding of C# anonymous types

If you’re missing any of these, just add the NuGet package and you’re good to go. The library is fully managed, so no COM interop or Office installation is required.

---

## Step 1: Define a Smart Marker Template – the Core of “repeat items in Excel”

The first thing we need is a template cell that tells Aspose.Cells how to iterate over our collection. Smart Markers use a simple placeholder syntax that lives directly inside the worksheet.

```csharp
// Put the template into cell A1
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +          // Start repeating the Orders collection
    "   ${Item:Repeat}\n" +        // For each Order, repeat the Item collection
    "      ${Item.Name}\n" +       // Insert the Name of each Item
    "   ${/Item}\n" +              // End Item repeat block
    "${/Orders}");                 // End Orders repeat block
```

**Why this matters:** The `${Orders:Repeat}` marker tells the processor to loop over the `Orders` array. Inside that loop we start another repeat block for `Item`. Every time the inner loop runs, `${Item.Name}` gets replaced with the actual name, like “Apple” or “Banana”. When the processor finishes, the template expands into as many rows as needed—exactly what you need to **generate Excel rows dynamically**.

> **Pro tip:** Keep the indentation inside the string; it translates to proper row alignment in the final sheet.

## Step 2: Build a Matching Data Model – “populate excel template c#” Made Simple

Our template expects an object with an `Orders` property, each order containing an `Item` array. We’ll create an anonymous object that mirrors this shape:

```csharp
// Create a simple data model that matches the template
var dataModel = new
{
    Orders = new[]
    {
        new
        {
            Item = new[]
            {
                new { Name = "Apple" },
                new { Name = "Banana" }
            }
        },
        // You can add more orders here – the template will repeat automatically
        new
        {
            Item = new[]
            {
                new { Name = "Orange" },
                new { Name = "Grape" },
                new { Name = "Mango" }
            }
        }
    }
};
```

**Why this matters:** The structure of the anonymous object must line up exactly with the markers. If you miss a property or name it differently, the Smart Marker engine will silently skip it, leaving empty rows. This is a common pitfall when trying to **populate excel template c#** for the first time.

## Step 3: Run the Smart Marker Processor – The Engine That Repeats Items

Now that we have a template and a data model, we hand both over to Aspose.Cells. The processor walks the worksheet, expands the repeat blocks, and writes the values.

```csharp
// Process the template with the data model
worksheet.SmartMarkerProcessor.Process(dataModel);
```

That’s literally all the code you need to **repeat items in Excel**. After the call finishes, the worksheet will contain:

| A (generated) |
|---------------|
| Apple         |
| Banana        |
| Orange        |
| Grape         |
| Mango         |

Each item appears on its own row, regardless of how many orders or items you added to the model.

## Full Working Example – From Start to Finish

Below is a complete, ready‑to‑run console application that demonstrates the whole flow. Copy it into a new C# project, add the Aspose.Cells NuGet package, and run it. An `Output.xlsx` file will appear in the bin directory.

```csharp
using System;
using Aspose.Cells;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            var workbook = new Workbook();
            var worksheet = workbook.Worksheets[0];

            // 2️⃣ Define the Smart Marker template (Step 1)
            worksheet.Cells["A1"].PutValue(
                "${Orders:Repeat}\n" +
                "   ${Item:Repeat}\n" +
                "      ${Item.Name}\n" +
                "   ${/Item}\n" +
                "${/Orders}");

            // 3️⃣ Build the data model (Step 2)
            var dataModel = new
            {
                Orders = new[]
                {
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Apple" },
                            new { Name = "Banana" }
                        }
                    },
                    new
                    {
                        Item = new[]
                        {
                            new { Name = "Orange" },
                            new { Name = "Grape" },
                            new { Name = "Mango" }
                        }
                    }
                }
            };

            // 4️⃣ Process the template (Step 3)
            worksheet.SmartMarkerProcessor.Process(dataModel);

            // 5️⃣ Save the result
            workbook.Save("Output.xlsx");
            Console.WriteLine("Excel file generated! Open Output.xlsx to see the repeated items.");
        }
    }
}
```

**Expected output:** Open `Output.xlsx` and you’ll see a column with the five fruit names, each occupying its own row. No manual copying required.

### What If My Collection Is Empty?

If `Orders` or any `Item` array is empty, the Smart Marker engine simply skips the block, leaving no rows. This is handy when you need to **generate Excel rows dynamically** based on optional data—nothing extra appears.

### Handling Large Data Sets

For thousands of rows, the processor is still fast because it works in memory and writes directly to the workbook. However, you might want to:

- Disable calculation (`workbook.CalculateFormula = false`) before processing.
- Use `MemoryStream` if you need to return the file via a web API without touching the file system.

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Markers don’t expand | Misspelled property name or wrong case | Ensure the anonymous object’s property names match the markers exactly (`Orders`, `Item`, `Name`). |
| Blank rows appear | Extra newline characters inside the template string | Trim trailing `\n` or keep the template concise. |
| Processor throws `NullReferenceException` | Data model contains `null` for a collection | Guard against `null` by initializing empty arrays (`new object[0]`). |
| Output file is corrupted | Workbook not saved properly (e.g., using wrong format) | Use `workbook.Save("file.xlsx")` with the `.xlsx` extension. |

## Extending the Template – More Than Just Names

Smart Markers support any property, formulas, and even conditional blocks. For example, to add a price column:

```csharp
worksheet.Cells["A1"].PutValue(
    "${Orders:Repeat}\n" +
    "   ${Item:Repeat}\n" +
    "      ${Item.Name}\t${Item.Price}\n" +
    "   ${/Item}\n" +
    "${/Orders}");
```

And update the data model:

```csharp
new { Name = "Apple", Price = 0.99M },
new { Name = "Banana", Price = 0.59M }
```

The result will be two columns—one for the name, one for the price—again generated **dynamically**.

## Conclusion

You now have a complete, self‑contained solution for **how to repeat items in Excel** using C#. By defining a Smart Marker template, mirroring it with a matching data model, and invoking `SmartMarkerProcessor.Process`, you can **generate Excel rows dynamically** for any collection and effortlessly **populate excel template c#** projects.

What’s next? Try adding totals, conditional formatting, or exporting the same data to CSV. The same pattern works with nested collections, grouping, and even custom objects—so feel free to experiment.

If you found this guide helpful, give it a star on GitHub, share it with teammates, or drop a comment below. Happy coding, and enjoy the power of automated Excel generation! 

![Screenshot of generated Excel rows showing how to repeat items in Excel](/images/repeat-items-excel.png "how to repeat items in Excel")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}