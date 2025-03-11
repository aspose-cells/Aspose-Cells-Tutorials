---
title: Check if Paper Size of Worksheet is Automatic
linktitle: Check if Paper Size of Worksheet is Automatic
second_title: Aspose.Cells .NET Excel Processing API
description: Discover how to check if the paper size of a worksheet is automatic using Aspose.Cells for .NET in our detailed step-by-step guide.
weight: 11
url: /net/worksheet-page-setup-features/check-automatic-paper-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Check if Paper Size of Worksheet is Automatic

## Introduction
When it comes to managing spreadsheets and ensuring that they are formatted perfectly for printing, one critical aspect to consider is the paper size settings. In this guide, we'll explore how to check if the paper size of a worksheet is set to automatic using Aspose.Cells for .NET. This library offers powerful tools for all your Excel-related needs, making your work not only easier but also more efficient.
## Prerequisites
Before diving into the actual coding, let’s make sure you have everything set up. Here are the prerequisites you need:
1. C# Development Environment: You need a C# IDE such as Visual Studio. If you haven’t installed it yet, head over to the Microsoft website.
2. Aspose.Cells Library: Ensure that you have the Aspose.Cells library. You can download it from [this link](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: Familiarity with C# programming concepts will help you understand the examples and code snippets effectively.
4. Sample Excel Files: Make sure you have sample Excel files that have the required page setup. For our example, you will need two files:
- `samplePageSetupIsAutomaticPaperSize-False.xlsx`
- `samplePageSetupIsAutomaticPaperSize-True.xlsx`
Having these prerequisites will set you up for success as we explore the functionality provided by Aspose.Cells.
## Import Packages
To begin, you need to import the necessary packages in your C# project. Here’s how you can do that:
### Create a New C# Project
- Open Visual Studio and create a new C# Console Application.
- Name it something like `CheckPaperSize`.
### Add Aspose.Cells Reference
- Right-click on your project in the Solution Explorer.
- Choose "Manage NuGet Packages".
- Search for "Aspose.Cells" and install it.
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Once you’ve got everything set up, you’re ready to get to the fun part!
Now, let’s break down the process into manageable steps.
## Step 1: Define Source and Output Directories
First, we need to specify where our sample Excel files are located and where we want to save any outputs. 
```csharp
// Source directory
string sourceDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path where your sample Excel files are stored. This is essential for the program to find the files it needs to work with.
## Step 2: Load the Workbooks
Next, we’ll load the two workbooks we prepared earlier. Here’s how you do it:
```csharp
// Load the first workbook having automatic paper size false
Workbook wb1 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-False.xlsx");
// Load the second workbook having automatic paper size true
Workbook wb2 = new Workbook(sourceDir + "samplePageSetupIsAutomaticPaperSize-True.xlsx");
```
We’re loading the two workbooks into memory. The first workbook is set to have the automatic paper size feature disabled, while the second one has it enabled. This setup allows us to compare them easily later on.
## Step 3: Access the Worksheets
Now we’ll access the first worksheet from both workbooks to check their paper size settings.
```csharp
// Access first worksheet of both workbooks
Worksheet ws11 = wb1.Worksheets[0];
Worksheet ws12 = wb2.Worksheets[0];
```
By accessing the first worksheet (index 0) from both workbooks, we're focusing on the relevant pages we want to investigate. 
## Step 4: Check the IsAutomaticPaperSize Property
Let’s take a moment to check the `IsAutomaticPaperSize` property from each worksheet.
```csharp
// Print the PageSetup.IsAutomaticPaperSize property of both worksheets
Console.WriteLine("First Worksheet of First Workbook - IsAutomaticPaperSize: " + ws11.PageSetup.IsAutomaticPaperSize);
Console.WriteLine("First Worksheet of Second Workbook - IsAutomaticPaperSize: " + ws12.PageSetup.IsAutomaticPaperSize);
```
Here, we are printing out whether each worksheet has the automatic paper size feature enabled or not. The property `IsAutomaticPaperSize` returns a boolean value (true or false), indicating the setting.
## Step 5: Final Output and Confirmation
Lastly, let’s put our program’s results in context and confirm it executed successfully.
```csharp
Console.WriteLine();
Console.WriteLine("DetermineIfPaperSizeOfWorksheetIsAutomatic executed successfully.\r\n");
```
After printing the settings, we print a success message to indicate that our program ran without any issues.
## Conclusion
In this tutorial, we covered how to check whether the paper size setting of worksheets in Excel files is set to automatic using Aspose.Cells for .NET. By following these steps, you now have the foundational skills to manipulate Excel files programmatically with ease and check for specific configurations like paper size. 
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful library designed for manipulating Excel document formats in .NET applications.
### Can I use Aspose.Cells for free?
Yes, Aspose offers a free trial version. You can download it [here](https://releases.aspose.com/).
### How do I purchase a license for Aspose.Cells?
You can buy a license through their purchase page found [here](https://purchase.aspose.com/buy).
### What types of Excel files can I work with using Aspose.Cells?
You can work with various Excel formats, including XLS, XLSX, CSV, and many others.
### Where can I find support for Aspose.Cells?
You can find support forums and resources [here](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
