---
category: general
date: 2026-05-23
description: Create excel workbook in C# and learn how to apply custom number format,
  set cell style programmatically, format cell scientific notation, then save workbook
  to xlsx.
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: en
og_description: Create excel workbook in C# quickly. Learn to apply custom number
  format, style cells programmatically, format scientific notation, and save to xlsx.
og_title: Create Excel Workbook in C# – Apply Custom Number Format
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Create Excel Workbook in C# – Apply Custom Number Format
url: /net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook in C# – Apply Custom Number Format

Create excel workbook in C# is easier than you might think. In this guide we’ll walk you through applying a custom number format, formatting a cell in scientific notation, setting the cell style programmatically, and finally saving the workbook to an xlsx file.

If you’ve ever stared at a blank spreadsheet and wondered how to automate the whole thing—from populating data to making numbers look exactly the way you need—this tutorial is for you. By the end you’ll have a fully‑functional Excel file that you can open in any spreadsheet program, and you’ll understand **why** each step matters, not just **how** to type the code.

## What You’ll Need

- **.NET 6+** (or any recent .NET Framework that supports the library)  
- **Aspose.Cells for .NET** (or another API that exposes `Workbook`, `Cell`, and `CellFormat` classes)  
- A modest amount of C# experience – if you can write a `Console.WriteLine`, you’re good to go.  

No extra configuration files, no COM interop, and certainly no manual Excel installation required.

---

## Create Excel Workbook – Initialize the Workbook Object

The first thing we have to do is spin up an empty workbook. Think of the `Workbook` class as the blank canvas on which you’ll paint rows, columns, and styles.

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

That’s it—one line and you have a brand‑new Excel file in memory. The `Workbook` constructor creates the default worksheet collection, so you can start adding data right away.

> **Pro tip:** If you need multiple sheets, you can call `workbook.Worksheets.Add()` before you start filling cells.

![Create excel workbook example](image-placeholder.png "Create excel workbook screenshot")

*Image alt text: create excel workbook example showing a blank Excel sheet in the IDE.*

## Apply Custom Number Format to a Cell

Now that the workbook exists, let’s put a number into cell **A1** and give it a custom format. Custom number formats let you control how numbers appear—currency, percentages, dates, or, in our case, scientific notation.

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

Why pull the style first? Because the `Cell` object stores a **Style** object that contains fonts, borders, alignment, and number formatting all in one place. By editing the `Custom` property we tell Excel, “show this value using scientific notation with two decimals.”

> **Common question:** *Can I use a built‑in format instead of a custom one?*  
> Yes—set `style.Number = 10` for a built‑in scientific format, but the custom string gives you precise control over decimal places.

## Set Cell Style Programmatically (Beyond Number Format)

Often you’ll want more than just a number format. Let’s add a bold font and a light gray background to make the cell stand out.

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

Notice we reuse the same `style` object we tweaked earlier. That’s the beauty of **set cell style programmatically**—you only fetch the style once, modify whatever properties you need, and write it back. No need to recreate objects or lose the number format you already set.

## Format Cell Scientific Notation (Edge‑Case Handling)

If you’re dealing with very large or very small numbers, scientific notation is a lifesaver. The custom format we used (`0.00E+00`) guarantees two digits after the decimal point and forces a plus sign for the exponent. Here’s a quick sanity check:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

When you open the resulting file, B2 will appear as `1.23E-05`, confirming the **format cell scientific notation** directive works for both large and tiny numbers.

## Save Workbook to XLSX

All the fun stops when you actually write the file to disk. The `Save` method handles the heavy lifting, converting the in‑memory representation into a proper `.xlsx` package.

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

That line accomplishes the **save workbook to xlsx** goal. If the directory doesn’t exist, `Save` will throw an exception—so make sure the folder is created beforehand or wrap the call in a try/catch block.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

Now you have a ready‑to‑share Excel file with a nicely formatted scientific number, bold styling, and a light gray background.

## Full Working Example

Below is the complete, copy‑paste‑ready program that ties every piece together. It compiles as a console app, but you can drop the logic into any C# project.

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Expected outcome:** Open `CustomFormatted.xlsx` and you’ll see:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

Both cells are bold, have a light gray fill, and display numbers in scientific notation with two decimal places.

---

## Wrap‑Up

We’ve just **create excel workbook** from scratch, **apply custom number format**, **format cell scientific notation**, **set cell style programmatically**, and **save workbook to xlsx**—all in a handful of lines of C#. The approach scales: just loop over rows, clone the `style` object, and you’ll have a fully‑styled report in seconds.

### What’s Next?

- **Dynamic formatting:** Switch formats based on value magnitude (e.g., currency vs. percentage).  
- **Multiple sheets:** Use `workbook.Worksheets.Add("Summary")` to build dashboards.  
- **Advanced styling:** Borders, conditional formatting, and data validation


## Related Tutorials

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}