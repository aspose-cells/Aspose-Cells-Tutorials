---
category: general
date: 2026-11-19
description: Learn how to duplicate worksheets based on data collections and fill them with values in a few steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: en
lastmod: 2026-11-19
og_description: Learn how to duplicate worksheets based on data collections and fill them with values.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Repeat worksheets – step‑by‑step guide
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: Learn how to duplicate worksheets based on data collections and fill them with values in a few steps.
  headline: Repeat worksheets using markers in a spreadsheet
  type: TechArticle
- description: Learn how to duplicate worksheets based on data collections and fill them with values in a few steps.
  name: Repeat worksheets using markers in a spreadsheet
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker, extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Repeat worksheets using markers in a spreadsheet
url: /net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Repeat worksheets using markers in a spreadsheet

If you need to **repeat worksheets** when generating Excel reports, this guide shows you a complete, runnable solution. By the end of the tutorial you’ll be able to **populate Excel with array** data, **generate multiple worksheets**, and **populate worksheet from list** using the SmartMarkerProcessor library.

Repeating a worksheet is a common requirement when each department, region, or time period needs its own tab. The example below demonstrates the exact steps, explains why each setting matters, and covers edge cases such as empty lists or custom naming.

## Prerequisites

Before you start, make sure you have:

- .NET 6.0 or later installed
- A reference to the **GroupDocs.Viewer** (or equivalent) NuGet package that contains `SmartMarkerProcessor`
- An Excel template workbook (`.xlsx`) with a marker like `${repeat:Dept}` placed in a row you want to repeat
- Basic familiarity with C# and LINQ (optional but helpful)

No additional third‑party libraries are required.

## Step 1: Create the SmartMarkerProcessor instance

The processor orchestrates the marker replacement and worksheet duplication. Instantiating it without arguments uses the default options.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Creating the processor early lets you configure global options before any data is applied. This is the foundation for **repeat worksheets** correctly.

## Step 2: Enable worksheet repetition

By default the processor replaces markers on the current sheet only. Setting `RepeatWorksheet` to `true` tells the engine to clone the entire worksheet for each item in the data collection.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Enabling this option is the key to **generate multiple worksheets**—the processor will create a new tab for every element in the `Dept` array and keep the original formatting.

## Step 3: Prepare the data source as an array or list

SmartMarkerProcessor works with any enumerable, but using an array makes the intent clear when you want to **populate worksheet from list**. Here we create an anonymous object that contains a `Dept` property holding a string array.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

If you already have a `List<string>` you can pass it directly; the processor will treat it the same way. The important part is that the property name (`Dept`) matches the marker `${repeat:Dept}` in the template.

## Step 4: Load the template worksheet

Assuming you have an `ExcelPackage` (from EPPlus) or a `Workbook` object, retrieve the worksheet you want to repeat. The variable `ws` represents that sheet.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

If you prefer a different library (e.g., ClosedXML), the same principle applies: obtain a worksheet object that implements the required interface.

## Step 5: Process the worksheet with the data

Now apply the data to the template. The processor clones the worksheet for each department, replaces the `${repeat:Dept}` marker with the actual department name, and leaves the rest of the sheet untouched.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

After `Process` completes, `ws` becomes the first of several worksheets—one per department. The original sheet’s name is preserved, while the duplicates receive incremental suffixes (e.g., “Sheet1 (1)”, “Sheet1 (2)”). You can rename them afterward if you need a custom naming scheme.

### Expected output

When you open the resulting workbook, you should see:

- **Sheet1** – the original template (often left blank or used as a master)
- **Sheet1 (1)** – populated with “HR”
- **Sheet1 (2)** – populated with “IT”
- **Sheet1 (3)** – populated with “Finance”

Each sheet contains the same layout but with the department name substituted where `${repeat:Dept}` appeared.

## Handling edge cases

### Empty or null arrays

If `Dept` is null or empty, the processor will not create any additional worksheets. To avoid a completely blank workbook, you can add a guard:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Custom worksheet names

The default naming scheme may not suit every reporting requirement. After processing, rename each sheet using a loop:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Populating additional columns

If you need to **populate excel with array** values beyond a single marker, extend the data object:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Then adjust the template markers to `${repeat:Dept.Name}` and `${repeat:Dept.Headcount}`. The processor will repeat the row for each department and fill both columns.

## Full working example

Below is a self‑contained console application that demonstrates the entire flow from template loading to saving the final workbook.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explanation of key sections**

- **Processor creation** – establishes the engine that will interpret markers.
- **RepeatWorksheet option** – activates the core feature that answers *how to repeat worksheets*.
- **Data source** – uses an array (`new[]`) to satisfy **populate excel with array**.
- **Template loading** – demonstrates a common way to obtain a worksheet object.
- **Processing** – performs the duplication and data insertion in one call.
- **Renaming** – shows how to turn the generic “(1)”, “(2)” names into meaningful titles, a typical requirement after **generate multiple worksheets**.

Running this program produces `Result.xlsx` with three department‑specific tabs, each populated from the array.

## Common pitfalls and pro tips

- **Marker spelling** – the marker must match the property name exactly (`${repeat:Dept}`). A typo prevents repetition.
- **Worksheet index** – after processing, the original sheet stays at index 0; generated sheets follow sequentially. Mis‑indexing can lead to renaming the wrong tab.
- **Large data sets** – generating hundreds of worksheets can increase file size dramatically. Consider splitting reports or using a single sheet with grouped sections if performance becomes an issue.
- **Thread safety** – `SmartMarkerProcessor` is not thread‑safe. Create a separate instance per thread if you process multiple workbooks in parallel.

## Conclusion

You now know **how to repeat worksheets** in Excel using SmartMarkerProcessor, how to **populate excel with array** data, how to **generate multiple worksheets**, and how to **populate worksheet from list** efficiently. The complete example ties all concepts together, and the optional renaming step lets you produce clean, user‑friendly tab names.

Next, you might explore:

- Using **populate worksheet from list** with complex objects (nested collections)
- Applying conditional formatting after worksheet duplication
- Exporting the generated workbook to PDF or CSV for downstream consumption

Feel free to adapt the code to your own reporting scenarios, and enjoy automating Excel workbooks with confidence!

## What should you learn next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Repeat Worksheets – Complete Guide for Excel Automation]({{< relref "cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation" >}})
- [Create Worksheet Per Item – How to Repeat Worksheet in C#]({{< relref "cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c" >}})
- [How to expand array in Excel and populate a template]({{< relref "cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template" >}})

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}