---
category: general
date: 2026-05-23
description: Create dynamic excel table using a template and JSON data. Learn how
  to load excel template, automate excel report, and populate excel from json quickly.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: en
og_description: Create dynamic excel table in minutes with a template and JSON. This
  tutorial shows how to load excel template, automate excel report, and populate excel
  from json.
og_title: Create Dynamic Excel Table – Smart Marker Guide
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Create Dynamic Excel Table – Smart Marker Guide
url: /net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Dynamic Excel Table – Smart Marker Guide

Ever needed to **create dynamic excel table** that expands automatically for each record in your data set? You’re not the only one. Whether you’re building a monthly sales dashboard or a customer‑wise invoice pack, the ability to **populate excel from json** without writing endless loops can save hours.

In this tutorial we’ll walk through a complete, hands‑on solution that shows you how to **load excel template**, embed a Smart Marker, feed it JSON, and finally **automate excel report** generation. By the end you’ll have a ready‑to‑run .NET project that produces a polished Excel workbook from a single JSON payload.

---

## What You’ll Need

- **Aspose.Cells for .NET** (or any library that supports Smart Markers). The example uses version 24.5, but any recent release works.
- Visual Studio 2022 (or your favorite C# IDE).
- A simple Excel template file (`template.xlsx`) placed in a folder you control.
- A JSON string containing a collection named `Customers`.

That’s it—no extra services, no database connections, just pure code.

---

## Step 1: Create a Template Workbook – Load Excel Template

The first thing we do is **load excel template** into memory. Think of the template as a canvas where a special placeholder tells the processor where to repeat rows.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** Loading the template once keeps the file I/O minimal and lets you reuse the same layout for many reports. It also isolates the Smart Marker logic from the rest of your code, which is a clean separation of concerns.

---

## Step 2: Insert a Smart Marker – Create Dynamic Excel Table

Now we embed a **Smart Marker** that will repeat a table for every entry in the `Customers` collection. The syntax `${Customers.RepeatWorksheet}` tells Aspose.Cells to clone the entire worksheet for each customer.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Pro tip:** If you only need to repeat rows instead of whole worksheets, use `${Customers.Repeat}` on the first row of the table. The worksheet‑level repeat is handy when each customer gets its own tab.

---

## Step 3: Prepare the SmartMarkerProcessor – Automate Excel Report

With the marker in place, we create a `SmartMarkerProcessor`. This object orchestrates the data binding between JSON and the Excel template.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

The processor is lightweight; you can reuse it for multiple JSON payloads if you like.

---

## Step 4: Feed JSON Data – Populate Excel from JSON

Here’s where the magic happens. We feed a JSON string that contains an array of customers. Each customer can have fields like `Name`, `Email`, and `Total`.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Why JSON?** JSON is language‑agnostic and easy to generate from APIs, databases, or even manual entry. Using `ApplyJson` means you don’t have to map objects manually; the processor does the heavy lifting.

---

## Step 5: Save the Result – Generate Excel Report JSON

Finally, we write the populated workbook to disk. The output file now contains a separate worksheet for each customer, each filled with the data from our JSON.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Expected Output

- **output.xlsx** will have three worksheets named `Sheet1`, `Sheet2`, `Sheet3` (or whatever naming convention your template uses).
- Each sheet will display the `Name`, `Email`, and `Total` values for a single customer.
- The layout you designed in `template.xlsx` (headers, styling, formulas) is preserved across all generated sheets.

---

## Full Working Example

Below is the complete, ready‑to‑run program. Copy‑paste it into a console app, adjust the file paths, and hit **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Run the program, open `output.xlsx`, and you’ll see a **create dynamic excel table** in action—each customer gets its own sheet, fully formatted as you designed.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if my JSON has nested objects?* | Smart Markers support dot notation (`${Customers.Address.City}`) as long as the JSON hierarchy matches. |
| *Can I name the generated worksheets after the customer?* | Yes—add a marker like `${Customers.Name}` in the worksheet name cell or use `processor.ApplyJson(customersJson, "Customers")` with a naming pattern. |
| *What about large data sets (10 k+ rows)?* | The processor streams data efficiently, but keep an eye on memory. Consider splitting the report into multiple files if you hit performance limits. |
| *Do I need a license for Aspose.Cells?* | A free evaluation works for testing, but a licensed version removes evaluation watermarks and grants full features. |
| *Can I use this approach with .NET Core?* | Absolutely—Aspose.Cells supports .NET 6/7/8. Just reference the NuGet package and the code stays the same. |

---

## Tips for Production‑Ready Implementations

- **Validate JSON** before feeding it to `ApplyJson`. A malformed payload will throw a `JsonParseException`.
- **Cache the template** if you generate many reports in a short time; loading from disk repeatedly is unnecessary I/O.
- **Lock the workbook** during processing if you run this in a multi‑threaded web service to avoid race conditions.
- **Add error handling** around `workbook.Save` to gracefully handle permission issues or locked files.
- **Customize styling** in the template (conditional formatting, formulas) to let the generated sheets retain business logic without extra code.

---

## Conclusion

You now have a solid, end‑to‑end pattern for how to **create dynamic excel table** using a template, Smart Markers, and JSON data. By **loading excel template**, inserting a repeat marker, and **populate excel from json**, you can **automate excel report** generation with just a few lines of C#.

Next steps? Try adding charts that reference the dynamic tables, or export the same JSON to a PDF using Aspose.Words. You could also experiment with **generate excel report json** from a database query to close the loop


## Related Tutorials

- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Create Dynamic Line Charts in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [How to Create Checkboxes in Excel using Aspose.Cells for .NET | Data Validation Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}