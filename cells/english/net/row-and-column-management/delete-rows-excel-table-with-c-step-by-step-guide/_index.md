---
category: general
date: 2026-02-28
description: Delete rows excel table in C# quickly. Learn how to add named range excel,
  access worksheet by name, and avoid duplicate name errors.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: en
og_description: Delete rows excel table using C#. This tutorial also shows how to
  add named range excel and access worksheet by name.
og_title: Delete Rows Excel Table with C# – Complete Guide
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Delete Rows Excel Table with C# – Step‑by‑Step Guide
url: /net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete Rows Excel Table with C# – Complete Programming Tutorial

Ever needed to **delete rows excel table** from a workbook but weren’t sure which API call to use? You’re not the only one—most developers hit the same wall when they first try to trim down a table programmatically.  

In this guide we’ll walk through a full, runnable example that not only removes rows from an Excel table, but also shows **how to add defined name** (aka a *named range*), how to **access worksheet by name**, and why adding a duplicate name on another sheet throws an `InvalidOperationException`.  

By the end of the article you’ll be able to:

* Grab a worksheet using its tab name.  
* Safely delete data rows from the first table on that sheet.  
* Create a named range that points to a specific address.  
* Understand the pitfalls of duplicate names across sheets.

No external documentation required—everything you need is right here.

---

## What You’ll Need

* **DevExpress Spreadsheet** (or any library that exposes `Workbook`, `Worksheet`, `ListObject` and `Names` objects).  
* A .NET project targeting **.NET 6** or later (the code compiles with .NET Framework 4.8 as well).  
* Basic familiarity with C#—if you can write a `foreach` loop, you’re good to go.

> **Pro tip:** If you’re using the free Community Edition of DevExpress, the APIs used below are identical to the commercial version.

---

## Step 1 – Access Worksheet by Name

The first thing you have to do is locate the sheet that contains the table you want to modify.  
Most developers reach for `Worksheets[0]` out of habit, but that couples your code to sheet order and breaks as soon as someone renames a tab.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Why this matters:* By using the sheet’s **name** instead of its index you avoid accidental edits to the wrong sheet when the workbook changes.  

If the name you provide doesn’t exist, the library throws a `KeyNotFoundException`, which you can catch to present a friendly error message.

---

## Step 2 – Delete Rows Excel Table (The Safe Way)

Now that you have the correct worksheet, let’s remove the data rows from the first table.  
A common mistake is to call `DeleteRows(1, rowCount‑1)`. Since **DevExpress 22.2** that overload is **prohibited** and throws an `InvalidOperationException`. The library expects you to delete rows **within the table’s data range**, not the header row.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **What if the table is empty?** The `if` guard prevents a call with `rowCount = 0`, which would otherwise raise an exception.

### Visual Overview  

![delete rows excel table example](image.png "Screenshot showing rows being removed from an Excel table")  

*Alt text: delete rows excel table example in C# code*

---

## Step 3 – How to Add Defined Name (Create a Named Range)

After cleaning up the table you might want to refer to a specific range later—say for a chart or a data validation list. That’s where **add named range excel** comes in.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

The `Names.Add` method takes two parameters: the identifier and the A1‑style address.  
Because we used **access worksheet by name** earlier, the address string can safely reference any sheet without worrying about index changes.

---

## Step 4 – Named Range on Another Sheet – Avoid Duplicate Name Errors

You might think you can reuse the same identifier on a different sheet, like this:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Unfortunately, Excel’s naming scope is **workbook‑wide**, not per‑sheet. The call above triggers an `InvalidOperationException` with the message *“A name with the same identifier already exists.”*  

### How to Work Around It

1. **Pick a unique name** (`MyTable_Sheet2`).  
2. **Delete the existing name** before re‑adding it (only if you truly want to replace it).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Full, Runnable Example

Putting everything together, here’s a self‑contained console app you can drop into Visual Studio and run against a sample `sample.xlsx` file.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Expected outcome**

* All data rows from the first table on **Sheet1** disappear, leaving only the header row.  
* The name **MyTable** now points to `Sheet1!$A$1:$C$5`.  
* A second name **MyTable_Sheet2** safely references a range on **Sheet2** without throwing an exception.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | Grab the correct `ListObject` by index (`worksheet.ListObjects[1]`) or by name (`worksheet.ListObjects["MyTable"]`). |
| *Can I delete rows from a table that spans multiple worksheets?* | No—tables are confined to a single sheet. You must repeat the delete logic for each sheet. |
| *Is there a way to delete only a subset of rows?* | Yes—use `table.DeleteRows(startRow, count)` where `startRow` is zero‑based within the table’s data area. |
| *Do named ranges survive after saving?* | Absolutely. Once you call `SaveDocument`, the names become part of the workbook’s XML. |
| *How do I list all defined names in the workbook?* | Iterate `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Conclusion

We’ve covered **delete rows excel table** using C#, demonstrated **add named range excel**, and showed the right way to **access worksheet by name** while avoiding the dreaded duplicate‑name exception.  

The complete solution lives in the code snippet above—copy, paste, and run it against your own files. From here you can expand the logic to handle multiple tables, dynamic range calculations, or even integrate with a UI.

**Next steps** you might explore:

* Use **named range on another sheet** to drive chart series.  
* Combine the delete logic with **ExcelDataReader** to import data before cleaning it.  
* Automate bulk updates across dozens of workbooks using a simple `foreach (var file in Directory.GetFiles(...))` loop.

Got more questions about Excel automation in C#? Drop a comment, and let’s keep the conversation going. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}