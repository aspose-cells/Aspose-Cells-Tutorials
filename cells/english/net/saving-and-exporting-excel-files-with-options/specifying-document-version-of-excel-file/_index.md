---
title: Specifying Document Version of Excel File Programmatically in .NET
linktitle: Specifying Document Version of Excel File Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to specify document properties like version, author, and title in an Excel file programmatically using Aspose.Cells for .NET with step-by-step instructions.
weight: 12
url: /net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specifying Document Version of Excel File Programmatically in .NET

## Introduction
Aspose.Cells for .NET is a powerful library that allows developers to programmatically manipulate Excel files with ease. Whether you’re looking to create Excel files from scratch or modify existing ones, Aspose.Cells offers a comprehensive API to achieve your goals. One such feature is specifying document properties like version, author, or title. This tutorial will walk you through how to specify the document version of an Excel file programmatically using Aspose.Cells for .NET.
## Prerequisites
Before we dive into the details, let’s ensure you have everything you need to follow along with this tutorial:
1. Aspose.Cells for .NET: You can download the latest version [here](https://releases.aspose.com/cells/net/). If you haven’t purchased a license yet, you can opt for a [temporary license](https://purchase.aspose.com/temporary-license/) to explore the features.
2. .NET Development Environment: You can use Visual Studio or any .NET-compatible IDE.
3. Basic Knowledge of C#: Understanding of C# programming will make it easier to follow along.
## Import Packages
Before you can start coding, you need to import the necessary namespaces from the Aspose.Cells library. This will give you access to the classes and methods required for Excel file manipulation.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
These two namespaces will be essential for interacting with the workbook and its built-in document properties.
Now, let’s break down the process of specifying document properties in an Excel file, including the version, title, and author.
## Step 1: Initialize the Workbook Object
The first step is to create a new instance of the `Workbook` object. This object represents the entire Excel file you’ll be working with.
```csharp
Workbook wb = new Workbook();
```
The `Workbook` class provides a representation of an Excel file. By instantiating it, we create a blank Excel workbook that we can manipulate.
## Step 2: Access Built-In Document Properties
Aspose.Cells offers built-in document properties, which include fields like title, author, and document version. You can access these properties through the `BuiltInDocumentProperties` collection.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
The `BuiltInDocumentPropertyCollection` class provides access to a collection of built-in document properties, such as the title, author, and other metadata typically associated with the document.
## Step 3: Set the Title of the Excel Document
Next, we’ll set the title of the Excel document. This metadata helps in identifying and managing the file later on.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Setting the title is important for document organization. This metadata can be seen in file properties and can be used by external systems to catalog or identify the document more effectively.
## Step 4: Specify the Author
The author of the document can also be specified to reflect who created or modified the file.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
This step helps in attributing the document to its creator, providing additional metadata for document management or collaboration scenarios.
## Step 5: Specify the Document Version
One of the most crucial properties we are addressing in this tutorial is the document version. This step lets you specify the version of the document, which is helpful when working in environments that require version control.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Setting the document version provides clarity regarding which version of the document or library was used to create the file. This is particularly important in environments that need to track file revisions or compatibility with different library versions.
## Step 6: Save the Excel File
Finally, you can save the Excel file with all the properties you have just set. Aspose.Cells allows you to save the file in various formats, but for this example, we’ll stick with the `.xlsx` format.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
The `Save` method is used to save the file to your specified directory. Here, we’re saving it as an Excel file in the `.xlsx` format. If needed, Aspose.Cells also supports formats like `.xls`, `.csv`, and `.pdf`, providing flexibility based on your project needs.
## Conclusion
In this tutorial, we walked through how to specify document properties, particularly the document version, in an Excel file using Aspose.Cells for .NET. Aspose.Cells is an extremely flexible and powerful tool that allows you to manipulate Excel files programmatically, making it a great asset for any .NET developer working with spreadsheets.
## FAQ's
### Can I modify other built-in properties using Aspose.Cells?  
Yes, you can modify other built-in properties such as the subject, keywords, and comments, among others.
### What file formats are supported by Aspose.Cells?  
Aspose.Cells supports a wide variety of formats including `.xls`, `.xlsx`, `.csv`, `.pdf`, and more.
### Do I need a license to use Aspose.Cells for .NET?  
You can explore Aspose.Cells with a [free trial](https://releases.aspose.com/) or apply for a [temporary license](https://purchase.aspose.com/temporary-license/) for extended testing.
### Can I use Aspose.Cells in a web application?  
Yes, Aspose.Cells can be used in both desktop and web applications. It’s highly versatile and integrates well with .NET web frameworks.
### Where can I get support for Aspose.Cells?  
You can access community and support through the [Aspose.Cells support forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
