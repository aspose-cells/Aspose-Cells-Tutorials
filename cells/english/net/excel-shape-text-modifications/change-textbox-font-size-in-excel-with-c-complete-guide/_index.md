---
category: general
date: 2026-05-30
description: Change textbox font size in Excel using C#. Learn how to modify excel
  textbox font quickly with step‑by‑step code.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: en
og_description: Change textbox font size in Excel using C#. This guide shows how to
  modify excel textbox font safely and efficiently.
og_title: Change Textbox Font Size in Excel with C# – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Change Textbox Font Size in Excel with C# – Complete Guide
url: /net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Change Textbox Font Size in Excel with C# – Complete Guide

Need to **change textbox font size** in an Excel worksheet from C#? You're in the right place. Whether you're generating reports, building a dashboard, or just tweaking a template, adjusting the appearance of a textbox can make your spreadsheet look far more professional.

In this tutorial we’ll also **modify excel textbox font** beyond just the size—think font family, boldness, and even handling multiple shapes. By the end you’ll have a ready‑to‑run snippet that touches every corner of the process, from opening the workbook to cleaning up COM objects. No fluff, just practical code you can drop into your project today.

## Prerequisites — What You’ll Need

Before we dive in, make sure you have the following on your machine:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | Provides the C# compiler and runtime. |
| **Microsoft.Office.Interop.Excel** NuGet package | Gives us the COM interop types needed to talk to Excel. |
| **Excel installed** (any recent version) | The Interop layer works only when the Office app is present. |
| **Basic C# knowledge** | You'll follow along easily, but we’ll explain every line. |

If any of these are missing, pause now and install them; the rest of the guide assumes they’re in place.

## Step 1: Set Up the Project and Import Namespaces

First things first—create a new console app (or integrate into an existing one) and pull in the interop namespace.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro tip:** If you’re targeting .NET 6+, add the `Microsoft.Office.Interop.Excel` package via `dotnet add package Microsoft.Office.Interop.Excel`. This ensures the `Excel` alias resolves correctly.

## Step 2: Open the Workbook and Grab the Target Worksheet

Now we need to launch Excel, open the file, and point to the sheet that holds the textbox. Wrapping this in a `try/finally` block guarantees the COM objects get released even if something goes wrong.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Why this matters

Opening the workbook via COM gives us a live object model—meaning any change we make reflects instantly in the file. Setting `Visible = false` speeds things up and avoids popping windows during automation.

## Step 3: Retrieve the Textbox Shape

Excel treats textboxes as `Shape` objects under the `Shapes` collection, not as a dedicated `TextBox` collection. That’s why the code below looks a bit different from the snippet you may have seen online.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Watch out:** The `Shapes` collection is 1‑based, so we add `+1` to the zero‑based `textboxIndex` you pass in. Forgetting this leads to “index out of range” errors that can be frustrating to debug.

## Step 4: Change Textbox Font Size (and Name)

Here’s where we finally **change textbox font size**. The `TextFrame2` property gives us access to the rich‑text formatting options, which include `Font.Name` and `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Why we use `TextFrame2`

`TextFrame2` is the newer object model introduced with Office 2007. It supports advanced typographic features and is generally more reliable than the older `TextFrame`. Using it ensures our **change textbox font size** operation works across modern Excel versions.

## Step 5: Save, Clean Up, and Verify

After tweaking the font, we need to persist the changes and release every COM reference. Skipping cleanup can leave orphaned Excel processes lingering in the background.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro tip:** If you need to **modify excel textbox font** on many worksheets, wrap the inner logic in a loop that iterates over `Workbook.Worksheets`. Just remember to reset `textboxIndex` for each sheet.

## Handling Edge Cases — Multiple Textboxes and Missing Shapes

Real‑world spreadsheets rarely contain just one textbox. Below are two quick strategies you can adopt without rewriting the whole method.

### 1. Change *all* textboxes on a sheet

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Identify a textbox by its **Name** instead of index

If you gave your textbox a meaningful name (e.g., “TitleBox”), you can fetch it directly:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Both approaches let you **modify excel textbox font** with precision, no matter how the workbook is structured.

## Visual Overview (Optional)

If you prefer a quick visual cue, imagine the following diagram:

![Screenshot showing Excel worksheet with a highlighted textbox – demonstrates how to change textbox font size](change-textbox-font-size.png)

*Alt text:* *change textbox font size in Excel – highlighted textbox ready for font modification.*

## Full Working Example

Putting everything together, here’s a single file you can copy‑paste into a console project and run immediately (just update the file path and sheet name).

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## What Should You Learn Next?

- [Changing Font Size in Excel](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [How to Customize Font Size in Excel Cells Using Aspose.Cells .NET | Complete Guide](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}