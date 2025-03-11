---
title: Get Page Dimensions of Worksheet
linktitle: Get Page Dimensions of Worksheet
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to get page dimensions in an Excel worksheet with Aspose.Cells for .NET. A step-by-step guide to customize A2, A3, A4, and Letter paper sizes.
weight: 13
url: /net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get Page Dimensions of Worksheet

## Introduction
If you're working with Excel files programmatically using Aspose.Cells for .NET, there may be times you need to access and set page dimensions of a worksheet. Knowing the dimensions can help with layouts, printing, and customization of Excel sheets for specific purposes. In this article, we’ll explore how to retrieve and display various page dimensions in Excel using Aspose.Cells for .NET. We'll go through a step-by-step tutorial to make sure you have all the details to get started confidently.
## Prerequisites
Before diving in, let’s ensure you have everything you need to follow along with this tutorial.
1. Aspose.Cells for .NET: Ensure you have Aspose.Cells for .NET installed. You can [download the library here](https://releases.aspose.com/cells/net/) or install it via NuGet in your .NET project.
2. .NET Environment: A compatible .NET development environment (e.g., Visual Studio).
3. License Setup: For the full functionality of Aspose.Cells, apply a license. You can [request a free temporary license](https://purchase.aspose.com/temporary-license/) for evaluation purposes.
Start with the free trial version of Aspose.Cells if you’re evaluating it for the first time.
## Import Packages
Before we jump into the code, you’ll need to import the Aspose.Cells namespace into your project to access all necessary classes and methods.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Let's break down the process into easy steps. Here, we’ll access different paper sizes, apply them to a worksheet, and print the dimensions for each.
## Step 1: Create a Workbook Instance
The first step is to create an instance of the `Workbook` class. This object will act as our main workbook containing worksheets that we can manipulate.
```csharp
Workbook book = new Workbook();
```
Think of `Workbook` as the main container for your Excel file. We need it to access and control individual worksheets.
## Step 2: Access the First Worksheet
Next, let’s access the first worksheet in the workbook. By default, a new workbook comes with one sheet, so we can directly reference it using an index of `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
The `Worksheets` collection in `Workbook` allows us to access each worksheet by index. Here, we grab the first sheet to start setting page dimensions.
## Step 3: Set Paper Size to A2 and Display Dimensions
Now that we have access to our worksheet, let’s set its paper size to A2. Setting the paper size is useful for formatting the page before printing or exporting it. Once we set the paper size, we’ll print the page dimensions in inches.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Here, we change the `PaperSize` property to `PaperA2`. After setting the size, `PageSetup.PaperWidth` and `PageSetup.PaperHeight` retrieve the width and height of the sheet in inches. This gives us a quick overview of the page dimensions.
## Step 4: Set Paper Size to A3 and Display Dimensions
Following the same steps as above, let’s adjust the page dimensions to A3 size. This change is useful for slightly larger prints or for fitting more content on one page.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3 size is double the size of A4, making it a good choice for large tables or detailed charts. Changing the paper size helps adapt the worksheet layout accordingly.
## Step 5: Set Paper Size to A4 and Display Dimensions
Now, let’s set the paper size to A4. This is the most commonly used page size for printing documents. We’ll display the updated dimensions afterward.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
If your target is a standard document format, A4 is typically the most suitable size. Knowing the dimensions can help in adjusting content layout to avoid printing issues.
## Step 6: Set Paper Size to Letter and Display Dimensions
Finally, we’ll set the paper size to the Letter format, which is commonly used in North America. Let’s print the dimensions one last time.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
The Letter size is widely used for documents in North America, so setting this size helps when collaborating with teams or clients based there.
## Conclusion
In this tutorial, we walked through how to set and retrieve page dimensions for different paper sizes using Aspose.Cells for .NET. By configuring page sizes like A2, A3, A4, and Letter, you can format Excel worksheets to suit specific printing and layout needs. This control over page dimensions is especially valuable for professional reporting and presentation, as it ensures your content fits perfectly on each page size.
## FAQ's
### How can I change the orientation of the page in Aspose.Cells?  
You can change the orientation using the `PageSetup.Orientation` property, setting it to either `PageOrientationType.Portrait` or `PageOrientationType.Landscape`.
### Can I set custom page dimensions in Aspose.Cells?  
Yes, you can set custom page dimensions by adjusting the margins and scaling options under `PageSetup` for more control.
### What is the default paper size in Aspose.Cells?  
The default paper size is typically A4. However, this may depend on regional settings and can be adjusted as needed.
### Is it possible to preview page layouts in Aspose.Cells?  
While Aspose.Cells does not offer a graphical preview, you can programmatically set up layouts and use print previews in Excel.
### How do I install Aspose.Cells for .NET?  
You can install Aspose.Cells using NuGet Package Manager in Visual Studio or download the DLL from the [Aspose.Cells download page](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
