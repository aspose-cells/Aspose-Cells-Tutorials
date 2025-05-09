---
title: Control External Resources in Excel to PDF in Aspose.Cells
linktitle: Control External Resources in Excel to PDF in Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Discover how to control external resources in Excel to PDF conversion using Aspose.Cells for .NET with our easy-to-follow guide.
weight: 12
url: /net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Control External Resources in Excel to PDF in Aspose.Cells

## Introduction
In today’s digital age, converting Excel spreadsheets to PDF documents is a common task. Whether it’s preparing reports, financial data, or presentation materials, you want to ensure that your PDFs look exactly how you intend them to. Aspose.Cells for .NET is a robust library that allows you to control this conversion process down to the last detail, especially when handling external resources like images that accompany your Excel files. In this guide, we're diving into how to control external resources during the Excel to PDF conversion process using Aspose.Cells. So, grab your favorite beverage, and let’s get started!
## Prerequisites
Before we jump into the nitty-gritty, let’s make sure you have everything you need to get rolling. Here’s a quick checklist:
1. Visual Studio or any .NET-compatible IDE: You’ll want an environment to write and test your code.
2. Aspose.Cells for .NET: If you haven’t installed it yet, head over to the [Aspose Downloads](https://releases.aspose.com/cells/net/) page and grab the latest version.
3. Basic Knowledge of C#: Familiarity with the C# programming language will be helpful. If you're unsure about any concepts, don’t hesitate to look them up.
4. A Sample Excel File: Prepare an Excel file with any external resources you would like to convert. You can use the provided sample file "samplePdfSaveOptions_StreamProvider.xlsx".
5. An Image File for Testing: This will be used as an external resource during the conversion. The image file "newPdfSaveOptions_StreamProvider.png" is a good placeholder.
## Import Packages
To kick things off, you’ll need to import the necessary namespaces from the Aspose.Cells library. This is crucial for accessing its functionalities. Make sure to add the following using directives at the top of your file:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
These packages will provide all the essential classes and methods you'll need to perform your tasks.
## Step 1: Create Your Stream Provider Class
The first order of business is to create a stream provider class that implements the `IStreamProvider` interface. This class will allow you to control how external resources are loaded.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Read the new image in a memory stream and assign it to Stream property
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
In this class:
- CloseStream: This method will be called when the stream is closed. For now, we're just writing a debug message for tracking.
- InitStream: This is where the magic begins. Here, you’ll read your external image as a byte array, convert it into a memory stream, and assign it to the `options.Stream` property.
## Step 2: Set Up Source and Output Directories
Now that your stream provider is ready, it’s time to establish where your Excel file is located and where you want to save your PDF.
```csharp
// Source directory
string sourceDir = "Your Document Directory";
// Output directory
string outputDir = "Your Document Directory";
```
Simply replace `"Your Document Directory"` with the actual path on your computer where your files reside. Keeping your files organized is key!
## Step 3: Load Your Excel File
Next, you’ll load the Excel file from which you want to create the PDF.
```csharp
// Load source Excel file containing external images
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
We’re using the `Workbook` class from Aspose.Cells, which represents your Excel file. The file can include various external resources like images that you want to control during conversion.
## Step 4: Set PDF Save Options
Before you save the workbook as a PDF, let's specify how you want it saved. You can adjust these options as per your requirements.
```csharp
// Specify Pdf Save Options - Stream Provider
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Save each sheet on a new page
```
Here, we're creating a new instance of `PdfSaveOptions`, which allows you to customize how your PDF will be formatted. The `OnePagePerSheet` option is handy for ensuring that each Excel sheet gets its own page in the final PDF.
## Step 5: Assign Your Stream Provider
With your PDF options set, you need to tell Aspose to use your custom stream provider for external resources.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
This line connects your `Workbook` instance with the `MyStreamProvider` class you created earlier. This means that whenever external resources are encountered during conversion, your provider will handle them as specified.
## Step 6: Save the Workbook as PDF
With everything set, it’s finally time to save your Excel workbook as a PDF.
```csharp
// Save the workbook to Pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
By calling the `Save` method on the workbook object and passing in your output directory along with the PDF options, you're converting the Excel file into a beautifully formatted PDF.
## Step 7: Confirm Successful Execution
To wrap things up, it’s always nice to confirm that your process has been successful!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Printing a success message to the console helps keep you informed about the status of your operation. It’s a good habit to include these little confirmations in your code.
## Conclusion
There you have it! By following these straightforward steps, you can expertly control how external resources are handled during Excel to PDF conversions using Aspose.Cells. This means that your documents can now include images and other external elements accurately, ensuring a polished final product every time.
## FAQ's
### What is Aspose.Cells?  
Aspose.Cells is a powerful library for .NET developers that allows you to create, manipulate, convert, and render Excel files in various formats.
### How do I download Aspose.Cells?  
You can download the latest version of Aspose.Cells from the [Download link](https://releases.aspose.com/cells/net/).
### Can I try Aspose.Cells for free?  
Yes! You can get a free trial by visiting the [Free trial page](https://releases.aspose.com/).
### Where can I find support for Aspose.Cells?  
For any support-related queries, you can visit the [Aspose Support forum](https://forum.aspose.com/c/cells/9).
### How can I obtain a temporary license for Aspose.Cells?  
You can apply for a temporary license [here](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
