---
title: Disabling Downlevel Revealed Comments while Saving to HTML
linktitle: Disabling Downlevel Revealed Comments while Saving to HTML
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to disable downlevel revealed comments when saving an Excel workbook to HTML using Aspose.Cells for .NET with this detailed step-by-step guide.
weight: 11
url: /net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Disabling Downlevel Revealed Comments while Saving to HTML

## Introduction
Have you ever needed to convert an Excel workbook to HTML and wanted to ensure that any unnecessary comments or hidden content didn’t get revealed during the process? That's where disabling downlevel revealed comments comes in handy. If you're using Aspose.Cells for .NET, you have full control over how your Excel workbooks are rendered as HTML files. In this tutorial, we’re going to walk you through a simple step-by-step guide to help you disable downlevel revealed comments while saving a workbook to HTML. 
By the end of this article, you’ll have a clear understanding of how to use this feature and ensure your HTML output is clean and comment-free.
## Prerequisites
Before we dive into the step-by-step guide, let’s cover a few things you’ll need to have in place to follow along smoothly:
1. Aspose.Cells for .NET: You’ll need to have the Aspose.Cells library installed. If you haven’t installed it yet, you can download it [here](https://releases.aspose.com/cells/net/).
2. IDE: A development environment like Visual Studio to write and execute your C# code.
3. Basic Knowledge of C#: Familiarity with C# syntax and object-oriented programming will help you follow along with the code.
4. Temporary or Licensed Version: You can either use the free trial or apply for a temporary license from [here](https://purchase.aspose.com/temporary-license/). This ensures the library works without any limitations.
Now that you’re ready, let’s jump right into it!
## Import Namespaces
Before we get into the code examples, it's essential to include the necessary namespaces for Aspose.Cells. Without these, your code won’t be able to access the methods and properties required for manipulating Excel files.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Make sure to place this line at the top of your C# file to import the Aspose.Cells namespace.
## Step 1: Set Up the Directory Paths
Before anything, we need to set up the source directory (where your Excel file is stored) and the output directory (where your HTML file will be saved). This is crucial because Aspose.Cells requires the exact file paths to access and save files.
```csharp
// Source directory where your Excel file is located
string sourceDir = "Your Document Directory";
// Output directory where the resulting HTML file will be saved
string outputDir = "Your Document Directory";
```
In this step, replace `"Your Document Directory"` with the actual file paths on your system. You can also create custom directories to better organize your input and output files.
## Step 2: Load the Excel Workbook
In this step, we will load the Excel workbook into memory so we can manipulate it. For demonstration purposes, we will be using a sample file named `"sampleDisableDownlevelRevealedComments.xlsx"`. You can use any workbook you prefer.
```csharp
// Load the sample workbook from the source directory
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
This creates a Workbook object that contains all the data and structure of your Excel file. From here, you can modify it, apply settings, and ultimately save it in a different format.
## Step 3: Set Up HTML Save Options
Now, we need to configure the HtmlSaveOptions object to disable downlevel revealed comments. This option ensures that any comments or hidden content won't be revealed in the resulting HTML file.
```csharp
// Create a new HtmlSaveOptions object to configure the save options
HtmlSaveOptions opts = new HtmlSaveOptions();
// Disable downlevel revealed comments
opts.DisableDownlevelRevealedComments = true;
```
By setting `DisableDownlevelRevealedComments` to `true`, you ensure that when you save the workbook as an HTML file, any downlevel comments will be disabled.
## Step 4: Save the Workbook as HTML
Once the HtmlSaveOptions object is configured, the next step is to save the workbook to HTML using the specified options. This is where the actual file conversion happens.
```csharp
// Save the workbook as an HTML file with the specified save options
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
In this line of code, we’re saving the workbook to the output directory you specified earlier, and applying the DisableDownlevelRevealedComments setting. The result will be a clean HTML file without any unwanted comments.
## Step 5: Verify and Execute
Finally, to ensure everything worked as expected, you can output a success message to the console.
```csharp
// Output a success message to the console
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
This lets you know that the operation completed without errors.
## Conclusion
And there you have it! You’ve successfully learned how to disable downlevel revealed comments while saving an Excel workbook to HTML using Aspose.Cells for .NET. With this feature, you can now control how your workbooks are rendered as HTML and avoid revealing any unnecessary content. Whether you're developing a web app or simply need clean HTML output, this method ensures your workbook conversions are precise and secure.
If you found this tutorial helpful, consider exploring other features of Aspose.Cells to further enhance your Excel processing capabilities.
## FAQ's
### What are downlevel revealed comments?
Downlevel revealed comments are typically used in web development to provide extra information for older browsers that don't support certain HTML features. In Excel-to-HTML conversions, they can sometimes reveal hidden content or comments, which is why disabling them can be useful.
### Can I enable downlevel comments if I need them?
Yes, simply set the `DisableDownlevelRevealedComments` property to `false` if you want to enable downlevel comments when saving your workbook as HTML.
### How do I obtain a temporary license for Aspose.Cells?
You can easily apply for a temporary license by visiting the [Aspose website](https://purchase.aspose.com/temporary-license/).
### Does disabling downlevel comments affect the appearance of the HTML?
No, disabling downlevel revealed comments doesn’t affect the visual appearance of the HTML output. It only prevents the exposure of extra information meant for older browsers.
### Can I save the workbook in other formats besides HTML?
Yes, Aspose.Cells supports a variety of output formats such as PDF, CSV, and TXT. You can explore more options in the [documentation](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
