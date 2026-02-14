---
category: general
date: 2026-02-14
description: Create discount template quickly and learn how to apply discount in spreadsheet,
  inject data into template, and define variable prefix for smart markers.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: en
og_description: Create discount template with C#. Learn to apply discount in spreadsheet,
  inject data into template, and define variable prefix for smart markers.
og_title: Create Discount Template – Full C# Walkthrough
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Create Discount Template in C# – Step‑by‑Step Guide
url: /net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Discount Template – Full C# Walkthrough

Ever needed to **create discount template** for a sales report but weren’t sure how to feed the numbers into a spreadsheet automatically? You’re not alone. In this tutorial we’ll show you exactly how to **create discount template**, then **apply discount in spreadsheet** cells, **inject data into template**, and even **define variable prefix** for your smart markers—all with clean C# code.

We’ll start by outlining the problem, then jump straight into a working solution you can copy‑paste. By the end you’ll have a reusable pattern that works whether you’re generating invoices, price‑lists, or any spreadsheet that needs dynamic discounts.

---

## What You’ll Learn

- How to design a discount‑aware spreadsheet template.
- How to configure a custom `VariablePrefix` / `VariableSuffix` so markers are easy to spot.
- How to pass an anonymous object (`discountData`) into the `SmartMarkerProcessor`.
- How the resulting formula (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) automatically computes the final price.
- Tips for handling edge cases like zero‑discount rows or multiple discount tiers.

**Prerequisites** – a recent .NET runtime (≥ .NET 6), a reference to the `Aspose.Cells` (or similar) library that provides `SmartMarkerProcessor`, and a basic understanding of C# syntax. Nothing exotic.

---

## Step 1: Create a Discount Template in Your Spreadsheet

First, open a new workbook (or use an existing one) and place a placeholder where the discount will be applied. Think of the template as a plain Excel file with “smart markers” that the processor will replace.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** By embedding `#Discount#` inside the formula we tell the processor exactly where the discount value belongs. The `SmartMarkerProcessor` will replace `#Discount#` with the number you provide later, leaving the rest of the formula untouched.

---

## Step 2: Define Variable Prefix for Smart Markers

Out‑of‑the‑box, many libraries look for `${Variable}` or `{{Variable}}`. In our case we want a clean, human‑readable marker, so we **define variable prefix** and suffix explicitly.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Using `#` keeps the markers short and easy to spot in Excel’s formula bar. If you ever need to avoid clashes with existing Excel functions, pick a different pair (e.g., `[[` and `]]`).

---

## Step 3: Inject Data into Template Using SmartMarkerProcessor

Now we feed the actual discount value. The processor will scan the worksheet, find every `#Discount#`, and replace it with the value from the anonymous object we pass.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

After this call, the formula in `B2` becomes:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

When the workbook calculates, `B2` shows **90**, i.e., a 10 % discount applied to the original price of 100.

**Why it works:** `StartSmartMarkerProcessing` walks every cell, looks for the `#Discount#` token, and substitutes the numeric value. Because the token sits inside an `IF` statement, the spreadsheet still handles cases where the discount might be zero.

---

## Step 4: Apply Discount in Spreadsheet – Verify the Result

Let’s trigger the calculation and output the final price to the console. This step proves that the **apply discount in spreadsheet** workflow succeeded.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

If you change `discountData.Discount` to `0.25` and rerun the processor, the output will automatically reflect a 25 % discount—no extra code required.

---

## Step 5: Handling Edge Cases & Multiple Discounts

### Zero‑Discount Rows

Sometimes a product isn’t on sale. To keep the formula robust, the `IF` you placed earlier already covers this scenario: when `#Discount#` is `0`, the original price passes through unchanged.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Multiple Discount Columns

If you need separate discounts per row, give each row its own marker, e.g., `#Discount1#`, `#Discount2#`, and pass a collection:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

The processor matches markers sequentially, so each row gets the correct value.

---

## Full Working Example

Below is the complete, copy‑ready program that incorporates every step above. Save it as `Program.cs`, add a reference to `Aspose.Cells`, and run.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Running this prints the expected numbers and produces an `DiscountedPricing.xlsx` file you can open in Excel to see the formula already resolved.

---

## Conclusion

You now know how to **create discount template**, **apply discount in spreadsheet**, **inject data into template**, and **define variable prefix** for smart markers—all with a handful of concise C# lines. The pattern scales—just change the anonymous object or feed a collection for bulk updates, and the same template will handle any discount scenario you throw at it.

Ready for the next level? Try:

- Adding tax calculations alongside discounts.
- Pulling discount percentages from a database instead of hard‑coding them.
- Using conditional formatting to highlight rows with high discounts.

Those extensions keep the core idea intact while expanding the utility of your discount template.

Got questions or a cool use‑case? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}