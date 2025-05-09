---
title: Read Created Time of Threaded Comments in Worksheet
linktitle: Read Created Time of Threaded Comments in Worksheet
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to read created time of threaded comments in Excel using Aspose.Cells for .NET. Step-by-step guide with code examples included.
weight: 21
url: /net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Read Created Time of Threaded Comments in Worksheet

## Introduction
When working with Excel files, managing comments can be a crucial aspect of data collaboration and feedback. If you’re using Aspose.Cells for .NET, you’ll find it incredibly powerful for handling various Excel functionalities, including threaded comments. In this tutorial, we’ll focus on how to read the created time of threaded comments in a worksheet. Whether you're a seasoned developer or just starting, this guide will walk you through the process step-by-step.
## Prerequisites
Before we dive into the code, let’s make sure you have everything you need to get started:
1. Aspose.Cells for .NET: Ensure that you have the Aspose.Cells library installed. You can download it from the [Aspose website](https://releases.aspose.com/cells/net/).
2. Visual Studio: A working installation of Visual Studio or any other .NET IDE where you can write and execute your C# code.
3. Basic Knowledge of C#: Familiarity with C# programming will help you understand the code snippets better.
4. Excel File: Have an Excel file ready with some threaded comments. For this example, we’ll use a file named `ThreadedCommentsSample.xlsx`.
Now that we have our prerequisites covered, let’s import the necessary packages.
## Import Packages
To get started with Aspose.Cells, you need to import the required namespaces. Here’s how to do it:
### Import the Aspose.Cells Namespace
Open your C# project in Visual Studio and add the following using directive at the top of your code file:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
This namespace allows you to access all the classes and methods provided by the Aspose.Cells library.
Now that we’ve set the stage, let’s break down the process of reading the created time of threaded comments into manageable steps.
## Step 1: Define the Source Directory
First, you need to specify the directory where your Excel file is located. This is crucial because the program needs to know where to look for the file.
```csharp
// Source directory
string sourceDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path to your Excel file. This could be something like `"C:\\Documents\\"`.
## Step 2: Load the Workbook
Next, you’ll load the Excel workbook that contains the threaded comments. Here’s how you do it:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
This line of code creates a new `Workbook` object by loading the specified Excel file. If the file is not found, an exception will be thrown, so ensure the path is correct.
## Step 3: Access the Worksheet
Once the workbook is loaded, the next step is to access the specific worksheet that contains the comments. In our case, we’ll access the first worksheet:
```csharp
// Access first worksheet
Worksheet worksheet = workbook.Worksheets[0];
```
This line retrieves the first worksheet (index 0) from the workbook. If your comments are located on a different worksheet, adjust the index accordingly.
## Step 4: Get Threaded Comments
Now, it’s time to retrieve the threaded comments from a specific cell. In this example, we’ll get comments from cell A1:
```csharp
// Get Threaded Comments
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
This line fetches all the threaded comments associated with cell A1. If there are no comments, the collection will be empty.
## Step 5: Iterate Through Comments
With the threaded comments retrieved, we can now loop through them and display the details, including the created time:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
This loop goes through each comment in the `threadedComments` collection and prints out the comment text, the author's name, and the time the comment was created.
## Step 6: Confirmation Message
Finally, after executing the comment reading logic, it’s always a good idea to provide a confirmation message. This helps in debugging and ensures that the code has executed successfully:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## Conclusion
Congratulations! You’ve successfully learned how to read the created time of threaded comments in an Excel worksheet using Aspose.Cells for .NET. This functionality can be incredibly useful for tracking feedback and collaboration in your Excel documents. With just a few lines of code, you can extract valuable information that can enhance your data analysis and reporting processes.
## FAQ's
### What is Aspose.Cells for .NET?
Aspose.Cells for .NET is a powerful library that allows developers to create, manipulate, and convert Excel files in .NET applications.
### How can I download Aspose.Cells for .NET?
You can download it from the [Aspose website](https://releases.aspose.com/cells/net/).
### Is there a free trial available?
Yes, you can try Aspose.Cells for free by visiting the [free trial page](https://releases.aspose.com/).
### Can I access comments from other cells?
Absolutely! You can modify the cell reference in the `GetThreadedComments` method to access comments from any cell.
### Where can I get support for Aspose.Cells?
For support, you can visit the [Aspose forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
