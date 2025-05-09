---
title: Specifying HTML CrossType in Output HTML Programmatically in .NET
linktitle: Specifying HTML CrossType in Output HTML Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to specify HTML CrossType in Aspose.Cells for .NET. Follow our step-by-step tutorial to convert Excel files to HTML with precision.
weight: 17
url: /net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specifying HTML CrossType in Output HTML Programmatically in .NET

## Introduction
When it comes to converting Excel files to HTML in .NET applications, you might find yourself needing to specify how cross-references are handled in the output. The HtmlSaveOptions class in Aspose.Cells for .NET provides various settings to control the conversion process, and one of those options is the HtmlCrossType. In this tutorial, we’ll walk through how to programmatically specify the HTML cross-type when exporting Excel files to HTML format. 
## Prerequisites
Before diving into the code, make sure you have the following:
- Aspose.Cells for .NET: Ensure you have the Aspose.Cells library installed in your project. You can download it from the [Aspose website](https://releases.aspose.com/cells/net/).
- Visual Studio: A working installation of Visual Studio or any other .NET development environment.
- Basic Knowledge of C#: Familiarity with C# programming will help you understand the examples better.
- Sample Excel File: Have a sample Excel file ready to work with. For this example, we'll use `sampleHtmlCrossStringType.xlsx`.
## Import Packages
To get started, you’ll need to import the necessary Aspose.Cells namespaces. Here’s how you can do it:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Let’s break this down step-by-step, making it easy for you to follow along and implement this functionality in your own projects.
## Step 1: Define Your Source and Output Directories
First, you need to set the directories for your source Excel file and where you want to save the output HTML file.
```csharp
// Source directory
string sourceDir = "Your Document Directory";
// Output directory
string outputDir = "Your Document Directory";
```
## Step 2: Load the Sample Excel File
Next, load your sample Excel file into a `Workbook` object. This is where all the magic begins.
```csharp
// Load the sample Excel file
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Here, replace `"Your Document Directory"` with the actual path where your Excel file is located. This line reads the Excel file into memory so you can manipulate it.
## Step 3: Specify HTML Save Options
Now, we’ll create an instance of `HtmlSaveOptions`, which allows you to configure how the Excel file will be converted to HTML.
```csharp
// Specify HTML Cross Type
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
In this step, we’ve set the `HtmlCrossStringType` to `HtmlCrossType.Default`, which is one of the options available for handling cross-references in the output HTML.
## Step 4: Change the Cross Type as Needed
You can specify different types for `HtmlCrossStringType` based on your requirements. Here are the various options you can use:
- `HtmlCrossType.Default`: The default cross type.
- `HtmlCrossType.MSExport`: Exports the HTML with MS Excel-like behavior.
- `HtmlCrossType.Cross`: Creates cross references.
- `HtmlCrossType.FitToCell`: Fits the cross references to the cell dimensions.
You can modify the `HtmlCrossStringType` like this:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// or 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Step 5: Save the Output HTML File
Once you've configured your options, it’s time to save the converted HTML file. Use the `Save` method on your `Workbook` object:
```csharp
// Output Html
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Here, we're naming the output file based on the `HtmlCrossStringType` we’ve set. This way, you can easily identify which cross type was used in the conversion.
## Step 6: Confirm Successful Execution
Finally, it’s always a good practice to confirm that your operation was successful. You can print a message to the console:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
This will let you know that the process has been completed without any errors.
## Conclusion
And there you have it! You’ve successfully specified the HTML cross-type for your Excel export in .NET using Aspose.Cells. This functionality is particularly useful when you need to maintain specific formatting or references in your HTML output, ensuring that your converted documents meet your requirements.
## FAQ's
### What is HtmlCrossType in Aspose.Cells?  
HtmlCrossType defines how cross-references in the Excel file are handled during HTML conversion. You can choose options like Default, MSExport, Cross, and FitToCell.
### Can I use Aspose.Cells for free?  
Aspose.Cells offers a free trial version. You can download it from their [website](https://releases.aspose.com/).
### How do I install Aspose.Cells in my .NET project?  
You can install Aspose.Cells via NuGet Package Manager in Visual Studio by running the command: `Install-Package Aspose.Cells`.
### Where can I find the documentation for Aspose.Cells?  
You can find comprehensive documentation on Aspose.Cells [here](https://reference.aspose.com/cells/net/).
### What should I do if I encounter an error while saving the HTML file?  
Make sure that the directory paths are correct and that you have write permissions for the output directory. If the issue persists, check the Aspose support forum for help.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
