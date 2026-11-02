---
category: general
date: 2026-03-18
description: Create Excel workbook C# with a comment and save workbook as XLSX. Learn
  how to add comment, generate excel comment, and automate Excel files.
draft: false
keywords:
- create excel workbook c#
- add excel comment
- save workbook as xlsx
- how to add comment
- generate excel comment
language: en
og_description: Create Excel workbook C# with a comment and save workbook as XLSX.
  Follow this step‑by‑step guide to add excel comment and generate excel comment programmatically.
og_title: Create Excel Workbook C# – Add Comment & Save as XLSX
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Create Excel Workbook C# – Add Comment & Save as XLSX
url: /net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook C# – Add Comment & Save as XLSX

Ever needed to **create Excel workbook C#** and stick a note inside a cell, but weren’t sure where to start? You’re not the only one—developers constantly ask *how to add comment* without opening Excel manually.  

In this tutorial you’ll get a complete, ready‑to‑run solution that shows **how to add excel comment**, **generate excel comment** with a Smart Marker, and **save workbook as xlsx** in a single, fluid flow. No dangling references, just pure code you can paste into Visual Studio and watch it work.

## What You’ll Learn

- Initialize an Excel workbook from scratch using C#.
- Insert a Smart Marker that becomes an Excel comment.
- Feed JSON data to turn the marker into a real comment.
- Persist the file as an `.xlsx` workbook.
- Optional approaches for adding comments without Smart Markers.

By the end you’ll have a self‑contained example that you can adapt to invoices, test reports, or any situation where a cell comment adds context.

### Prerequisites

- .NET 6 (or .NET Framework 4.7+).  
- **Aspose.Cells for .NET** NuGet package – the library that powers the Smart Marker feature.  
- A basic C# development environment (Visual Studio, VS Code, Rider…).

> **Pro tip:** If you’re on a budget, Aspose offers a free trial that’s fully functional for development and testing.

---

## Step 1: Create Excel Workbook C# – Setting Up the Project

First, let’s spin up a new console app and pull in the Aspose.Cells package.

```bash
dotnet new console -n ExcelCommentDemo
cd ExcelCommentDemo
dotnet add package Aspose.Cells
```

Now open `Program.cs`. The very first thing we do is **create a new workbook**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1️⃣: Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // creates an empty Excel file in memory
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

Why start with a brand‑new workbook? It guarantees a clean slate, eliminates hidden formatting, and lets you control everything from the ground up—perfect for automated report generation.

---

## Step 2: How to Add Comment – Using a Smart Marker

Smart Markers are placeholders that Aspose replaces with data at runtime. By embedding a marker that follows the **`${Comment:UserComment}`** pattern, we tell the engine to turn the placeholder into an actual comment.

```csharp
        // Step 2️⃣: Place a Smart Marker in B2 that will become a comment
        ws.Cells["B2"].PutValue("${Comment:UserComment}");
```

Notice the `Comment:` prefix? That’s the cue for the processor to treat the value as a comment rather than plain text. If you’re wondering *“does this work with other cell types?”*—yes, you can apply the same marker to any cell, even merged ranges.

---

## Step 3: Prepare the JSON Data – What the Comment Will Say

The next piece is the data source. Here we use a simple JSON string, but you could as well feed a DataTable, a List, or even a custom object.

```csharp
        // Step 3️⃣: Define JSON that supplies the comment text
        string json = "{ \"UserComment\": \"Reviewed by QA\" }";
```

Feel free to swap `"Reviewed by QA"` with any dynamic value—perhaps a timestamp, a user name, or a link to an issue tracker. The key name (`UserComment`) must match the marker’s identifier.

---

## Step 4: Generate Excel Comment – Processing the Smart Marker

Now we hand the JSON to the Smart Marker processor. This is the moment where **generate excel comment** actually happens.

```csharp
        // Step 4️⃣: Process the marker and turn it into a real comment
        ws.SmartMarkerProcessor.Process(json);
```

Behind the scenes, Aspose parses the JSON, finds the `UserComment` field, and injects it as a comment attached to cell **B2**. The cell’s visible value remains the original placeholder text, but Excel will show the comment when you hover over it.

---

## Step 5: Save Workbook as XLSX – Persisting the Result

Finally, we write the workbook to disk. This satisfies the **save workbook as xlsx** requirement.

```csharp
        // Step 5️⃣: Save the file – you’ll see the comment in B2 when you open it
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Open `output.xlsx` in Excel, hover over cell **B2**, and you’ll see the comment *“Reviewed by QA”* appear. That’s it—no manual steps, no COM interop, just pure C#.

---

## Alternative: How to Add Comment Without Smart Markers

If you prefer a more direct approach, you can create a comment object yourself:

```csharp
// Direct comment creation (no Smart Marker)
Comment comment = ws.Comments[ws.Comments.Add("B2")];
comment.Note = "Directly added comment";
```

This method is handy when the comment text is already known at compile time, or when you need to set additional properties like author, width, or height. However, **generate excel comment** via Smart Markers shines when you have a data‑driven scenario with many rows and columns.

---

## Pro Tips & Common Pitfalls

| Situation | What to Watch For | Recommended Fix |
|-----------|-------------------|-----------------|
| Large datasets (10k+ rows) | Smart Marker processing can be memory‑intensive | Use `SmartMarkerProcessor.Process` overload that streams data, or split the workbook into chunks |
| Need custom author name | Default author is blank | `comment.Author = "MyApp";` after creating the comment |
| Want the comment visible by default | Excel hides comments until hover | Set `comment.Visible = true;` |
| Working with older Excel versions | `.xlsx` may not be supported | Save as `SaveFormat.Xls` instead, but note that some comment features differ |

---

## Expected Output

- **Workbook file:** `output.xlsx` placed in the project’s bin folder.  
- **Cell B2:** Shows the placeholder text `${Comment:UserComment}` (you can hide it by setting the cell’s font color to white).  
- **Comment attached to B2:** Displays “Reviewed by QA” when hovered.

![Create Excel workbook C# example showing comment in cell B2](https://example.com/placeholder-image.png "Create Excel workbook C# example showing comment in cell B2")

*Image alt text:* **Create Excel workbook C# example showing comment in cell B2**

---

## Recap – What We Achieved

We **created an Excel workbook C#**, inserted a **Smart Marker** that turned into an **excel comment**, fed JSON to **generate excel comment**, and finally **saved workbook as xlsx**. The entire flow is encapsulated in a few dozen lines of clean, self‑contained C# code.

---

## What’s Next? Extending the Solution

- **Batch comment generation:** Loop through a DataTable and apply a Smart Marker to each row to add row‑specific notes.  
- **Styling comments:** Adjust font size, color, or even add rich‑text using the `Comment.RichText` collection.  
- **Export to PDF:** Use `workbook.Save("output.pdf", SaveFormat.Pdf);` to share reports with comments intact.  

If you’re curious about **add excel comment** programmatically in other contexts—like using OpenXML SDK or EPPlus—those libraries also support comment creation, though the API surface differs.

---

### Final Thoughts

Adding a comment to an Excel file from C# doesn’t have to be a chore. By leveraging Aspose.Cells’ Smart Marker engine you get a concise, data‑driven way to **add excel comment**, **generate excel comment**, and **save workbook as xlsx** with minimal boilerplate.  

Give it a spin, tweak the JSON, and watch how quickly you can turn raw data into a polished, comment‑rich spreadsheet. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}