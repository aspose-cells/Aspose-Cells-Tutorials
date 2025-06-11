---
title: Position Picture (Proportional) in Excel
linktitle: Position Picture (Proportional) in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to position images proportionally in Excel using Aspose.Cells for .NET. Make your spreadsheets more visually appealing.
weight: 14
url: /net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Position Picture (Proportional) in Excel

## Introduction
Are you tired of those pixelated images that never seem to fit just right in your Excel spreadsheets? Picture this: you have a beautiful logo that needs to be displayed prominently in your Excel sheet, but it ends up being squished, stretched, or poorly placed. No one wants that! Well, hold on to your seats because today you’re going to learn how to position images proportionally in Excel using the Aspose.Cells library for .NET. This powerful library makes it a breeze to manipulate Excel files, be it for reporting, data analysis, or just sprucing up your presentations. Let’s dive into the nitty-gritty of aligning your pictures perfectly!
## Prerequisites
Before we dive into the actual coding, there are a few things you need to have set up on your machine:
1. Visual Studio: Make sure you have Visual Studio installed, as it will provide a convenient environment for your .NET project.
2. Aspose.Cells Library: You’ll need the Aspose.Cells library. You can grab a free trial or purchase it from the [Aspose website](https://purchase.aspose.com/buy).
3. Basic Knowledge of C#: A little familiarity with C# programming will go a long way in understanding the examples we’ll be discussing.
4. An Image File: Have an image ready (like your logo) that you want to insert into the Excel sheet.
Now that you have everything in place, let’s get into the coding!
## Import Packages
To start using Aspose.Cells in your project, you need to import the specific namespaces. Here’s how to do that:
### Create a New Project
In Visual Studio, create a new project:
- Open Visual Studio.
- Click on "Create a new project."
- Choose "Class Library (.NET Framework)" or "Console Application", depending on your preference.
### Install Aspose.Cells
You can add the Aspose.Cells package to your project via NuGet. Here’s how:
- Right-click on your project in the Solution Explorer.
- Select "Manage NuGet Packages."
- Search for "Aspose.Cells" and click "Install."
### Add Using Directives
At the top of your code file, include the following directives:
```csharp
using System.IO;
using Aspose.Cells;
```
These directives will give you access to the classes you'll need to manipulate your Excel files.
Now, let’s break this down into detailed steps to successfully position an image proportionally in Excel.
## Step 1: Set Up Your Directory
First things first, ensure that you have a designated folder for your documents. Here’s how to create a directory if it doesn’t exist:
```csharp
string dataDir = "Your Document Directory";
// Create directory if it is not already present.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
This snippet creates a new directory (if it doesn’t exist) to store your Excel files. Just replace `"Your Document Directory"` with the actual path where you want your files saved.
## Step 2: Instantiate a Workbook
Next, let’s create a new workbook:
```csharp
Workbook workbook = new Workbook();
```
This line initializes a new workbook object, giving you a blank canvas to work on.
## Step 3: Add a New Worksheet
Now that we have our workbook set up, let’s add a new worksheet to it:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
This will add a new worksheet and return the index of that sheet, which we can use to manipulate it later.
## Step 4: Access the New Worksheet
To manipulate the newly added worksheet, you need to access it:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Now, `worksheet` will allow us to add content and images to that specific sheet.
## Step 5: Insert the Picture
Now comes the exciting part! Let’s add your beautiful image. Replace `"logo.jpg"` with the name of your image file:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
This line adds the image at cell F6 (since rows and columns are zero-indexed, `5` refers to the sixth cell).
## Step 6: Access the Added Picture
Once the image is inserted, you can access it like so:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
This enables you to manipulate the picture properties.
## Step 7: Position the Picture Proportionally
Now, let’s position the picture proportionally:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Here, `UpperDeltaX` and `UpperDeltaY` adjust the position of the image relative to the cell’s dimensions. You can tweak these values to get your image just right.
## Step 8: Save Your Changes
Finally, save your workbook to preserve all changes:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
This line saves your workbook as `book1.out.xls` in the designated directory.
## Conclusion
And there you have it! You’ve just learned how to position pictures proportionally in Excel using Aspose.Cells for .NET. It's not just about inserting images; it’s about making them look perfect in your spreadsheets. Just remember: a well-placed picture can elevate your data presentation significantly.
Have fun experimenting with different images and placements, and don't hesitate to dive deeper into the rich features that Aspose.Cells offers. Your Excel sheets are about to get a serious makeover!
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful library for .NET that enables users to create, manipulate, and convert Excel files without needing Microsoft Excel installed.
### Can I use Aspose.Cells for free?
Yes, Aspose.Cells offers a free trial, which you can download [here](https://releases.aspose.com/).
### Where can I find the documentation?
You can access the comprehensive [documentation](https://reference.aspose.com/cells/net/) for Aspose.Cells.
### Does Aspose.Cells support all image formats?
Aspose.Cells supports various formats including JPEG, PNG, BMP, GIF, and TIFF.
### How can I get support for Aspose.Cells?
For any queries, feel free to visit the [support forum](https://forum.aspose.com/c/cells/9) where you can ask your questions.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
