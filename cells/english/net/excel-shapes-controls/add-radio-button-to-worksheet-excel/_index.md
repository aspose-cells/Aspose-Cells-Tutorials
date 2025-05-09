---
title: Add Radio Button to Worksheet in Excel
linktitle: Add Radio Button to Worksheet in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to add radio buttons to an Excel worksheet using Aspose.Cells for .NET with this easy step-by-step guide. Perfect for creating interactive Excel forms.
weight: 19
url: /net/excel-shapes-controls/add-radio-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Add Radio Button to Worksheet in Excel

## Introduction
Ever wondered how to spice up your Excel sheets with interactive elements like radio buttons? Whether you’re building a survey, a form, or an analysis tool, adding radio buttons can really enhance user interaction. In this tutorial, we'll walk you through the process of adding radio buttons to your Excel sheets using Aspose.Cells for .NET. We’ll break everything down into easy-to-follow steps, ensuring you’ll be a pro by the end of this article. Ready to dive in? Let’s get started!
## Prerequisites
Before we jump into the fun part of adding radio buttons, let’s ensure you have everything set up to get started.
1. Aspose.Cells for .NET: First, make sure you’ve downloaded and installed the [Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) library. You can grab it via NuGet in Visual Studio or from the download page.
2. IDE (Integrated Development Environment): You’ll need an IDE like Visual Studio to write and execute your C# code.
3. .NET Framework: Ensure you have .NET Framework 4.0 or above installed on your machine. Aspose.Cells requires this to work.
4. Basic Understanding of C#: Familiarity with C# syntax and .NET programming will make things easier as you follow along.
Once you’ve got everything in place, we’re ready to roll!
## Import Packages
Before coding, it's essential to import the necessary namespaces to avoid any errors later on. Add the following to your code:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
These imports are essential for accessing workbook functionalities, adding radio buttons, and handling file operations.
## Step 1: Setting Up the Workbook
First things first, let’s create a new Excel workbook.
To begin, you’ll need to instantiate a new `Workbook` object. This will represent your Excel file in code.
```csharp
// Instantiate a new Workbook.
Workbook excelbook = new Workbook();
```
In this step, you're creating a blank workbook. Imagine it as your blank canvas where you'll add radio buttons in subsequent steps.
## Step 2: Adding and Formatting a Cell Value
Next, let’s add a title to the worksheet. We’ll add some text to cell `C2` and format it to make it bold. This step adds context to your radio buttons.
### Insert Text in Cell
```csharp
// Insert a value in cell C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Make the Text Bold
```csharp
// Set the font text in cell C2 to bold.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
Here, we’ve added a simple title, “Age Groups,” in cell `C2`, and made it bold so it stands out. Easy, right?
## Step 3: Adding the First Radio Button
Now comes the exciting part: adding your first radio button to the worksheet!
### Add a Radio Button
```csharp
// Add a radio button to the first sheet.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
This line adds the radio button to a specific position on your worksheet. The numbers represent its placement and size. Think of it like setting the button’s X and Y coordinates.
### Set Radio Button Text
```csharp
// Set its text string.
radio1.Text = "20-29";
```
Here, we’ve given the radio button a label, “20-29,” representing an age group.
### Link the Radio Button to a Cell
```csharp
// Set A1 cell as a linked cell for the radio button.
radio1.LinkedCell = "A1";
```
This links the radio button to cell `A1`, meaning the result of the button selection will be stored in that cell.
### Add 3D Effect
```csharp
// Make the radio button 3-D.
radio1.Shadow = true;
```
Because we want this radio button to pop, we’ve added a 3D effect.
### Customize the Radio Button’s Line
```csharp
// Set the weight of the radio button line.
radio1.Line.Weight = 4;
// Set the dash style of the radio button line.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
These lines of code adjust the thickness and dash style of the radio button’s border to make it more visually appealing.
## Step 4: Adding Additional Radio Buttons
Let’s add two more radio buttons for the remaining age groups: "30-39" and "40-49." The steps are the same, just with slight variations in the coordinates and labels.
### Add the Second Radio Button
```csharp
// Add another radio button to the first sheet.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Set its text string.
radio2.Text = "30-39";
// Set A1 cell as a linked cell for the radio button.
radio2.LinkedCell = "A1";
// Make the radio button 3-D.
radio2.Shadow = true;
// Set the weight of the radio button.
radio2.Line.Weight = 4;
// Set the dash style of the radio button.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Add the Third Radio Button
```csharp
// Add another radio button to the first sheet.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Set its text string.
radio3.Text = "40-49";
// Set A1 cell as a linked cell for the radio button.
radio3.LinkedCell = "A1";
// Make the radio button 3-D.
radio3.Shadow = true;
// Set the weight of the radio button.
radio3.Line.Weight = 4;
// Set the dash style of the radio button.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Step 5: Saving the Excel File
Once all your radio buttons are added and formatted, it’s time to save the file.
```csharp
// Save the excel file.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
In this step, the workbook is saved to your specified directory. It’s that simple—your interactive worksheet is now ready!
## Conclusion
There you have it! You’ve just added radio buttons to an Excel worksheet using Aspose.Cells for .NET. This tutorial covered everything from setting up the workbook, inserting and formatting a value, adding multiple radio buttons, and linking them to a cell. Now, you’re all set to create interactive Excel sheets that not only look great but also provide an enhanced user experience. Have fun exploring more possibilities with Aspose.Cells!
## FAQ's
### Can I add more radio buttons to different sheets?  
Absolutely! You can repeat the process on any sheet within the workbook by specifying the correct worksheet index.
### Can I customize the appearance of the radio buttons further?  
Yes, Aspose.Cells provides a variety of customization options, including changing colors, sizes, and other formatting attributes.
### How can I detect which radio button is selected?  
The linked cell (e.g., A1) will show the index of the selected radio button. You can check the value of the linked cell to find out which one is selected.
### Is there a limit to the number of radio buttons I can add?  
No, there’s no hard limit on the number of radio buttons you can add. However, it’s good to keep the interface user-friendly.
### Can I use Aspose.Cells with other programming languages?  
Yes, Aspose.Cells supports multiple programming languages, including Java. But this tutorial specifically focuses on .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
