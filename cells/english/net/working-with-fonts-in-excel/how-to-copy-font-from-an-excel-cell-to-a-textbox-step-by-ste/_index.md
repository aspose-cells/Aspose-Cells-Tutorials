---
category: general
date: 2026-02-15
description: how to copy font and apply cell style in C# with a simple example. Learn
  how to get cell style and use cell formatting to set textbox font size.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: en
og_description: how to copy font from a worksheet cell and apply cell style to a TextBox.
  This guide shows how to get cell style, use cell formatting, and set textbox font
  size.
og_title: how to copy font from an Excel cell – Complete C# tutorial
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: how to copy font from an Excel cell to a TextBox – Step‑by‑Step Guide
url: /net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to copy font from an Excel cell to a TextBox – Complete C# Tutorial

Ever needed to **copy font** from a spreadsheet cell and make a UI text box look exactly the same? You're not the only one. In many reporting tools or custom dashboards you’ll find yourself pulling data from Excel and then trying to keep the visual fidelity—font family, size, and colour—intact.  

The good news is that with just a few lines of C# you can **get cell style**, read its font properties, and **apply cell style** to any text‑box control. In this tutorial we’ll walk through a complete, runnable example that shows how to **use cell formatting** and even **set textbox font size** programmatically.

---

## What You’ll Learn

- How to retrieve a `TextBox` object from a grid component (`gridJs` in our sample)
- How to read the font family, size, and colour from a specific Excel cell (`B2`)
- How to copy those font attributes to the text box so the UI mirrors the spreadsheet
- Common pitfalls (e.g., colour conversion) and a few **pro tips** to keep your code robust
- A ready‑to‑run code snippet that you can drop into a console app or WinForms project

**Prerequisites**  
You should have:

1. .NET 6+ (or .NET Framework 4.8) installed  
2. The EPPlus NuGet package (for Excel handling)  
3. A grid control that exposes a `TextBoxes` dictionary (the example uses a fictional `gridJs` but the idea works with any UI library)

Now, let’s get our hands dirty.

---

## Step 1: Set Up the Project and Load the Worksheet

First, create a new console or WinForms project and add EPPlus:

```bash
dotnet add package EPPlus --version 6.*
```

Then, load the workbook and grab the cell whose style you want to copy.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Why this matters:** EPPlus gives you direct access to the `Style` object, which contains the `Font` sub‑object. From there you can read `Name`, `Size`, and `Color`. This is the core of the **get cell style** operation.

---

## Step 2: Grab the Target TextBox from Your Grid

Assuming your UI grid (`gridJs`) stores text boxes in a dictionary keyed by column name, you can retrieve the one you want like so:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

If you’re using WinForms, `notesTextBox` could be a `TextBox` control; for WPF it might be a `TextBox` element, and for a web‑based grid it could be a JavaScript interop object. The key point is that you have a reference you can manipulate.

---

## Step 3: Transfer the Font Family

Now that we have both the source style and the destination control, copy the font family.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro tip:** Not all UI frameworks expose a `FontFamily` property that accepts a plain string. In WinForms you’d set `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`. Adjust accordingly.

---

## Step 4: Transfer the Font Size

Font size is stored as a `float` in EPPlus. Apply it directly:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

If your control uses points (which most do), you can assign the value without conversion. For CSS‑based grids you might need to append `"pt"`.

---

## Step 5: Transfer the Font Colour

Colour conversion is the trickiest part because EPPlus stores colours as ARGB integers, while many UI frameworks expect a `System.Drawing.Color` or a CSS hex string.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Why this works:** `GetColor()` resolves theme‑based colours and returns a concrete `System.Drawing.Color`. If the cell uses the default colour (no explicit setting), we default to black to avoid null reference exceptions.

---

## Full Working Example

Putting everything together, here’s a minimal console app that reads an Excel file, extracts the font from **B2**, and applies it to a mock text box.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Expected output (assuming B2 uses Arial, 12 pt, blue):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Run the program, open your UI, and you’ll see the “Notes” text box now mirrors the exact font styling of cell **B2**. No manual tweaking required.

---

## Frequently Asked Questions & Edge Cases

### What if the cell uses a theme colour instead of an explicit RGB value?

EPPlus’s `GetColor()` automatically resolves theme colours to a concrete `System.Drawing.Color`. However, if you’re using an older library that only returns the theme index, you’ll need to map that index to a colour palette yourself.

### Can I copy other style attributes (e.g., bold, italic)?

Absolutely. The `ExcelStyle.Font` object also exposes `Bold`, `Italic`, `Underline`, and `Strike`. Just set the corresponding properties on your UI control:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### What if the grid control doesn’t expose a `FontColor` property?

Most modern UI frameworks do, but if yours only accepts a CSS string, convert the `Color` to hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### How do I handle multiple cells at once?

Loop over the desired range, fetch each cell’s style, and apply it to the corresponding text box. Remember to cache the style objects if you’re processing many rows to avoid performance hits.

---

## Pro Tips & Common Pitfalls

- **Cache the ExcelPackage** – opening and closing the file for each cell is expensive. Load the workbook once, then reuse the `ExcelWorksheet` object.
- **Watch out for null colours** – a cell that inherits the default colour returns `null`. Always provide a fallback (black or the control’s default).
- **Mind DPI scaling** – if you’re targeting high‑DPI monitors, font sizes may appear slightly larger. Adjust using `Graphics.DpiX` if needed.
- **Thread safety** – EPPlus isn’t thread‑safe. If you’re processing many sheets in parallel, create a separate `ExcelPackage` per thread.

---

## Conclusion

You now know **how to copy font** from an Excel cell and **apply cell style** to any text‑box control using C#. By retrieving the cell’s `Style`, extracting its `Font` properties, and assigning them to the UI element, you preserve visual consistency without manual copying.  

The complete solution—loading the workbook, getting the cell style, and setting the textbox’s font family, size, and colour—covers the core of **use cell formatting** and demonstrates how to **set textbox font size** correctly.  

Next, try extending the example to copy background colours, borders, or even entire cell contents. If you’re working with a data‑grid library that supports rich cell rendering, you can now feed it the exact same styling information you pulled from Excel, keeping your UI and reports perfectly in sync.

Got more questions? Drop a comment or explore related topics such as “dynamic Excel‑to‑UI binding” and “theme‑aware colour conversion”. Happy coding!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}