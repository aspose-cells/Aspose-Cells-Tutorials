---
title: Set Default Font for PDF Save Options
linktitle: Set Default Font for PDF Save Options
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to set default fonts for PDF save options using Aspose.Cells for .NET, ensuring your documents look perfect every time.
weight: 11
url: /net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Set Default Font for PDF Save Options

## Introduction
When it comes to generating reports, invoices, or any other documents in PDF format, ensuring that your content looks just right is paramount. Fonts play a vital role in maintaining the visual appeal and readability of your documents. However, what happens when the font you used in your Excel file isn’t available on the system where you're generating your PDF? That’s where Aspose.Cells for .NET comes in handy. This powerful library allows you to set default fonts for your PDF save options, ensuring your documents look professional and consistent, no matter where they’re opened.
## Prerequisites
Before we get started, make sure you have the following:
1. Visual Studio: You'll need a development environment like Visual Studio to write and execute your code.
2. Aspose.Cells for .NET: You can download the latest version from [this link](https://releases.aspose.com/cells/net/). Alternatively, you can install it via NuGet Package Manager in Visual Studio.
3. Basic Knowledge of C#: Understanding the basics of C# will help you follow along with the code examples.
4. Sample Excel File: Have a sample Excel file ready for testing. You can create one with various fonts and styles to see how Aspose.Cells handles missing fonts.
## Import Packages
Before you can use Aspose.Cells in your project, you need to import the necessary packages. Here’s how to do it:
1. Open Your Project: Launch Visual Studio and open your existing project or create a new one.
2. Add References: Right-click on your project in the Solution Explorer and select "Manage NuGet Packages."
3. Install Aspose.Cells: Search for "Aspose.Cells" and click the "Install" button.
4. Add Using Directives: At the top of your C# file, include the following namespaces:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Step 1: Set Up Your Directories
Before working with files, it’s important to define the source and output directories. This will make it easier to locate your input Excel file and save the generated output files.
```csharp
// Source directory
string sourceDir = "Your Document Directory";
// Output directory
string outputDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path to your directories.
## Step 2: Open the Excel File
Now that we have our directories set up, let’s open the Excel file that you want to work with. The `Workbook` class in Aspose.Cells is used to load the Excel document.
```csharp
// Open an Excel file
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Make sure to replace the filename with your actual file name.
## Step 3: Set Up Image Rendering Options
Next, we need to configure the rendering options for converting our Excel sheet to an image format. We’ll create an instance of `ImageOrPrintOptions`, specifying the image type and default font.
```csharp
// Rendering to PNG file format
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
In this code snippet, we set the `CheckWorkbookDefaultFont` property to `false`, which means that if any fonts are missing, the specified default font (“Times New Roman”) will be used instead.
## Step 4: Render the Sheet as an Image
Now, let’s render the first sheet of the workbook as a PNG image. We’ll use the `SheetRender` class to accomplish this.
```csharp
// Render the first worksheet to an image
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Step 5: Change Image Type and Render to TIFF
If you want to render the same sheet to a different image format, like TIFF, you can simply change the `ImageType` property and repeat the rendering process.
```csharp
// Set to TIFF format
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Step 6: Configure PDF Save Options
Next up, let’s set up the PDF save options. We will create an instance of `PdfSaveOptions`, set the default font, and specify that we want to check for missing fonts.
```csharp
// Configure PDF save options
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Step 7: Save the Workbook as a PDF
With the save options configured, it’s time to save our Excel workbook as a PDF file. 
```csharp
// Save the workbook to PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Step 8: Confirm Execution
Finally, it’s a good practice to let the user know that the process has completed successfully. You can achieve this by using a simple console message.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusion
Aspose.Cells provides a flexible and robust way to handle Excel file manipulations, making it easier for developers to create visually appealing documents that maintain their formatting. Whether you’re working on reports, financial documents, or any other form of data presentation, having control over font rendering can significantly enhance your output quality.
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful .NET library that allows developers to manipulate Excel files without needing Microsoft Excel installed. It supports various file formats and offers rich features for working with spreadsheets.
### How can I set a default font for my Excel files?
You can set a default font using the `PdfSaveOptions` class and specify the desired font name. This ensures that even if a font is missing, your document will use the default font you've specified.
### Can I convert Excel files to formats other than PDF?
Absolutely! Aspose.Cells allows you to convert Excel files to various formats, including images (PNG, TIFF), HTML, CSV, and more.
### Is Aspose.Cells free to use?
Aspose.Cells is a commercial product, but you can try it out for free with a limited trial version. For full functionality, you’ll need to purchase a license.
### Where can I find support for Aspose.Cells?
You can find support for Aspose.Cells by visiting the [Aspose forum](https://forum.aspose.com/c/cells/9), where you can ask questions and share insights with other users and developers.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
