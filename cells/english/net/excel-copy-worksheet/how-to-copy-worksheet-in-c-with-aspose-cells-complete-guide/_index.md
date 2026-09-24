---
category: general
date: 2026-03-30
description: How to copy worksheet in C# using Aspose.Cells – step‑by‑step guide covering
  copy cell range, copy columns between sheets, copy worksheet pivot table and add
  new worksheet code.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: en
og_description: Learn how to copy worksheet in C# with Aspose.Cells. This guide shows
  copy cell range, preserve pivot tables, copy columns between sheets, and add new
  worksheet code.
og_title: How to Copy Worksheet in C# – Full Aspose.Cells Tutorial
tags:
- Aspose.Cells
- C#
- Excel Automation
title: How to Copy Worksheet in C# with Aspose.Cells – Complete Guide
url: /net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Copy Worksheet in C# with Aspose.Cells – Complete Guide

Ever wondered **how to copy worksheet** in C# without losing a single pivot table or formula? You're not alone—many developers hit a wall when they need to duplicate a sheet while keeping all the goodies intact. In this tutorial we’ll walk through a practical, end‑to‑end solution that not only copies the data but also preserves the **copy worksheet pivot table**, handles **copy cell range**, and shows the **add new worksheet code** you’ll need.

We'll cover everything from loading the source workbook to saving the destination file, so you can copy columns between sheets, preserve objects, and keep your code clean. No vague references, just a complete, runnable example you can drop into your project today.

## What This Tutorial Covers

- Loading an existing Excel file with Aspose.Cells  
- Using **add new worksheet code** to create a target sheet  
- Defining a **copy cell range** that includes a pivot table  
- Setting up **CopyOptions** to keep charts, formulas, and pivot tables intact  
- Executing **copy columns between sheets** with row‑wise precision  
- Saving the result and verifying that the worksheet was copied correctly  

By the end of this guide you’ll be able to answer the question “how to copy worksheet” confidently, whether you’re automating reports or building a spreadsheet‑driven UI.

---

## How to Copy Worksheet – Overview

Before we dive into code, let’s outline the high‑level flow. Think of it as a recipe:

1. **Load** the source workbook (`Source.xlsx`).  
2. **Add** a fresh worksheet to hold the copy (`add new worksheet code`).  
3. **Define** the area you want to duplicate (`copy cell range`).  
4. **Configure** copy options so the pivot table survives (`copy worksheet pivot table`).  
5. **Copy** rows and columns (`copy columns between sheets`).  
6. **Save** the new workbook (`Destination.xlsx`).  

That’s it—six steps, no magic. Each step is explained below with code snippets and the reasoning behind it.

---

## Step 1 – Load the Source Workbook

First things first: you need a `Workbook` instance pointing at the file you want to duplicate. This step is essential because Aspose.Cells works directly with the file system, not with the Office UI.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Why this matters:* Loading the file creates an in‑memory representation of every sheet, cell, and object. Without this, there’s nothing to copy, and any attempt to `add new worksheet code` later would fail because the source data isn’t present.

---

## Step 2 – Add a New Worksheet (add new worksheet code)

Now we need a place to paste the copied data. This is where the **add new worksheet code** shines. You can name the sheet anything you like; here we call it `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro tip:* If you plan to copy multiple sheets, call `Worksheets.Add` inside a loop and give each sheet a unique name. That way you avoid name collisions and keep your workbook tidy.

---

## Step 3 – Define the Copy Cell Range

A **copy cell range** tells Aspose.Cells exactly which rows and columns to duplicate. In many real‑world scenarios the range includes a pivot table, so we must be precise.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Why we need this:* By explicitly stating the range, you avoid copying the entire sheet (which can be wasteful) and you guarantee that the pivot table lives inside the copied area. This is the core of **how to copy worksheet** when you only need part of the sheet.

---

## Step 4 – Set Copy Options (preserve copy worksheet pivot table)

Aspose.Cells offers a `CopyOptions` object that controls what gets pasted. To keep the pivot table, charts, and formulas, we set `PasteType.All` and enable `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Explanation:* `PasteType.All` is the most inclusive option, while `PasteSpecial` tells the engine to treat complex objects—like pivot tables—properly. Skipping this step is a common pitfall; the copied sheet would lose its interactive features.

---

## Step 5 – Copy Rows and Columns (copy columns between sheets)

Now comes the heavy lifting: actually moving the data. We’ll use `CopyRows` and `CopyColumns` to handle **copy columns between sheets**. Doing both ensures that merged cells and column widths are preserved.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*What’s happening:* `CopyRows` moves the data row‑by‑row, while `CopyColumns` does the same column‑by‑column. Running both guarantees that the entire rectangular block is duplicated, which is essential when you need to **copy columns between sheets** that have different column widths or hidden columns.

---

## Step 6 – Save the Workbook

Finally, write the changes back to disk. This step completes the **how to copy worksheet** process.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verification tip:* Open `Destination.xlsx` and check that the `"Copy"` sheet looks identical to the original, pivot tables are functional, and column widths match. If anything looks off, revisit the `CopyOptions` settings.

---

## Edge Cases & Common Variations

### Copying Multiple Worksheets

If you need to duplicate several sheets, wrap the above logic in a `foreach` loop:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Preserving Formulas Across Different Workbooks

When the source and destination workbooks have different named ranges, set `copyOptions` to `PasteType.Formulas` in addition to `All`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Large Ranges and Performance

For massive datasets (hundreds of thousands of rows), consider using `CopyRows` only and skipping `CopyColumns` if column widths are not critical. This can shave off a few seconds.

---

## Full Working Example

Below is the complete, ready‑to‑run program that embodies everything we’ve discussed. Paste it into a console app, adjust the file paths, and hit **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Expected result:** Opening `Destination.xlsx` shows a sheet named **Copy** that mirrors the first sheet of `Source.xlsx`—including any pivot tables, formatting, and column widths. The original file remains untouched.

---

## Frequently Asked Questions

**Q: Does this work with .xlsx files created by Excel 2019?**  
A: Absolutely. Aspose.Cells supports all modern Excel formats, so the same code works for `.xlsx`, `.xlsm`, and even older `.xls` files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}