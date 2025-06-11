---
title: Reading Numbers Spreadsheet Programmatically in .NET
linktitle: Reading Numbers Spreadsheet Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to read Numbers spreadsheets and convert them to PDF using Aspose.Cells for .NET in this detailed tutorial.
weight: 18
url: /net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Reading Numbers Spreadsheet Programmatically in .NET

## Introduction
In today's digital world, data management is a vital skill, and spreadsheets are at the forefront of data organization. But what if you need to work with a Numbers spreadsheet—those files created by Apple’s Numbers app—using .NET? Don’t worry; you’re not alone! In this tutorial, we’ll walk through the process of reading a Numbers spreadsheet programmatically with Aspose.Cells for .NET. You’ll learn how to load a Numbers file and convert it to PDF.
## Prerequisites
Before we get started, there are a few things you need to have in place:
1. Aspose.Cells for .NET: Make sure you have the Aspose.Cells library installed. You can download it [here](https://releases.aspose.com/cells/net/).
2. Visual Studio: It’s recommended to have Visual Studio (or any other .NET-compatible IDE) installed on your machine.
3. Basic Knowledge of C#: A little familiarity with C# programming will help you follow along smoothly.
4. Your Document Directory: You’ll need a directory where your Numbers file is stored, along with a location to save the converted PDF.
Once you’ve got these prerequisites covered, you’re all set to start!
## Import Packages
To begin with, we need to import the necessary packages into our C# project. This is a crucial step because it allows us to leverage the functionalities provided by the Aspose.Cells library.
1. Open your C# project in Visual Studio.
2. Add a reference to the Aspose.Cells library:
   - If you’re using NuGet, simply run the following command in the Package Manager Console:
```
 Install-Package Aspose.Cells
 ```
3. Import the necessary namespaces in your code:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Now that we’ve imported the necessary packages, let’s move on to the step-by-step guide for reading a Numbers spreadsheet.
## Step 1: Specify the Source and Output Directories
In this step, we’ll set up the directories where your source Numbers file is located and where you want to save the output PDF.
```csharp
// Source directory
string sourceDir = "Your Document Directory"; // Update this to your actual directory
// Output directory
string outputDir = "Your Document Directory"; // Update this to your actual directory
```
Here, we’re defining two string variables, `sourceDir` and `outputDir`, to specify the locations of the input and output files. Make sure to replace `"Your Document Directory"` with the actual paths on your system.
## Step 2: Set Up Load Options for Numbers Format
Next, we’ll specify the load options for reading a Numbers spreadsheet. This step is essential as it tells Aspose how to interpret the Numbers file.
```csharp
// Specify load options; we want to load the Numbers spreadsheet
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
We create a `LoadOptions` object and specify the format as `LoadFormat.Numbers`. This tells the Aspose.Cells library that we’re working with a Numbers file. 
## Step 3: Load the Numbers Spreadsheet into a Workbook
Now, it’s time to load the actual Numbers spreadsheet into a `Workbook` object.
```csharp
// Load the Numbers spreadsheet into the workbook with the above load options
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
We instantiate a `Workbook` object and pass the file path of the Numbers file along with our load options. Make sure that the file name (`sampleNumbersByAppleInc.numbers`) matches the actual name of your Numbers file.
## Step 4: Save the Workbook as a PDF
Once the Numbers file is loaded successfully, the next step is to save it in a different format—specifically, PDF.
```csharp
// Save the workbook to PDF format
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
Here, we call the `Save` method on the `Workbook` object, specifying the output file path and the format we want to save it in. In this case, we’re saving it as a PDF. Ensure that the output file name (`outputNumbersByAppleInc.pdf`) is unique and doesn’t overwrite any existing files.
## Step 5: Confirm Success
Finally, let’s add a message to confirm that our operation was successful.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
This line of code will print a success message to the console once everything is done. It’s always nice to have feedback, right?
## Conclusion
And there you have it! You’ve successfully read a Numbers spreadsheet and converted it to PDF using Aspose.Cells for .NET. This powerful library allows you to manipulate spreadsheets effortlessly, making your data management tasks a breeze. Whether you're developing applications or just need to handle spreadsheets more efficiently, Aspose.Cells is a fantastic tool to have in your toolkit.
## FAQ's
### What types of files can Aspose.Cells read?  
Aspose.Cells can read a variety of file formats, including XLS, XLSX, CSV, and Numbers files. 
### Can I edit Numbers files using Aspose.Cells?  
Yes, you can read, manipulate, and save Numbers files with Aspose.Cells.
### Is Aspose.Cells free to use?  
Aspose.Cells offers a free trial, but you'll need a license for extended use. Check the pricing [here](https://purchase.aspose.com/buy).
### What do I do if I encounter an error while loading a Numbers file?  
Make sure you’re using the correct load options and that the file path is accurate. For more support, visit the [Aspose Support Forum](https://forum.aspose.com/c/cells/9).
### How can I get a temporary license for Aspose.Cells?  
You can apply for a temporary license [here](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
