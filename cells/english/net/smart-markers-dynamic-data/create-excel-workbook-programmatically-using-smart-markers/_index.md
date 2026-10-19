---
category: general
date: 2026-09-24
description: Create Excel workbook programmatically and learn how to create multiple
  detail sheets, then save workbook as xlsx file with a clear C# example.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: en
lastmod: 2026-09-24
og_description: Create Excel workbook programmatically, see how to create multiple
  detail sheets and save workbook as xlsx file in a single, runnable example.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Create Excel workbook programmatically – full C# guide
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Create Excel workbook programmatically using Smart Markers
url: /net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook programmatically using Smart Markers

If you need to **create Excel workbook programmatically**, this guide shows you exactly how to do it with Aspose.Cells .NET. You’ll also discover **how to create multiple detail sheets** from a single data source and finally **save workbook as xlsx file** without any manual steps.  

The solution is self‑contained: we walk through every line of code, explain why each setting matters, and cover common pitfalls such as duplicate sheet names. By the end you’ll have a ready‑to‑run console application that produces a workbook with a master sheet and a set of detail sheets.

## What you’ll need

| Prerequisite | Reason |
|--------------|--------|
| .NET 6.0 SDK or later | Provides the runtime for the C# console app |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Supplies `Workbook`, `SmartMarkerProcessor`, and `SmartMarkerOptions` classes |
| A simple data source (e.g., `DataTable` or a list of objects) | Supplies the values that Smart Markers will expand |
| Visual Studio 2022 or any editor that supports .NET | Makes it easy to compile and run the code |

> **Pro tip:** Install the Aspose.Cells package via the CLI before you start:  
> `dotnet add package Aspose.Cells`

## Step 1: Set up the project and import namespaces

Create a new console project and bring the required namespaces into scope.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Why this matters*: `Aspose.Cells` handles the workbook lifecycle, while `Aspose.Cells.SmartMarkers` gives you the powerful Smart Marker engine that can generate many sheets from a single template.

## Step 2: Create the Excel workbook programmatically

The first concrete action is to instantiate a `Workbook`. This object represents the entire Excel file in memory.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

If you prefer to start from a template that already contains header rows or formatting, replace `new Workbook()` with `new Workbook("Template.xlsx")`. The rest of the process works identically.

## Step 3: Prepare a Smart Marker template

Smart Markers work on cell contents that contain placeholders like `&=Employees.Name`. For this tutorial we’ll add a simple template directly via code, but you could also edit the sheet manually in Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Why this matters*: The placeholder `&=Employees.Name` tells the Smart Marker processor to iterate over the `Employees` collection. Each iteration will spawn a new worksheet because we’ll configure the processor to create a **detail sheet** for every row.

## Step 4: Build a data source that contains multiple rows

We’ll use a `DataTable` as a quick way to simulate a collection of employee records.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

You can replace this with any `IEnumerable` (e.g., `List<Employee>`) – Smart Markers accept any data source that implements `IEnumerable`.

## Step 5: Configure Smart Marker options – how to create multiple detail sheets

By default, Smart Markers write data back to the same sheet. To generate **multiple detail sheets**, you must set the `DetailSheetNewName` property. This also demonstrates **how to create multiple detail sheets** without naming conflicts.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

If the data source contains duplicate names, the processor automatically appends a numeric suffix (e.g., `Detail_1`, `Detail_2`). This prevents runtime errors and ensures all detail sheets are saved.

## Step 6: Process the Smart Markers

Now we invoke the processor, passing the data source and the options we just defined.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Why this matters*: The processor reads the placeholder `&=Employees.Name`, iterates over each row of `employees`, creates a new sheet called “Detail”, and writes the row data into that sheet. The original sheet remains as a summary or master sheet.

## Step 7: Save workbook as xlsx file

Finally, persist the workbook to disk using the **save workbook as xlsx file** pattern.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

The `SaveFormat.Xlsx` enum guarantees that the file is stored in the modern Office Open XML format, which is compatible with Excel 2007+ and most cloud services.

## Full, runnable example

Copy the following code into `Program.cs` of a .NET console project and run it. The program will generate `detail.xlsx` in the `output` folder, containing one master sheet and three detail sheets (one per employee).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Expected output**

- `output/detail.xlsx` contains:
  - **Sheet1** – the original template with the header “Employee Report”.
  - **Detail** – first detail sheet with Alice’s record.
  - **Detail_1** – second detail sheet with Bob’s record.
  - **Detail_2** – third detail sheet with Carol’s record.

Open the file in Excel and you’ll see each employee on its own sheet, proving that we successfully **create multiple detail sheets** and **save workbook as xlsx file**.

## Common questions & edge‑case handling

| Question | Answer |
|----------|--------|
| *What if I need a custom name for each detail sheet?* | Set `DetailSheetNewName = "Employee_"` and include a column named `SheetName` in the data source. The processor will append the value of `SheetName` to the base name. |
| *Can I keep the original sheet as a summary of all details?* | Yes. The master sheet remains untouched; you can add formulas that reference the generated detail sheets. |
| *What happens when the data source is empty?* | No detail sheets are created, but the workbook still saves. Consider checking `employees.Rows.Count` before processing if you need special handling. |
| *Is it possible to use an existing template file?* | Replace `new Workbook()` with `new Workbook("Template.xlsx")`. All Smart Marker logic works the same way. |

## Conclusion

You now know **how to create Excel workbook programmatically**, how to **create multiple detail sheets** using Smart Markers, and how to **save workbook as xlsx file** with Aspose.Cells. The complete example can be adapted for invoices, reports, or any scenario where a master‑detail Excel output is required.

### Next steps

- Explore other Smart Marker features such as **group markers** and **conditional formatting**.
- Replace the `DataTable` with a real database query to generate large‑scale reports.
- Use `Workbook.Save("output.pdf", SaveFormat.Pdf)` to export the same data to PDF for distribution.

Feel free to experiment with different naming schemes, styling, or additional worksheets—your new programmatic Excel generation skills are ready for production use. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}