---
category: general
date: 2026-10-10
description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
  guide also covers how to delete row by index and remove row by index using Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: en
lastmod: 2026-10-10
og_description: Delete entire row in an Excel workbook using C#. Follow this guide
  to learn how to delete row by index, remove row by index, and safely save the file.
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: Delete entire row in Excel with C# – complete programming guide
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: How to delete entire row in an Excel file using C#
url: /net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete entire row in an Excel file using C#

If you need to **delete entire row** in an Excel workbook, this guide shows you exactly how to do it with C#. Whether you are cleaning up imported data or building a reporting tool, the steps below let you remove a row by its index and save the result without losing other data.

You’ll also see how the same approach answers the question **how to delete row** by index, how to **remove row by index**, and why this works for **delete row excel** scenarios in C#.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code works with .NET Framework 4.6+ as well)  
* The **Aspose.Cells for .NET** library (available via NuGet: `Install-Package Aspose.Cells`)  
* Basic familiarity with C# console or desktop projects  

No additional Excel interop or COM components are required, which keeps the solution lightweight and safe for server‑side execution.

## Step 1: Set up the project and import namespaces

Create a new console application (or add the code to an existing project) and add the required `using` directives:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Why this matters*: Importing `Aspose.Cells` gives you access to `Workbook`, `Worksheet`, and the `DeleteRows` method that performs the actual row removal.

## Step 2: Load the workbook and select the worksheet

You must load the source file (`input.xlsx`) and obtain the worksheet you want to modify. The first worksheet is accessed with index `0`.

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tip**: If you need to work with a specific sheet, replace the index with the sheet name: `workbook.Worksheets["Data"]`.

## Step 3: Delete the entire row by its zero‑based index

Aspose.Cells uses zero‑based indexing, so the first row is `0`. To delete row 5 (the sixth visual row), call `DeleteRows` with `DeleteOptions.DeleteEntireRow`.

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Explanation*:

* `ws.Cells[5, 0]` points to the first cell of the row you want to delete.  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` tells Aspose.Cells to remove **1** row, and the `DeleteEntireRow` flag ensures that **the whole row** disappears, shifting rows below upward.

### How to delete row by index in other scenarios

* **Delete multiple consecutive rows** – change the first argument to the number of rows you want to erase:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **Delete the last row** – use `ws.Cells.MaxDataRow` to get the index of the bottommost populated row:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

These snippets answer the **remove row by index** requirement while keeping the code easy to read.

## Step 4: Save the workbook with the row removed

After the deletion, write the modified workbook back to disk. You can overwrite the original file or create a new one.

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

If you need to keep the original file unchanged, simply change the output path. The `Save` method supports many formats (`.xls`, `.csv`, `.pdf`, etc.) – just change the file extension.

## Full working example

Putting everything together, here is a complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Expected output**: After running the program, `output.xlsx` will contain all original rows except the one that started at visual row 6. All data below the removed row shifts up automatically, preserving formulas and formatting.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Index out of range** | Trying to delete a row index that doesn’t exist (e.g., `ws.Cells[1000,0]` in a 200‑row sheet) | Use `ws.Cells.MaxDataRow` to verify the highest valid index before calling `DeleteRows`. |
| **Partial row deletion** | Omitting `DeleteOptions.DeleteEntireRow` results in only cell contents being cleared | Always pass `DeleteOptions.DeleteEntireRow` when you need the whole row removed. |
| **Unexpected formula changes** | Deleting rows that are part of a formula range can break references | Re‑evaluate formulas after deletion (`workbook.CalculateFormula()`) if your workbook relies on dynamic ranges. |
| **Saving to a read‑only location** | The `Save` call throws an exception if the folder is protected | Ensure the target directory is writable or run the program with appropriate permissions. |

Addressing these concerns makes the solution robust for production use and satisfies the **delete row excel** and **delete row c#** queries.

## Advanced: Deleting rows based on a condition

Sometimes you need to remove rows that meet a certain criterion (e.g., rows where column A is empty). The following loop demonstrates a safe way to scan from bottom to top and delete matching rows:

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

Scanning upward prevents the index shift problem that occurs when deleting rows while iterating forward.

## Conclusion

You now know how to **delete entire row** in an Excel workbook using C#. The guide covered:

* Loading a workbook and selecting a worksheet  
* Using `DeleteRows` with `DeleteOptions.DeleteEntireRow` to **how to delete row** by index  
* Saving the modified file safely  
* Edge‑case handling, performance tips, and a conditional‑deletion example  

With this knowledge you can confidently implement **remove row by index** functionality, automate data clean‑up, and integrate Excel manipulation into any C# application.  

**Next steps**: explore other Aspose.Cells features such as inserting rows, copying ranges, or converting the workbook to PDF—each of which builds on the same `Workbook` and `Worksheet` objects you just mastered. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Delete an Excel Row Using Aspose.Cells .NET&#58; A Comprehensive Guide](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Protect Header Row in Excel](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}