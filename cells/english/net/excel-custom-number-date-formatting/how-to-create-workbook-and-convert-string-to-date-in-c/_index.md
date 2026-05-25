---
category: general
date: 2026-02-15
description: How to create workbook, convert string to date, and format cell as date
  with Aspose.Cells. Learn to set cell number format and read Excel date easily.
draft: false
keywords:
- how to create workbook
- convert string to date
- format cell as date
- set cell number format
- read excel date
language: en
og_description: How to create workbook, convert string to date, and format the cell
  as a date. Complete step‑by‑step guide for reading Excel dates.
og_title: How to create workbook and convert string to date in C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: How to create workbook and convert string to date in C#
url: /net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create workbook and convert string to date in C#

Ever wondered **how to create workbook** that turns a plain text like `"R3-04-01"` into a real `DateTime` value? You're not the only one—many developers hit this snag when pulling data from legacy systems or user input. The good news? With a few lines of C# and Aspose.Cells you can do it in a snap, no manual parsing required.

In this tutorial we’ll walk through the entire process: creating a workbook, inserting a date string, applying a proper **format cell as date**, forcing the engine to **set cell number format**, and finally **read excel date** back as a `DateTime`. By the end you’ll have a runnable snippet you can drop into any .NET project.

## Prerequisites

- .NET 6+ (or .NET Framework 4.7.2+)
- **Aspose.Cells for .NET** NuGet package (`Install-Package Aspose.Cells`)
- A basic understanding of C# syntax
- An IDE like Visual Studio or VS Code (any will do)

No extra configuration is needed—Aspose.Cells handles all the heavy lifting internally.

## Step 1: How to create workbook – initialize the Excel file

First, we need a fresh workbook object. Think of it as a blank notebook where each worksheet is a page.

```csharp
using Aspose.Cells;

 // Step 1: Create a new workbook
 var workbook = new Workbook();          // Empty workbook with one default sheet
```

*Why this matters:* Creating the workbook gives us a container for cells, styles, and formulas. Without it, there’s nowhere to put the date string.

## Step 2: Convert string to date – insert the raw text

Now we drop the raw date string into cell **A1** of the first worksheet. The string uses a custom format (`R3-04-01`) that Excel doesn’t recognize out‑of‑the‑box.

```csharp
 // Step 2: Insert a date string into cell A1 of the first worksheet
 var targetCell = workbook.Worksheets[0].Cells["A1"];
 targetCell.PutValue("R3-04-01");        // Raw text, not yet a date
```

*Why we do this:* `PutValue` stores the literal text. If we tried to set a `DateTime` directly, the custom format would be lost. Keeping it as text lets us later apply a **set cell number format** that tells Excel how to interpret it.

## Step 3: Format cell as date – apply style number 14

Excel’s built‑in date style 14 corresponds to `mm-dd-yy`. By assigning this style we tell the engine, “Treat the content of this cell as a date.”

```csharp
 // Step 3: Apply a date number format (style number 14) to the cell
 targetCell.SetStyle(new Style { Number = 14 });
```

*What happens under the hood:* The `Number` property maps to Excel’s internal number‑format IDs. When the workbook recalculates, Excel will try to coerce the text into a serial date using the supplied format.

## Step 4: Set cell number format – force recalculation

Excel won’t magically convert the text until we ask it to evaluate formulas (or, in this case, re‑interpret the cell). Calling `CalculateFormula` triggers that conversion.

```csharp
 // Step 4: Recalculate any formulas so the cell value is interpreted as a date
 workbook.CalculateFormula();
```

*Tip:* If you’re working with many cells, you can call `CalculateFormula` once after you finish all formatting—this saves a few milliseconds.

## Step 5: Read Excel date – get the DateTime value

Finally, we pull the `DateTime` representation out of the cell. Aspose.Cells exposes it via `DateTimeValue`.

```csharp
 // Step 5: Retrieve the DateTime representation and display it
 Console.WriteLine(targetCell.DateTimeValue);
```

**Expected output (assuming the default Gregorian calendar):**

```
2023-04-01 00:00:00
```

Notice how the `"R3-"` prefix is ignored because Excel’s date parser focuses on the numeric portion when the style is a date. If your strings contain other prefixes, you might need to preprocess them, but for many legacy formats this approach works perfectly.

## Full Working Example

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook
        var workbook = new Workbook();

        // Step 2: Insert a date string into cell A1 of the first worksheet
        var targetCell = workbook.Worksheets[0].Cells["A1"];
        targetCell.PutValue("R3-04-01");

        // Step 3: Apply a date number format (style number 14) to the cell
        targetCell.SetStyle(new Style { Number = 14 });

        // Step 4: Recalculate any formulas so the cell value is interpreted as a date
        workbook.CalculateFormula();

        // Step 5: Retrieve the DateTime representation and display it
        Console.WriteLine(targetCell.DateTimeValue);
    }
}
```

Save this as `Program.cs`, restore the Aspose.Cells package, and run `dotnet run`. You should see the formatted `DateTime` printed to the console.

## Common Variations & Edge Cases

### Different date strings

If your source data looks like `"2023/04/01"` or `"01‑Apr‑2023"`, you can still rely on the same workflow—just change the **Number** property to a format that matches the pattern (e.g., `Number = 15` for `d-mmm-yy`).  

### Locale‑specific formats

Excel respects the workbook’s locale settings. To force US‑style parsing, set the workbook’s culture:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

### When the string isn’t recognised

Sometimes Excel can’t infer a date (e.g., `"R3-13-40"`). In those cases, pre‑process the string:

```csharp
string raw = "R3-04-01";
string cleaned = raw.Replace("R3-", "");   // Remove the prefix
targetCell.PutValue(cleaned);
```

Then apply the same number format.

## Pro Tips & Pitfalls

- **Pro tip:** Use `StyleFlag` to modify only the number format, leaving other style attributes untouched.  
  ```csharp
  var style = targetCell.GetStyle();
  style.Number = 14;
  var flag = new StyleFlag { Number = true };
  targetCell.SetStyle(style, flag);
  ```
- **Watch out for:** Over‑writing existing styles on a cell that already has borders or fonts. The `StyleFlag` approach prevents that.
- **Performance note:** If you’re processing thousands of rows, batch the `CalculateFormula` call after you finish all updates; calling it per row adds unnecessary overhead.

## Conclusion

You now know **how to create workbook**, **convert string to date**, **format cell as date**, **set cell number format**, and finally **read excel date** back into a `DateTime`. The pattern is simple: insert raw text, apply a date style, force recalculation, then read the value.  

From here you can extend the logic to entire columns, import CSV data, or even generate reports that automatically translate legacy date strings into proper Excel dates.  

Ready to level up? Try applying a custom number format (`Number = 22`) to display dates as `yyyy-mm-dd`, or explore Aspose.Cells’ `DateTimeConversion` utilities for more complex scenarios.

Happy coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}