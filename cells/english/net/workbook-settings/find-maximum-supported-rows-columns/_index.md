---
title: Find Max Rows and Columns Supported by XLS and XLSX Formats
linktitle: Find Max Rows and Columns Supported by XLS and XLSX Formats
second_title: Aspose.Cells .NET Excel Processing API
description: Discover the maximum rows and columns supported by XLS and XLSX formats using Aspose.Cells for .NET. Maximize your Excel data management with this comprehensive tutorial.
weight: 11
url: /net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Find Max Rows and Columns Supported by XLS and XLSX Formats

## Introduction
In the world of Excel, managing large datasets can be a daunting task, especially when it comes to handling the maximum number of rows and columns supported by different file formats. This tutorial will guide you through the process of finding the maximum rows and columns supported by the XLS and XLSX formats using the Aspose.Cells for .NET library. By the end of this article, you'll have a comprehensive understanding of how to utilize this powerful tool to handle your Excel-related tasks efficiently.
## Prerequisites
Before we dive into the tutorial, ensure that you have the following prerequisites in place:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) or [.NET Core](https://dotnet.microsoft.com/en-us/download) installed on your system.
2. [Aspose.Cells for .NET](https://releases.aspose.com/cells/net/) library downloaded and referenced in your project.
If you haven't already, you can download the Aspose.Cells for .NET library from the [website](https://releases.aspose.com/cells/net/) or install it via [NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Import Packages
To get started, you'll need to import the necessary packages from the Aspose.Cells for .NET library. Add the following using statements at the top of your C# file:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Step 1: Find the Maximum Rows and Columns Supported by the XLS Format
Let's start by exploring the maximum rows and columns supported by the XLS (Excel 97-2003) format.
```csharp
// Print message about XLS format.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Create workbook in XLS format.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Print the maximum rows and columns supported by XLS format.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
In this step, we:
1. Print a message to indicate that we're working with the XLS format.
2. Create a new `Workbook` instance using the `FileFormatType.Excel97To2003` enum, which represents the XLS format.
3. Retrieve the maximum rows and columns supported by the XLS format using the `Workbook.Settings.MaxRow` and `Workbook.Settings.MaxColumn` properties, respectively. We add 1 to these values to get the actual maximum row and column numbers (since they are zero-based).
4. Print the maximum rows and columns to the console.
## Step 2: Find the Maximum Rows and Columns Supported by the XLSX Format
Next, let's explore the maximum rows and columns supported by the XLSX (Excel 2007 and later) format.
```csharp
// Print message about XLSX format.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Create workbook in XLSX format.
wb = new Workbook(FileFormatType.Xlsx);
// Print the maximum rows and columns supported by XLSX format.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
In this step, we:
1. Print a message to indicate that we're working with the XLSX format.
2. Create a new `Workbook` instance using the `FileFormatType.Xlsx` enum, which represents the XLSX format.
3. Retrieve the maximum rows and columns supported by the XLSX format using the `Workbook.Settings.MaxRow` and `Workbook.Settings.MaxColumn` properties, respectively. We add 1 to these values to get the actual maximum row and column numbers (since they are zero-based).
4. Print the maximum rows and columns to the console.
## Step 3: Display a Success Message
Finally, let's display a success message to indicate that the "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" example has executed successfully.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
This step simply prints a success message to the console.
## Conclusion
In this tutorial, you've learned how to use the Aspose.Cells for .NET library to find the maximum rows and columns supported by the XLS and XLSX file formats. By understanding the limitations of these formats, you can better plan and manage your Excel-based projects, ensuring that your data fits within the supported ranges.
## FAQ's
### What is the maximum number of rows supported by the XLS format?
The maximum number of rows supported by the XLS (Excel 97-2003) format is 65,536.
### What is the maximum number of columns supported by the XLS format?
The maximum number of columns supported by the XLS (Excel 97-2003) format is 256.
### What is the maximum number of rows supported by the XLSX format?
The maximum number of rows supported by the XLSX (Excel 2007 and later) format is 1,048,576.
### What is the maximum number of columns supported by the XLSX format?
The maximum number of columns supported by the XLSX (Excel 2007 and later) format is 16,384.
### Can I use the Aspose.Cells for .NET library to work with other Excel file formats?
Yes, the Aspose.Cells for .NET library supports a wide range of Excel file formats, including XLS, XLSX, ODS, and more. You can explore the [documentation](https://reference.aspose.com/cells/net/) to learn about the available features and functionalities.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
