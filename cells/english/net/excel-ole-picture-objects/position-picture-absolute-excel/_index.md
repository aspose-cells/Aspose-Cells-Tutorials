---
title: Position Picture (Absolute) in Excel
linktitle: Position Picture (Absolute) in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to position images absolutely in Excel using Aspose.Cells for .NET with this comprehensive step-by-step tutorial.
weight: 13
url: /net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Position Picture (Absolute) in Excel

## Introduction
Have you ever found yourself struggling to position images correctly in an Excel spreadsheet? You’re not alone! Many users face this challenge, especially when their data visualization needs require absolute positioning for better aesthetics or clarity. Well, look no further; this guide will walk you through the straightforward process of positioning pictures absolutely in an Excel worksheet using Aspose.Cells for .NET. Whether you’re a developer working on Excel manipulation or a data analyst looking to enhance your reports, our step-by-step tutorial is here to simplify your Excel experiences with images!
## Prerequisites
Before diving into the code and specifics, there are a few things you need to have ready:
1. Aspose.Cells library: Ensure you have the latest version of the Aspose.Cells for .NET library. You can download it from the [releases page](https://releases.aspose.com/cells/net/).
2. Development Environment: Make sure you have a working .NET development environment set up. You can use Visual Studio or any other IDE of your choice.
3. Basic Knowledge of C#: Familiarity with C# programming language will be beneficial to understand the code snippets.
4. Image File: Have an image file (e.g., “logo.jpg”) saved in your designated document directory that you plan to insert into your Excel sheet.

## Import Packages
To get started, let’s ensure we import the necessary packages for our project. Your project file should include the following namespaces:
```csharp
using System.IO;
using Aspose.Cells;
```
By importing these namespaces, we ensure that our program can leverage the features provided by Aspose.Cells.
Let’s break this down into manageable steps for clarity.
## Step 1: Set Up Your Document Directory
In this initial step, you need to define the directory where your documents are located. This is essential for the program to know where to save or fetch files. Here's how you can set it up:
```csharp
string dataDir = "Your Document Directory";
```
Simply replace `"Your Document Directory"` with the actual path where your image file is located. This might be something like `"C:\\Users\\YourUsername\\Documents\\"`.
## Step 2: Instantiating a Workbook Object
Next, you need to create a new instance of the `Workbook` class. This object represents your Excel file:
```csharp
Workbook workbook = new Workbook();
```
At this point, you have a workbook ready to be populated with data and images.
## Step 3: Adding a New Worksheet
Now that you have the workbook, you need to add a worksheet to it. This is where the magic of adding and positioning images will happen:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
This line creates a new worksheet within your workbook and returns its index, which we store in the variable `sheetIndex`.
## Step 4: Obtaining the New Worksheet
Let’s reference the newly created worksheet. Using the index we just got, we can access the worksheet and manipulate it:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Now you can work with the `worksheet` object to add content, including images.
## Step 5: Adding a Picture
Now for the exciting part! Here’s where we add the picture to our worksheet. We specify the row and column indices where we want the picture to be anchored (in this case, at cell "F6," which is row 5 and column 5):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
This line effectively locks the image at the specified location relative to the entire worksheet. However, right now, it’s still subject to resizing along with cells.
## Step 6: Accessing the Newly Added Picture
To manipulate the picture further, you need to access its properties:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
With this, you gain access to the properties of the image we just added!
## Step 7: Setting Absolute Positioning for the Picture
To position the picture absolutely (in pixels), you will need to define its position using the `Left` and `Top` properties. This is where you will have control over where the image appears:
```csharp
picture.Left = 60;
picture.Top = 10;
```
You can adjust both values as needed; they represent the horizontal and vertical positioning of the image, respectively.
## Step 8: Saving the Excel File
Finally, after making all your modifications, it’s time to save the workbook:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
This will create an Excel file named `book1.out.xls` in your previously defined document directory, containing your worksheet with the picture placed absolutely.

## Conclusion
And there you have it! You’ve successfully positioned a picture in an Excel sheet with absolute positioning using Aspose.Cells for .NET. This straightforward process not only enhances the visual presentation of your Excel documents but also ensures that the images stay exactly where you want them — regardless of any changes made to cell sizes and row heights. Now, whether you’re preparing a report or creating a dashboard, you can ensure your pictures are perfectly placed every time.
## FAQ's
### What is Aspose.Cells for .NET?
Aspose.Cells for .NET is a .NET library that enables developers to create, manipulate, and convert Excel spreadsheets programmatically without the need for Microsoft Excel.
### Can I perform other image manipulations using Aspose.Cells?
Yes, beyond positioning, you can also resize, rotate, and modify images within Excel spreadsheets using the Aspose.Cells library.
### Is Aspose.Cells free to use?
Aspose.Cells is a commercial product, but you can start with a free trial available on their [free trial page](https://releases.aspose.com/).
### How do I obtain a temporary license for Aspose.Cells?
You can apply for a temporary license via the [temporary license page](https://purchase.aspose.com/temporary-license/) provided by Aspose.
### Where can I find more examples and documentation?
The [Aspose.Cells documentation](https://reference.aspose.com/cells/net/) contains extensive resources, including code examples and more detailed features.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
