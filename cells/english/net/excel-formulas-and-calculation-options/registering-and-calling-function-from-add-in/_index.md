---
title: Registering and Calling Function from Add-In in Excel
linktitle: Registering and Calling Function from Add-In in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Discover how to register and call functions from add-ins in Excel using Aspose.Cells for .NET with our easy step-by-step tutorial.
weight: 20
url: /net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Registering and Calling Function from Add-In in Excel

## Introduction
Do you want to enhance your Excel experience by calling functions from an add-in? If yes, you’re in the right place! Excel add-ins are like the fairy godmothers of spreadsheets; they magically expand functionality, giving you a bunch of new tools at your fingertips. And with Aspose.Cells for .NET, it’s easier than ever to register and use these add-in functions. 
In this guide, I’ll walk you through the process of registering and calling a function from an Excel add-in using Aspose.Cells for .NET. We’ll break everything down step-by-step, so you’ll feel like a pro in no time!
## Prerequisites
Before we dive into the coding wizardry, let’s cover what you need to have in place:
1. Visual Studio: Make sure you have Visual Studio set up on your machine. This is where we’ll write and run our code.
2. Aspose.Cells Library: You’ll need the Aspose.Cells library installed. You can grab it from their [download page](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: A little understanding of C# will go a long way; it’ll help you follow along seamlessly.
4. Excel Add-Ins: You should have an add-in file (like `.xlam`) that contains the functions you want to register and use.
5. A Sample Excel Add-In: For this tutorial, we’ll use an Excel add-in named `TESTUDF.xlam`. So make sure you have this at your disposal!
Now that you’re set up, let’s roll up our sleeves and get to coding!
## Importing Packages
To get started, you’ll need to import some essential namespaces at the top of your C# file. Here’s what you need to include:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
These namespaces will allow you to access the classes and methods we’ll be using in this tutorial.
Let’s break this down into manageable steps. By the end of this guide, you’ll have a solid understanding of how to register add-in functions and use them in your Excel workbooks.
## Step 1: Set Up Your Source and Output Directories
Before you can register your add-in, you need to define where your add-in and output files will live.
```csharp
// Source directory
string sourceDir = "Your Document Directory";
// Output directory
string outputDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path where your `.xlam` file and output files will be saved. This is just like setting the stage before the show begins.
## Step 2: Create an Empty Workbook
Next, you’ll want to create a blank workbook where we can play around with add-in functions.
```csharp
// Create empty workbook
Workbook workbook = new Workbook();
```
This line of code creates a new workbook that will serve as our playground. Think of it as a fresh canvas, ready for your creative strokes.
## Step 3: Register the Add-In Function
Now, let’s get to the heart of the matter! It’s time to register your add-in function. Here's how to do it:
```csharp
// Register macro enabled add-in along with the function name
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
This line registers the add-in function named `TEST_UDF` found in the `TESTUDF.xlam` add-in file. The `false` parameter means that the add-in is not loaded in an ‘isolated’ mode. 
## Step 4: Register Additional Functions (If Any)
If you have more functions registered in the same add-in file, you can register those too!
```csharp
// Register more functions in the file (if any)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
Here, you can see how easy it is to add more functions from the same add-in. Just keep stacking them like building blocks!
## Step 5: Access the Worksheet
Let’s move on and access the worksheet where we’ll be using our function. 
```csharp
// Access first worksheet
Worksheet worksheet = workbook.Worksheets[0];
```
We’re accessing the first worksheet in the workbook to place our formula. It’s like opening the door to the room where the fun happens.
## Step 6: Access a Specific Cell
Next up, we need to choose which cell we want to use for our formula. 
```csharp
// Access first cell
var cell = worksheet.Cells["A1"];
```
Here we’re pointing to cell A1. This is where we’re going to drop our magic formula. You could think of it as pinning a target on your treasure map!
## Step 7: Set the Formula
Now it’s time for the grand unveiling! Let’s set the formula that calls our registered function.
```csharp
// Set formula name present in the add-in
cell.Formula = "=TEST_UDF()";
```
With this line, we’re telling Excel to use our function within cell A1. It’s like giving Excel a command and saying, “Hey, do this!”
## Step 8: Save the Workbook
Last but not the least, it’s time to save our masterpiece.
```csharp
// Save workbook to output XLSX format.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
Here, we’re saving our workbook as an XLSX file. This final step is like putting your painting in a frame and getting ready to showcase it!
## Step 9: Confirm Execution
Finally, let’s wrap it all up by printing a success message to the console.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
This line acts as our victory flag. It’s a nice little touch to confirm everything went smoothly.
## Conclusion 
And there you have it! You’ve not only learned how to register and call functions from Excel add-ins using Aspose.Cells for .NET, but you also gained a deeper understanding of each step involved. Life is just a bit easier now, isn't it? So why not try it out for yourself? Dive into those Excel add-ins and give your spreadsheets a new level of interactivity and functionality.
## FAQ's
### What is an Excel Add-In?  
An Excel Add-In is a program that adds custom features, functions, or commands to Excel, allowing users to extend its capabilities.
### Can I use Aspose.Cells without installing it locally?  
No, you need to install the Aspose.Cells library to use it in your .NET applications.
### How do I get a temporary license for Aspose.Cells?  
You can visit their [temporary license page](https://purchase.aspose.com/temporary-license/) for more information.
### Is it possible to call multiple functions from a single add-in?  
Yes! You can register multiple functions from the same add-in file using the `RegisterAddInFunction` method.
### Where can I find more documentation on Aspose.Cells?  
You can explore their comprehensive documentation on the site [here](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
