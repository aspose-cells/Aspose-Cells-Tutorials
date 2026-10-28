---
category: general
date: 2026-05-30
description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
  workbook, filter rows by value, and streamline your spreadsheet tasks.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: en
og_description: How to use AutoFilter in C# Excel automation. Master creating Excel
  workbook, filtering rows by value, and automating spreadsheets with ease.
og_title: How to Use AutoFilter in C# Excel Automation – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
url: /net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use AutoFilter in C# Excel Automation – Complete Guide

Ever wondered **how to use AutoFilter** when you’re generating Excel files from C# code? You’re not alone—many developers hit that snag when they need to hide rows that don’t match a certain criterion.  

In this tutorial we’ll walk through a concrete, runnable example that **creates an Excel workbook**, adds a table, and then **filters rows by value** in column B. By the end you’ll have a clean, reusable snippet you can drop into any C# project that needs Excel automation.

## What You’ll Learn

- Set up a C# project with the Aspose.Cells (or Microsoft.Office.Interop) library.  
- **Create Excel workbook** programmatically and add a styled table.  
- Apply **AutoFilter** to show only rows where **column B** equals a specific string.  
- Remove the filter entirely, restoring the full dataset.  
- Tips for handling edge cases like missing columns or multiple filter criteria.

No prior Excel‑VBA experience required; just a basic grasp of C# and NuGet packages.

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Modern runtimes give you better performance and easier package management. |
| Aspose.Cells for .NET (or Microsoft.Office.Interop.Excel) installed via NuGet | This library gives us the `Workbook`, `Worksheet`, and `Table` objects used in the code. |
| A code editor (Visual Studio, VS Code, Rider, etc.) | You’ll need to compile and run the example. |
| Basic C# knowledge | The tutorial explains *why* each line exists, not just *what* it does. |

You can install Aspose.Cells with:

```bash
dotnet add package Aspose.Cells
```

---

## How to Use AutoFilter with Aspose.Cells in C#

Below is the full, self‑contained program. Save it as `Program.cs` in a console project and run – you’ll get `FilteredWorkbook.xlsx` in the output folder.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### How the Code Works

1. **Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]` grabs the default sheet.  
2. **Filling sample data** – We write a tiny dataset so you can see the filter in action.  
3. **Adding a table** – `ListObjects.Add` converts the range into an Excel table, which automatically supports filtering and styling.  
4. **Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the engine: “Show only rows where the second column (B) equals *Apple*.”  
5. **Saving files** – Two files are written: one filtered, one with the filter removed, proving that `RemoveAutoFilter()` works as expected.

> **Pro tip:** If you need to filter by multiple criteria (e.g., “Apple” *or* “Banana”), use the overload `Filter(int columnIndex, string criteria1, string criteria2)` or pass an array of strings.

---

## Filtering Rows by Value – Common Variations

While the example above focuses on **filter column B**, you might want to filter other columns or use numeric criteria. Here’s a quick cheat sheet:

| Desired filter | Code snippet |
|----------------|--------------|
| Text match in column C | `table.AutoFilter.Filter(2, "Cherry");` |
| Numbers greater than 10 in column C | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| Multiple values in column B | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Edge case:** If the column header is misspelled or the column index is out of range, Aspose.Cells throws an `ArgumentException`. Guard against this by checking `table.ListColumns.Count` before applying the filter.

---

## Removing the AutoFilter – When to Reset

Sometimes you need to present the full dataset again (e.g., after a user clears a search box). Calling `table.RemoveAutoFilter()` does the trick in a single line. If you’re using Microsoft.Office.Interop instead, you’d call `worksheet.AutoFilterMode = false;`.

---

## Full Working Example Recap

Below is the *entire* program again, stripped of comments for those who prefer a concise view:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Running this yields two files:

- **FilteredWorkbook.xlsx** – only rows with *Apple* visible.  
- **UnfilteredWorkbook.xlsx** – the original data restored.

---

## Frequently Asked Questions

**Q: Does this work with older .xls files?**  
A: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the file extension or using `SaveOptions`.

**Q: What if I need to filter *after* the workbook is already saved?**  
A: Load the file with `new Workbook("path.xlsx")`, apply the filter, then `Save` again.

**Q: Can I apply a filter to a *range* that isn’t a table?**  
A: Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`. However, tables give you built‑in styling and easier column referencing.

---

## Image – Visual Confirmation

![Screenshot showing AutoFilter applied to column B in an Excel workbook created with C#](/images/autofilter-column-b.png "AutoFilter on column B")

*(The image illustrates the filtered view where only rows containing “Apple” remain.)*

---

## Conclusion

We’ve just covered **how to use AutoFilter** in a C#‑driven Excel automation scenario, from **creating an Excel workbook** to **filtering rows by value** in **column B**, and finally **removing the filter** when it’s no longer needed. The core steps—initialize, add a table, apply the filter, and clean up—are reusable across any project that needs to **excel automation c#**.

Ready for the next challenge? Try:

- Adding conditional formatting to highlight filtered rows.  
- Exporting the filtered data to a CSV for downstream processing.  
- Combining multiple filters (e.g., “Apple” *and* quantity > 8).

Experiment, break things, and then fix them—


## What Should You Learn Next?

- [How to Implement AutoFilter in Excel using Aspose.Cells for .NET (Data Analysis Guide)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [How to Use Autofilter Not Contains in Aspose.Cells .NET for Excel Data Analysis](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [How to Implement Excel Autofilter 'EndsWith' Using Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}