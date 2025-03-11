---
title: Ungroup Rows and Columns in Excel with Aspose.Cells
linktitle: Ungroup Rows and Columns in Excel with Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to ungroup rows and columns in Excel using Aspose.Cells for .NET with this comprehensive guide. Simplify your Excel data manipulation.
weight: 15
url: /net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ungroup Rows and Columns in Excel with Aspose.Cells

## Introduction
When it comes to handling Excel files, you may find yourself in situations where you need to ungroup rows and columns. Whether you're cleaning up a spreadsheet or reformatting data for better presentation, Aspose.Cells for .NET is a fantastic tool that simplifies the process. In this tutorial, I’ll guide you through the steps to ungroup rows and columns in Excel using Aspose.Cells. By the end, you'll have a solid understanding of how to work with Excel files programmatically.
## Prerequisites
Before diving into the code, let's ensure you have everything set up. Here’s what you’ll need:
1. Visual Studio: You should have a working version of Visual Studio installed on your machine. If you don’t have it yet, you can download it from [Visual Studio’s site](https://visualstudio.microsoft.com/).
2. Aspose.Cells for .NET: You will need to download the Aspose.Cells library. You can grab it from the [Aspose Releases page](https://releases.aspose.com/cells/net/). Ensure you have the necessary licenses, which can be purchased or obtained through a [temporary license](https://purchase.aspose.com/temporary-license/).
3. Basic Knowledge of C#: A foundational understanding of C# programming will help you follow along more easily.
Once you have everything ready, we can jump into the fun part: the code!
## Import Packages
To get started, you need to import the necessary packages in your C# project. Here’s how you do it:
1. Open your project in Visual Studio.
2. Add a reference to the Aspose.Cells library. You can do this by right-clicking on the References in your project and selecting Add Reference. Browse to the location where you saved the Aspose.Cells DLL.
3. At the top of your C# file, add the following using directives:
```csharp
using System.IO;
using Aspose.Cells;
```
Now that everything is set up, let’s walk through the steps to ungroup rows and columns in your Excel sheet. 
## Step 1: Define the Document Directory
First, you need to specify the directory where your Excel file is located. You can set this up as follows:
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path on your computer where the Excel file is saved. 
## Step 2: Create a File Stream
Next, you need to create a file stream to open the Excel file. This is how you can do that:
```csharp
// Creating a file stream containing the Excel file to be opened
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Here, you’re opening the file named `book1.xls`. Make sure this file exists in your specified directory, or else you’ll run into a file not found error.
## Step 3: Instantiate a Workbook Object
Now, let’s load the Excel file into a Workbook object. This allows you to manipulate the workbook programmatically:
```csharp
// Instantiating a Workbook object
// Opening the Excel file through the file stream
Workbook workbook = new Workbook(fstream);
```
With this line of code, you've successfully loaded the Excel file into memory and are ready to work with it.
## Step 4: Access the Worksheet
After you have the workbook, the next step is to access the specific worksheet where you want to ungroup rows and columns. Here’s how to do that:
```csharp
// Accessing the first worksheet in the Excel file
Worksheet worksheet = workbook.Worksheets[0];
```
In this case, we’re accessing the first worksheet. If your data is on a different sheet, you can change the index accordingly.
## Step 5: Ungroup Rows
Now comes the exciting part! Let’s ungroup the first six rows (from row 0 to row 5). Use the following code:
```csharp
// Ungrouping first six rows (from 0 to 5)
worksheet.Cells.UngroupRows(0, 5);
```
This method removes any grouping that has been applied to the specified rows. It’s as easy as that!
## Step 6: Ungroup Columns
Just like rows, you can ungroup columns as well. Here’s how to ungroup the first three columns (from column 0 to column 2):
```csharp
// Ungrouping first three columns (from 0 to 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Step 7: Save the Modified Excel File
Once you’ve ungrouped the rows and columns, the next step is to save the changes back to an Excel file. You can do this by using the `Save` method:
```csharp
// Saving the modified Excel file
workbook.Save(dataDir + "output.xls");
```
In this example, we’re saving the modified file as `output.xls`. You can change the filename to whatever you prefer.
## Step 8: Close the File Stream
Finally, to free up resources, you should close the file stream:
```csharp
// Closing the file stream to free all resources
fstream.Close();
```
This is a good practice to ensure that your application doesn’t hold onto file handles longer than necessary.
## Conclusion
And there you have it! You’ve successfully learned how to ungroup rows and columns in an Excel file using Aspose.Cells for .NET. With just a few lines of code, you can make significant changes to your Excel files programmatically. Whether you’re automating reports or preparing data for analysis, mastering these techniques can save you a ton of time.
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful library for working with Excel files in .NET applications, allowing for easy manipulation, conversion, and creation of spreadsheets.
### Can I ungroup rows and columns in Excel using other libraries?
Yes, there are other libraries available for Excel manipulation in .NET, but Aspose.Cells offers extensive features and ease of use.
### Is there a way to undo changes after saving?
Once you save an Excel file, the previous state cannot be restored unless you have a backup of the original file.
### How do I get support for Aspose.Cells?
You can find support by visiting the [Aspose Support forum](https://forum.aspose.com/c/cells/9), where you can ask questions and find solutions.
### Can I use Aspose.Cells without a license?
Yes, you can use Aspose.Cells for free with certain limitations, and you can start with a [temporary license](https://purchase.aspose.com/temporary-license/) for full functionality.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
