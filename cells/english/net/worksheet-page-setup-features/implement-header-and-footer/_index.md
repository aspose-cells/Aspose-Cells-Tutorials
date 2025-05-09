---
title: Implement Header and Footer in Worksheet
linktitle: Implement Header and Footer in Worksheet
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to set up headers and footers in Excel worksheets using Aspose.Cells for .NET with a step-by-step tutorial, practical examples, and useful tips.
weight: 22
url: /net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implement Header and Footer in Worksheet

## Introduction

When working with Excel spreadsheets, headers and footers play a key role in delivering important contextual information, like file names, dates, or page numbers, to your audience. Whether you’re automating reports or generating dynamic files, Aspose.Cells for .NET makes it straightforward to customize headers and footers in worksheets programmatically. This guide dives into a comprehensive, step-by-step approach to add headers and footers with Aspose.Cells for .NET, giving your Excel files that extra polish and professionalism.

## Prerequisites

Before you begin, make sure you have the following in place:

1. Aspose.Cells for .NET: You’ll need Aspose.Cells for .NET installed. [Download it here](https://releases.aspose.com/cells/net/).
2. IDE Setup: Visual Studio (or your preferred IDE) with .NET framework installed.
3. License: While you can get started with the free trial, obtaining a full or temporary license will unlock Aspose.Cells' full potential. [Get a temporary license](https://purchase.aspose.com/temporary-license/).

The documentation for Aspose.Cells is a handy resource for reference throughout this process. You can find it [here](https://reference.aspose.com/cells/net/).

## Importing Packages

In your project, import the required namespaces:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

By importing this package, you’ll have access to the classes and methods needed to work with headers, footers, and other Excel functionalities within Aspose.Cells.

In this guide, we’ll break down each step so you can easily follow along, even if you’re new to Aspose.Cells or .NET.

## Step 1: Set Up Your Workbook and Page Setup

First things first: create a new workbook and access the worksheet’s page setup. This will give you the tools you need to modify the header and footer for the worksheet.

```csharp
// Define the path to save your document
string dataDir = "Your Document Directory";

// Instantiate a Workbook object
Workbook excel = new Workbook();
```

Here, we’ve created a `Workbook` object, which represents our Excel file. The `PageSetup` of the worksheet is where we can modify header and footer options.


## Step 2: Access the Worksheet and PageSetup Properties

In Aspose.Cells, each worksheet has a `PageSetup` property that controls layout features, including headers and footers. Let’s get the `PageSetup` object for our worksheet.

```csharp
// Obtain the reference to the PageSetup of the first worksheet
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

With this, `pageSetup` now holds all the settings needed to customize headers and footers.


## Step 3: Set the Left Section of the Header

Headers in Excel are divided into three sections: left, center, and right. Let’s start by setting the left section to display the worksheet name.

```csharp
// Set worksheet name at the left section of the header
pageSetup.SetHeader(0, "&A");
```

Using `&A` allows you to dynamically display the worksheet name. This is particularly helpful if you have multiple sheets in a workbook and want each header to reflect its sheet title.


## Step 4: Add Date and Time to the Center of the Header

Next, let’s add the current date and time to the center section of the header. Additionally, we’ll use a custom font for styling.

```csharp
// Set date and time in the center section of the header with bold font
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

In this code:
- `&D` inserts the current date.
- `&T` inserts the current time.
- `"Times New Roman,Bold"` applies Times New Roman in bold to these elements.


## Step 5: Display File Name in the Right Section of the Header

To complete the header, let’s show the file name on the right side, along with a font adjustment.

```csharp
// Display file name in the right section of the header with custom font size
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` represents the file name, making it clear which file the printed pages belong to.
- `&12` changes the font size to 12 for this section.


## Step 6: Add Text with Custom Font to the Left Footer Section

Moving on to footers! We’ll start by setting up the left footer section with custom text and a specified font style.

```csharp
// Add custom text with font style to the left section of the footer
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

The `&\"Courier New\"&14` setting in the above code applies "Courier New" font with size 14 to the specified text (`123`). The rest of the text remains in the default footer font.


## Step 7: Insert Page Number in the Center of the Footer

Including page numbers in the footer is a great way to help readers keep track of multi-page documents.

```csharp
// Insert page number in the center section of the footer
pageSetup.SetFooter(1, "&P");
```

Here, `&P` adds the current page number to the footer’s center section. It’s a small detail, but crucial for professional-looking documents.


## Step 8: Show Total Page Count in the Right Footer Section

Finally, let’s complete the footer by displaying the total page count in the right section.

```csharp
// Display total page count in the right section of the footer
pageSetup.SetFooter(2, "&N");
```

- `&N` provides the total page count, letting readers know how long the document is.


## Step 9: Save the Workbook

Once you’ve set up your headers and footers, it’s time to save the workbook. This is the final step to generate an Excel file with fully customized headers and footers.

```csharp
// Save the Workbook
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

This line saves the file to your designated directory with the custom headers and footers in place.


## Conclusion

Adding headers and footers to Excel worksheets is a valuable skill for creating organized, professional documents. With Aspose.Cells for .NET, you have complete control over your Excel files’ headers and footers, from displaying the worksheet name to inserting custom text, date, time, and even dynamic page numbers. Now that you've seen each step in action, you can take your Excel automation to the next level.

## FAQ's

### Can I use different fonts for different sections of headers and footers?  
Yes, Aspose.Cells for .NET allows you to specify fonts for each section of the header and footer using specific font tags.

### How do I remove headers and footers?  
You can clear headers and footers by setting the header or footer text to an empty string with `SetHeader` or `SetFooter`.

### Can I insert images into headers or footers with Aspose.Cells for .NET?  
Currently, Aspose.Cells primarily supports text in headers and footers. Images may require a workaround, such as inserting images into the worksheet itself.

### Does Aspose.Cells support dynamic data in headers and footers?  
Yes, you can use various dynamic codes (like `&D` for date or `&P` for page number) to add dynamic content.

### How can I adjust the header or footer height?  
Aspose.Cells provides options within the `PageSetup` class to adjust header and footer margins, giving you control over spacing.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
