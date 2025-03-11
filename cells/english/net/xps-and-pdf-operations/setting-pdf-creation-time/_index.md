---
title: Setting PDF Creation Time in .NET
linktitle: Setting PDF Creation Time in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to set PDF creation time in .NET using Aspose.Cells. Follow our step-by-step guide for seamless Excel to PDF conversion.
weight: 11
url: /net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Setting PDF Creation Time in .NET

## Introduction
In today’s digital age, the ability to convert documents into different formats is crucial for many applications. One common need is to convert Excel spreadsheets into PDF files. Not only does this preserve the formatting, but it also makes sharing and printing much easier. If you're a developer working with .NET, Aspose.Cells is a fantastic library that simplifies this process. In this tutorial, we’ll dive into how to set the PDF creation time when converting an Excel file to PDF using Aspose.Cells for .NET.
## Prerequisites
Before we jump into the nitty-gritty of the code, let’s ensure you have everything you need to get started.
### What You Need
1. Visual Studio: Make sure you have Visual Studio installed on your machine. This will be your development environment.
2. Aspose.Cells for .NET: Download the Aspose.Cells library from the [website](https://releases.aspose.com/cells/net/). You can also start with a free trial to test its functionalities.
3. Basic Knowledge of C#: Familiarity with C# programming will help you understand the code snippets better.
4. Excel File: Have an Excel file ready for conversion. For this example, we’ll use a file named `Book1.xlsx`.
Now that you have the prerequisites sorted, let’s get into the fun part—importing the necessary packages and writing the code!
## Import Packages
To begin, you need to import the required namespaces in your C# file. This is crucial as it allows you to access the classes and methods provided by the Aspose.Cells library.
### Open Your C# Project
Open Visual Studio and either create a new project or open an existing one where you want to implement the PDF conversion feature.
### Add Aspose.Cells Reference
You can add the Aspose.Cells library to your project by right-clicking on your project in the Solution Explorer, selecting “Manage NuGet Packages,” and searching for “Aspose.Cells.” Install the package.
### Import Namespaces
At the top of your C# file, include the following namespaces:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
These namespaces will give you access to the Workbook class and other essential functionalities.

Now that we have our packages imported, let’s break down the process of converting an Excel file to a PDF while setting the creation time.
## Step 1: Define the Document Directory
First, you need to specify the directory where your documents are stored. This is where your Excel file is located and where the output PDF will be saved.
```csharp
string dataDir = "Your Document Directory"; // Specify your document directory
```
Replace `"Your Document Directory"` with the actual path where your `Book1.xlsx` file is located. This path will help the application locate the file for processing.
## Step 2: Load the Excel File
Next, you’ll load the Excel file into a `Workbook` object. This is where Aspose.Cells shines, as it allows you to work with Excel files effortlessly.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Path to your Excel file
Workbook workbook = new Workbook(inputPath); // Load the Excel file
```
The `Workbook` class is used to load and manipulate Excel files. By passing the input path, you’re telling the application which file to work with.
## Step 3: Create PdfSaveOptions
Now, it’s time to create an instance of `PdfSaveOptions`. This class allows you to specify various options for saving your workbook as a PDF, including the creation time.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Create PdfSaveOptions instance
options.CreatedTime = DateTime.Now; // Set the creation time to now
```
By setting `options.CreatedTime` to `DateTime.Now`, you’re ensuring that the PDF will reflect the current date and time when it was created.
## Step 4: Save the Workbook as PDF
Finally, you’ll save the workbook as a PDF file using the options you just defined.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Save as PDF
```
This line of code takes the workbook and saves it in PDF format at the specified location. The `options` parameter is passed to include the creation time in the PDF metadata.

## Conclusion
And there you have it! You've successfully converted an Excel file to a PDF using Aspose.Cells for .NET, complete with a creation timestamp. This feature can be incredibly useful when you need to keep track of document versions or when you want to provide recipients with information about when the document was created.
If you’re looking to explore more features of Aspose.Cells, don’t hesitate to check out the [documentation](https://reference.aspose.com/cells/net/).
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful library for .NET that allows developers to create, manipulate, and convert Excel files.
### Can I use Aspose.Cells for free?
Yes, you can start with a free trial available on the [Aspose website](https://releases.aspose.com/).
### How do I set other PDF properties?
You can set various PDF properties using the `PdfSaveOptions` class, such as page size, compression, and more.
### Is it possible to convert multiple Excel files at once?
Yes, you can loop through a list of files and apply the same conversion process to each one.
### Where can I get support for Aspose.Cells?
You can get support from the Aspose community on their [support forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
