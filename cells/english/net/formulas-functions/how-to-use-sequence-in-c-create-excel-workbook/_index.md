---
category: general
date: 2026-07-03
description: How to use SEQUENCE in C# to generate incremental numbers in Excel. Learn
  to create Excel workbook C# and ASP.NET create Excel file with a few lines of code.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: en
og_description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
  Step‑by‑step guide to create Excel workbook C# and ASP.NET create Excel file.
og_title: How to Use SEQUENCE in C# – Create Excel Workbook
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: How to Use SEQUENCE in C# – Create Excel Workbook
url: /net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use SEQUENCE in C# – Create Excel Workbook

Ever wondered **how to use SEQUENCE** to spit out a list of numbers in an Excel sheet from C#? You're not the only one. Whether you're building a reporting dashboard, feeding a data‑grid, or just need a quick way to generate IDs, mastering this trick saves you from fiddling with loops.

In this tutorial we'll **create an Excel workbook in C#**, drop a `SEQUENCE` dynamic‑array formula into cell A1, and end up with a nice column of incremental numbers. We'll also see how to serve that file from an ASP.NET controller—yes, **ASP.NET create Excel file** is covered too. By the end you’ll be able to **generate incremental numbers Excel**‑style with a single line of code.

## What You’ll Need

- .NET 6+ (the code works on .NET Framework 4.6+ as well)  
- The **Aspose.Cells for .NET** NuGet package (or any library that exposes `Workbook`/`Worksheet` objects)  
- A basic ASP.NET Core or MVC project if you want to try the web‑download part  

That’s it. No extra COM interop, no Office installation required.

---

## How to Use SEQUENCE to Generate Incremental Numbers

The Excel `SEQUENCE(rows, [columns], [start], [step])` function returns a **spill** range. In our case we want 5 rows, 1 column, start at 10, step 2. The formula looks like this:

```excel
=SEQUENCE(5,1,10,2)
```

When Excel evaluates it, cells A1:A5 will contain **10, 12, 14, 16, 18**. The beauty is that we don’t need to write any C# loops—the formula does the heavy lifting.

Below is the complete C# snippet that creates a workbook, inserts the formula, forces calculation, and saves the file.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Expected output** – open *DynamicArray.xlsx* and you’ll see:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

That’s the whole **how to use sequence** story in C#. Simple, right? But let’s dig a little deeper.

### Why Use SEQUENCE Instead of a Loop?

- **Performance** – Excel does the math on its own engine, which is highly optimized.
- **Maintainability** – The formula is self‑documenting; anyone opening the sheet instantly knows the intent.
- **Dynamic resizing** – Change the `rows` argument and the spill range expands automatically.

---

## Create Excel Workbook C# – Step by Step

If you’re new to **create excel workbook c#**, the following checklist helps you avoid common pitfalls.

1. **Add the Aspose.Cells package**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (You can also use ClosedXML or EPPlus, but the API shown matches the code above.)

2. **Set a license** (optional for trial).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instantiate `Workbook`** – this gives you a fresh, blank workbook.

4. **Reference the worksheet** – `workbook.Worksheets[0]` is the default sheet named *Sheet1*.

5. **Apply the SEQUENCE formula** – as shown earlier.

6. **Calculate** – `workbook.CalculateFormula()` forces the spill; otherwise the file would contain the formula only.

7. **Save** – you can write to disk, a `MemoryStream`, or directly to an HTTP response.

### Pro Tip

If you need the workbook in memory (e.g., to send it over a web API), use a `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Create Excel File – Streaming to the Browser

Now that we know **create excel workbook c#**, let’s integrate it into an ASP.NET Core controller so users can download the file on the fly.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

When a user hits `/api/excel/download`, the browser prompts a download of *DynamicArray.xlsx*. The file already contains the **generated incremental numbers excel** column thanks to the `SEQUENCE` formula.

### What If the Client Uses an Older Excel Version?

Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019. If you need backward compatibility, fall back to a manual fill:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

That snippet shows the classic **generate incremental numbers excel** approach without relying on the new function.

---

## Common Questions & Edge Cases

- **Do I need to enable iterative calculation?**  
  No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()` call is enough.

- **What if I want a horizontal spill?**  
  Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.

- **Can I combine SEQUENCE with other functions?**  
  Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows from another column.

- **Is the workbook size a concern?**  
  The file size impact of a formula is negligible. Only when you start populating millions of cells manually does size become an issue.

---

## Conclusion

We’ve walked through **how to use sequence** in C# to **create excel workbook c#**, served that workbook via **ASP.NET create excel file**, and demonstrated a clean way to **generate incremental numbers excel** without writing any loops. The key takeaway: let Excel’s own dynamic‑array engine do the counting, and let your .NET code focus on orchestration.

Feel free to experiment—swap the `rows`, `start`, or `step` arguments, spill horizontally, or blend the formula with `IF` or `FILTER` for more sophisticated reports. When you’re ready, try chaining multiple sheets together or exporting the workbook as CSV for downstream systems.

Got a twist you’d like to share? Drop a comment below, or ping me on GitHub. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}