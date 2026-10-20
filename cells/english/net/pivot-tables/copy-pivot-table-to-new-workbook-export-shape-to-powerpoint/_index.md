---
category: general
date: 2026-10-20
description: Copy pivot table to new workbook using Aspose.Cells and learn how to
  export an editable shape to PowerPoint in a single guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: en
lastmod: 2026-10-20
og_description: Copy pivot table to new workbook using Aspose.Cells and export an
  editable shape to PowerPoint—step‑by‑step code you can run today.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Copy pivot table to new workbook, export shape to PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Copy pivot table to new workbook, export shape to PowerPoint
url: /net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table to new workbook, export shape to PowerPoint

If you need to **copy pivot table to new workbook** while preserving its functionality, this guide shows you exactly how to do it with Aspose.Cells. You’ll also see the quickest way to **export an editable shape to PowerPoint**, so the textbox remains editable after the conversion.

Many developers assume that copying a range that contains a pivot table will lose the pivot logic, or that shapes become static images when saved as PPTX. This tutorial disproves those myths and gives you a reliable, production‑ready solution.

In the following sections you will:

* Load a source workbook and copy a range that includes a pivot table.
* Create a destination workbook that contains the same pivot table.
* Add a textbox shape, modify its text, and save the workbook as a PowerPoint presentation where the textbox stays editable.
* Understand why each API call is required and how to avoid common pitfalls.

**Prerequisites**

* .NET 6.0 or later (the code also works with .NET Framework 4.7+).
* Aspose.Cells for .NET installed (`Install-Package Aspose.Cells`).
* Basic knowledge of C# and Visual Studio (or any IDE you prefer).

---

## Copy pivot table to new workbook

This step‑by‑step section demonstrates how to copy a range that contains a pivot table and retain the pivot definition in the new file.

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` is the entry point for any Excel manipulation in Aspose.Cells. Selecting the correct worksheet ensures we work with the exact pivot table location.

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
The pivot table lives inside a specific block of cells. By specifying a `CellArea` that fully encloses the pivot, Aspose.Cells knows to copy the underlying pivot cache as well.

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
A fresh workbook guarantees no conflicting named ranges or existing pivots, making the copy operation clean.

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` is part of the **Aspose.Cells copy rows** API. It copies both cell values and the hidden pivot cache, so the pivot table remains functional after the move.

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Open `CopyWithPivot.xlsx` in Excel. The pivot table appears exactly as it did in the source file, and you can refresh or modify it normally.

---

## Export editable shape to PowerPoint

Now we’ll add a textbox shape, change its content, and save the workbook as a PPTX file. The shape stays fully editable when opened in PowerPoint.

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` creates a **editable textbox in PowerPoint**‑compatible shape. The coordinates are in points; adjust them to fit your layout.

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
Directly accessing the `Shape` object lets you change properties such as `Text`, `Font`, or `Fill`. This step demonstrates how to programmatically set the initial content.

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Open `Presentation.pptx` in Microsoft PowerPoint. The textbox appears on the first slide, and you can double‑click it to edit the text just like any native PowerPoint shape.

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | A worksheet containing the original pivot table, fully functional (refresh works). |
| `Presentation.pptx` | A single slide with an editable textbox that reads “Change me in PowerPoint”. |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – If you only copy cell values (e.g., using `CopyRows` with the `PasteOptions` flag set to `PasteValues`), the pivot cache is omitted and the table becomes static. Always use the default `CopyRows` overload as shown.
* **Shape positioning** – `AddTextBox` uses point units, not Excel cell indices. Test the coordinates on a sample file to avoid off‑slide placement.
* **File format mismatch** – Saving a workbook as PPTX with `SaveFormat.Pptx` automatically converts all supported shapes. Attempting to save as `Pdf` will rasterize the shape, making it non‑editable.

---

## Conclusion

You now know how to **copy pivot table to new workbook** and how to **export an editable shape to PowerPoint** using Aspose.Cells for .NET. The complete, runnable code examples cover every required API call, explain why each step matters, and show the expected results.

Next, you might explore:

* **Working with charts** – copy charts together with pivot tables (`Aspose.Cells copy rows between worksheets`).
* **


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}