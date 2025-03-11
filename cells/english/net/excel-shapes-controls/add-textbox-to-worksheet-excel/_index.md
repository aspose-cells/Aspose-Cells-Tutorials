---
title: Add a TextBox to Worksheet in Excel
linktitle: Add a TextBox to Worksheet in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to add customizable text boxes to Excel using Aspose.Cells for .NET in this step-by-step tutorial.
weight: 14
url: /net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add a TextBox to Worksheet in Excel

## Introduction
Are you keen to enhance your Excel spreadsheets with unique visuals that can engage your audience? Adding text boxes is a great way to accomplish this! With Aspose.Cells for .NET, you can easily integrate text boxes into your Excel worksheets, making your documents more informative and visually appealing. This step-by-step guide will walk you through the simple process of adding text boxes using Aspose.Cells, showcasing how to personalize them with text, colors, hyperlinks, and more!
## Prerequisites
Before we dive into the coding marvel, here are the essential prerequisites to ensure a smooth sailing experience:
1. .NET Development Environment: You’ll need a working .NET framework along with an IDE like Visual Studio. Make sure it’s updated to the latest version!
2. Aspose.Cells for .NET: Ensure that you have the Aspose.Cells library downloaded. You can grab the latest version from [here](https://releases.aspose.com/cells/net/).
3. Basic Programming Knowledge: Familiarity with C# and some general concepts of handling Excel files will make this tutorial easier!
## Import Packages
Make sure to import the necessary packages at the beginning of your C# file. Here’s how you can do that:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Install Aspose.Cells
If you haven't done so already, you can add Aspose.Cells through NuGet Package Manager in Visual Studio:
1. Open Visual Studio.
2. Go to `Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`.
3. Search for “Aspose.Cells” and install it for your project.
Now that we’ve laid the groundwork, let’s jump into the fun part!
## Step 1: Setting Up Your Document Directory
First off, let’s set up the directory where all your Excel documents will be stored. It’s essential to ensure that this directory exists before we begin creating our workbook.
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory"; 
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
This code snippet will create a directory named `Your Document Directory` (please substitute this with your actual path) if it doesn’t already exist. Easy peasy, right?
## Step 2: Instantiating a New Workbook
Next, we need to create a new workbook where we’ll be adding our text boxes. This can be easily done with a few lines of code:
```csharp
// Instantiate a new Workbook.
Workbook workbook = new Workbook();
```
This line of code creates a new Excel workbook. Simple and straightforward!
## Step 3: Accessing the First Worksheet
Now that we have our workbook ready, let’s get the first worksheet where we will add our text box:
```csharp
// Get the first worksheet in the book.
Worksheet worksheet = workbook.Worksheets[0];
```
Just like that, you now have access to the first worksheet named `worksheet`. It’s time to make it shine!
## Step 4: Adding a TextBox
Alright, it’s time to add in our first text box! Here’s how to do it:
```csharp
// Add a new textbox to the collection.
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
In this line, we’re specifying the row and column where the text box will be placed, as well as setting its width and height (160 and 200, respectively). Feel free to adjust these numbers based on your layout!
## Step 5: Getting the TextBox Object
After adding the text box, we need to get a reference to it so we can customize its content:
```csharp
// Get the textbox object.
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
Now, `textbox0` is your golden ticket to modifying this text box!
## Step 6: Filling the TextBox with Content
Next, let’s provide some text for the text box:
```csharp
// Fill the text.
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
Inserting text into your text box is as simple as that! 
## Step 7: Customize TextBox Appearance
How about we spruce it up a little? You can adjust font colors, styles, and more!
```csharp
// Set the font color.
textbox0.Font.Color = Color.Blue;
// Set the font to bold.
textbox0.Font.IsBold = true;
// Set the font size.
textbox0.Font.Size = 14;
// Set font attribute to italic.
textbox0.Font.IsItalic = true;
```
Feel free to play around with different colors and styles to see what pops best visually!
## Step 8: Adding a Hyperlink
Want to turn your text box into a clickable link? Let’s do just that:
```csharp
// Add a hyperlink to the textbox.
textbox0.AddHyperlink("http://www.aspose.com/");
```
Now anyone clicking your text box will be transported to the Aspose website. It’s like magic!
## Step 9: Setting TextBox Placement Type
You have different choices on how you want the text box to behave in relation to your worksheet. Here’s an example of how to set it to be free floating:
```csharp
// Set the placement.
textbox0.Placement = PlacementType.FreeFloating;
```
Alternatively, if you want it to resize and move with cells, you can set it like this:
```csharp
// Set the placement type as the textbox will move and resize with cells.
textbox1.Placement = PlacementType.MoveAndSize;
```
## Step 10: Customizing Line and Fill Formats
Here’s how you can change the appearance of the text box's border and fill:
```csharp
// Get the fill format of the textbox.
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// Get the line format type of the textbox.
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// Set the line weight.
lineformat.Weight = 6;
// Set the dash style to squaredot.
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
With this, you can customize your text box further, adding visuals that suit your style.
## Step 11: Adding Another TextBox
No one said we could only add one text box! Let’s put in another one with some different text:
```csharp
// Add another textbox.
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// Get the second textbox.
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// Input some text to it.
textbox1.Text = "This is another simple text box";
```
Now you’re really jazzing up your Excel sheet with multiple text boxes!
## Step 12: Saving Your Workbook
Finally, it's time to save our masterpiece! Here’s the last line of code for the day:
```csharp
// Save the excel file.
workbook.Save(dataDir + "book1.out.xls");
```
With just this one line of code, you've created and modified an Excel file with customizable text boxes!
## Conclusion
Congratulations! You've successfully navigated through the world of text boxes in Excel using Aspose.Cells for .NET. You’ve not only learned how to add a text box but also how to customize it to make your spreadsheets more engaging. From changing colors and styles to even adding hyperlinks, the possibilities are virtually endless! 
Are you ready to start transforming your Excel documents? Let your creativity shine, and experiment with different layouts!
## FAQ's
### What is Aspose.Cells for .NET?
Aspose.Cells for .NET is a powerful library that allows developers to create, manipulate, and convert Excel files effortlessly.
### Can I try Aspose.Cells before buying?
Yes! You can download and use a free trial version [here](https://releases.aspose.com/).
### Where can I find the documentation for Aspose.Cells?
You can access comprehensive documentation at [Aspose.Cells Documentation](https://reference.aspose.com/cells/net/).
### Is there support available if I run into issues?
Absolutely! If you need help, head over to the [Aspose Forum](https://forum.aspose.com/c/cells/9) for assistance.
### Can I use Aspose.Cells without a license?
While you can use a free trial version, to access full functionality, you will need to purchase a license. Check out the pricing [here](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
