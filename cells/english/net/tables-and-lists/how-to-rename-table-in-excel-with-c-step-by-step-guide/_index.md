---
category: general
date: 2026-08-11
description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
  Excel workbook, add named range, and avoid rename conflicts.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to rename table
- create excel workbook
- add named range
- how to add range
- rename excel table
language: en
lastmod: 2026-08-11
og_description: How to rename table in Excel with C# using Aspose.Cells. This guide
  shows you how to create Excel workbook, add named range, and safely rename an Excel
  table.
og_image_alt: Screenshot of C# code that renames an Excel table
og_title: How to rename table in Excel with C# – complete programming tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  headline: How to rename table in Excel with C# – step‑by‑step guide
  type: TechArticle
- description: How to rename table in Excel with C# using Aspose.Cells. Learn to create
    Excel workbook, add named range, and avoid rename conflicts.
  name: How to rename table in Excel with C# – step‑by‑step guide
  steps:
  - name: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
    text: '**Create Excel workbook** – instantiate a `Workbook` and add some sample
      data.'
  - name: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
    text: '**Add a named range** – use `Worksheets.Names.Add` to create a range called
      `MyRange`.'
  - name: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
    text: '**Create an Excel table (ListObject)** – convert the data into a table
      so we have something to rename.'
  - name: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
    text: '**Rename the table** – attempt to set the table’s `Name` property to the
      same identifier as the named range.'
  - name: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
    text: '**Handle name conflicts** – catch the exception, explain why it occurs,
      and show a safe rename strategy.'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
- Automation
title: How to rename table in Excel with C# – step‑by‑step guide
url: /net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to rename table in Excel with C# – step‑by‑step guide

If you need to **how to rename table** in an Excel file programmatically, this tutorial shows you the exact approach using Aspose.Cells for .NET. You’ll see how to **create Excel workbook**, define a **named range**, and rename an existing Excel table without causing a name conflict.

The solution works for any .NET project that targets .NET 6 or later and requires only the Aspose.Cells NuGet package. By the end of the guide you can rename an Excel table safely and understand why a conflict can arise when a table name matches a defined range.

## Prerequisites

- .NET 6 SDK or newer installed  
- Visual Studio 2022 (or any C# IDE)  
- Aspose.Cells for .NET package (`dotnet add package Aspose.Cells`)  

No additional Excel interop assemblies are required because Aspose.Cells works completely in memory.

## Overview of the solution

1. **Create Excel workbook** – instantiate a `Workbook` and add some sample data.  
2. **Add a named range** – use `Worksheets.Names.Add` to create a range called `MyRange`.  
3. **Create an Excel table (ListObject)** – convert the data into a table so we have something to rename.  
4. **Rename the table** – attempt to set the table’s `Name` property to the same identifier as the named range.  
5. **Handle name conflicts** – catch the exception, explain why it occurs, and show a safe rename strategy.

Each step is explained in detail below.

## Step 1: How to create Excel workbook and populate data

Creating a workbook is the foundation for any Excel automation task. The `Workbook` class represents the entire file in memory.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Fill some sample data in cells A1:C4
        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);
```

**Why this matters:** The workbook must contain data before you can create a table. Aspose.Cells stores data in a zero‑based collection, so `Worksheets[0]` always refers to the first sheet.

## Step 2: How to add named range to the worksheet

A **named range** lets you refer to a specific cell or range by a friendly identifier. Adding a range is straightforward:

```csharp
        // 2️⃣ Define a named range called "MyRange" that points to cell A1
        // The range string follows Excel notation: SheetName!$A$1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");
```

**Why this matters:** Named ranges are stored in the workbook’s global name collection. If a table later receives the same name, Aspose.Cells throws a `CellException` because Excel does not allow duplicate names.

## Step 3: How to add an Excel table (ListObject)

A table provides structured data handling, filtering, and styling. In Aspose.Cells it is called a **ListObject**.

```csharp
        // 3️⃣ Convert the data range A1:C4 into an Excel table
        // The range string includes the header row.
        int firstRow = 0;   // zero‑based index for row 1
        int firstCol = 0;   // column A
        int totalRows = 4;  // rows 1‑4
        int totalCols = 3;  // columns A‑C

        // Create the ListObject (table) and give it an initial name
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(firstRow, firstCol, totalRows, totalCols, true)];
        table.Name = "InitialTable";
```

**Why this matters:** The table now exists with the name `InitialTable`. Renaming it demonstrates the **how to rename table** process.

## Step 4: How to rename Excel table and handle conflicts

Attempting to rename the table to `MyRange` will clash with the named range we created earlier. The following code shows the proper pattern for detecting and resolving the conflict.

```csharp
        // 4️⃣ Try to rename the table to "MyRange"
        try
        {
            table.Name = "MyRange";   // This will raise an exception
            Console.WriteLine("Table renamed successfully.");
        }
        catch (Exception ex)
        {
            // 5️⃣ Handle the name conflict gracefully
            Console.WriteLine("Name conflict detected: " + ex.Message);

            // Resolve by choosing a unique name
            string safeName = GetUniqueTableName(workbook, "MyRange");
            table.Name = safeName;
            Console.WriteLine($"Table renamed to safe identifier: {safeName}");
        }

        // Save the workbook to verify the result
        workbook.Save("RenamedTable.xlsx");
    }

    /// <summary>
    /// Generates a unique table name that does not exist as a named range or another table.
    /// </summary>
    static string GetUniqueTableName(Workbook wb, string baseName)
    {
        int counter = 1;
        string candidate = baseName + "_" + counter;

        // Check against workbook names and existing table names
        while (NameExists(wb, candidate))
        {
            counter++;
            candidate = baseName + "_" + counter;
        }
        return candidate;
    }

    /// <summary>
    /// Returns true if the identifier is already used as a named range or table name.
    /// </summary>
    static bool NameExists(Workbook wb, string name)
    {
        // Check named ranges
        foreach (Name n in wb.Worksheets.Names)
        {
            if (string.Equals(n.TextToRefer, name, StringComparison.OrdinalIgnoreCase))
                return true;
        }

        // Check existing tables
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (ListObject lo in ws.ListObjects)
            {
                if (string.Equals(lo.Name, name, StringComparison.OrdinalIgnoreCase))
                    return true;
            }
        }
        return false;
    }
}
```

### What the code does

| Step | Action | Reason |
|------|--------|--------|
| **Try rename** | `table.Name = "MyRange"` | Demonstrates the conflict scenario. |
| **Catch exception** | Prints the conflict message. | Gives you immediate feedback about the problem. |
| **Generate safe name** | `GetUniqueTableName` adds a numeric suffix until the name is free. | Guarantees that the new table name does **not** collide with any existing named range or table. |
| **Save workbook** | `workbook.Save("RenamedTable.xlsx")` | Persists the changes so you can open the file in Excel and verify the result. |

**Expected output** when you run the program:

```
Name conflict detected: A name with the same text already exists.
Table renamed to safe identifier: MyRange_1
```

Opening `RenamedTable.xlsx` shows a table named `MyRange_1` and a separate named range `MyRange` pointing to cell A1.

## Why the conflict occurs and best practices for rename excel table

- Excel stores **named ranges** and **table names** in the same namespace.  
- When you attempt to assign a table name that already exists as a range, Aspose.Cells throws a `CellException`.  
- The recommended approach is to **check for existing names first** (as shown in `NameExists`) or to use a naming convention that guarantees uniqueness (e.g., prefixing tables with `tbl_`).  

Applying this pattern prevents runtime errors and makes your automation robust.

## Additional tips for working with Aspose.Cells

- **Pro tip:** Use `Workbook.Worksheets.Names.Remove("MyRange")` if you intentionally want to replace the range with a table name.  
- **Watch out for case sensitivity:** Excel treats names case‑insensitively; the helper methods use `OrdinalIgnoreCase` to emulate Excel’s behavior.  
- **Performance:** If you are processing many worksheets, cache the name collection instead of iterating repeatedly.

## Complete example in one block

Below is the full program you can copy‑paste into a console project. It includes all steps from creating the workbook to safely renaming the table.

```csharp
using System;
using Aspose.Cells;

class RenameTableDemo
{
    static void Main()
    {
        // Create workbook and populate data
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        sheet.Cells["A1"].PutValue("ID");
        sheet.Cells["B1"].PutValue("Name");
        sheet.Cells["C1"].PutValue("Score");

        sheet.Cells["A2"].PutValue(1);
        sheet.Cells["B2"].PutValue("Alice");
        sheet.Cells["C2"].PutValue(85);

        sheet.Cells["A3"].PutValue(2);
        sheet.Cells["B3"].PutValue("Bob");
        sheet.Cells["C3"].PutValue(92);

        sheet.Cells["A4"].PutValue(3);
        sheet.Cells["B4"].PutValue("Carol");
        sheet.Cells["C4"].PutValue(78);

        // Add named range "MyRange" pointing to A1
        workbook.Worksheets.Names.Add("MyRange", "Sheet1!$A$1");

        // Convert the data range into a table named "InitialTable"
        ListObject table = sheet.ListObjects[sheet.ListObjects.Add(0, 0, 4, 3, true)];
        table.Name = "InitialTable";

        // Attempt to rename the table to "MyRange" – this will conflict
        try
        {
            table.Name = "MyRange";
            Console


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [How to Implement Named Range Formulas in .NET using Aspose.Cells for Excel Automation](/cells/english/net/formulas-functions/implement-named-range-formulas-net-aspose-cells/)
- [How to Add Slicers to Excel Tables Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/advanced-features/add-slicers-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}