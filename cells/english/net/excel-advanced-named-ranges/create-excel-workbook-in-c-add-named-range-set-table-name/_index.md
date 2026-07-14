---
category: general
date: 2026-07-13
description: Create Excel Workbook in C# and learn how to add named range, assign
  name to table, and handle naming conflicts—all in one clear example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- add named range
- assign name to table
- set table name
- how to add range
language: en
lastmod: 2026-07-13
og_description: Create Excel Workbook in C# with Aspose.Cells. Learn how to add named
  range, set table name, and resolve naming conflicts in a concise, runnable guide.
og_image_alt: Screenshot showing an Excel workbook with a named range and a table
  name set using C# code
og_title: Create Excel Workbook in C# – Add Named Range & Set Table Name
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  headline: Create Excel Workbook in C# – Add Named Range & Set Table Name
  type: TechArticle
- description: Create Excel Workbook in C# and learn how to add named range, assign
    name to table, and handle naming conflicts—all in one clear example.
  name: Create Excel Workbook in C# – Add Named Range & Set Table Name
  steps:
  - name: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
    text: '**Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells
      you what the object is.'
  - name: '**Stay within 255 characters** – Excel’s limit for names.'
    text: '**Stay within 255 characters** – Excel’s limit for names.'
  - name: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
    text: '**Avoid spaces and special characters** – only letters, numbers, and underscores
      are safe.'
  - name: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
    text: '**Validate before assigning** – a quick `if (!sheet.Names.Contains(name))`
      check prevents the clash we demonstrated.'
  type: HowTo
- questions:
  - answer: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`.
      The `Names.Add` method accepts that format.
    question: Can I add a named range that spans multiple worksheets?
  - answer: Absolutely. You can pass a formula string instead of a static address,
      such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.
    question: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?
  - answer: 'Just set `table.Name = " ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
      - [How to Implement a Named Range with Workbook Scope in Aspose.Cells Java for
      Enhanced Excel Data Management](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
      - [Excel Automation&#58; Create a Workbook and Add a ListBox Using Aspose.Cells
      for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: What if I need to rename an existing table?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel Automation
- .NET
title: Create Excel Workbook in C# – Add Named Range & Set Table Name
url: /net/excel-advanced-named-ranges/create-excel-workbook-in-c-add-named-range-set-table-name/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook in C# – Complete Guide to Adding Named Ranges and Setting Table Names

Ever needed to **create Excel workbook** from scratch and wondered where to put a named range or how to give a table its own identifier? You're not the only one. In many reporting or data‑export scenarios, you’ll find yourself juggling ranges, tables, and the occasional naming clash.  

In this tutorial we’ll walk through a fully runnable example that **creates an Excel workbook**, **adds a named range**, and then **assigns a name to a table**—showing you exactly what to do when the names collide. By the end you’ll know the “how” and the “why” behind each step, plus a few tips to keep your code clean.

> **Quick win:** The code uses the **Aspose.Cells** library, which works with .NET 6+ and requires no Excel installation on the server.

---

## What You’ll Need

- **.NET 6 SDK** (or any recent .NET version)  
- **Aspose.Cells for .NET** NuGet package  
- A decent IDE (Visual Studio, Rider, or VS Code)  
- Basic C# knowledge—nothing fancy, just the usual `using` statements

If you’ve got those, we can jump straight into the **create excel workbook** process.

---

## ## Create Excel Workbook – Step‑by‑Step Overview

Below is the complete, copy‑paste‑ready program. It demonstrates everything from workbook creation to handling a naming conflict when you try to **assign name to table**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();

            // Step 2: Add some sample data so we have a table to work with
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Product");
            sheet.Cells["B1"].PutValue("Price");
            sheet.Cells["A2"].PutValue("Apple");
            sheet.Cells["B2"].PutValue(0.99);
            sheet.Cells["A3"].PutValue("Banana");
            sheet.Cells["B3"].PutValue(0.59);
            sheet.Cells["A4"].PutValue("Cherry");
            sheet.Cells["B4"].PutValue(2.99);
            sheet.Cells["A5"].PutValue("Date");
            sheet.Cells["B5"].PutValue(3.49);

            // Step 3: Convert the data range into a table (default name Table1)
            int tableIndex = sheet.Tables.Add(sheet.Cells.CreateRange("A1:B5"), true);
            ListObject table = sheet.Tables[tableIndex];
            // At this point the table name is "Table1"

            // Step 4: Add a named range that covers the same cells
            // This is the "add named range" part of the tutorial
            sheet.Names.Add("MyRange", "A1:B5");

            // Step 5: Try to give the table the same name – this will cause a conflict
            try
            {
                table.Name = "MyRange"; // <-- assign name to table
            }
            catch (Exception ex)
            {
                // Step 6: Handle the naming conflict by outputting the error message
                Console.WriteLine("Naming conflict detected:");
                Console.WriteLine(ex.Message);
            }

            // Optional: Save the workbook to verify everything works
            workbook.Save("DemoWorkbook.xlsx");
        }
    }
}
```

**Expected output** when you run the program:

```
Naming conflict detected:
A name with the same text already exists.
```

And if you open *DemoWorkbook.xlsx* you’ll see a table named **Table1** and a named range called **MyRange**—exactly what we intended, minus the clash.

---

## ## Add Named Range – Why It Matters

A **named range** is essentially an alias for a cell block. Instead of constantly referring to `A1:B5`, you can write `MyRange` in formulas, data validations, or even in code. This improves readability and reduces the chance of typo‑related bugs.

In the snippet above we call:

```csharp
sheet.Names.Add("MyRange", "A1:B5");
```

- The first argument is the **name** you’ll use later.  
- The second argument is the **address** (relative to the worksheet).  

If you ever need to **how to add range** dynamically, you can build the address string with `Cell.GetRefersTo()` or use `Range refRange = sheet.Cells.CreateRange(startRow, startCol, totalRows, totalCols)`.

---

## ## Assign Name to Table – Handling Conflicts

Tables (also called *list objects*) already have a built‑in name property. By default Aspose.Cells names them `Table1`, `Table2`, etc. When you try to give a table the same identifier as an existing named range, the library throws an exception—just like Excel does.

Why does this happen?

- Excel’s naming scope is **workbook‑wide** for both ranges and tables.  
- Duplicate names would make formulas ambiguous, so the engine blocks it.

### Pro tip

If you really need a table to share a logical name with a range, consider **prefixing** one of them, e.g.:

```csharp
table.Name = "tbl_MyRange";   // safe, no conflict
```

Or rename the range first:

```csharp
sheet.Names["MyRange"].Name = "DataRange";
```

Both approaches keep the naming space tidy and avoid runtime errors.

---

## ## Set Table Name – Best Practices

When you **set table name** programmatically, keep these guidelines in mind:

1. **Use a consistent prefix** (`tbl_`, `rng_`, etc.) – it instantly tells you what the object is.
2. **Stay within 255 characters** – Excel’s limit for names.
3. **Avoid spaces and special characters** – only letters, numbers, and underscores are safe.
4. **Validate before assigning** – a quick `if (!sheet.Names.Contains(name))` check prevents the clash we demonstrated.

Here’s a helper method you can drop into any project:

```csharp
static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
{
    string finalName = desiredName;
    int suffix = 1;
    while (sheet.Names.Contains(finalName) || sheet.Tables.Contains(finalName))
    {
        finalName = $"{desiredName}_{suffix}";
        suffix++;
    }
    table.Name = finalName;
}
```

Calling `SafeSetTableName(sheet, table, "MyRange")` will automatically turn `MyRange` into `MyRange_1` if a conflict exists, ensuring the **create excel workbook** operation never aborts unexpectedly.

---

## ## Full Working Example – Putting It All Together

Below is a compact version that you can copy straight into a console app. It includes the safety routine and demonstrates the end‑to‑end flow.

```csharp
using System;
using Aspose.Cells;

namespace ExcelNamingDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the workbook
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Populate a simple dataset
            ws.Cells["A1"].PutValue("Item");
            ws.Cells["B1"].PutValue("Quantity");
            ws.Cells["A2"].PutValue("Pen");
            ws.Cells["B2"].PutValue(10);
            ws.Cells["A3"].PutValue("Notebook");
            ws.Cells["B3"].PutValue(5);

            // Turn data into a table
            int tblIdx = ws.Tables.Add(ws.Cells.CreateRange("A1:B3"), true);
            ListObject tbl = ws.Tables[tblIdx];

            // Add a named range covering the same cells
            ws.Names.Add("MyRange", "A1:B3");

            // Safely assign a name to the table
            SafeSetTableName(ws, tbl, "MyRange");

            // Save to verify
            wb.Save("FinalDemo.xlsx");
            Console.WriteLine($"Table name set to: {tbl.Name}");
        }

        static void SafeSetTableName(Worksheet sheet, ListObject table, string desiredName)
        {
            string candidate = desiredName;
            int i = 1;
            while (sheet.Names.Contains(candidate) || sheet.Tables.Contains(candidate))
            {
                candidate = $"{desiredName}_{i}";
                i++;
            }
            table.Name = candidate;
        }
    }
}
```

Running this script produces `FinalDemo.xlsx` where the table is called `MyRange_1` (or another unique suffix) and the range remains `MyRange`. No exception, no mystery—just clean, deterministic naming.

---

## ## Frequently Asked Questions (FAQ)

**Q: Can I add a named range that spans multiple worksheets?**  
A: Yes, but you must qualify the address with the sheet name, e.g., `"Sheet1!A1:B5"`. The `Names.Add` method accepts that format.

**Q: Does Aspose.Cells support dynamic named ranges (like OFFSET formulas)?**  
A: Absolutely. You can pass a formula string instead of a static address, such as `"=OFFSET(Sheet1!$A$1,0,0,COUNT(Sheet1!$A:$A),2)"`.

**Q: What if I need to rename an existing table?**  
A: Just set `table.Name = "

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}