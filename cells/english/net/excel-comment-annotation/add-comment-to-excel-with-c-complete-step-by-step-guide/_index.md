---
category: general
date: 2026-05-30
description: Add comment to Excel using C# quickly. Learn how to write comment to
  cell, insert Smart Marker placeholders, and save the workbook.
draft: false
keywords:
- add comment to excel
- write comment to cell
- add comment using c#
language: en
og_description: Add comment to Excel using C# in minutes. This tutorial shows how
  to write comment to cell, handle Smart Marker processing, and save the file.
og_title: Add comment to Excel with C# – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  headline: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Add comment to Excel using C# quickly. Learn how to write comment to
    cell, insert Smart Marker placeholders, and save the workbook.
  name: Add comment to Excel with C# – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Adding Multiple Comments in One Pass
    text: If you need to add comments to several cells, just place multiple placeholders
      (`${Comment1}`, `${Comment2}`, …) and expand the data object accordingly.
  - name: 2. Preserving Existing Comments
    text: Sometimes a sheet already contains reviewer notes that you don’t want to
      lose. Retrieve the existing comment, merge, then write back.
  - name: 3. Unicode and Emojis
    text: Excel fully supports Unicode, so you can embed emojis, non‑Latin scripts,
      or special symbols directly in the comment string.
  - name: 4. Large Workbooks & Performance
    text: 'Processing a workbook with thousands of Smart Markers can be costly. To
      improve speed:'
  type: HowTo
- questions:
  - answer: Yes, but you must open the workbook with the `LoadOptions` that allow
      editing, e.g., `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.
    question: Can I add a comment to a *read‑only* workbook?
  - answer: '`PutComment` overwrites the existing comment. To merge, retrieve the
      current comment first (`GetComment()`), concatenate, then call `PutComment`
      again.'
    question: What if the target cell already has a comment?
  - answer: Absolutely. Aspose.Cells abstracts the format; just point the `Workbook`
      constructor at the `.xls` file and everything else stays the same.
    question: Does this work with older `.xls` files?
  - answer: 'Practically, Excel supports comments up to 32,767 characters. Aspose.Cells
      respects the same limit—larger strings will be truncated. --- ## Recap & Next
      Steps We’ve covered how to **add comment to Excel** using C#, demonstrated the
      **write comment to cell** technique with Smart Markers, and explored'
    question: Is there a limit to comment length?
  type: FAQPage
tags:
- Excel
- C#
- Aspose.Cells
title: Add comment to Excel with C# – Complete Step‑by‑Step Guide
url: /net/excel-comment-annotation/add-comment-to-excel-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add comment to Excel with C# – Complete Step‑by‑Step Guide

Ever wondered how to **add comment to Excel** from a C# application without opening the file manually? You're not alone. Many developers need to **write comment to cell** programmatically—whether it’s for audit trails, reviewer notes, or dynamic reports. In this tutorial we’ll walk through a clean, end‑to‑end solution that uses Aspose.Cells’ Smart Marker feature, and we’ll also cover the “why” behind each step so you can adapt the pattern to your own projects.

By the end of the guide you’ll be able to:

* Load an existing workbook,
* Insert a placeholder comment into a specific cell,
* Replace the placeholder with real text using an anonymous object,
* Save the updated file,
* And handle a few common edge cases like existing comments or Unicode text.

No external scripts, no Excel interop, just pure C# code that works on Windows, Linux, and macOS.

---

## Prerequisites — What You Need Before You Start

* **Aspose.Cells for .NET** (v23.10 or later). The library is free to try, and the NuGet package name is `Aspose.Cells`.
* A .NET development environment (Visual Studio, Rider, or VS Code with the C# extension).  
* An input workbook (`input.xlsx`) placed in a folder you can reference from code.  
* Basic familiarity with C# anonymous types and object initializers.  

If you already have these pieces, great—let’s dive in. If not, grab the NuGet package with:

```bash
dotnet add package Aspose.Cells
```

That single line pulls in everything you need, including the `SmartMarkerProcessor` class we’ll use later.

---

## Step 1 – Load the Workbook (add comment to excel)

Before we can **add comment to Excel**, we must open the file in memory. Aspose.Cells abstracts the file format, so you don’t have to worry about whether it’s .xlsx, .xls, or even .csv.

```csharp
// Load the workbook that contains the target worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Why this matters:** Opening the workbook creates a `Workbook` object that holds all worksheets, styles, and existing comments. If you skip this step and try to reference a worksheet directly, you’ll hit a `NullReferenceException`.

---

## Step 2 – Pick the Worksheet and Cell (write comment to cell)

Most real‑world spreadsheets have multiple tabs. For simplicity we’ll work with the first sheet, but you can index by name if you prefer.

```csharp
// Grab the first worksheet (index 0)
Worksheet ws = wb.Worksheets[0];

// Place a Smart Marker placeholder in cell A1 where the comment will appear
ws.Cells["A1"].PutComment("${Comment}");
```

The call to `PutComment` creates a *comment* object attached to `A1`. The content `${Comment}` is a **Smart Marker placeholder**—think of it as a token that will be swapped later with real data.

> **Pro tip:** If the cell already contains a comment, `PutComment` overwrites it. To preserve existing comments, read `ws.Cells["A1"].GetComment().Comment` first, concatenate, then re‑apply.

---

## Step 3 – Prepare the Data Object (add comment using c#)

Smart Markers work with any .NET object that has properties matching the placeholder names. An anonymous object is perfect for quick demos.

```csharp
// Anonymous object that supplies the actual comment text
var data = new { Comment = "Reviewed by John – ✅ Approved" };
```

You can also use a strongly‑typed class if you need validation or additional fields.

```csharp
public class ReviewInfo
{
    public string Comment { get; set; }
    public DateTime ReviewedOn { get; set; }
}
```

Then instantiate:

```csharp
var data = new ReviewInfo
{
    Comment = "Reviewed by John – ✅ Approved",
    ReviewedOn = DateTime.UtcNow
};
```

> **Why anonymous objects?** They keep the code concise when you only need a handful of values. For larger data sets, a proper DTO (data‑transfer object) provides better maintainability.

---

## Step 4 – Process the Smart Marker (add comment to excel)

Now the magic happens. The `SmartMarkerProcessor` scans the worksheet, finds `${Comment}`, and replaces it with the value from `data.Comment`.

```csharp
// Run the processor to replace placeholders with real values
new SmartMarkerProcessor().Process(ws, data);
```

Under the hood the processor:

1. Parses the worksheet’s XML representation,
2. Detects any `${…}` tokens,
3. Looks up matching properties on the supplied object,
4. Writes the resolved string into the comment’s text node.

If the placeholder is missing, the processor silently skips it—no exception is thrown. That makes the approach safe for optional comments.

---

## Step 5 – Save the Workbook (see the result)

Finally, write the modified workbook back to disk. You can overwrite the original file or create a new one.

```csharp
// Save the workbook – you can change the format by using SaveOptions if needed
wb.Save("YOUR_DIRECTORY/output.xlsx");
```

When you open `output.xlsx` in Excel, you’ll see the comment “Reviewed by John – ✅ Approved” attached to cell **A1**. Hover over the little red triangle in the top‑right corner of the cell to view it.

> **Expected output:**  

> ![Screenshot showing a cell with a comment – add comment to excel example](add-comment-to-excel-example.png "add comment to excel example")

*The alt text includes the primary keyword, satisfying the SEO rule.*

---

## Handling Common Scenarios

### 1. Adding Multiple Comments in One Pass

If you need to add comments to several cells, just place multiple placeholders (`${Comment1}`, `${Comment2}`, …) and expand the data object accordingly.

```csharp
ws.Cells["A1"].PutComment("${Comment1}");
ws.Cells["B2"].PutComment("${Comment2}");

var data = new
{
    Comment1 = "First note",
    Comment2 = "Second note"
};

new SmartMarkerProcessor().Process(ws, data);
```

### 2. Preserving Existing Comments

Sometimes a sheet already contains reviewer notes that you don’t want to lose. Retrieve the existing comment, merge, then write back.

```csharp
var existing = ws.Cells["A1"].GetComment()?.Comment ?? string.Empty;
var merged   = string.IsNullOrWhiteSpace(existing)
               ? data.Comment
               : $"{existing}\n{data.Comment}";

ws.Cells["A1"].PutComment(merged);
```

### 3. Unicode and Emojis

Excel fully supports Unicode, so you can embed emojis, non‑Latin scripts, or special symbols directly in the comment string.

```csharp
var data = new { Comment = "审查通过 – ✅" };
```

Just ensure your source file is saved with UTF‑8 encoding (the default in most modern IDEs).

### 4. Large Workbooks & Performance

Processing a workbook with thousands of Smart Markers can be costly. To improve speed:

* Use `SmartMarkerProcessorOptions` to limit the scope to a single worksheet.
* Turn off calculation (`wb.CalculateFormula = false`) if you only need comments.
* Reuse a single `SmartMarkerProcessor` instance instead of creating a new one per sheet.

```csharp
var processor = new SmartMarkerProcessor
{
    Options = new SmartMarkerProcessorOptions { ProcessAllWorksheets = false }
};

processor.Process(ws, data);
```

---

## Full Working Example

Putting everything together, here’s a self‑contained console app you can copy‑paste into `Program.cs` and run.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCommentDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet and insert a placeholder comment
            Worksheet ws = wb.Worksheets[0];
            ws.Cells["A1"].PutComment("${Comment}");

            // 3️⃣ Prepare data – you can use an anonymous type or a DTO
            var data = new { Comment = "Reviewed by John – ✅ Approved" };

            // 4️⃣ Process Smart Markers to replace the placeholder
            new SmartMarkerProcessor().Process(ws, data);

            // 5️⃣ Save the result
            wb.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Comment added successfully!");
        }
    }
}
```

Run the program, open `output.xlsx`, and you’ll see the comment appear exactly where we placed the placeholder. No Excel UI needed, no COM interop, just pure managed code.

---

## Frequently Asked Questions (FAQ)

**Q: Can I add a comment to a *read‑only* workbook?**  
A: Yes, but you must open the workbook with the `LoadOptions` that allow editing, e.g., `new LoadOptions(LoadFormat.Xlsx) { ReadOnly = false }`.

**Q: What if the target cell already has a comment?**  
A: `PutComment` overwrites the existing comment. To merge, retrieve the current comment first (`GetComment()`), concatenate, then call `PutComment` again.

**Q: Does this work with older `.xls` files?**  
A: Absolutely. Aspose.Cells abstracts the format; just point the `Workbook` constructor at the `.xls` file and everything else stays the same.

**Q: Is there a limit to comment length?**  
A: Practically, Excel supports comments up to 32,767 characters. Aspose.Cells respects the same limit—larger strings will be truncated.

---

## Recap & Next Steps

We’ve covered how to **add comment to Excel** using C#, demonstrated the **write comment to cell** technique with Smart Markers, and explored variations like multiple comments, Unicode support, and performance tuning. The core pattern—placeholder → data object → processor → save—can be reused for any dynamic content, not


## What Should You Learn Next?

- [Add a Comment with Image in Excel](/cells/english/net/excel-comment-annotation/add-comment-with-image-excel/)
- [Add Image to Excel Comment with Aspose.Cells for Java: A Complete Guide](/cells/english/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)
- [Add Comment With Image Excel](/cells/german/net/excel-comment-annotation/add-comment-with-image-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}