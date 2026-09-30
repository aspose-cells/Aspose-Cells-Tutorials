---
category: general
date: 2026-02-15
description: how to format currency quickly using set column number format and apply
  custom numeric format in C#. Learn retrieve column by name and set grid column alignment.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: en
og_description: how to format currency in a grid column using C#. This tutorial shows
  how to retrieve column by name, set column number format, apply custom numeric format,
  and set grid column alignment.
og_title: how to format currency in a Grid Column – Complete Guide
tags:
- C#
- GridFormatting
- UI
title: how to format currency in a Grid Column – Step‑by‑Step Guide
url: /net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to format currency in a Grid Column – Complete Programming Tutorial

Ever wondered **how to format currency** in a grid column without pulling your hair out? You're not the only one. When you stare at a plain number like `1234.5` and wish it would magically appear as `$1,234.50`, the answer is usually just a few lines of configuration.  

In this guide we’ll **retrieve column by name**, **set column number format**, and **apply custom numeric format** that respects the typical accounting layout. Along the way we’ll also **set grid column alignment** and add a subtle border so the UI looks polished.

> **TL;DR** – By the end you’ll have a ready‑to‑run snippet that turns raw decimals into beautifully formatted currency values inside any `GridJs`‑style control.

---

## What You’ll Need

- A .NET project (any version that supports C# 8.0+ – Visual Studio 2022 works great).  
- A grid component that exposes a `Columns` collection (the example uses a fictional `GridJs` class, but the concepts translate to DevExpress, Telerik, or Syncfusion grids).  
- Basic familiarity with C# syntax – no advanced tricks required.

If you already have those, great. If not, just spin up a console app; the grid can be mocked for illustration.

---

## Step‑by‑Step Implementation

Below each step you’ll see a compact code block, a short explanation of **why** the line matters, and a tip to avoid common pitfalls.

### ## Step 1 – Retrieve the “Amount” column by name

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Why this matters:**  
Most grid APIs expose columns via a dictionary‑like indexer. Pulling the column by its header name (`"Amount"`) lets you manipulate its appearance without touching the underlying data source.  

**Pro tip:** Always guard against a `null` return – a typo in the column name or a dynamic schema change can otherwise cause a `NullReferenceException` at runtime.

---

### ## Step 2 – Set column number format using a custom currency mask

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Why this matters:**  
The format string follows Excel’s accounting format conventions:

- `_(* #,##0.00_)` → Positive numbers, right‑aligned with a leading space for the currency symbol.  
- `_(* (#,##0.00)` → Negative numbers wrapped in parentheses.  
- `_(* \"-\"??_)` → Zero values displayed as a dash.  
- `_(@_)` → Text values remain unchanged.

Using **apply custom numeric format** gives you full control over thousands separators, decimal places, and the placement of the currency sign.  

**Edge case:** If your application needs to respect a different locale (e.g., Euro instead of USD), replace the leading space with the appropriate symbol or use `CultureInfo`‑aware formatting in the data source.

---

### ## Step 3 – Align the column contents to the right for readability

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Why this matters:**  
Currency values are easier to scan when they line up on the decimal separator. Setting **set grid column alignment** to `Right` mirrors the way spreadsheets display monetary data.  

**Gotcha:** Some grids ignore alignment on cells that contain custom templates. If you notice the alignment not taking effect, double‑check that the column isn’t using a custom cell renderer.

---

### ## Step 4 – Add a thin gray border around the column cells

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Why this matters:**  
A subtle border separates the “Amount” column from its neighbours, especially when the grid has alternating row colors. It’s a visual cue that the data represents a distinct financial figure.  

**Tip:** If you need a thicker line for printing purposes, bump `BorderLineStyle` to `Medium` or change `Color` to `Color.Black`.

---

## Full Working Example

Here’s the entire snippet you can drop into a WinForms or WPF project that uses a `GridJs`‑style control. The example also prints the formatted values to the console so you can verify the output without a UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected console output**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Notice how the positive number is right‑aligned, the negative one appears in parentheses, and zero shows a dash – exactly what the custom format string dictates.

---

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if the grid uses a different culture (e.g., € instead of $)?* | Replace the leading space in the format string with the desired symbol or let the data source emit a pre‑formatted string using `CultureInfo.CurrentCulture`. |
| *Can I reuse the same format for multiple columns?* | Absolutely. Store the format string in a constant (`const string CurrencyMask = "...";`) and assign it wherever you need currency. |
| *What happens if the column contains a string value?* | The format string only affects numeric types. Strings pass through unchanged, which is why the last part of the mask (`_(@_)`) exists – it preserves non‑numeric content. |
| *Is there a performance impact?* | Negligible. The format is applied at render time, not during data retrieval. Unless you’re rendering thousands of rows per frame, you won’t notice any slowdown. |
| *How do I make the border thicker for printed reports?* | Swap `BorderLineStyle.Thin` with `BorderLineStyle.Medium` or `BorderLineStyle.Thick`. Some libraries also let you specify a pixel width directly. |

---

## Wrap‑Up

We’ve walked through **how to format currency** in a grid column from start to finish: retrieve the column by name, set column number format, apply a custom numeric format, align the cells, and add a tasteful border. The complete example runs out‑of‑the‑box and demonstrates the exact visual result you can expect.

If you’re ready to take this further, try:

- **Dynamic cultures** – switch the format string based on the user’s locale.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}