---
title: Using Built-In Number Formats in Excel Programmatically
linktitle: Using Built-In Number Formats in Excel Programmatically
second_title: Aspose.Cells .NET Excel Processing API
description: Automate number formatting in Excel using Aspose.Cells for .NET. Learn how to apply date, percentage, and currency formats programmatically.
weight: 10
url: /net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Using Built-In Number Formats in Excel Programmatically

## Introduction
In this tutorial, we’ll walk you through how to use built-in number formats in Excel using Aspose.Cells for .NET. We’ll cover everything from setting up your environment to applying different formats such as dates, percentages, and currencies. Whether you're a seasoned pro or just dipping your toes into the .NET ecosystem, this guide will have you formatting Excel cells like a breeze.
## Prerequisites
Before diving in, make sure you have the following:
- Aspose.Cells for .NET library installed. You can [download it here](https://releases.aspose.com/cells/net/).
- A working knowledge of C# and basic .NET programming.
- Visual Studio or any .NET IDE installed on your machine.
- A valid Aspose license or [temporary license](https://purchase.aspose.com/temporary-license/).
- .NET framework installed (version 4.0 or higher).
  
If you’re missing any of the above, follow the links provided to set everything up. Ready? Let’s jump into the fun part!
## Import Packages
Before we get started with the tutorial, make sure to import the necessary namespaces for working with Aspose.Cells for .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Once you've imported these, you're all set to manipulate Excel files programmatically. Now, let's dive into the step-by-step guide!
## Step 1: Create or Access Your Excel Workbook
In this step, you will create a new workbook. Think of this as opening a new Excel file, except you’re doing it through code!
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instantiating a Workbook object
Workbook workbook = new Workbook();
```
Here, we’re simply instantiating a new `Workbook` object. This acts as your Excel file, ready for data manipulation. You can also load an existing file by providing its path.
## Step 2: Access the Worksheet
Excel workbooks can contain multiple worksheets. In this step, we’ll access the first worksheet in your workbook:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
We are now accessing the first worksheet in the workbook. If you need to manipulate additional sheets, you can reference them using their index or name.
## Step 3: Add Data to Cells
Let’s start adding some data to specific cells. First, we’ll insert the current system date into cell "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
This line inserts the current date into cell A1. Pretty cool, right? Imagine doing this manually for hundreds of cells—it’d be a nightmare. Now, we’ll move on to formatting!
## Step 4: Format Date in Cell "A1"
Next, let’s format that date in a more readable format, like "15-Oct-24". This is where Aspose.Cells really shines:
1. Retrieve the Cell's Style:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Here, we're grabbing the style of cell A1. Think of this as grabbing the cell’s "fashion" before making any tweaks.
2. Set the Date Format:
```csharp
style.Number = 15;
```
Setting the `Number` property to 15 applies the desired date format. This is a built-in number format code for displaying dates in the format "d-mmm-yy".
3. Apply the Style to the Cell:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
This line applies the style changes to the cell. Now, instead of a default date format, you'll see something much more user-friendly like "15-Oct-24."
## Step 5: Add and Format a Percentage in Cell "A2"
Let’s move on to formatting percentages. Imagine you want to insert a value and display it as a percentage. In this step, we’ll add a numeric value to cell "A2" and format it as a percentage:
1. Insert Numeric Value:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
This inserts the number 20 into cell A2. You might be thinking, "That’s just a plain number—how do I turn it into a percentage?" Well, we’re about to get to that.
2. Retrieve the Style and Set Percentage Format:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Format as percentage
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Here, we’re adding 2546 to cell A3. Next, we’ll format this number to show up as currency.
2. Retrieve the Style and Set Currency Format:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Format as currency
worksheet.Cells["A3"].SetStyle(style);
```
Setting the `Number` property to 6 applies the currency format. Now the value in cell A3 will display as "2,546.00," complete with commas and two decimal places.
## Step 7: Save the Excel File
Now that we’ve applied all the formatting magic, it’s time to save the file:
```csharp
// Saving the Excel file
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
This line saves the Excel file in the Excel 97-2003 format. You can change the `SaveFormat` to suit your needs. And just like that, you’ve created and formatted an Excel file programmatically!
## Conclusion
Congratulations! You’ve successfully learned how to use Aspose.Cells for .NET to apply built-in number formats to cells in an Excel file. From dates to percentages and currencies, we’ve covered some of the most common formatting needs for Excel data processing. Now, instead of manually formatting cells, you can automate the entire process—saving you time and reducing errors.
## FAQ's
### Can I apply custom number formats using Aspose.Cells for .NET?
Yes! In addition to built-in formats, Aspose.Cells also supports custom number formats. You can create highly specific formats using the `Custom` property in the `Style` class.
### How can I format a cell as a currency with a specific symbol?
To apply a specific currency symbol, you can use custom formatting by setting the `Style.Custom` property.
### Can I format entire rows or columns?
Absolutely! You can apply styles to entire rows or columns using the `Rows` or `Columns` collections in the `Worksheet` object.
### How can I format multiple cells at once?
You can use the `Range` object to select multiple cells and apply styles to them all at once.
### Do I need Microsoft Excel installed to use Aspose.Cells?
No, Aspose.Cells works independently of Microsoft Excel, so you don't need Excel installed on your machine.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
