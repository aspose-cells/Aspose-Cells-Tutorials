---
title: Customizing Display Formats with User-Defined Numbers
linktitle: Customizing Display Formats with User-Defined Numbers
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to customize display formats with Aspose.Cells for .NET. Format dates, percentages, and currency using this step-by-step guide.
weight: 11
url: /net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Customizing Display Formats with User-Defined Numbers

## Introduction
Working with Excel files often requires custom formatting of cells to present data in a more meaningful and user-friendly way. Imagine you’re building an Excel file for a report. You don’t just want raw numbers. You want dates, percentages, and currencies to look sleek and professional, right? That's where custom display formats come into play. In this tutorial, we’re diving deep into Aspose.Cells for .NET to show you how to customize the display format of numbers using user-defined settings.
## Prerequisites
Before you begin, make sure you’ve got everything ready to follow along with this tutorial. Here’s what you’ll need:
- Aspose.Cells for .NET installed. [Download it here](https://releases.aspose.com/cells/net/).
- Basic knowledge of C# and .NET framework.
- A valid license for Aspose.Cells. If you don't have one, grab a [free trial](https://releases.aspose.com/) or request a [temporary license](https://purchase.aspose.com/temporary-license/).
- An IDE like Visual Studio.
- .NET Framework 4.0 or higher.
If you’re missing anything, don’t worry. You can always revisit these links to download the necessary files or seek help from the [Aspose support forum](https://forum.aspose.com/c/cells/9).
## Import Namespaces
Before jumping into the code, you need to import the required namespaces to access all the necessary Aspose.Cells functionalities.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
These two namespaces will be your core tools in this tutorial. Now, let's move on to the fun part:
## Step 1: Setting Up the Project Directory
First, you need a place to store your files, right? Let’s create a directory to save the output Excel file. In this step, we’ll also make sure the directory exists before saving anything.
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- We’re defining a `dataDir` variable to store the path where the output Excel file will go.
- We then check if the directory exists using `System.IO.Directory.Exists()`.
- If the directory doesn’t exist, it will be created using `System.IO.Directory.CreateDirectory()`.
## Step 2: Create a New Workbook and Add a Worksheet
Now that we’ve got our directory, let’s create a new Excel workbook and add a worksheet to it.
```csharp
// Instantiating a Workbook object
Workbook workbook = new Workbook();
// Adding a new worksheet to the Excel object
int i = workbook.Worksheets.Add();
// Obtaining the reference of the newly added worksheet by passing its sheet index
Worksheet worksheet = workbook.Worksheets[i];
```
- First, we create a new `Workbook` object. Think of this as your Excel file.
- We add a new worksheet to this workbook using the `Add()` method and store the index in variable `i`.
- We reference this worksheet using the `workbook.Worksheets[i]`.
## Step 3: Adding Date to a Cell and Customizing Its Format
Now, let’s insert the current date into a cell and format it to display in a custom way. Instead of the default date format, we’ll set a custom format like `d-mmm-yy`.
```csharp
// Adding the current system date to "A1" cell
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Getting the style of A1 cell
Style style = worksheet.Cells["A1"].GetStyle();
// Setting the custom display format to show date as "d-mmm-yy"
style.Custom = "d-mmm-yy";
// Applying the style to A1 cell
worksheet.Cells["A1"].SetStyle(style);
```
- We add the current system date to cell `A1` using `PutValue(DateTime.Now)`.
- We retrieve the current style of cell `A1` using `GetStyle()`.
- We modify the cell’s style by setting `style.Custom = "d-mmm-yy"`, which formats the date to show the day, abbreviated month, and year.
- Finally, we apply the new style to the cell with `SetStyle()`.
## Step 4: Formatting a Cell as a Percentage
Next up, let’s work with numbers. We’ll add a numeric value to another cell, say `A2`, and format it as a percentage.
```csharp
// Adding a numeric value to "A2" cell
worksheet.Cells["A2"].PutValue(20);
// Getting the style of A2 cell
style = worksheet.Cells["A2"].GetStyle();
// Setting the custom display format to show value as percentage
style.Custom = "0.0%";
// Applying the style to A2 cell
worksheet.Cells["A2"].SetStyle(style);
```
- We add the value `20` to cell `A2`.
- We retrieve the style of cell `A2` and set the custom format to `0.0%` to display the value as a percentage (i.e., 20%).
- Lastly, we apply the style to the cell using `SetStyle()`.
## Step 5: Formatting a Cell as Currency
Let’s add another value, say to cell `A3`, and format it to display as currency. To make things more interesting, we’ll use a format that displays positive values as currency in pounds and negative values in dollars.
```csharp
// Adding a numeric value to "A3" cell
worksheet.Cells["A3"].PutValue(2546);
// Getting the style of A3 cell
style = worksheet.Cells["A3"].GetStyle();
// Setting the custom display format to show value as currency
style.Custom = "£#,##0;[Red]$-#,##0";
// Applying the style to A3 cell
worksheet.Cells["A3"].SetStyle(style);
```
- We add the value `2546` to cell `A3`.
- We set a custom format `£#,##0;[Red]$-#,##0`, which displays positive values with a pound sign and negative values in red with a dollar sign.
- We apply the style to the cell using `SetStyle()`.
## Step 6: Saving the Workbook
The final step is to save the workbook as an Excel file. We’ll use the Excel 97-2003 format for this tutorial.
```csharp
// Saving the Excel file
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- The `Save()` method saves the workbook in the specified directory.
- We choose `SaveFormat.Excel97To2003` to ensure compatibility with older versions of Excel.
## Conclusion
There you have it! We just created an Excel file, added custom date, percentage, and currency formats to specific cells using Aspose.Cells for .NET, and saved the file. Custom formatting makes your Excel files much more readable and professional. Don’t forget to explore other formatting options in Aspose.Cells, like conditional formatting, for even more control over how your data looks.
## FAQ's
### How can I apply more complex formatting options in Aspose.Cells?
You can combine different formatting styles, such as font color, borders, and background colors, with custom number formats.
### Can I apply a custom number format to a range of cells?
Yes, Aspose.Cells allows you to apply a style to a range of cells using the `Range.SetStyle()` method.
### What other file formats can I save the workbook in?
Aspose.Cells supports many formats, including XLSX, CSV, and PDF. Simply change the `SaveFormat` in the `Save()` method.
### Can I format negative numbers differently?
Absolutely! You can use custom number formats to display negative numbers with different colors or symbols.
### Is Aspose.Cells for .NET free?
Aspose.Cells offers a free trial, but for full functionality, you will need a valid license. You can get a [temporary license here](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
