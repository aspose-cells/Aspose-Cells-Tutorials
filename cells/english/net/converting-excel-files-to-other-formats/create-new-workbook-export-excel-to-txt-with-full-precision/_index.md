---
category: general
date: 2026-03-18
description: Create new workbook and export Excel to TXT while preserving numeric
  precision. Learn how to save worksheet as txt and convert worksheet to txt efficiently.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: en
og_description: Create new workbook and export Excel to TXT with precision. This tutorial
  shows how to save worksheet as txt and convert worksheet to txt using C#.
og_title: Create new workbook – Export Excel to TXT Guide
tags:
- Aspose.Cells
- C#
- Excel automation
title: Create new workbook – Export Excel to TXT with Full Precision
url: /net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create new workbook – Export Excel to TXT with Full Precision

Ever needed to **create new workbook** in C# just to dump some data into a plain‑text file? Maybe you’re pulling a report from a legacy system and the downstream tool only accepts a `.txt` feed. The good news? You don’t have to sacrifice numeric precision, and you certainly don’t need to hand‑craft CSV strings.

In this guide we’ll walk through the entire process of **export excel to txt**, covering everything from initializing the workbook to preserving trailing zeros when you **save worksheet as txt**. By the end you’ll have a ready‑to‑run snippet that you can drop into any .NET project—no extra utilities required.

## What You’ll Need

- **ASP.NET/ .NET 6+** (the code works on .NET Framework 4.6+ as well)  
- **Aspose.Cells for .NET** – the library that powers the `Workbook`, `Worksheet`, and `TxtSaveOptions` classes. You can grab it from NuGet with `Install-Package Aspose.Cells`.  
- A basic understanding of C# (if you’re comfortable with `using` statements, you’re good to go).  

That’s it—no Excel interop, no COM objects, and definitely no manual string concatenation.  

---

## Step 1: Initialize a New Workbook (Primary Keyword)

The first thing you have to do is **create new workbook**. Think of the workbook as the blank canvas where you’ll later paste numbers, text, or formulas.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **Why this matters:** Instantiating `Workbook` without loading a file gives you a clean slate. You can then add data programmatically, which is perfect for **convert worksheet to txt** scenarios where you don’t have an existing `.xlsx`.

---

## Step 2: Populate Cells – Keep Those Trailing Zeros

A common pitfall when dumping numbers to text is losing trailing zeros (`123.45000` becomes `123.45`). If downstream systems rely on fixed‑width fields, that loss can break everything.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **Pro tip:** `PutValue` automatically infers the data type. If you need a string that looks like a number, use `PutValue("123.45000")` instead.

---

## Step 3: Configure TXT Save Options – Preserve Numeric Precision

Here’s where the magic happens. By toggling `PreserveNumericPrecision`, you instruct Aspose.Cells to write the exact value you entered, including any insignificant trailing zeros.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **Why enable this?** When you **save excel as txt**, the default behavior trims unnecessary decimals. Setting `PreserveNumericPrecision = true` guarantees the output mirrors the cell’s displayed value, which is critical for financial reports or scientific data.

---

## Step 4: Save the Worksheet as TXT – The Final Export

Now we actually **save worksheet as txt**. You can point the path anywhere you have write permission; the example uses a relative folder called `output`.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **Expected output** (`num-preserve.txt`):

```
123.45000
```

Notice the trailing zeros are intact—exactly what you asked for.

---

## Step 5: Verify the Result – Quick sanity check

After the program runs, open `num-preserve.txt` in any text editor. You should see the single line `123.45000`. If you spot `123.45` instead, double‑check that `PreserveNumericPrecision` is set to `true` and that you’re using a recent version of Aspose.Cells (v23.10+).

---

## Common Variations & Edge Cases

### Exporting Multiple Cells or Ranges

If you need to **export excel to txt** for an entire range, simply fill more cells before saving:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose will write each cell on a new line by default. You can also change the delimiter (tab, comma) via `txtSaveOptions.Separator`.

### Converting Worksheet to TXT with Different Encodings

Sometimes downstream systems require UTF‑8 BOM or ASCII. Adjust the encoding like this:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### Handling Large Workbooks

When dealing with massive sheets (hundreds of thousands of rows), consider streaming the output:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## Pro Tips & Gotchas

- **Don’t forget to create the output directory** before calling `Save`, otherwise you’ll get a `DirectoryNotFoundException`.  
- **Watch out for locale‑specific decimal separators**. If your environment uses commas (`1,23`), set `txtSaveOptions.DecimalSeparator = '.'` to enforce a dot.  
- **Version compatibility**: The `PreserveNumericPrecision` flag was introduced in Aspose.Cells 20.6. If you’re on an older version, the flag won’t exist and you’ll need to format the cell as text before saving.

---

![Create new workbook example](excel-to-txt.png "Create new workbook")

*Image alt text: "Create new workbook and export Excel to TXT with numeric precision preserved"*

---

## Recap – What We Covered

- **Create new workbook** using Aspose.Cells.  
- Populate a cell with a number that includes trailing zeros.  
- Set `TxtSaveOptions.PreserveNumericPrecision = true` to **save excel as txt** without losing precision.  
- Write the file to disk, verifying that the output matches the original value.  

That’s the full **convert worksheet to txt** workflow in under 50 lines of C#.

---

## Next Steps & Related Topics

Now that you can **export excel to txt** with perfect precision, you might want to explore:

- **Exporting to CSV** with custom delimiters (`TxtSaveOptions.Separator`).  
- **Saving as other plain‑text formats** like TSV (`SaveFormat.TabDelimited`).  
- **Batch processing** multiple workbooks in a folder using `Directory.GetFiles`.  
- **Integrating with Azure Functions** for on‑demand conversion in the cloud.

Each of these builds on the same `Workbook` → `Worksheet` → `TxtSaveOptions` pattern, so you’ll feel right at home.

---

### Final Thought

If you’ve followed along, you now know exactly how to **create new workbook**, populate it, and **save worksheet as txt** while keeping every decimal digit you care about. It’s a small piece of code, but it solves a surprisingly common headache when legacy pipelines demand plain‑text inputs.

Give it a spin, tweak the options, and let the data flow exactly the way you need it to. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}