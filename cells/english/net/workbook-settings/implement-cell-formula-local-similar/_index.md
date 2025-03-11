---
title: Implement Cell Formula Local Similar to Range Formula Local
linktitle: Implement Cell Formula Local Similar to Range Formula Local
second_title: Aspose.Cells .NET Excel Processing API
description: Discover how to implement a cell formula that is similar to the range formula local functionality in Aspose.Cells for .NET. Learn to customize built-in Excel function names and more.
weight: 13
url: /net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implement Cell Formula Local Similar to Range Formula Local

## Introduction
Aspose.Cells for .NET is a powerful and flexible spreadsheet manipulation API that allows you to programmatically create, manipulate, and convert Excel files. One of the many features offered by Aspose.Cells is the ability to customize the behavior of built-in Excel functions, including the ability to create your own local function names. In this tutorial, we'll walk you through the steps to implement a cell formula that is similar to the range formula local functionality in Aspose.Cells for .NET.
## Prerequisites
Before you begin, make sure you have the following:
1. Microsoft Visual Studio 2010 or later installed on your system.
2. The latest version of the Aspose.Cells for .NET library installed in your project. You can download the library from the [Aspose.Cells for .NET download page](https://releases.aspose.com/cells/net/).
## Import Packages
To get started, you'll need to import the necessary packages in your C# project. Add the following using statements at the top of your code file:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Step 1: Create a Custom Globalization Settings Class
The first step is to create a custom `GlobalizationSettings` class that will allow you to override the default behavior of Excel functions. In this example, we'll be changing the names of the `SUM` and `AVERAGE` functions to `UserFormulaLocal_SUM` and `UserFormulaLocal_AVERAGE`, respectively.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //Change the SUM function name as per your needs.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //Change the AVERAGE function name as per your needs.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Step 2: Create a New Workbook and Assign the Custom Globalization Settings
Next, create a new Workbook instance and assign the custom `GlobalizationSettings` implementation class to the Workbook's `Settings.GlobalizationSettings` property.
```csharp
//Create workbook
Workbook wb = new Workbook();
//Assign GlobalizationSettings implementation class
wb.Settings.GlobalizationSettings = new GS();
```
## Step 3: Access the First Worksheet and a Cell
Now, let's access the first worksheet in the workbook and a specific cell within that worksheet.
```csharp
//Access first worksheet
Worksheet ws = wb.Worksheets[0];
//Access some cell
Cell cell = ws.Cells["C4"];
```
## Step 4: Assign Formulas and Print the FormulaLocal
Finally, let's assign the `SUM` and `AVERAGE` formulas to the cell and print the resulting `FormulaLocal` values.
```csharp
//Assign SUM formula and print its FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//Assign AVERAGE formula and print its FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Conclusion
In this tutorial, you've learned how to implement a cell formula that is similar to the range formula local functionality in Aspose.Cells for .NET. By creating a custom `GlobalizationSettings` class, you can override the default behavior of Excel functions and customize the local function names to suit your needs. This can be particularly useful when working with localized or internationalized Excel documents.
## FAQ's
### What is the purpose of the `GlobalizationSettings` class in Aspose.Cells?
The `GlobalizationSettings` class in Aspose.Cells allows you to customize the behavior of built-in Excel functions, including the ability to change the local function names.
### Can I override the behavior of functions other than `SUM` and `AVERAGE`?
Yes, you can override the behavior of any built-in Excel function by modifying the `GetLocalFunctionName` method in your custom `GlobalizationSettings` class.
### Is there a way to reset the function names back to their default values?
Yes, you can reset the function names by either removing the custom `GlobalizationSettings` class or by returning an empty string from the `GetLocalFunctionName` method.
### Can I use this feature to create custom functions in Aspose.Cells?
No, the `GlobalizationSettings` class is designed to override the behavior of built-in Excel functions, not to create custom functions. If you need to create custom functions, you can use the `UserDefinedFunction` class in Aspose.Cells.
### Is this feature available in all versions of Aspose.Cells for .NET?
Yes, the `GlobalizationSettings` class and the ability to customize function names is available in all versions of Aspose.Cells for .NET.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
