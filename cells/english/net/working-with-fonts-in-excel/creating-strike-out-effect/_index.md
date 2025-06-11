---
title: Creating Strike Out Effect on Text in Excel
linktitle: Creating Strike Out Effect on Text in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to apply a strikeout effect on text in Excel with Aspose.Cells for .NET in this detailed step-by-step tutorial.
weight: 15
url: /net/working-with-fonts-in-excel/creating-strike-out-effect/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Creating Strike Out Effect on Text in Excel

## Introduction
When it comes to Excel, visual elements are just as important as the data itself. Whether you're highlighting important changes or marking items that are no longer relevant, the strikeout effect on text is a classic way to manage visual representation in spreadsheets. In this guide, we will walk you through the process of implementing a strikeout effect on text in Excel using Aspose.Cells for .NET. This tutorial will not only cover the necessary prerequisites but will also provide a step-by-step approach to ensure you can replicate this effect with ease.
## Prerequisites
Before diving into the tutorial, make sure you have the following prerequisites met:
1. Development Environment: You should have a .NET development environment set up. This could be Visual Studio or any other IDE you prefer that supports .NET development.
2. Aspose.Cells for .NET: Ensure that you have Aspose.Cells installed in your project. You can download it from the following link: [Download Aspose.Cells](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: A fundamental understanding of C# programming is helpful as the examples will be coded in C#.
4. .NET Framework: Ensure that your project is targeting a compatible .NET Framework version, usually .NET Core or .NET Framework 4.5 and above.
## Import Packages
Before you write any code, you need to import the required namespaces from Aspose.Cells. This is crucial for accessing various features provided by the library. Here’s how you can import the necessary namespaces:
```csharp
using System.IO;
using Aspose.Cells;
```
With these imports, you’ll have access to the Workbook, Worksheet, and Style classes that will be used throughout this tutorial.
Now that we have set the stage, let's break down the process into manageable steps. Each step will be accompanied by clear instructions to guide you through creating a strikeout effect on text in Excel.
## Step 1: Define the Document Directory
Start by defining the path where your Excel documents will be stored. This will be the location for saving your output files.
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual directory path where you want to save your Excel file. This sets up the directory for your output.
## Step 2: Create the Directory
Next, you need to ensure that the directory you specified in the previous step exists. If it doesn't exist, you can create it programmatically.
```csharp
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
This code checks whether the directory exists and creates it if not. This helps in avoiding errors when you try to save your file later on.
## Step 3: Instantiate a Workbook Object
Now, it’s time to create a new Workbook object. This is the foundation of your Excel file where you will be adding data and applying formats.
```csharp
// Instantiating a Workbook object
Workbook workbook = new Workbook();
```
The `Workbook` class represents an Excel file. By creating an instance of this class, you are essentially creating a new Excel document.
## Step 4: Add a New Worksheet
Each workbook can contain multiple worksheets. Let's go ahead and create a new worksheet in your workbook.
```csharp
// Adding a new worksheet to the Excel object
int i = workbook.Worksheets.Add();
```
The `Add` method of the `Worksheets` collection adds a new worksheet to the workbook and returns its index. 
## Step 5: Obtain the Reference of the New Worksheet
Once you have created the worksheet, you need to reference it for future operations.
```csharp
// Obtaining the reference of the newly added worksheet by passing its sheet index
Worksheet worksheet = workbook.Worksheets[i];
```
Here, you are fetching the newly created worksheet using its index (`i`). This gives you access to manipulate the worksheet.
## Step 6: Access a Cell
You’ll want to access a specific cell in your worksheet where you will apply the strikeout format. In this example, we’re using cell `A1`.
```csharp
// Accessing the "A1" cell from the worksheet
Aspose.Cells.Cell cell = worksheet.Cells["A1"];
```
In Excel, cells are referred to by their column and row identifiers (e.g., "A1"). We’re obtaining a reference to cell `A1` for further manipulation.
## Step 7: Add Value to the Cell
Next, let’s insert some text into the cell. We’ll write “Hello Aspose!” in cell `A1`.
```csharp
// Adding some value to the "A1" cell
cell.PutValue("Hello Aspose!");
```
The `PutValue` method is used to assign a string value to the cell. You can modify this string to anything you want to be displayed.
## Step 8: Obtain the Style of the Cell
Now that we have text in our cell, it’s time to access the cell’s style to apply our desired formatting, including the strikeout effect.
```csharp
// Obtaining the style of the cell
Style style = cell.GetStyle();
```
The `GetStyle` method retrieves the current style of the cell, allowing you to modify properties like font type, size, and effects.
## Step 9: Set the Strikeout Effect
Let’s apply the strikeout effect to the text in the cell. We will modify the font style of the cell.
```csharp
// ExStart:SetStrikeout
// Setting the strike out effect on the font
style.Font.IsStrikeout = true;
// ExEnd:SetStrikeout
```
By setting `IsStrikeout` to true, you’re instructing Excel to visually cross out the text in the selected cell strikethrough - much like visually marking something off a list.
## Step 10: Apply the Style to the Cell
After modifying the style, you need to apply it back to the cell to reflect the changes.
```csharp
// Applying the style to the cell
cell.SetStyle(style);
```
The `SetStyle` method updates the cell with the new style, which now includes the strikeout formatting.
## Step 11: Save the Excel File
Finally, it’s time to save your workbook to the specified directory. In this example, we’re saving the file with the name `book1.out.xls`.
```csharp
// Saving the Excel file
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
The `Save` method writes the workbook to the disk in the 97-2003 Excel format. You can specify different formats if needed.
## Conclusion
Creating a strikeout effect on text in Excel using Aspose.Cells for .NET is a straightforward process when you break it down step by step. By following this guide, you now have the skills to enhance your spreadsheets with visual cues, making your data not only informative but also visually engaging.
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful library for managing Excel files in .NET applications, enabling you to create, manipulate, and convert Excel documents programmatically.
### Can I use Aspose.Cells for free?
Yes, you can use it for free during a trial period. A free trial is available at [Aspose.Cells Free Trial](https://releases.aspose.com/).
### How do I purchase Aspose.Cells?
You can purchase a license for Aspose.Cells through their website [Buy Aspose.Cells](https://purchase.aspose.com/buy).
### Are there examples available for using Aspose.Cells?
Yes, you can find plenty of examples and code snippets in the [Aspose.Cells Documentation](https://reference.aspose.com/cells/net/).
### Where can I get support for Aspose.Cells?
You can get community support and help from the [Aspose Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
