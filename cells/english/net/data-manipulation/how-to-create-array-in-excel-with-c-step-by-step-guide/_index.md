---
category: general
date: 2026-02-28
description: How to create array in Excel using C#. Learn to generate numbers, evaluate
  formula, create excel workbook and save excel file in minutes.
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: en
og_description: How to create array in Excel using C#. This tutorial shows how to
  generate numbers, evaluate a formula, create workbook and save the file.
og_title: How to Create Array in Excel with C# – Complete Guide
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: How to Create Array in Excel with C# – Step‑by‑Step Guide
url: /net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Array in Excel with C# – Complete Programming Tutorial

Ever wondered **how to create array** in Excel programmatically with C#? You're not the only one—developers constantly ask for a quick way to generate a block of numbers without manually typing them. In this guide we’ll walk through the exact steps to **create excel workbook**, drop a formula that **generates numbers**, **evaluate the formula**, and finally **save excel file** so you can open it in Excel and see the result.

We'll use the Aspose.Cells library because it gives us full control over formulas and calculation without needing Excel installed. If you prefer another library the concepts stay the same—just swap the API calls.

## What This Tutorial Covers

- Setting up a C# project with the required NuGet package.  
- Creating a new workbook (that’s the *create excel workbook* part).  
- Writing a formula that builds a 4‑row × 3‑col array using `SEQUENCE` and `WRAPCOLS`.  
- Forcing the engine to **evaluate the formula** so the array materialises.  
- Saving the workbook to disk (**save excel file**) and checking the output.  

By the end you’ll have a runnable program that produces an Excel sheet looking like this:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![How to create array in Excel – resulting sheet after running the C# code](image.png)

*(Image alt text includes the primary keyword “how to create array” for SEO.)*

---

## Prerequisites

- .NET 6.0 SDK or later (the code works on .NET Framework 4.6+ as well).  
- Visual Studio 2022 or any editor you like.  
- NuGet package **Aspose.Cells** (free trial available).  

No extra Excel installation is required because Aspose.Cells does the calculation engine internally.

---

## Step 1: Set Up the Project and Import Aspose.Cells

To start, create a console app and add the library:

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

Now open **Program.cs** and add the namespace:

```csharp
using Aspose.Cells;
```

*Why this matters*: Importing `Aspose.Cells` gives us the `Workbook`, `Worksheet`, and calculation classes we’ll need to **create excel workbook** and work with formulas.

---

## Step 2: Create the Workbook and Target Worksheet

We need a fresh workbook object; the first worksheet (`Worksheets[0]`) will host our array.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*Explanation*: The `Workbook` class represents the entire Excel file. By default it contains one sheet, which is perfect for a simple demo. If you ever need more sheets you can call `workbook.Worksheets.Add()` later.

---

## Step 3: Write a Formula That **Generates Numbers** and Forms an Array

Excel’s dynamic‑array functions (`SEQUENCE` and `WRAPCOLS`) let us produce a block of values with a single formula. Here’s the exact string we’ll assign:

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*Why this works*:  
- `SEQUENCE(12,1,1,1)` returns a vertical list of the numbers 1‑12.  
- `WRAPCOLS(...,3)` takes that list and fills it across three columns, automatically spilling into the next rows.  

If you open the workbook in Excel **without** evaluating the formula first, you’ll see only the formula text in `A1`. The next step forces the calculation.

---

## Step 4: **Evaluate the Formula** So the Array Materialises

Aspose.Cells doesn’t automatically recalculate formulas on write, so we explicitly invoke the calculation engine:

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*What’s happening*: `Calculate()` walks through every cell that contains a formula, computes its result, and writes the values back. This is the **how to evaluate formula** part of our tutorial. After this call, cells A1:C4 contain the numbers 1‑12, just like a native Excel spill.

---

## Step 5: **Save Excel File** and Verify the Result

Finally we persist the workbook to disk:

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Open `output.xlsx` in Excel and you’ll see the 4 × 3 array we generated. If you’re using a version of Excel older than 365/2019, the dynamic‑array functions won’t be recognized—Aspose.Cells will still write the evaluated values, so the file remains usable.

*Pro tip*: Use `SaveFormat.Xlsx` if you need to force a specific format, e.g., `workbook.Save(outputPath, SaveFormat.Xlsx);`.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete program. Paste it into **Program.cs**, run `dotnet run`, and you’ll get `output.xlsx` in the project folder.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**Expected output** (console):

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

Open the file and you’ll see the numbers 1‑12 arranged exactly as shown earlier.

---

## Variations & Edge Cases

### 1. Older Excel Versions Without Dynamic Arrays  
If your audience uses Excel 2016 or earlier, `SEQUENCE` and `WRAPCOLS` won’t exist. A quick workaround is to generate the numbers in C# and write them directly:

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

This manual loop mimics the same result, albeit with more code. The **how to generate numbers** concept stays identical.

### 2. Changing the Size of the Array  
Want a 5 × 5 grid of numbers 1‑25? Just tweak the `SEQUENCE` arguments and the `WRAPCOLS` column count:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. Using Named Ranges for Reuse  
You can assign the spilled range to a name for later formulas:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

Now any other sheet can reference `MyArray` directly.

---

## Common Pitfalls & How to Avoid Them

| Pitfall | Why It Happens | Fix |
|---|---|---|
| **Formula not spilling** | `Calculate()` omitted or called before setting the formula. | Always call `workbook.Calculate()` **after** assigning the formula. |
| **File saved but empty** | Using `SaveFormat.Csv` accidentally. | Use `SaveFormat.Xlsx` or omit the format to let Aspose infer. |
| **Dynamic

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}