---
title: Export Custom Properties to PDF from Excel
linktitle: Export Custom Properties to PDF from Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to export custom properties from Excel to PDF using Aspose.Cells for .NET in this step-by-step guide. Streamline your data sharing.
weight: 10
url: /net/excel-file-handling/export-custom-properties-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Custom Properties to PDF from Excel

## Introduction
When working with Excel files, one often encounters the need to share data in a universally accepted format, such as PDF. Exporting custom properties from Excel files to PDFs can be a daunting task without the right tools. That’s where Aspose.Cells for .NET comes in, offering a robust solution to make this process seamless and efficient. In this article, we’ll walk you through the steps required to export custom properties from an Excel file to PDF format using Aspose.Cells for .NET. By the end of this guide, you’ll be equipped with all the knowledge needed to tackle this task head-on!
## Prerequisites
Before we dive into the nitty-gritty, let’s go over a few prerequisites you’ll need:
1. .NET Environment: Ensure you have a .NET development environment set up, like Visual Studio.
2. Aspose.Cells for .NET: Download and install the latest version of Aspose.Cells for .NET. You can find it [here](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: Familiarity with C# programming will help you follow along with the code examples more easily.
## Import Packages
To get started, you'll first need to import the necessary packages into your project. Here’s how you can do that:
### Create a New Project
1. Open Visual Studio.
2. Click on “Create a new project”.
3. Select “Console App (.NET Framework)” or “Console App (.NET Core)” based on your preference and click “Next”.
4. Name your project and click "Create".
### Add Aspose.Cells to Your Project
To use Aspose.Cells, you need to add it as a reference:
1. Right-click on the project in the Solution Explorer.
2. Select “Manage NuGet Packages”.
3. Search for “Aspose.Cells” and install the latest version.
Now that your packages are imported, you’re ready to start coding.

```csharp
using System.IO;
using System.Web;
using Aspose.Cells;
using System;
```

Now, let’s get down to the crucial part: the step-by-step guide for exporting custom properties from an Excel file to a PDF document. Buckle up!
## Step 1: Set Up Your Directories
Before you start coding, you need to define your input and output directories. This is where you will read the Excel file and where the generated PDF will be saved.
```csharp
// Input directory
string sourceDir = "Your Document Directory";
// Output directory
string outputDir = "Your Document Directory";
```
In this code snippet, replace `"Your Document Directory"` with the actual path where your files are located or where you want to save them.
## Step 2: Load the Excel File
Next, you’ll need to load the Excel file that contains the custom properties. This is done using the `Workbook` class in Aspose.Cells.
```csharp
// Load excel file containing custom properties
Workbook workbook = new Workbook(sourceDir + "sampleWithCustProps.xlsx");
```
Here, make sure that `sampleWithCustProps.xlsx` is the name of your Excel document, and it should reside in the specified directory.
## Step 3: Create PdfSaveOptions
Once your workbook is loaded, it’s time to set up the options for saving the PDF. You’ll create an instance of `PdfSaveOptions` and set the proper properties.
```csharp
// Create an instance of PdfSaveOptions and pass SaveFormat to the constructor
Aspose.Cells.PdfSaveOptions pdfSaveOpt = new Aspose.Cells.PdfSaveOptions();
```
This line initiates the PDF save options that you'll customize shortly.
## Step 4: Configure the Custom Properties Export
You’ll want to specify how the custom properties should be exported. In this case, we will use the `Standard` option for exporting.
```csharp
// Set CustomPropertiesExport property to PdfCustomPropertiesExport.Standard
pdfSaveOpt.CustomPropertiesExport = Aspose.Cells.Rendering.PdfCustomPropertiesExport.Standard;
```
By setting this property, the custom properties from your Excel document will be included in the PDF.
## Step 5: Save the Workbook as PDF
Now that everything is set, it’s time to actually save your workbook as a PDF file using the defined options.
```csharp
// Save the workbook to PDF format while passing the object of PdfSaveOptions
workbook.Save(outputDir + "outSampleWithCustProps.pdf", pdfSaveOpt);
```
In this line, `outSampleWithCustProps.pdf` will be the name of your new PDF file, so make sure it’s unique to avoid any overwriting.
## Step 6: Confirm Success
Finally, let’s confirm that the operation was successful by printing a message to the console:
```csharp
Console.WriteLine("ExportCustomPropertiesToPDF executed successfully.");
```
This message will appear in your console to let you know everything went smoothly.
## Conclusion
And there you have it! You’ve learned how to export custom properties from an Excel file to a PDF document using Aspose.Cells for .NET. This approach not only makes data sharing easier but also ensures that the custom metadata you've input into your Excel files remains intact and accessible in the PDF format. Whether you’re dealing with project documentation, reports, or data summaries, this method is a valuable addition to your toolkit. Don’t hesitate to explore the Aspose.Cells documentation [here](https://reference.aspose.com/cells/net/) for even more powerful functionalities.
## FAQ's
### What are custom properties in Excel?
Custom properties are metadata fields that you can associate with an Excel workbook, such as the author’s name, title, or custom data specific to your needs.
### Can I export custom properties in different formats?
Yes, besides PDF, other formats supported by Aspose.Cells also allow exporting custom properties, depending on your needs.
### Is a license required for Aspose.Cells?
A license is required for commercial use, but you can also try the product for free initially. Check out the [temporary license](https://purchase.aspose.com/temporary-license/) options.
### Where can I find support for Aspose.Cells?
You can find community support and ask questions in the Aspose forum [here](https://forum.aspose.com/c/cells/9).
### Can I customize the saved PDF output?
Absolutely! The `PdfSaveOptions` class provides various properties that allow for detailed customization of the PDF output.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
