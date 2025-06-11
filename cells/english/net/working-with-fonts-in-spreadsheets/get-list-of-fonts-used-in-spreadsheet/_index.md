---
title: Get List of Fonts Used in Spreadsheet
linktitle: Get List of Fonts Used in Spreadsheet
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to fetch and list fonts from Excel spreadsheets using Aspose.Cells for .NET with this easy-to-follow tutorial.
weight: 10
url: /net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Get List of Fonts Used in Spreadsheet

## Introduction
Ever found yourself scrolling through an Excel spreadsheet, wondering about the fonts used in its various cells? Maybe you've encountered an old document and would love to know what typography choices were made? Well, you’re in luck! With Aspose.Cells for .NET, it’s like having a toolbox that lets you sift through and uncover those font secrets hidden in your spreadsheets. In this guide, we’ll take you through how to easily retrieve a list of all the fonts used in an Excel file. Buckle up, and let’s dive into the world of spreadsheets!
## Prerequisites
Before we jump into code, there are a few things you'll need to get started. Don’t worry, it’s really straightforward. Here’s a checklist of what you need:
1. Visual Studio: Make sure you have a version of Visual Studio installed on your machine. This is where we’ll write our code.
2. Aspose.Cells for .NET: You need to have Aspose.Cells library available. If you haven't downloaded it yet, you can grab it from the [site](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: A little understanding of C# programming will definitely help you navigate through the code easily.
4. A Sample Excel File: You will need a sample Excel file, like "sampleGetFonts.xlsx," to work with. This is where we’ll apply our font exploration.
Once you have everything squared away, you're ready to jump into coding!
## Import Packages
To kick things off, let’s import the necessary namespaces. In .NET, importing packages is akin to inviting the right guests to your party—without them, things just won’t work smoothly.
Here’s how to import Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
With this simple line, we're inviting the core functionality of Aspose.Cells into our project. Now, let's move on to loading the workbook.
## Step 1: Set the Document Directory
First things first—before we dive into the code, you need to set the path to your document directory. This is where your Excel file sits. 
```csharp
string dataDir = "Your Document Directory";
```
You’ll replace “Your Document Directory” with the actual path where your Excel file is located. Think of this as telling the program, “Hey, here’s where I’ve stashed my Excel file; go check it out!”
## Step 2: Load the Source Workbook
It's time to load up the Excel file. We'll create a new instance of the `Workbook` class and pass in the file's path. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
What’s happening here? We’re basically opening the door to our spreadsheet. The `Workbook` class allows us to interact with the contents of the Excel file. 
## Step 3: Get All Fonts
Now comes the magic moment—let's actually retrieve the fonts! The `GetFonts()` method is our golden ticket.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
Here, we're asking the workbook to spill the beans about all the fonts used within it. The `fnts` array will hold our treasures.
## Step 4: Print the Fonts
Finally, let’s take those fonts and print them out. This will help us verify what we’ve found.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
This loop runs through each font in our `fnts` array, outputting them to the console one by one. It's like showing off all the cool typography choices you have in your Excel file!
## Conclusion
And there you have it! With just a few lines of code, you've successfully retrieved and printed the list of fonts used in your Excel spreadsheet using Aspose.Cells for .NET. This is not just about fonts; it’s about understanding the subtleties of your documents, enhancing your presentations, and mastering the art of typography in your spreadsheets. Whether you’re a developer or someone who simply loves tinkering with Excel, this little snippet could be a game-changer. 
## FAQ's
### Do I need to install Aspose.Cells separately?
Yes, you need to download and reference the library in your project. 
### Can I use Aspose.Cells for other formats?
Absolutely! Aspose.Cells works with multiple Excel formats, like XLSX, XLS, and CSV.
### Is there a free trial available?
Yes, you can grab a free trial from the [download link](https://releases.aspose.com/).
### How can I get technical support?
If you need help, the [Aspose support forum](https://forum.aspose.com/c/cells/9) is a great resource.
### Is Aspose.Cells compatible with .NET Core?
Yes, Aspose.Cells is compatible with .NET Core projects as well.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
