---
title: Change Source Data of Pivot Table Programmatically in .NET
linktitle: Change Source Data of Pivot Table Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to change pivot table source data programmatically using Aspose.Cells for .NET with our comprehensive step-by-step tutorial.
weight: 10
url: /net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Change Source Data of Pivot Table Programmatically in .NET

## Introduction
In the world of data analysis, few tools shine as bright as Microsoft Excel. Every day, countless users depend on Excel for managing and analyzing data, but behind the scenes, it's a lot more complex than just clicking and dragging. If you've ever wanted to programmatically manipulate Excel files—specifically, to change the source data of a pivot table—you're in the right place! In this guide, we'll explore how you can achieve this using Aspose.Cells for .NET. Whether you’re a seasoned developer or just dipping your toes into the sea of programming, you'll find this tutorial packed with valuable information that’s easy to follow.
## Prerequisites
Before we get started on our journey of changing the source data of a pivot table, let’s make sure you’ve got everything set up and ready to go:
1. Visual Studio: Ensure you have a copy of Microsoft Visual Studio installed, as we'll be writing our code here.
2. Aspose.Cells Library: You’ll need to have the Aspose.Cells library downloaded and referenced in your project. You can download it [here](https://releases.aspose.com/cells/net/).
3. Basic Knowledge of C#: While this tutorial is simplified, having a grasp of C# will help you better understand the code.
4. Excel File: You should have a sample Excel file (like "Book1.xlsx") containing a pivot table that we can manipulate.
Alright, with these prerequisites in check, we can proceed to import the necessary packages and get coding!
## Import Packages
First things first—let's import the packages we’ll need. Open up your C# project in Visual Studio and add the following using directives at the top of your code file:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
These namespaces will give you access to the essential classes needed for working with Excel files and manipulating their content using Aspose.Cells.

Now, let’s break down the process into manageable steps. We'll walk through opening an Excel file, modifying the worksheet, changing the pivot table's data source, and saving the results.
## Step 1: Define Your Document Directory
First, you need to specify where your Excel file is located. Modify the `dataDir` variable to point to the folder containing your "Book1.xlsx".
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
This line sets up the directory where your Excel file is stored, making it easier to access later on.
## Step 2: Specify the Input Path
Next, let’s create a string to specify the full path to your input Excel file:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
This helps in streamlining your file access; you won’t have to keep typing the same path multiple times throughout your code.
## Step 3: Create a File Stream
Now it’s time to open the Excel file. We’ll create a `FileStream` that lets you read the content of the Excel file:
```csharp
// Creating a file stream containing the Excel file to be opened
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
This line opens the file in read mode, allowing us to access its data.
## Step 4: Load the Workbook
With the file stream in place, the next step is to load the workbook:
```csharp
// Opening the Excel file through the file stream
Workbook workbook = new Workbook(fstream);
```
This command takes your Excel file and loads it into a `Workbook` object. Once loaded, you can manipulate the file as needed.
## Step 5: Access the Worksheet
Time to dive into the specifics. We’ll access the first worksheet in the workbook:
```csharp
// Accessing the first worksheet in the Excel file
Worksheet worksheet = workbook.Worksheets[0];
```
This gives you direct access to the data within the first worksheet, making it easy to modify.
## Step 6: Populate New Data
Next, we want to insert new data into the cells. In this example, we’ll add some sample data:
```csharp
// Populating new data to the worksheet cells
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
Here, we’re putting the values "Golf", "Qtr4", and `7000` into specific cells. You can change these values to whatever suits your needs.
## Step 7: Change the Named Range
Now, we’ll change the named range that the pivot table refers to. This involves creating or updating a range:
```csharp
// Changing named range "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
By defining a new range, we ensure that the pivot table uses this new data when it refreshes.
## Step 8: Save the Modified Excel File
After all the changes, it’s crucial to save your work! Let’s save the modified workbook:
```csharp
// Saving the modified Excel file
workbook.Save(dataDir + "output.xls");
```
This command saves the workbook to a new file, so you don’t overwrite your original file unless you want to!
## Step 9: Close the File Stream
Finally, it’s essential to close the file stream to release any resources you're using:
```csharp
// Closing the file stream to free all resources
fstream.Close();
```
This step ensures that your application doesn't leak memory and remains efficient.
## Conclusion
Congratulations! You've just successfully changed the source data of a pivot table programmatically in .NET using Aspose.Cells. This functionality opens up many possibilities for automating Excel tasks and improving your workflow. Whether you're updating financial reports, tracking sales data, or even just playing around with datasets, having the ability to do this programmatically can save you heaps of time and reduce the risk of errors.

## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful .NET library for working with Excel files, allowing users to create, modify, and manipulate Excel documents programmatically.
### Can I change the source data of existing pivot tables using this method?
Absolutely! This method allows you to update the data source for existing pivot tables within your Excel workbook.
### Do I need to have Office installed to use Aspose.Cells?
Nope! Aspose.Cells is a standalone library, meaning you don’t need Microsoft Office installed to work with Excel files.
### Is Aspose.Cells free to use?
Aspose.Cells offers a free trial version, but for full functionality, you will have to purchase a license. You can find the details [here](https://purchase.aspose.com/buy).
### Where can I find more examples and support?
For more examples and support, check out the [Aspose.Cells documentation](https://reference.aspose.com/cells/net/) and their community forum [here](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
