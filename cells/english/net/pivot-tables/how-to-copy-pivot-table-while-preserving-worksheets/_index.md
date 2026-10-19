---
category: general
date: 2026-09-15
description: Learn how to copy pivot table, copy worksheet with pivot, and save workbook
  as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: en
lastmod: 2026-09-15
og_description: How to copy pivot table, copy worksheet with pivot, and save workbook
  as pptx using Aspose.Cells. Follow the complete, runnable C# examples.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: How to copy pivot table and export worksheets – full C# guide
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to copy pivot table while preserving worksheets
url: /net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot table while preserving worksheets

If you need to **how to copy pivot table** from one workbook to another without losing the underlying pivot cache, this guide provides a ready‑to‑run solution. You’ll also see how to **copy worksheet with pivot** and how to **save workbook as pptx** while keeping editable text boxes intact. All examples use the latest Aspose.Cells for .NET, so you can drop the code into any C# project and see immediate results.

Working with Excel files programmatically often involves moving data between workbooks, exporting to presentations, or inserting complex Smart Markers. The three code snippets below cover those common scenarios and explain why each step matters.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* Aspose.Cells for .NET (version 25.11 or newer) referenced in your project  
* A folder named `YOUR_DIRECTORY` where the sample files will be read from and written to  

No additional NuGet packages are required.

---

## How to copy pivot table with Aspose.Cells

Copying a range that contains a pivot table while preserving the pivot cache is a frequent requirement. The following steps demonstrate the exact sequence you need.

### Step 1 – Load the source workbook that holds the pivot table

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Why*: Aspose.Cells reads the workbook into memory, giving you access to worksheets, cells, and pivot tables.

### Step 2 – Create an empty destination workbook

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Why*: Starting with a blank workbook guarantees that no hidden styles or named ranges interfere with the copy operation.

### Step 3 – Copy the rows that include the pivot table

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Why*: `CopyRows` copies the raw cell values, formats, and underlying pivot cache references. The range must include the entire pivot table area.

### Step 4 – Copy the columns that contain the pivot table

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Why*: Pivot tables span both rows and columns; copying columns ensures the full table layout is retained.

### Step 5 – Transfer the prepared sheet into the destination workbook

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Why*: The `Copy` method clones the worksheet, including the pivot cache, so the destination workbook shows an identical pivot table.

### Step 6 – Save the result – the pivot table remains intact

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Why*: Persisting the workbook writes all internal structures, guaranteeing that the pivot can be refreshed later.

**Pro tip**: After copying, you can call `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` to update the data if the source data changed.

---

## Copy worksheet with pivot – a concise alternative

If you simply need to duplicate an entire worksheet that already contains a pivot table, you can skip the row/column copy steps and use the worksheet‑level `Copy` method directly.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

This approach is useful when the worksheet does not contain extra data outside the pivot area. The **copy worksheet with pivot** operation preserves all formatting, named ranges, and pivot caches automatically.

---

## Save workbook as PPTX with editable text boxes

Exporting an Excel sheet that contains an editable textbox to PowerPoint can be required for reporting dashboards. The code below shows **save workbook as pptx** while keeping the textbox editable.

### Step 1 – Load the workbook that includes the textbox

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Step 2 – Configure PPTX save options

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Why*: Setting `ExportEditableTextBox` tells Aspose.Cells to translate the Excel textbox into a PowerPoint shape that remains editable after export.

### Step 3 – Save the workbook as PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Expected result**: Open `Result.pptx` in PowerPoint, select the textbox, and edit its content just like any native shape.

**Common question**: *What if I need to keep the textbox locked?*  
Set `pptxOptions.ExportEditableTextBox = false`; the shape will be converted to a static image instead.

---

## Export a Smart Marker that contains a JSON array as a single cell value

Smart Markers let you populate Excel templates with complex data structures. Below is a complete example that demonstrates **how to copy pivot table**‑style data handling while inserting a JSON array into a single cell.

### Step 1 – Prepare the SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Step 2 – Insert a Smart Marker into cell A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Step 3 – Define the data source with a JSON‑style array

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Step 4 – Process the workbook

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Step 5 – Save the resulting workbook

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Result verification**: Open `JsonSingleCell.xlsx` and confirm that cell A1 reads `A,B,C`. This demonstrates how to treat a collection as a single cell value, a pattern often needed when exporting data for downstream systems.

---

## Full working example

Below is a single program that combines the three scenarios. You can copy the code into a console app, adjust the file paths, and run it to see all three outputs.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Running this program produces:

* `CopyWithPivot.xlsx` – a perfect copy of the original pivot table.  
* `Result.pptx` – a PowerPoint slide with an editable textbox.  
* `JsonSingleCell.xlsx` – a sheet where the JSON array appears in a single cell.

---

## Conclusion

You now know **how to copy pivot table** safely, how to **copy worksheet with pivot** in a single call, and how to **save workbook as pptx** while preserving editable text boxes. These patterns cover the most common Excel‑to‑PowerPoint and Excel‑to‑JSON workflows you’ll encounter in enterprise automation projects.

Next, consider exploring:

* Refreshing copied pivot tables programmatically (`PivotTable.Refresh()`)  
* Exporting to other formats such as PDF or HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Using advanced Smart Marker options like custom functions or conditional formatting  

Feel free to experiment with different ranges, multiple worksheets, or larger JSON structures. The Aspose.Cells API gives you fine‑grained control, so you can adapt these examples to any real‑world scenario. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}