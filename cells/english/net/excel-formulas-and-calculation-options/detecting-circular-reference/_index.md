---
title: Detecting Circular Reference in Excel Programmatically
linktitle: Detecting Circular Reference in Excel Programmatically
second_title: Aspose.Cells .NET Excel Processing API
description: Easily detect circular references in Excel using Aspose.Cells for .NET. Follow our step-by-step guide to ensure accurate calculations in your spreadsheets.
weight: 13
url: /net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Detecting Circular Reference in Excel Programmatically

## Introduction
When it comes to working with Excel files, one of the most frustrating issues you might encounter is a circular reference. This happens when a formula refers back to its own cell, either directly or indirectly, creating a loop that can confuse Excel's calculation engine. But fear not! With Aspose.Cells for .NET, you can programmatically detect these pesky circular references, ensuring your spreadsheets remain functional and accurate. In this guide, we’ll walk you through the process step-by-step, making it as simple as pie.
## Prerequisites
Before we dive into the nitty-gritty of detecting circular references, let’s ensure you have everything you need to get started:
1. Visual Studio: Make sure you have Visual Studio installed on your machine. This will be your development environment.
2. .NET Framework: Ensure that you’re using a compatible version of the .NET Framework (at least .NET Framework 4.0).
3. Aspose.Cells Library: You need to have the Aspose.Cells library. You can download it from the [Aspose website](https://releases.aspose.com/cells/net/).
4. Basic Knowledge of C#: Familiarity with C# programming will be beneficial, as we’ll be writing code in this language.
5. Excel File: Have an Excel file ready that contains circular references for testing. You can create a simple one or download a sample.
Now that we have our prerequisites in place, let’s move on to the fun part!
## Import Packages
Before you can start coding, you need to import the necessary packages. Here’s how to do it:
### Create a New Project
- Open Visual Studio and create a new C# Console Application project.
### Add Aspose.Cells Reference
- Right-click on your project in the Solution Explorer.
- Select "Manage NuGet Packages."
- Search for “Aspose.Cells” and install the latest version.
### Import Required Namespaces
At the top of your `Program.cs` file, import the necessary namespaces:
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

Now that we have everything set up, let’s dive into the code to detect circular references in an Excel file.
## Step 1: Define the Input Directory
First, you need to specify the directory where your Excel file is located. This is where you'll load your Excel file.
```csharp
// Input directory
string sourceDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path to your Excel file.
## Step 2: Load the Workbook with LoadOptions
Next, you’ll load your Excel workbook. This is where the magic begins!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
Here, we’re creating a new instance of `LoadOptions` and loading the workbook from the specified path. Make sure your Excel file name matches!
## Step 3: Enable Iteration Settings
To allow for circular references, you need to enable the iteration settings in the workbook.
```csharp
objWB.Settings.Iteration = true;
```
This tells Aspose.Cells to allow circular references during calculation.
## Step 4: Create Calculation Options and Circular Monitor
Now, let’s create the calculation options and our custom circular monitor.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
Here, we’re creating an instance of `CalculationOptions` and a custom `CircularMonitor`. This monitor will help track any circular references found during calculations.
## Step 5: Calculate the Formulas
Now, it’s time to calculate the formulas in your workbook.
```csharp
objWB.CalculateFormula(copts);
```
This line executes the calculation and checks for circular references.
## Step 6: Count Circular References
After the calculation, you can count how many circular references were found.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
This will output the number of circular references detected in your Excel file.
## Step 7: Display Results
Finally, let’s display the results and confirm that our method executed successfully.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## Step 8: Implement the CircularMonitor Class
To complete the process, you’ll need to implement the `CircularMonitor` class. This class will inherit from `AbstractCalculationMonitor` and handle the detection of circular references.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
This class captures the details of each circular reference found, including the worksheet name and cell index.
## Conclusion
Detecting circular references in Excel using Aspose.Cells for .NET is a straightforward process once you break it down into manageable steps. By following this guide, you can easily identify and handle circular references in your spreadsheets, ensuring your calculations remain accurate and reliable. Whether you're a seasoned developer or just starting out, Aspose.Cells provides powerful tools to enhance your Excel manipulation capabilities. 
## FAQ's
### What is a circular reference in Excel?
A circular reference occurs when a formula refers back to its own cell, causing an endless loop in calculations.
### How can I detect circular references programmatically?
You can use the Aspose.Cells library in .NET to programmatically detect circular references by implementing a custom calculation monitor.
### What are the prerequisites for using Aspose.Cells?
You need Visual Studio, the .NET Framework, and the Aspose.Cells library installed.
### Can I use Aspose.Cells for free?
Yes, Aspose.Cells offers a free trial that you can use to explore its features.
### Where can I find more information about Aspose.Cells?
You can visit the [Aspose.Cells documentation](https://reference.aspose.com/cells/net/) for detailed information and examples.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
