---
category: general
date: 2026-02-21
description: Create cell style in C# quickly. Learn how to apply style to a cell,
  center text in cell, set cell alignment, and master cell formatting.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: en
og_description: Create cell style in C# and learn how to apply style to a cell, center
  text in cell, and set cell alignment with a clear, step‑by‑step guide.
og_title: Create cell style in C# – Apply style to a cell and center text
tags:
- C#
- Aspose.Cells
- Excel automation
title: Create cell style in C# – How to apply style to a cell and center text
url: /net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create cell style in C# – Complete Guide to Applying Styles and Centering Text

Ever needed to **create cell style** in an Excel worksheet but weren’t sure where to start? You’re not alone. In many automation projects, the ability to **apply style to cell** objects is the difference between a bland spreadsheet and a polished report.  

In this tutorial we’ll walk through a full, runnable example that shows you **how to center text** inside a cell, set the alignment, and add a thin border—all in just a few lines of C#. By the end you’ll know exactly why each piece matters and how to tweak it for your own scenarios.

## What You’ll Walk Away With

- A clear understanding of the **create cell style** workflow using Aspose.Cells (or any similar library).
- The exact code you can copy‑paste into a console app to **apply style to cell**.
- Insight into **center text in cell**, **set cell alignment**, and handle edge cases like merged cells or custom number formats.
- Tips for extending the style—different fonts, background colors, or conditional formatting.

> **Prerequisite:** Visual Studio 2022 (or any C# IDE) and the Aspose.Cells for .NET NuGet package. No other dependencies are required.

---

## Step 1: Set Up Your Project and Import Namespaces

Before we can **create cell style**, we need a project that references the Excel library.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Why this matters:* Importing `Aspose.Cells` gives us access to the `Workbook`, `Worksheet`, `Style`, and `Border` classes. If you’re using a different library (e.g., EPPlus), the class names change but the concept stays the same.

---

## Step 2: Create a Workbook and Grab the First Cell

Now we **create cell style** by first getting a reference to the cell we want to format.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Notice we used `Cell` instead of the generic `var`—explicit typing makes the code clearer for newcomers. The call to `PutValue` writes a string so we can see the style effect later.

---

## Step 3: Define the Style – Center Text, Add a Thin Border

Here’s the heart of the **create cell style** operation. We’ll set horizontal alignment, a thin border, and a few optional niceties.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Why we do this:*  
- **HorizontalAlignment** and **VerticalAlignment** together answer the “**how to center text** in a cell?” question.  
- Adding all four borders ensures the cell looks like a boxed label, which is useful for headers.  
- The background color isn’t required, but it demonstrates how you can extend the style later.

---

## Step 4: Apply the Defined Style to the Selected Cell

Now that the style exists, we **apply style to cell** with a single method call.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

That’s it—Aspose.Cells takes care of copying the style into the cell’s internal style collection. If you need the same formatting on a range, you can use `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`.

---

## Step 5: Save the Workbook and Verify the Result

A quick save lets you open the file in Excel and confirm that the text is truly centered and the border appears.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Expected output:* When you open **StyledCell.xlsx**, cell **A1** contains “Hello, styled world!” centered both horizontally and vertically, surrounded by a thin gray border, and set against a light‑gray background.

---

## Common Variations & Edge Cases

### 1. Center Text in a Merged Region

If you merge cells **A1:C1** and still want the text centered, you must apply the style to the top‑left cell **after** merging:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Using a Numeric Format

Sometimes you need to **set cell alignment** *and* display numbers with a specific format:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

The alignment stays centered while the number appears as `12,345.68`.

### 3. Reusing Styles Efficiently

Creating a new `Style` for every cell can hurt performance. Instead, create one style object and reuse it across many cells or ranges. The `StyleFlag` class lets you apply only the parts you care about, saving memory.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro Tips & Pitfalls to Watch

- **Don’t forget vertical alignment** – centering only horizontally often looks off, especially with taller rows.
- **Border types**: `CellBorderType.Thin` works for most reports, but you can switch to `Medium` or `Dashed` for visual hierarchy.
- **Color handling**: When targeting .NET Core, use `System.Drawing.Color` from the `System.Drawing.Common` package; otherwise you’ll hit a runtime error.
- **Saving format**: If you need compatibility with older Excel versions, change `SaveFormat.Xlsx` to `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt text: screenshot showing a cell with centered text and thin border created by the create cell style tutorial.*

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Run this program, open **StyledCell.xlsx**, and you’ll see the exact result described earlier. Feel free to change the text, border style, or background color to match your branding.

---

## Conclusion

We’ve just **created cell style** from scratch, **applied style to cell**, and demonstrated **how to center text** both horizontally and vertically. By mastering these building blocks you can now format headers, highlight totals, or build entire report templates without ever leaving C#.  

If you’re curious about the next steps, try:

- **Applying the same style to a whole row** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Adding conditional formatting** to change the background based on cell values.
- **Exporting to PDF** while preserving the style.

Remember, styling is just as much about readability as it is about aesthetics. Experiment, iterate, and soon your spreadsheets will look as professional as your code.

*Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}