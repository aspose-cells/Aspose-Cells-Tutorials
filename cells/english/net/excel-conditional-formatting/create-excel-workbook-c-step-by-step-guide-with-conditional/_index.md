---
category: general
date: 2026-03-27
description: Create Excel workbook C# with Aspose.Cells, apply conditional formatting,
  import datatable to excel and save workbook as xlsx—all in one tutorial.
draft: false
keywords:
- create excel workbook c#
- apply conditional formatting
- import datatable to excel
- save workbook as xlsx
- create excel file programmatically
language: en
og_description: Create Excel workbook C# using Aspose.Cells, apply conditional formatting,
  import datatable to excel and save workbook as xlsx in minutes.
og_title: Create Excel Workbook C# – Complete Guide with Conditional Formatting
tags:
- Aspose.Cells
- C#
- Excel automation
title: Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting
url: /net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook C# – Complete Programming Tutorial

Ever needed to **create excel workbook c#** on the fly but weren’t sure where to start? You're not the only one—many developers hit that wall when they first automate reports. In this guide we’ll show you exactly how to create excel workbook c# with Aspose.Cells, apply conditional formatting, import datatable to excel and finally save workbook as xlsx.  

What you’ll get out of this tutorial is a ready‑to‑run console app that produces a colorful Excel file, plus a clear explanation of every line so you can adapt it to your own projects. No external docs required; just copy, paste, and run.  

### Prerequisites

- .NET 6+ (or .NET Framework 4.7.2+) installed  
- Visual Studio 2022 or any C# editor you like  
- Aspose.Cells for .NET (you can grab a free trial NuGet package)  

If you’ve got those, let’s dive in.

## Create Excel Workbook C# – Initialize the Workbook

The first thing you have to do is **create excel workbook c#** by instantiating the `Workbook` class. This object represents the entire Excel file in memory.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                // <-- creates the workbook
        Worksheet worksheet = workbook.Worksheets[0];      // first sheet (Sheet1)
```

> **Why this matters:** The `Workbook` class abstracts the file format, so you don’t have to juggle low‑level XML or COM interop. It also gives you access to styles, tables, and smart markers right out of the box.

## Apply Conditional Formatting

Now that the workbook exists, let’s **apply conditional formatting** to highlight rows where the quantity exceeds 100. Conditional formatting lives on the worksheet, not the cell, which makes it reusable.

```csharp
        // Step 4: Apply conditional formatting to highlight quantities > 100
        int cfIndex = worksheet.ConditionalFormattings.Add();               // add a new CF collection
        var conditionalFormatting = worksheet.ConditionalFormattings[cfIndex];
        var condition = conditionalFormatting.AddCondition(
            FormatConditionType.CellValue, OperatorType.Greater, "100");   // > 100

        // Define the style that will be applied when the condition is true
        condition.Style = workbook.CreateStyle();
        condition.Style.Font.Color = Color.Red;               // red font
        condition.Style.Pattern = BackgroundType.Solid;       // solid background
        condition.Style.ForegroundColor = Color.Yellow;      // yellow fill
```

> **Pro tip:** If you need more complex rules (e.g., between two values), just call `AddCondition` again with `OperatorType.Between`.

## Write Headers and Smart Markers

Before we **import datatable to excel**, we need placeholder cells—smart markers—that the library will replace with actual data. Think of them as template tags.

```csharp
        // Step 2: Write the header row
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // Step 3: Define smart markers that will be replaced by data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");
```

> **Why smart markers?** They let you keep your Excel layout separate from code. You design the sheet once, then just feed a `DataTable` and the library does the rest.

## Import DataTable to Excel

Here’s the core of **import datatable to excel**. We build a `DataTable` that mirrors the smart marker fields and hand it over to `ImportDataTable`.

```csharp
        // Step 5: Build a simple DataTable that matches the smart marker fields
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // Step 6: Populate the worksheet with the DataTable via smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");
```

> **Edge case:** If your table has more columns than you need, just omit the extra columns from the smart markers; they’ll be ignored.

## Save Workbook as XLSX

Finally, we **save workbook as xlsx** to disk. The `Save` method automatically determines the format from the file extension.

```csharp
        // Step 7: Save the result to an Excel file
        workbook.Save("SmartMarkersConditional.xlsx");   // <-- saves as .xlsx
    }
}
```

That’s the entire program. When you run it, you’ll see a file named `SmartMarkersConditional.xlsx` in the output folder.

### Expected Output

| Product | Quantity | Status |
|---------|----------|--------|
| Apple   | 120      | High   |
| Banana  | 80       | Low    |
| Cherry  | 150      | High   |

The rows with **Quantity > 100** (Apple and Cherry) will have red text on a yellow background thanks to the conditional formatting we added earlier.

## Create Excel File Programmatically – Full Source Listing

Below is the complete, ready‑to‑copy source code. It contains every piece we discussed, plus a few extra comments for clarity.

```csharp
using Aspose.Cells;
using Aspose.Cells.Tables;
using System.Data;
using System.Drawing;

class SmartMarkerConditionalDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write header cells
        worksheet.Cells["A1"].PutValue("Product");
        worksheet.Cells["B1"].PutValue("Quantity");
        worksheet.Cells["C1"].PutValue("Status");

        // 3️⃣ Insert smart markers – placeholders for our data
        worksheet.Cells["A2"].PutValue("&=Products.ProductName");
        worksheet.Cells["B2"].PutValue("&=Products.Quantity");
        worksheet.Cells["C2"].PutValue("&=Products.Quantity > 100 ? \"High\" : \"Low\"");

        // 4️⃣ Apply conditional formatting (highlight >100)
        int cfIdx = worksheet.ConditionalFormattings.Add();
        var cf = worksheet.ConditionalFormattings[cfIdx];
        var cond = cf.AddCondition(FormatConditionType.CellValue, OperatorType.Greater, "100");
        cond.Style = workbook.CreateStyle();
        cond.Style.Font.Color = Color.Red;
        cond.Style.Pattern = BackgroundType.Solid;
        cond.Style.ForegroundColor = Color.Yellow;

        // 5️⃣ Build a DataTable that matches the markers
        DataTable products = new DataTable();
        products.Columns.Add("ProductName");
        products.Columns.Add("Quantity", typeof(int));
        products.Rows.Add("Apple", 120);
        products.Rows.Add("Banana", 80);
        products.Rows.Add("Cherry", 150);

        // 6️⃣ Import the DataTable – this replaces the smart markers
        worksheet.Cells.ImportDataTable(products, true, "A2");

        // 7️⃣ Save the workbook – this will create an .xlsx file
        workbook.Save("SmartMarkersConditional.xlsx");
    }
}
```

> **Tip:** If you need to generate multiple sheets, just repeat steps 2‑6 on a new `Worksheet` instance obtained via `workbook.Worksheets.Add()`.

## Why Use Aspose.Cells for C# Excel Automation?

- **Performance:** Works entirely in memory, no COM interop, so it’s fast even with large datasets.  
- **Feature‑rich:** Supports smart markers, conditional formatting, charts, pivot tables, and more.  
- **Cross‑platform:** Works on Windows, Linux, and macOS with .NET Core/5/6+.  

If you’re stuck on a particular feature—say, adding a chart or protecting a sheet—just search “asp​ose.cells add chart c#” and you’ll find a similar pattern.

## Next Steps & Related Topics

- **Export to PDF:** After you’ve **create excel workbook c#**, you can instantly export to PDF with `workbook.Save("output.pdf")`.  
- **Read existing Excel files:** Use `new Workbook("ExistingFile.xlsx")` to modify a template.  
- **Bulk import:** For massive data, consider `ImportArray` or `ImportDataTable` with `ImportOptions` to improve speed.  

Feel free to experiment with different conditional rules, colors, or even add a total row using formulas. The sky’s the limit when you **create excel file programmatically**.

---

*Ready to try it yourself? Grab the code, run it, and open the generated `SmartMarkersConditional.xlsx`. If you hit any snags, drop a comment below—happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}