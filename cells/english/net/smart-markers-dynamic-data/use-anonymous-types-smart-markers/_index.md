---
title: Use Anonymous Types with Smart Markers Aspose.Cells
linktitle: Use Anonymous Types with Smart Markers Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to use anonymous types with smart markers in Aspose.Cells for dynamic Excel report generation in .NET. Follow our easy guide.
weight: 17
url: /net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Use Anonymous Types with Smart Markers Aspose.Cells

## Introduction
When it comes to generating dynamic Excel reports in .NET applications, Aspose.Cells stands out as a powerful tool. One of its best features is the capability to work with smart markers and anonymous types. If you’re new to this concept, don’t worry! This guide will break down everything you need to know, from prerequisites to hands-on examples, all while keeping it engaging and easy to follow.
## Prerequisites
Before we dive into the code, let's ensure you have everything you need to smoothly run the examples in this tutorial.
### 1. .NET Environment
Make sure you have a functioning .NET environment set up on your local machine. You can use Visual Studio or any other IDE of your choice.
### 2. Aspose.Cells Library
You'll need the Aspose.Cells library. If you haven't downloaded it yet, you can easily find it [here](https://releases.aspose.com/cells/net/). You can also try it out with a free trial available at [this link](https://releases.aspose.com/).
### 3. Basic Knowledge of C#
A fundamental understanding of C# programming will help you navigate through the tutorial more easily. If terms like classes, objects, and properties are familiar to you, you're good to go!
## Import Packages
To use the Aspose.Cells library in your project, you must import the related namespaces. Add the following using directives at the top of your C# file:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
These namespaces will give you access to all the necessary classes and methods that will be discussed later.
Now, let’s get into the meat of the tutorial! You’ll see how to create an Excel file with smart markers using a custom class. Don’t worry; we'll break everything down into manageable steps!
## Step 1: Create a Custom Class
First up, we need a simple class to represent the data we want to add to our Excel file. This class will hold information about a person.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
Here, we are defining a class called `Person` with two properties, `Name` and `Age`. The constructor initializes these properties. 
## Step 2: Set Up the Workbook Designer
Next, let’s create an instance of the `WorkbookDesigner` class, which we’ll use to design our Excel file with smart markers.
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
// Instantiate the workbook designer object.
WorkbookDesigner report = new WorkbookDesigner();
```
Replace `"Your Document Directory"` with your actual file path where you want to save the Excel file. The `WorkbookDesigner` class is the heart of this operation, where you define your template.
## Step 3: Add Markers to Cells
Now, we need to add smart markers to the worksheet. These markers will be placeholders for the data we will input later.
```csharp
// Get the first worksheet in the workbook.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Input some markers to the cells.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
We designate the first worksheet and set values for the header cells. The smart markers are prefixed with `&=` which tells Aspose that these are placeholders for data to be inserted later.
## Step 4: Create a List of People
Now let’s create a list of people using our `Person` class that we will use to populate the smart markers.
```csharp
// Instantiate the list collection based on the custom class.
IList<Person> list = new List<Person>();
// Provide values for the markers using the custom class object.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
We create a list and add instances of `Person` to it. This list serves as our data source when populating the Excel template.
## Step 5: Set Data Source and Process Markers
After we have our list ready, we need to set it as the data source for our `WorkbookDesigner` instance and then process the markers.
```csharp
// Set the data source.
report.SetDataSource("MyProduct", list);
// Process the markers.
report.Process(false);
```
The `SetDataSource` method links our previously defined list to the markers. The `Process` method replaces the smart markers in the workbook with actual values from our objects.
## Step 6: Save the Excel File
Finally, we will save the modified workbook to our designated directory.
```csharp
// Save the excel file.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
This line saves the workbook to the specified file path. You can open this file using Excel to see the inserted data.
## Conclusion
And there you have it! You've successfully created an Excel file using smart markers in Aspose.Cells with your own custom class. This method not only makes your data management more dynamic but also keeps your code clean and organized.
So, whether you're generating reports for analytics, tracking information, or any other data-related task, smart markers are your ally in making Excel reports more manageable and flexible!
## FAQ's
### What are smart markers in Aspose.Cells?
Smart markers are special placeholders in your Excel document that allow you to dynamically insert data during runtime.
### Can I use anonymous types for smart markers?
Yes! Smart markers can be used with any object type, including anonymous types, as long as they match the expected data structure.
### Is Aspose.Cells free to use?
Aspose.Cells is a paid product, but you can start with a free trial to explore its features.
### What file formats does Aspose.Cells support?
It supports a wide range of file formats, including XLS, XLSX, CSV, and more.
### Where can I find more information about Aspose.Cells?
For more details, check out the [documentation](https://reference.aspose.com/cells/net/) or visit the [support forum](https://forum.aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
