---
category: general
date: 2026-03-21
description: Create Excel workbook C# and learn how to add comment to Excel, fill
  comment automatically using Smart Markers. Step‑by‑step guide for developers.
draft: false
keywords:
- create excel workbook c#
- add comment to excel
- how to add comment
- how to fill comment
- fill excel comment
language: en
og_description: Create Excel workbook C# and quickly add comment to Excel, then fill
  comment using Smart Markers. Complete tutorial with code.
og_title: Create Excel Workbook C# – Add and Fill Comments
tags:
- C#
- Excel automation
- Aspose.Cells
title: Create Excel Workbook C# – Add and Fill Comments with Smart Markers
url: /net/excel-comment-annotation/create-excel-workbook-c-add-and-fill-comments-with-smart-mar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook C# – Add and Fill Comments with Smart Markers

Ever needed to **create Excel workbook C#** and wondered how to embed a comment that updates itself automatically? You're not the only one. In many reporting scenarios you want a cell comment that says *“Created by Alice on 2024‑07‑15”* without hard‑coding the name or date each time.  

In this tutorial we’ll show you exactly **how to add comment to Excel**, then **how to fill comment** using Aspose.Cells’ Smart Markers. By the end you’ll have a ready‑to‑run program that creates a workbook, injects a dynamic comment, and saves the file—all in a few tidy steps.

> **What you’ll get:** a complete, compilable C# console app, an explanation of every line, tips for common pitfalls, and ideas for extending the solution.

## Prerequisites

- .NET 6.0 SDK or later (the code works with .NET Core and .NET Framework as well)  
- Visual Studio 2022 or any IDE you prefer  
- **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`) – this library powers the `Workbook`, `Worksheet`, and `SmartMarkerProcessor` classes used below.  
- Basic familiarity with C# syntax – if you’ve written a `Console.WriteLine`, you’re good to go.

Now that the groundwork is out of the way, let’s dive in.

![Create Excel workbook C# example screenshot](excel-workbook.png "Create Excel workbook C# example")

## Step 1: Initialise a New Workbook – Create Excel Workbook C# Basics

First we need a clean workbook object. Think of `Workbook` as the blank canvas; without it you can’t place any cells, rows, or comments.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // fresh Excel file
            Worksheet worksheet = workbook.Worksheets[0];    // default sheet named "Sheet1"
```

**Why this matters:** `Workbook` automatically creates a default worksheet, so you don’t have to call `Add` unless you need extra tabs. Accessing `Worksheets[0]` is the fastest way to start populating data.

## Step 2: Insert a Smart Marker Comment – How to Add Comment with Tokens

Next we place a comment in cell **B2** that contains Smart Marker tokens (`«UserName»` and `«CreatedDate»`). These tokens will be replaced later with actual values.

```csharp
            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";
```

**Explanation:**  
- `CreateComment()` creates the comment object if none exists; otherwise it returns the existing one.  
- The `Note` property holds the visible text. By wrapping the placeholders in `« »` we tell Aspose.Cells that they are **Smart Markers** – placeholders that can be swapped out in one shot.

> **Pro tip:** If you need a multi‑line comment, use `\n` inside the string, e.g., `"Line1\nLine2"`.

## Step 3: Prepare the Data Object – How to Fill Comment Dynamically

Smart Markers need a data source. In C# the easiest way is an anonymous type that matches the placeholder names.

```csharp
            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now   // will be formatted automatically
            };
```

**Why an anonymous type?**  
It’s lightweight, requires no extra class file, and matches the property names (`UserName`, `CreatedDate`) exactly to the token names. If you prefer a strongly‑typed model, just create a class with the same properties.

## Step 4: Process Smart Markers – How to Fill Comment Using the Data Object

Now the magic happens. The `SmartMarkerProcessor` scans the workbook for any `«…»` tokens and swaps them with values from `markerData`.

```csharp
            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);
```

**What’s under the hood?**  
`SmartMarkerProcessor` walks through each cell, comment, header, etc., looking for the `«Token»` pattern. When it finds one, it uses reflection to read the matching property from `markerData` and writes the value back. No manual loops required.

## Step 5: Save the Workbook – Fill Excel Comment and Persist the File

Finally we write the workbook to disk. The comment now reads something like *“Created by Alice on 03/21/2026 10:15 AM”*.

```csharp
            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Result verification:** Open `CommentFilled.xlsx` in Excel, hover over cell **B2**, and you’ll see the comment with the actual user name and timestamp. No further code changes needed for future runs—just change `markerData` values.

---

## Common Variations & Edge Cases

### Using a Custom Date Format

If you want the date in `yyyy‑MM‑dd` format, adjust the data object:

```csharp
CreatedDate = DateTime.Now.ToString("yyyy-MM-dd")
```

### Adding Multiple Comments

You can repeat **Step 2** for other cells. Each comment can have its own set of tokens, or share the same ones if the information is universal.

### Working with Existing Workbooks

Instead of `new Workbook()`, load an existing file:

```csharp
Workbook workbook = new Workbook(@"ExistingFile.xlsx");
```

The rest of the steps stay identical—Smart Markers work on both new and pre‑existing files.

### Handling Null Values

If a token might be missing, wrap the property in a nullable type or provide a fallback:

```csharp
UserName = user?.Name ?? "Unknown"
```

The processor will insert *“Unknown”* when the source is `null`.

---

## Full Working Example (Copy‑Paste Ready)

Below is the **entire program** you can drop into a console app project and run immediately (just replace `YOUR_DIRECTORY` with a real folder path).

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Add a comment that contains Smart Marker tokens
            var comment = worksheet.Cells["B2"].CreateComment();
            comment.Note = "Created by «UserName» on «CreatedDate»";

            // Step 3: Prepare the data that will replace the tokens
            var markerData = new
            {
                UserName = "Alice",
                CreatedDate = DateTime.Now
            };

            // Step 4: Process the Smart Markers in the worksheet using the data object
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
            processor.Process(worksheet, markerData);

            // Step 5: Save the workbook with the filled comment
            string outputPath = @"YOUR_DIRECTORY\CommentFilled.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Run the program, open the generated file, and you’ll see the dynamic comment in cell **B2**. Easy, right?

---

## Frequently Asked Questions (FAQ)

**Q: Does this work with .NET Framework 4.7?**  
A: Absolutely. Aspose.Cells supports .NET Framework 4.0+ and .NET Core/5/6/7. Just reference the appropriate DLL or NuGet package.

**Q: Can I use this approach for data validation or conditional formatting?**  
A: Smart Markers are primarily for inserting values into cells, comments, headers, and footers. For conditional formatting you’d still use the normal `Style` APIs.

**Q: What if I need to add a comment to a **different** worksheet?**  
A: Retrieve the target worksheet (`workbook.Worksheets["MySheet"]`) and repeat **Step 2** on that sheet’s cells.

---

## Next Steps & Related Topics

- **How to add comment to Excel** programmatically for multiple cells (loop through a range).  
- **Fill Excel comment** with data from a database (use a `DataTable` as the data source for Smart Markers).  
- Explore **Smart Marker arrays** to generate tables automatically.  
- Learn about **Aspose.Cells styling** to format the comment’s font, color, and size.

Experiment with the snippets, swap out the data source, and you’ll quickly master **how to fill comment** in any Excel automation scenario.

---

### Wrap‑Up

We’ve just walked through the entire process of **create excel workbook c#**, **add comment to excel**, and **fill excel comment** using Smart Markers. The solution is compact, reusable, and ready for production.  

Give it a try, tweak the placeholders, and let the library handle the heavy lifting. If you run into any snags, drop a comment below—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}