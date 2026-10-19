---
category: general
date: 2026-02-28
description: Learn how to add custom property to an Excel workbook in C# and write
  console output fast. Includes load excel workbook c# and access custom properties
  c#.
draft: false
keywords:
- how to add custom property
- load excel workbook c#
- write console output c#
- access custom properties c#
- get first worksheet c#
language: en
og_description: How to add custom property in Excel using C# explained in detail.
  Load workbook, access custom properties, and write console output.
og_title: How to Add Custom Property in Excel with C# – Complete Guide
tags:
- C#
- Excel
- Aspose.Cells
- CustomProperties
title: How to Add Custom Property in Excel with C# – Step‑by‑Step Guide
url: /net/document-properties/how-to-add-custom-property-in-excel-with-c-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add Custom Property in Excel with C# – Step‑by‑Step Guide

Ever wondered **how to add custom property** to an Excel file using C#? In this tutorial we’ll walk through loading an Excel workbook, accessing custom properties, and printing the result to the console. It’s a pretty common scenario when you need to tag a sheet with metadata like “Department” or “Budget” without altering the visible data.

What you’ll get out of this guide is a complete, copy‑and‑paste‑ready solution that shows you how to **load excel workbook c#**, retrieve the **first worksheet c#**, add and read **custom properties c#**, and finally **write console output c#**. No vague references to external docs—everything you need is right here, plus a few pro tips to keep you from hitting the usual pitfalls.

---

## Prerequisites

- **.NET 6.0** or later (the code works with .NET Framework 4.6+ as well).  
- **Aspose.Cells for .NET** (free trial or licensed version). If you prefer an open‑source alternative, EPPlus works similarly; just swap the namespace and class names.  
- A basic C# development environment (Visual Studio, VS Code, Rider—any will do).  
- An Excel file named `input.xlsx` placed in a folder you can reference, e.g., `C:\Data\input.xlsx`.

> **Pro tip:** When you install Aspose.Cells via NuGet, the package automatically adds the necessary `using Aspose.Cells;` directive, so you won’t have to hunt down DLLs manually.

---

## Step 1 – Load Excel Workbook C# (The Starting Point)

Before you can play with custom properties, you need the workbook object in memory.

```csharp
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

// Define the path to your Excel file
string workbookPath = @"C:\Data\input.xlsx";

// Load the workbook – this is the classic way to load excel workbook c#
Workbook wb = new Workbook(workbookPath);
```

**Why this matters:** Loading the workbook creates a full‑featured `Workbook` instance that gives you access to worksheets, cells, and the hidden `CustomProperties` collection. Skipping this step or using a wrong path will throw a `FileNotFoundException`, which is why we explicitly define the path up front.

---

## Step 2 – Get First Worksheet C# (Where the Magic Happens)

Most spreadsheets have a default sheet you want to work with. Aspose.Cells stores worksheets in a zero‑based collection, so the first one is index `0`.

```csharp
// Retrieve the first worksheet – get first worksheet c# is as simple as this
Worksheet worksheet = wb.Worksheets[0];
```

**What’s the benefit?** By targeting the first worksheet directly, you avoid looping through the collection when you only need one sheet. If your file has multiple sheets and you need a different one, just change the index or use `Worksheets["SheetName"]`.

---

## Step 3 – Add Custom Property (The Core of How to Add Custom Property)

Now we finally answer the primary question: **how to add custom property** to a worksheet.

```csharp
// Add a custom property named "Department" with value "Finance"
worksheet.CustomProperties.Add("Department", "Finance");

// Add a numeric custom property named "Budget" with value 1,250,000
worksheet.CustomProperties.Add("Budget", 1250000);
```

### Behind the scenes

- `CustomProperties` is a collection that lives on the `Worksheet` object, not the workbook.  
- The `Add` method accepts a string key and an object value, so you can store text, numbers, dates, or even boolean flags.  
- Aspose.Cells automatically persists these properties into the underlying Excel file when you save it later.

> **Watch out:** If you try to add a property with a duplicate name, Aspose will throw an `ArgumentException`. To update an existing property, use `worksheet.CustomProperties["Budget"].Value = newValue;`.

---

## Step 4 – Retrieve and Use Custom Property (Access Custom Properties C#)

Reading back a property is just as easy as writing it. This step demonstrates **access custom properties c#** and also shows how to **write console output c#**.

```csharp
// Retrieve the "Budget" value from the custom properties collection
var budget = worksheet.CustomProperties["Budget"].Value;

// Optional: Cast to the expected type if you need numeric operations
decimal budgetAmount = Convert.ToDecimal(budget);
```

**Why cast?** The `Value` property returns an `object`. Converting it to a numeric type lets you perform calculations—say, adding tax or comparing budgets—without extra boxing/unboxing overhead.

---

## Step 5 – Write Console Output C# (Seeing the Result)

Finally, we display the retrieved budget in the console. This satisfies the **write console output c#** requirement.

```csharp
// Display the budget amount in the console
Console.WriteLine($"Budget: {budgetAmount:C0}");
```

The `:C0` format specifier prints the number as currency without decimal places, e.g., `Budget: $1,250,000`. Feel free to adjust the format string to match your locale.

---

## Step 6 – Save the Workbook (Persisting the Changes)

If you want the custom properties to survive beyond the current session, you must save the workbook.

```csharp
// Save the workbook to a new file so you don't overwrite the original
string outputPath = @"C:\Data\output_with_properties.xlsx";
wb.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

**Note:** Even though custom properties are attached to the worksheet, they are stored inside the `.xlsx` package, so the file size grows only marginally.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete program that ties all the steps together. Paste it into a new console project and hit **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook – how to add custom property starts here
            string workbookPath = @"C:\Data\input.xlsx";
            Workbook wb = new Workbook(workbookPath);

            // 2️⃣ Get the first worksheet – get first worksheet c#
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Add custom properties – this is the core of how to add custom property
            worksheet.CustomProperties.Add("Department", "Finance");
            worksheet.CustomProperties.Add("Budget", 1250000);

            // 4️⃣ Retrieve the budget – access custom properties c#
            var budget = worksheet.CustomProperties["Budget"].Value;
            decimal budgetAmount = Convert.ToDecimal(budget);

            // 5️⃣ Write console output – write console output c#
            Console.WriteLine($"Budget: {budgetAmount:C0}");

            // 6️⃣ Save the workbook so the properties persist
            string outputPath = @"C:\Data\output_with_properties.xlsx";
            wb.Save(outputPath);
            Console.WriteLine($"Workbook saved to {outputPath}");

            // Keep console window open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Expected console output**

```
Budget: $1,250,000
Workbook saved to C:\Data\output_with_properties.xlsx
Press any key to exit...
```

Run the program, open `output_with_properties.xlsx` in Excel, then go to **File → Info → Properties → Advanced Properties → Custom**. You’ll see “Department” = “Finance” and “Budget” = 1250000 listed there.

---

## Common Questions & Edge Cases

### What if the workbook is password‑protected?

Aspose.Cells lets you open a protected file by passing a `LoadOptions` object with the password:

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx) { Password = "mySecret" };
Workbook wb = new Workbook(workbookPath, loadOptions);
```

### Can I add custom properties to the workbook itself instead of a single sheet?

Yes—use `wb.CustomProperties` instead of `worksheet.CustomProperties`. The API is identical, but the scope changes from per‑sheet to the whole file.

### Does this work with .xls (Excel 97‑2003) files?

Absolutely. Aspose.Cells abstracts the format, so the same code works with `.xls`, `.xlsx`, `.xlsm`, etc. Just ensure the file extension matches the actual format.

### How do I delete a custom property?

```csharp
worksheet.CustomProperties.Remove("Department");
```

Removing a property is safe; if the key doesn’t exist, nothing happens.

---

## Pro Tips & Pitfalls

- **Avoid hard‑coding paths** in production code. Use `Path.Combine` and configuration files to keep things flexible.  
- **Dispose the workbook** if you’re processing many files in a loop. Wrap it in a `using` block or call `wb.Dispose()` manually.  
- **Watch out for culture‑specific number formats** when converting the `object` value. `Convert.ToDecimal` respects the current thread culture, so set `CultureInfo.InvariantCulture` if you need consistent parsing.  
- **Batch add properties**: If you have dozens of metadata items, consider looping over a dictionary to keep the code DRY.

---

## Conclusion

We’ve just covered **how to add custom property** to an Excel worksheet using C#. From loading the workbook, getting the first worksheet, adding and reading custom properties, to writing the result to the console and persisting the file—you now have a full‑stack, copy‑ready solution.  

Next, you might explore **access custom properties c#** at the workbook level, or experiment with more complex data types like dates and booleans. If you’re curious about automating report generation, check out our guide on **write console output c#** for logging large data sets, or dive into the **load excel workbook c#** series for advanced sheet manipulation.

Feel free to tweak the property names, add your own metadata, and integrate this pattern into larger data‑processing pipelines. Happy coding, and may your spreadsheets stay richly annotated!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}