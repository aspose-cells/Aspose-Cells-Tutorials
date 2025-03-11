---
title: Add List Box to Worksheet in Excel
linktitle: Add List Box to Worksheet in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to add a list box to an Excel worksheet using Aspose.Cells for .NET. Follow our easy, step-by-step guide and make your Excel sheets interactive.
weight: 20
url: /net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add List Box to Worksheet in Excel

## Introduction
Adding interactive elements to your Excel worksheets, like a list box, can improve data management and presentation significantly. Whether you're creating an interactive form or a custom data entry tool, the ability to control user input with a list box is invaluable. Aspose.Cells for .NET provides an efficient way to add and manage these controls in your Excel files. In this guide, we'll walk you through the process of adding a list box to a worksheet using Aspose.Cells for .NET.
## Prerequisites
Before diving into the coding, ensure you have the following tools and resources in place:
- Aspose.Cells for .NET Library: You can download it from the [Aspose.Cells for .NET download page](https://releases.aspose.com/cells/net/).
- Development Environment: Any IDE that supports .NET development, such as Visual Studio.
- .NET Framework: Make sure your project is targeting a supported version of the .NET framework.
Also, consider getting a [temporary license](https://purchase.aspose.com/temporary-license/) if you want to explore all the features without limitations.
## Import Packages
Before you start, make sure you’ve imported the necessary Aspose.Cells namespaces. Here’s how to do that:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
In this tutorial, we will break down the process of adding a list box into multiple simple steps. Follow each step closely to ensure everything works as expected.
## Step 1: Setting Up Your Document Directory
Before you create any Excel file, you need a location to save it. Here’s how to set up the directory:
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
// Create directory if it does not already exist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In this step, you're defining where your file will be stored. The code checks whether the directory exists, and if it doesn’t, it creates one for you. This ensures that you don't run into any "file not found" errors later on.
## Step 2: Create a New Workbook and Access the First Worksheet
Next, we’ll create a new workbook and access the first worksheet where we’ll add our list box.
```csharp
// Create a new Workbook.
Workbook workbook = new Workbook();
// Get the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
```
A workbook is essentially your Excel file. Here, we’re creating a new workbook and accessing the first worksheet, which is where we’ll place our list box. Think of this as creating a blank canvas where you’ll be painting the controls.
## Step 3: Input Data for the List Box
Before we add the list box, we need to populate some data that the list box will reference.
```csharp
// Get the worksheet cells collection.
Cells cells = sheet.Cells;
// Input a value for the label.
cells["B3"].PutValue("Choose Dept:");
// Set the label to bold.
cells["B3"].GetStyle().Font.IsBold = true;
// Input values for the list box.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Here, we’re adding some text into the worksheet. The label "Choose Dept:" is placed in cell B3, and its font is set to bold. In column A, we’re inserting values that will serve as the input range for our list box, representing different departments. This input range is what users will choose from when interacting with the list box.
## Step 4: Add the List Box to the Worksheet
Now that we’ve set up the data, let’s add the list box control itself.
```csharp
// Add a new list box.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
This code adds the list box to the worksheet. The parameters define the position and size of the list box. The list box is placed at row 2, column 0 with a width of 122 and height of 100. These are the coordinates and size that determine where the list box will appear in the worksheet.
## Step 5: Set List Box Properties
Next, we’ll set various properties for the list box to make it fully functional.
```csharp
// Set the placement type.
listBox.Placement = PlacementType.FreeFloating;
// Set the linked cell.
listBox.LinkedCell = "A1";
// Set the input range.
listBox.InputRange = "A2:A7";
// Set the selection type.
listBox.SelectionType = SelectionType.Single;
// Set the list box with 3-D shading.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: This property makes sure the list box stays in its position regardless of how the worksheet is modified.
- LinkedCell: This sets a cell (in this case, A1) where the selected value from the list box will be displayed.
- InputRange: This tells the list box where to look for its list of options (A2 to A7, which we set earlier).
- SelectionType.Single: This restricts the user to selecting only one item from the list box.
- Shadow: The shadow effect gives the list box a more three-dimensional appearance, making it visually appealing.
## Step 6: Save the Excel File
Finally, let’s save our workbook with the list box included.
```csharp
// Save the workbook.
workbook.Save(dataDir + "book1.out.xls");
```
This line of code saves the workbook to the directory we set up earlier. The file is named "book1.out.xls" but you can choose any name that suits your project.
## Conclusion
And there you have it! You've successfully added a list box to an Excel worksheet using Aspose.Cells for .NET. With just a few lines of code, we created a fully functional list box, making the worksheet more interactive and dynamic. This tutorial should give you a solid foundation to explore other controls and features in Aspose.Cells for .NET. Keep experimenting, and soon, you’ll master the library’s vast functionality!
## FAQ's
### Can I allow multiple selections in the list box?  
Yes, you can change the `SelectionType` to `SelectionType.Multi` to allow multiple selections.
### Can I change the appearance of the list box?  
Absolutely! Aspose.Cells allows you to customize the look of the list box, including its size, font, and even color.
### What if I need to remove the list box later?  
You can access and remove the list box from the `Shapes` collection using `sheet.Shapes.RemoveAt(index)`.
### Can I link the list box to a different cell?  
Yes, simply change the `LinkedCell` property to any other cell where you want to display the selected value.
### How do I add more items to the list box?  
Just update the input range by inserting more values into the specified cells, and the list box will automatically update.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
