---
title: Extract OLE Object from Excel
linktitle: Extract OLE Object from Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to extract OLE objects from Excel files using Aspose.Cells for .NET. Step-by-step guide for easy extraction.
weight: 10
url: /net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract OLE Object from Excel

## Introduction
In today's tech-savvy world, dealing with Excel files is a common task, especially for those in data analysis, finance, and project management. One often-overlooked aspect is the handling of OLE (Object Linking and Embedding) objects within Excel spreadsheets. These could be embedded documents, images, or even complex data types that play a crucial role in enhancing the functionality and richness of your Excel files. If you're an Aspose.Cells user looking to extract these OLE objects programmatically using .NET, you're in the right place! This guide will walk you through the process step-by-step, ensuring you understand not just how to do it, but also why each part of the process is significant.
## Prerequisites
Before we dive into the nitty-gritty details of extracting OLE objects, there are a few things you must have in place:
1. Basic Knowledge of C#: If you’re familiar with C#, you’re already on the right path. If not, don’t worry! We’ll keep things straightforward.
2. Aspose.Cells Installed: You’ll need the Aspose.Cells library. You can download it from the site [here](https://releases.aspose.com/cells/net/).
3. A Compatible Development Environment: Make sure you have a .NET development environment set up, such as Visual Studio, ready to go.
4. A Sample Excel File: You’ll need an Excel file with OLE objects embedded for testing. 
Once you have these prerequisites in place, we can begin our journey into the world of OLE object extraction.
## Import Packages
First, let's import the necessary packages that we'll use in our tutorial. In your C# project, you will need to include the Aspose.Cells namespace. Here’s how you can do it:
```csharp
using System.IO;
using Aspose.Cells;
```
## Step 1: Set the Document Directory
In this step, we’ll define the path where our Excel file is located. You might wonder why this is important. It’s like setting the stage for a performance—it helps the script know where to find the actors (in our case, the Excel file).
```csharp
string dataDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path where your Excel file (`book1.xls`) is stored.
## Step 2: Open the Excel File
Now that we have our document directory set up, the next step is to open the Excel file. Think of this as opening a book before you start reading—it’s essential to see what’s inside.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## Step 3: Access the OLE Object Collection
Every worksheet in an Excel workbook can contain various objects, including OLE objects. Here, we’re accessing the first worksheet's OLE object collection. It’s similar to selecting a page to check out embedded images and documents.
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## Step 4: Loop Through the OLE Objects
Now comes the fun part—looping through all the OLE objects in our collection. This step is crucial as it allows us to handle multiple OLE objects efficiently. Imagine going through a treasure chest to find valuable items!
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    // Further logic to handle each object
}
```
## Step 5: Specify the Output Filename
As we dig deeper into each OLE object, we need to come up with a filename for the extracted objects. Why? Because once we extract them, we want to keep everything organized so we can easily find our treasures later.
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## Step 6: Determine the File Format Type
Each OLE object can be of different types (e.g., documents, spreadsheets, images). It’s crucial to determine the format type so you can extract it correctly. It’s like knowing the recipe for a dish—you need to know the ingredients!
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        // Handle other file formats
        break;
}
```
## Step 7: Save the OLE Object
Now, let’s move on to saving the OLE object. If the object is an Excel file, we will save it using a `MemoryStream` which allows us to handle the data in memory before writing it out. This step is akin to packaging your treasure before sending it off to a friend.
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
For other types of files, we’ll use a `FileStream` to create the file on the disk.
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## Conclusion
And just like that, you’ve successfully navigated the waters of OLE object extraction with Aspose.Cells for .NET! By following these steps, you can easily extract and manage embedded objects from your Excel files. Remember, like any valuable skill, practice makes perfect. So, take your time experimenting with different Excel files, and soon you’ll become an OLE extraction pro!
## FAQ's
### What are OLE objects in Excel?
OLE objects are technology that allows embedding and linking to documents and data in other applications within an Excel worksheet.
### Why would I need to extract OLE objects?
Extracting OLE objects allows you to access and manipulate embedded documents or images independently from the original Excel file.
### Can Aspose.Cells handle all types of embedded files?
Yes, Aspose.Cells can manage various OLE objects, including Word documents, Excel sheets, PowerPoint presentations, and images.
### How do I install Aspose.Cells for .NET?
You can install Aspose.Cells by downloading it from their [release page](https://releases.aspose.com/cells/net/).
### Where can I find support for Aspose.Cells?
You can get support for Aspose.Cells on their [support forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
