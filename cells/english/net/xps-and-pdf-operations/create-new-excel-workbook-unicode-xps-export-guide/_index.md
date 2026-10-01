---
category: general
date: 2026-05-30
description: Create new excel workbook and learn how to write unicode in excel, export
  excel to xps, and write special character in excel using Aspose.Cells.
draft: false
keywords:
- create new excel workbook
- how to write unicode in excel
- export excel to xps
- write special character in excel
language: en
og_description: Create new excel workbook, write unicode in excel, and export excel
  to xps with a complete, step‑by‑step tutorial.
og_title: Create New Excel Workbook – Unicode & XPS Export
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Create new excel workbook and learn how to write unicode in excel,
    export excel to xps, and write special character in excel using Aspose.Cells.
  headline: Create New Excel Workbook – Unicode & XPS Export Guide
  type: TechArticle
- description: Create new excel workbook and learn how to write unicode in excel,
    export excel to xps, and write special character in excel using Aspose.Cells.
  name: Create New Excel Workbook – Unicode & XPS Export Guide
  steps:
  - name: Edge Cases & Tips
    text: '| Situation | How to Handle | |-----------|----------------| | The target
      font doesn’t support the variation selector | Set the cell style to a font that
      does (e.g., “Noto Sans CJK”). | | You need to write multiple Unicode strings
      quickly | Loop through an array of strings and call `PutValue` inside'
  - name: Verifying the Result
    text: "Open the generated `UnicodeDemo.out.xps` with Windows XPS Viewer. You should
      see the cell **A1** displaying the kanji **\U00020BB7** with the variant glyph
      (if your system font supports it). If the character looks like a box, double‑check
      that the font used in the worksheet supports the variation selector."
  - name: Expected Output
    text: 'When you run the program, the console prints something like:'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells writes the underlying file in the OpenXML format (`.xlsx`),
      which Excel 2007+ can read. The XPS export is independent of the Excel version.
    question: Does this work with older versions of Excel?
  - answer: "Emojis are also Unicode code points. Use the same `PutValue` method,
      e.g., `sheet.Cells[\"B2\"].PutValue(\"\U0001F600\")` for a grinning face."
    question: What if I need to write emojis?
  - answer: You can adjust the worksheet’s `PageSetup` properties before saving, such
      as `sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;`.
    question: Can I set the XPS page size?
  - answer: 'Minimal. Aspose.Cells processes strings efficiently, but if you’re handling
      millions of cells, consider batching writes or using `Cells.ImportDataTable`.
      ## Pro Tips for a Smooth Experience - **Font Embedding:** When you need the
      XPS to look identical on any machine, embed the font into the workbook'
    question: Is there a performance impact when writing many Unicode cells?
  type: FAQPage
tags:
- excel
- aspnet
- unicode
- xps
title: Create New Excel Workbook – Unicode & XPS Export Guide
url: /net/xps-and-pdf-operations/create-new-excel-workbook-unicode-xps-export-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Excel Workbook – Unicode & XPS Export Guide

Ever wondered how to **create new excel workbook** that can handle fancy characters and still be printable as an XPS file? You're not the only one. Many developers hit a wall when they need to store a Unicode glyph—like a Japanese kanji with a variation selector—inside an Excel cell, then ship it off as a high‑fidelity XPS document.  

In this tutorial we’ll walk through exactly that: we’ll **create new excel workbook**, show you **how to write unicode in excel**, demonstrate **export excel to xps**, and even cover the quirks of **write special character in excel**. By the end you’ll have a ready‑to‑run code sample, a clear understanding of why each step matters, and a few pro tips to keep you from common pitfalls.

## Prerequisites

- .NET 6.0 or later (the code works with .NET Framework 4.6+ as well)
- Aspose.Cells for .NET (free trial or licensed version)
- A simple IDE like Visual Studio or VS Code
- Basic C# knowledge—nothing fancy, just the usual `using` statements

If you already have these, great—let’s dive in.

## Step 1: Create New Excel Workbook with Aspose.Cells

The first thing you need is a fresh workbook object. Think of it as a blank canvas where every sheet, cell, and style lives.

```csharp
using Aspose.Cells;

namespace ExcelUnicodeDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // The workbook now contains one default worksheet (index 0)
            // You can add more sheets later if needed
        }
    }
}
```

> **Why this matters:** Instantiating `Workbook` automatically adds a default worksheet, which saves you a line of code later. This is the foundation for **create new excel workbook** operations—without it, nothing else can happen.

## Step 2: Access the First Worksheet

Once the workbook exists, you need a reference to a sheet where you’ll drop your Unicode text.

```csharp
// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

> **Pro tip:** If you plan to generate multiple sheets, use `workbook.Worksheets.Add("MySheet")` and keep track of the index or name. For a simple demo, the default sheet is perfectly fine.

## Step 3: How to Write Unicode in Excel Cells

Now comes the fun part—writing a special character. In this example we’ll insert the character `𠮷` followed by a variation selector `U+FE00`. This combination is often used to request a specific glyph variant.

```csharp
// Step 3: Write a character that includes a variation selector into cell A1
// The string literal uses an escaped Unicode sequence for the variation selector
sheet.Cells["A1"].PutValue("𠮷\uFE00");

// Optional: Adjust the column width so the character isn’t cut off
sheet.AutoFitColumn(0);
```

> **What’s happening?**  
> - `"𠮷"` is a Unicode code point outside the BMP (Basic Multilingual Plane), so it’s represented as a surrogate pair in UTF‑16.  
> - `\uFE00` is the variation selector‑1. When combined, many fonts display a slightly different glyph.  
> - `PutValue` automatically detects the string type and stores it as a Unicode cell value, which satisfies the **write special character in excel** requirement.

### Edge Cases & Tips

| Situation | How to Handle |
|-----------|----------------|
| The target font doesn’t support the variation selector | Set the cell style to a font that does (e.g., “Noto Sans CJK”). |
| You need to write multiple Unicode strings quickly | Loop through an array of strings and call `PutValue` inside the loop. |
| Excel shows � (replacement char) | Verify the file is saved with UTF‑8 encoding (Aspose.Cells does this automatically). |

## Step 4: Export Excel to XPS – The Final Destination

With the Unicode character safely stored, the last piece is to generate an XPS document. XPS preserves layout, fonts, and vector graphics, making it ideal for printing or archival.

```csharp
// Step 4: Save the workbook as an XPS document
string outputPath = @"C:\Temp\UnicodeDemo.out.xps";
workbook.Save(outputPath, SaveFormat.Xps);

// Inform the user
Console.WriteLine($"Workbook exported to XPS at: {outputPath}");
```

> **Why export to XPS?** The `SaveFormat.Xps` option creates a fixed‑layout file that mirrors the on‑screen view of the workbook. This is especially useful when you need to share a read‑only version that maintains exact formatting—perfect for reports, invoices, or legal documents.

### Verifying the Result

Open the generated `UnicodeDemo.out.xps` with Windows XPS Viewer. You should see the cell **A1** displaying the kanji **𠮷** with the variant glyph (if your system font supports it). If the character looks like a box, double‑check that the font used in the worksheet supports the variation selector.

## Full Working Example

Here’s the entire program in one place—copy, paste, and run.

```csharp
using System;
using Aspose.Cells;

namespace ExcelUnicodeDemo
{
    class Program
    {
        static void Main()
        {
            // Create a new workbook (primary step for create new excel workbook)
            Workbook workbook = new Workbook();

            // Access the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // Write a Unicode character with a variation selector into cell A1
            // This demonstrates how to write unicode in excel
            sheet.Cells["A1"].PutValue("𠮷\uFE00");
            sheet.AutoFitColumn(0); // Ensure the column is wide enough

            // Save as XPS (export excel to xps)
            string outputPath = @"C:\Temp\UnicodeDemo.out.xps";
            workbook.Save(outputPath, SaveFormat.Xps);

            Console.WriteLine($"Workbook exported to XPS at: {outputPath}");
            Console.WriteLine("Done! Check the XPS file to see the special character.");
        }
    }
}
```

### Expected Output

When you run the program, the console prints something like:

```
Workbook exported to XPS at: C:\Temp\UnicodeDemo.out.xps
Done! Check the XPS file to see the special character.
```

Opening the XPS file shows **A1** containing the special character **𠮷** with its variation selector applied.

## Common Questions & Gotchas

**Q: Does this work with older versions of Excel?**  
A: Yes. Aspose.Cells writes the underlying file in the OpenXML format (`.xlsx`), which Excel 2007+ can read. The XPS export is independent of the Excel version.

**Q: What if I need to write emojis?**  
A: Emojis are also Unicode code points. Use the same `PutValue` method, e.g., `sheet.Cells["B2"].PutValue("\U0001F600")` for a grinning face.

**Q: Can I set the XPS page size?**  
A: You can adjust the worksheet’s `PageSetup` properties before saving, such as `sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;`.

**Q: Is there a performance impact when writing many Unicode cells?**  
A: Minimal. Aspose.Cells processes strings efficiently, but if you’re handling millions of cells, consider batching writes or using `Cells.ImportDataTable`.

## Pro Tips for a Smooth Experience

- **Font Embedding:** When you need the XPS to look identical on any machine, embed the font into the workbook (`workbook.Fonts.AddFont("path/to/font.ttf")`).  
- **Memory Management:** For large workbooks, wrap the `Workbook` in a `using` block or call `workbook.Dispose()` after saving to release unmanaged resources.  
- **Testing Unicode:** Use an online Unicode explorer to copy‑paste characters; this avoids typing errors with surrogate pairs.  
- **Error Handling:** Wrap the save call in a try‑catch to gracefully handle I/O issues (`DirectoryNotFoundException`, `UnauthorizedAccessException`).

## Conclusion

We’ve covered everything you need to **create new excel workbook**, **how to write unicode in excel**, **export excel to xps**, and **write special character in excel** using Aspose.Cells. The step‑by‑step code shows the complete flow—from initializing the workbook, inserting a Unicode glyph with a variation selector, to producing a faithful XPS snapshot.  

Now you can adapt this pattern to generate multilingual reports, preserve exact layout for archiving, or simply impress your teammates with clean Unicode handling. Want to go further? Try adding images, styling cells with rich fonts, or generating multiple worksheets in a single XPS file. The sky’s the limit.

Got a question or a cool use case? Drop a comment below, and happy coding!

![Screenshot of the XPS output showing the special Unicode character – create new excel workbook](/images/xps-unicode-output.png)


## What Should You Learn Next?

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}