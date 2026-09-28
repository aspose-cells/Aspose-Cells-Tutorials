---
category: general
date: 2026-09-27
description: Learn how to add comment to Excel with C# by processing a smart marker.
  Complete guide includes setup, code, and verification.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add comment to excel
- Aspose.Cells
- C# Excel automation
- smart marker processor
- Excel comment object
- worksheet comment
language: en
lastmod: 2026-09-27
og_description: Add comment to Excel in C# quickly. This tutorial shows how to use
  Aspose.Cells smart markers to insert comments programmatically.
og_image_alt: Screenshot of an Excel cell showing a comment added by code – add comment
  to excel example
og_title: Add comment to Excel with Aspose.Cells smart markers – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to add comment to Excel with C# by processing a smart marker.
    Complete guide includes setup, code, and verification.
  headline: How to add comment to Excel using Aspose.Cells smart markers
  type: TechArticle
- description: Learn how to add comment to Excel with C# by processing a smart marker.
    Complete guide includes setup, code, and verification.
  name: How to add comment to Excel using Aspose.Cells smart markers
  steps:
  - name: Place a `${Cell:Comment=Property}` marker in the worksheet.
    text: Place a `${Cell:Comment=Property}` marker in the worksheet.
  - name: Provide a data object that contains the comment text.
    text: Provide a data object that contains the comment text.
  - name: Call `SmartMarkerProcessor.Process` to replace the marker with a real Excel
      comment.
    text: Call `SmartMarkerProcessor.Process` to replace the marker with a real Excel
      comment.
  - name: Save and verify the workbook.
    text: Save and verify the workbook.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: How to add comment to Excel using Aspose.Cells smart markers
url: /net/excel-comment-annotation/how-to-add-comment-to-excel-using-aspose-cells-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to add comment to Excel using Aspose.Cells smart markers

If you need to **add comment to Excel** programmatically, this guide shows a concise, production‑ready way using Aspose.Cells smart markers. Whether you generate reports, annotate data, or build an audit trail, you’ll see exactly how to inject a comment into a cell without manual editing.

The tutorial covers everything you need: creating a workbook, preparing the data object, processing the smart marker, and verifying the result. No external documentation is required—just copy, paste, and run.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the example uses C# 10 syntax)
* Aspose.Cells for .NET 23.12 or newer – install via NuGet: `Install-Package Aspose.Cells`
* A development environment such as Visual Studio 2022 or VS Code

These requirements ensure the **C# Excel automation** code runs without compatibility issues.

## Step 1: Set up the workbook and worksheet

First, create a new workbook and add a worksheet that will hold the smart marker. The worksheet name is arbitrary; we’ll use `"Data"` for clarity.

```csharp
using Aspose.Cells;
using System;

class AddCommentDemo
{
    static void Main()
    {
        // Create a new workbook
        var workbook = new Workbook();

        // Access the first worksheet and rename it
        var ws = workbook.Worksheets[0];
        ws.Name = "Data";

        // Place a placeholder smart marker in cell A1
        ws.Cells["A1"].PutValue("${A1:Comment=Note}");

        // Continue with data preparation...
```

**Why this step matters:**  
The **Excel comment object** is not created directly; instead, a smart marker tells Aspose.Cells where to insert the comment when processing the data object. By writing the marker `${A1:Comment=Note}` into `A1`, we define the target cell and the comment type (`Comment`) linked to the property `Note`.

## Step 2: Prepare the data object containing the comment text

The smart marker processor reads properties from a plain .NET object. Here we create an anonymous object with a single property `Note` that holds the comment text.

```csharp
        // Step 2: Prepare the data object containing the comment text
        var commentData = new { Note = "Reviewed on " + DateTime.Today.ToString("d") };
```

**Why this matters:**  
The **smart marker processor** maps the `Note` property to the `${A1:Comment=Note}` placeholder. You can extend the object with additional fields for other markers, making the solution scalable for complex worksheets.

## Step 3: Process the smart marker to insert the comment

Now invoke `SmartMarkerProcessor.Process` to replace the placeholder with an actual comment in the worksheet.

```csharp
        // Step 3: Process the smart marker, inserting the comment from the data object
        ws.SmartMarkerProcessor.Process("${A1:Comment=Note}", commentData);
```

**Explanation:**  
* `ws.SmartMarkerProcessor` is part of **Aspose.Cells** and knows how to interpret the `${...}` syntax.  
* The `Comment` keyword tells the library to create an Excel comment attached to cell `A1`.  
* The value of `Note` becomes the comment’s text.

### Pro tip
If you need to add a comment to multiple cells, place additional smart markers (e.g., `${B2:Comment=Note}`) and reuse the same data object or a collection of objects. The processor will handle each marker independently.

## Step 4: Save the workbook and verify the comment

Finally, write the workbook to a file and open it in Excel to confirm that the comment appears.

```csharp
        // Step 4: Save the workbook
        string outputPath = "AddCommentResult.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the comment.");

        // Optional: programmatically verify the comment (useful for unit tests)
        var comment = ws.Comments[0]; // first comment in the worksheet
        Console.WriteLine($"Comment text in A1: {comment.Note}");
    }
}
```

When you open **AddCommentResult.xlsx**, hover over cell A1 and you’ll see the comment “Reviewed on MM/DD/YYYY”. The console output also prints the comment text, proving that the insertion succeeded without manual inspection.

## Handling edge cases and variations

| Situation | Recommended approach |
|-----------|----------------------|
| **Empty or null comment text** | Provide a default value: `var commentData = new { Note = string.IsNullOrEmpty(input) ? "No comment" : input };` |
| **Multiple rows with different comments** | Use a collection of objects and a range smart marker, e.g., `${A2:A10:Comment=Note}` with a list of data objects. |
| **Styling the comment** | After processing, iterate `ws.Comments` and adjust `comment.Font` or `comment.Color` as needed. |
| **Large worksheets** | Process smart markers once per worksheet to avoid performance penalties; reuse the same `SmartMarkerProcessor` instance. |

These variations ensure your **add comment to Excel** solution remains robust across real‑world scenarios.

## Complete, runnable example

Below is the full program you can copy into a new console project. It includes all necessary `using` directives and saves the output file in the project’s root folder.

```csharp
using Aspose.Cells;
using System;

class AddCommentDemo
{
    static void Main()
    {
        // 1️⃣ Create a workbook and worksheet
        var workbook = new Workbook();
        var ws = workbook.Worksheets[0];
        ws.Name = "Data";

        // Insert the smart marker placeholder into A1
        ws.Cells["A1"].PutValue("${A1:Comment=Note}");

        // 2️⃣ Prepare the data object with the comment text
        var commentData = new { Note = "Reviewed on " + DateTime.Today.ToString("d") };

        // 3️⃣ Process the smart marker to add the comment
        ws.SmartMarkerProcessor.Process("${A1:Comment=Note}", commentData);

        // 4️⃣ Save the workbook
        const string outputPath = "AddCommentResult.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}.");

        // Verify programmatically (optional)
        var comment = ws.Comments[0];
        Console.WriteLine($"Comment in A1: {comment.Note}");
    }
}
```

**Expected output**

```
Workbook saved to AddCommentResult.xlsx.
Comment in A1: Reviewed on 9/27/2026
```

Opening the generated file shows a comment attached to cell A1 with the same text.

## Conclusion

You now know how to **add comment to Excel** using Aspose.Cells smart markers in C#. The process is straightforward:

1. Place a `${Cell:Comment=Property}` marker in the worksheet.  
2. Provide a data object that contains the comment text.  
3. Call `SmartMarkerProcessor.Process` to replace the marker with a real Excel comment.  
4. Save and verify the workbook.

From here you can expand the technique to batch‑process multiple rows, apply styling, or integrate the workflow into larger reporting pipelines. Happy coding, and enjoy the power of **C# Excel automation** with Aspose.Cells!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Add Comment Excel – How to Populate an Excel Template with Smart Markers in](/cells/english/net/excel-comment-annotation/add-comment-excel-how-to-populate-an-excel-template-with-sma/)
- [Add Image to Excel Comment with Aspose.Cells for Java: A Complete Guide](/cells/english/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)
- [Comment automatiser les Smart Markers Excel avec Aspose.Cells pour Java](/cells/french/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}