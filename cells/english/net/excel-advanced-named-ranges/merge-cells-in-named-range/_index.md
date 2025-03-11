---
title: Merge Cells in Named Range in Excel
linktitle: Merge Cells in Named Range in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to merge cells in a named range using Aspose.Cells for .NET in this step-by-step tutorial. Discover how to format, style, and automate Excel reports.
weight: 11
url: /net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Merge Cells in Named Range in Excel

## Introduction

When working with Excel files programmatically, one of the common tasks you might encounter is merging cells within a named range. Whether you're automating report generation, building dashboards, or simply managing large datasets, merging cells is an essential technique. In this tutorial, we'll explore how to merge cells in a named range using Aspose.Cells for .NET—a powerful library that allows developers to manipulate Excel files without needing Microsoft Excel installed.

## Prerequisites

Before we start, make sure you have the following ready:

- Aspose.Cells for .NET: You can download it from the [Aspose.Cells releases page](https://releases.aspose.com/cells/net/).
- .NET Framework installed on your machine.
- Basic understanding of C#: Familiarity with concepts like classes, methods, and objects will help.

## Import Packages

Before we jump into coding, you need to import the necessary namespaces. These namespaces will give you access to the Aspose.Cells library's functionality.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

With the prerequisites and packages out of the way, let’s move to the fun part: coding!

Here’s a breakdown of how you can merge cells in a named range in an Excel sheet using Aspose.Cells for .NET.

## Step 1: Create a New Workbook

The first thing we need is a workbook. A workbook in Excel terms is the equivalent of an Excel file. Let’s create one.

```csharp
// Instantiate a new Workbook.
Workbook wb1 = new Workbook();
```

By initializing a new workbook, we now have an empty Excel file ready to be manipulated. It’s like starting with a blank canvas!

## Step 2: Access the First Worksheet

Every workbook contains worksheets, and in this case, we want to work with the first one. Let's grab it!

```csharp
// Get the first worksheet in the workbook.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Think of the worksheet as the individual tabs in an Excel file where the actual data lives. By default, we’re accessing the very first tab.

## Step 3: Create a Range of Cells

Now that we have our worksheet, it's time to create a range. A range refers to a block of cells, which can span multiple rows and columns.

```csharp
// Create a range.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Here, we’re selecting cells from D6 to I12—a block that covers multiple rows and columns. We’ll soon be merging this range!

## Step 4: Name the Range

Naming a range makes it easier to reference later, especially when dealing with large datasets.

```csharp
// Name the range.
mrange.Name = "TestRange";
```

By naming this range "TestRange," we can quickly retrieve it later in the code, without needing to specify the cell coordinates again.

## Step 5: Merge the Range of Cells

Now for the magic—merging the cells within the range we just created!

```csharp
// Merge the cells of the range.
mrange.Merge();
```

This step merges all the cells from D6 to I12 into one single cell. Perfect for things like titles or summaries!

## Step 6: Retrieve the Named Range

Once the cells are merged, we may want to apply some formatting. Let’s first retrieve our named range.

```csharp
// Get the range.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Retrieving the range by name allows us to perform further operations, like adding styles or inputting data.

## Step 7: Define a Style for the Merged Cells

What good is a merged cell if it doesn’t look polished? Let’s create a style object to align the text and apply a background color.

```csharp
// Define a style object.
Style style = wb1.CreateStyle();

// Set the alignment.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Here, we're aligning the text both horizontally and vertically in the center, and setting a light blue (aqua) background color. Stylish, right?

## Step 8: Apply the Style to the Range

After defining the style, it’s time to apply it to the merged range.

```csharp
// Create a StyleFlag object.
StyleFlag flag = new StyleFlag();

// Make the relative style attribute ON.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Apply the style to the range.
range1.ApplyStyle(style, flag);
```

The `StyleFlag` tells Aspose.Cells which style properties to apply—alignment, shading, etc. This gives you granular control over how the style is applied.

## Step 9: Input Data Into the Merged Range

What’s a formatted range without content? Let’s add some text.

```csharp
// Input data into the range.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

This places the text "Welcome to Aspose APIs" into the first cell of our merged range. With the cell being merged, this text will span across all the cells from D6 to I12.

## Step 10: Save the Excel File

Finally, let’s save the workbook as an Excel file.

```csharp
// Save the Excel file.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Here, the workbook is saved with the name "outputMergeCellsInNamedRange.xlsx" in your specified directory.

## Conclusion

And there you have it! You’ve successfully merged cells in a named range, applied some beautiful formatting, and even input some data—all with Aspose.Cells for .NET. Whether you're working on automating reports, manipulating Excel files, or just learning new techniques, this step-by-step guide should give you the foundation you need.

## FAQ's

### Can I merge multiple non-contiguous ranges in Aspose.Cells?  
No, you can only merge contiguous cells in Aspose.Cells.

### Can I undo a merge operation programmatically?  
Once cells are merged, you can unmerge them using the `UnMerge()` method in Aspose.Cells.

### Does merging cells remove the data in them?  
If there is any data in the cells before merging, it will retain the data from the first cell of the range.

### Can I apply different styles to individual cells within a merged range?  
No, a merged range acts as a single cell, so you cannot apply different styles to individual cells within it.

### How do I access a merged cell after merging?  
After merging, you can still access the merged cell using its top-left corner’s coordinates.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
