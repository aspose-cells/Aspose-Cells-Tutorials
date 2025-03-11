---
title: Specify Far East & Latin Font in Excel
linktitle: Specify Far East & Latin Font in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to specify Far East and Latin fonts in Excel using Aspose.Cells for .NET in this comprehensive and easy-to-follow tutorial.
weight: 17
url: /net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Specify Far East & Latin Font in Excel

## Introduction
Are you looking to enhance your Excel reports or documents with specific font requirements? Whether you're dealing with multiple languages or simply striving for a unique aesthetic in your spreadsheets, understanding how to specify Far East and Latin fonts in Excel is a crucial skill. Lucky for you, we have a solution! In this tutorial, we explore how to use Aspose.Cells for .NET to implement this feature seamlessly. Let's dive in!
## Prerequisites
Before we jump into the nitty-gritty, there are a few things you’ll need to set up before getting started with Aspose.Cells:
### .NET Framework or .NET Core
Make sure you have .NET Framework or .NET Core installed on your machine. This library works well with both.
### Installation of Aspose.Cells
You’ll need to download the Aspose.Cells library. You can [download it from here](https://releases.aspose.com/cells/net/). If you’re not familiar with installing NuGet packages, follow [this guide](https://www.nuget.org/).
### Integrated Development Environment (IDE)
Having an IDE such as Visual Studio or JetBrains Rider can simplify coding, debugging, and running your project.
### Basic Knowledge of C#
Familiarity with C# programming will be very beneficial for following this tutorial.
## Import Packages
Before we can work with Aspose.Cells, we need to import the necessary packages into our project. Here’s how you can do that:
### Create a New Project
1. Open your IDE and create a new Console Application project.
2. Name your project something descriptive, like `FontSpecifyingApp`.
### Add Aspose.Cells NuGet Package
1. Right-click on your project in the Solution Explorer.
2. Select `Manage NuGet Packages...`.
3. Search for `Aspose.Cells` and install it.
By the end of these steps, you should have everything in place to start coding!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
With the setup done, it’s time to roll up your sleeves and get down to coding. Specifically, we’ll create a new Excel workbook and specify both the Far East and Latin fonts for text boxes. Here’s how to do it step by step:
## Step 1: Set Up the Output Directory
We begin by specifying where we want to save our Excel file. This is crucial because we want to ensure that our output file is stored in a location that's easily accessible.
```csharp
// Output directory
string outputDir = "Your Document Directory";
```
## Step 2: Create an Empty Workbook
Now that we have our directory set up, let’s create a new workbook where we’ll add our content. This is similar to starting with a fresh canvas before painting.
```csharp
// Create empty workbook.
Workbook wb = new Workbook();
```
## Step 3: Access the First Worksheet
Next, we want to work with a worksheet from our workbook. Think of a worksheet as a page in your book where all the magic happens.
```csharp
// Access first worksheet.
Worksheet ws = wb.Worksheets[0];
```
## Step 4: Add a Textbox
Now, we’ll be adding a textbox to our worksheet. This is where we’ll type in our text. Imagine this as creating a text box within a slide of a presentation.
```csharp
// Add textbox inside the worksheet.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Step 5: Set the Text of the Textbox
Let’s type in some text. In this example, we're going to input Japanese characters to demonstrate the Far East font. It's as simple as writing in a textbox on your computer!
```csharp
// Set the text of the textbox.
tb.Text = "こんにちは世界"; // This means "Hello World" in Japanese.
```
## Step 6: Specify the Fonts
Now comes the exciting part! We’ll set both the Latin and Far East fonts for the text. This is akin to choosing the perfect font for a fancy wedding invitation!
```csharp
// Specify the Far East and Latin name of the font.
tb.TextOptions.LatinName = "Comic Sans MS"; // This is our chosen Latin font.
tb.TextOptions.FarEastName = "KaiTi"; // This is our desired Far East font.
```
## Step 7: Save the Output Excel File
Finally, let’s save our workbook! This step wraps up our task and ensures that all the hard work we've done is saved properly. 
```csharp
// Save the output Excel file.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Step 8: Confirmation Message
To let us know that everything has executed successfully, we’ll print a confirmation message to the console:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Conclusion
And there you have it! You've successfully specified Far East and Latin fonts in an Excel workbook using Aspose.Cells for .NET. This skill not only gives your documents a professional touch but also enriches the reading experience for users across different languages.
Feel free to experiment with different fonts and styles to find a combination that fits your specific needs. Happy coding!
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a .NET library for creating and managing Excel spreadsheets without needing Microsoft Excel installed on your machine. 
### Can I use Aspose.Cells for web applications?
Yes! Aspose.Cells can be used for both desktop applications and web applications built with .NET.
### Is there a free version of Aspose.Cells?
Yes, Aspose offers a free trial. You can [download it here](https://releases.aspose.com/).
### How do I get support for Aspose.Cells?
You can ask for support and find valuable resources on the [Aspose forums](https://forum.aspose.com/c/cells/9).
### Where can I buy Aspose.Cells?
You can purchase Aspose.Cells directly from the [Aspose website](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
