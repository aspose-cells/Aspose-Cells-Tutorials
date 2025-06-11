---
title: Read And Write External Connection Of XLSB File
linktitle: Read And Write External Connection Of XLSB File
second_title: Aspose.Cells for .NET API Reference
description: Learn how to manage external connections in XLSB files using Aspose.Cells for .NET in this comprehensive tutorial.
weight: 130
url: /net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Read And Write External Connection Of XLSB File

## Introduction

Hey there, Excel enthusiasts! Are you ready to dive into the fascinating world of XLSB files and external connections? If you've ever worked with Excel, you know how powerful and versatile it can be, but sometimes it comes with its quirks—especially when dealing with connections to external databases. That’s where Aspose.Cells for .NET comes to the rescue! This nifty library allows you to manipulate Excel files in a straightforward manner. In this article, we'll walk you through a step-by-step guide on how to read and write external connections in an XLSB file.

## Prerequisites

Before we get started, here are a few things you’ll need:

1. Basic Knowledge of C#: Knowing your way around the C# programming language will help immensely. If you're comfortable writing C# code, you're good to go!
2. Aspose.Cells for .NET: You’ll need to have this library installed in your development environment. If you haven't done that yet, you can easily download it [here](https://releases.aspose.com/cells/net/). 
3. An IDE: You’ll need a code editor or an Integrated Development Environment (IDE) such as Visual Studio. 
4. Sample XLSB File: We'll be working with a sample XLSB file that contains external connections. You can create your own or download samples online. 

Once you have all these prerequisites in place, we're ready to jump into the code!

## Import Packages

To begin with, let’s import the necessary packages in our project. Make sure you have added a reference to Aspose.Cells in your project. Here is how you can do that in C#:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

These imports give you access to the functionality you’ll need to manipulate Excel files and their connections.

## Step 1: Set Up Directories

Before working with your XLSB file, you need to set up your source and output directories. This step is essential for keeping your files organized.

```csharp
// Source directory
string sourceDir = "Your Document Directory";
// Output directory
string outputDir = "Your Output Directory";
```

In this code snippet, `"Your Document Directory"` and `"Your Document Directory"` are assumed to fetch the respective paths for where your input and output files will reside. You can replace these methods with hardcoded paths if you prefer.

## Step 2: Load the XLSB File

Now it's time to load your Excel file into a Workbook object. This gives you the ability to manipulate the data within.

```csharp
// Load the source Excel Xlsb file
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

Just make sure that your XLSB file is located in the specified `sourceDir`. If the path is correct, your workbook will be ready for manipulation!

## Step 3: Access External Connections

With the workbook loaded, you can access its external connections. In our case, we'll retrieve the first database connection.

```csharp
// Read the first external connection which is actually a DB-Connection
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

Here, `DataConnections[0]` refers to the first connection in the workbook. We’re casting it as a `DBConnection` type for further manipulation.

## Step 4: Extract Connection Information

Now that you have access to the database connection, let's extract and print its details to the console. This will help us see exactly what we're working with.

```csharp
// Print the Name, Command and Connection Info of the DB-Connection
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

This step allows you to verify the current state of your external connection. You'll see the connection name, the command used, and the connection info printed to the console.

## Step 5: Modify the Connection

Sometimes, a name change is all that's needed to make things clearer or to match new naming conventions. Let’s change the existing connection name to something more relevant.

```csharp
// Modify the Connection Name
dbCon.Name = "NewCust";
```

This line of code effectively renames your connection from its original name to "NewCust". It’s a simple yet impactful change!

## Step 6: Save Your Changes

After making modifications, you’ll want to save your changes back to the XLSB file. Here’s how to do it:

```csharp
// Save the Excel Xlsb file
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

This line of code saves your updated workbook, retaining all your changes, including the new connection name.

## Step 7: Confirm Execution

Finally, let’s confirm that everything worked smoothly. A simple message at the end will make it clear.

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

This message will reassure you that your code ran successfully, and all the changes were saved as expected.

## Conclusion

And there you have it! You’ve successfully learned how to read and write external connections in XLSB files using Aspose.Cells for .NET. By following these steps, you can effectively manage your Excel data connections, making your work with Excel much more streamlined and less frustrating. Remember, whether you’re handling extensive datasets or simply organizing your information, Aspose.Cells has the tools you need.

## FAQ's

### What is an XLSB file?  
An XLSB file is a binary Excel file format that stores spreadsheet data in a binary format, making it more compact and faster to open.

### How do I install Aspose.Cells for .NET?  
You can easily download it from the Aspose website [here](https://releases.aspose.com/cells/net/).

### Can I use Aspose.Cells for free?  
Yes! You can start with a free trial, which is available [here](https://releases.aspose.com/).

### Does Aspose.Cells support other file formats?  
Absolutely! Aspose.Cells supports a variety of file formats, including XLSX, CSV, and more.

### Where can I seek help if I run into issues?  
You can get support from the Aspose forums [here](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
