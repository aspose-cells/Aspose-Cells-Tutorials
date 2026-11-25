---
category: general
date: 2026-11-25
description: Create Excel workbook C# and save as XLSB while setting worksheet custom
  property for report metadata.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- save workbook as xlsb
- set worksheet custom property
- Aspose.Cells Excel export
- C# Excel automation
language: en
lastmod: 2026-11-25
og_description: Create Excel workbook C# and save as XLSB. This guide shows how to
  set a worksheet custom property so your reports retain owner information.
og_image_alt: Screenshot of a C# program creating an Excel workbook and saving it
  as XLSB
og_title: Create Excel workbook C# – save as XLSB with custom properties
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  headline: Create Excel workbook C# and save as XLSB
  type: TechArticle
- description: Create Excel workbook C# and save as XLSB while setting worksheet custom
    property for report metadata.
  name: Create Excel workbook C# and save as XLSB
  steps:
  - name: '**Create a new workbook** – the in‑memory representation of an Excel file.'
    text: '**Create a new workbook** – the in‑memory representation of an Excel file.'
  - name: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
    text: '**Set worksheet custom property** – attach key/value metadata to the first
      sheet.'
  - name: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
    text: '**Save workbook as XLSB** – write the file in the binary XLSB format, which
      keeps the custom property intact.'
  type: HowTo
tags:
- excel
- csharp
- xlsb
- custom-properties
title: Create Excel workbook C# and save as XLSB
url: /net/saving-and-exporting-excel-files-with-options/create-excel-workbook-c-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel workbook C# and save as XLSB

If you need to **create Excel workbook C#** for a reporting routine, you probably also want the file to keep extra metadata such as the report owner. This tutorial shows you how to **set worksheet custom property** and then **save workbook as XLSB** in a single, reproducible workflow.

You’ll finish with a binary‑encoded XLSB file that opens in Excel, preserves the custom property, and is ready for distribution. No external scripts are required—just the Aspose.Cells for .NET library and a few lines of C#.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 (or later) installed – Aspose.Cells supports .NET Standard 2.0+.
* A valid Aspose.Cells license (or a free evaluation key).  
* Visual Studio 2022 or any C# IDE you prefer.

Add the NuGet package:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Use the **Aspose.Cells** free trial to avoid runtime licensing errors while testing.

## Create Excel workbook C# – overview

The process consists of three atomic actions:

1. **Create a new workbook** – the in‑memory representation of an Excel file.
2. **Set worksheet custom property** – attach key/value metadata to the first sheet.
3. **Save workbook as XLSB** – write the file in the binary XLSB format, which keeps the custom property intact.

Each step is illustrated with full, runnable code.

![Create Excel workbook C# screenshot](excel_workbook.png)

## Step 1: Initialize a new workbook

```csharp
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook
            Workbook workbook = new Workbook();          // creates a default workbook with one worksheet
            Worksheet worksheet = workbook.Worksheets[0]; // reference to the first worksheet
```

**Why this matters** – `Workbook` is the entry point for all Excel operations. When you instantiate it without parameters, Aspose.Cells creates a clean workbook with a single worksheet, which is perfect for programmatic generation.

## Step 2: Set worksheet custom property

```csharp
            // Step 2: Add a custom property to the worksheet (e.g., the report owner)
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
```

*`set worksheet custom property`* is the exact call that stores the **ReportOwner** key with value **Alice** inside the sheet’s custom‑property collection. Excel can later read this property via **File → Info → Properties → Advanced Properties**.

> **Common question:** *What if I need multiple properties?*  
> Just call `Add` repeatedly with different names, e.g., `worksheet.CustomProperties.Add("Department", "Finance");`.

## Step 3: Save workbook as XLSB

```csharp
            // Step 3: Save the workbook in XLSB format – the custom property is preserved
            string outputPath = @"YOUR_DIRECTORY\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);
        }
    }
}
```

The **save workbook as xlsb** line writes the file using the binary XLSB format. Compared with the classic XLSX, XLSB loads faster for large datasets and retains custom properties without extra steps.

### Expected result

After running the program:

* `custom_props.xlsb` appears in `YOUR_DIRECTORY`.
* Opening the file in Excel shows a single sheet with no visible data (we only added metadata).
* Navigate to **File → Info → Properties → Advanced Properties → Custom** – you’ll see **ReportOwner = Alice**.

## Verifying the custom property programmatically (optional)

If you want to confirm that the property survived the round‑trip, you can reload the file:

```csharp
            // Verify the property after loading
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            System.Console.WriteLine($"Report owner: {owner}"); // should print "Alice"
```

Running this snippet prints:

```
Report owner: Alice
```

## Edge cases and best practices

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Large workbooks (>10 000 rows)         | Use **XLSB** because its binary compression reduces memory footprint.          |
| Need to preserve culture‑specific data| Set `Workbook.Settings.CultureInfo` before adding values.                     |
| Multiple worksheets need the same property| Loop through `workbook.Worksheets` and add the property to each sheet.        |
| Running on Linux/macOS                 | Ensure the Aspose.Cells .NET Standard build is referenced; no Windows‑only APIs. |

> **Watch out for:** Saving to a directory without write permission will throw `UnauthorizedAccessException`. Always validate the path or use `Path.GetTempPath()` for temporary files.

## Full, runnable example

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomation
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create Excel workbook C#
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Set worksheet custom property
            worksheet.CustomProperties.Add("ReportOwner", "Alice");
            worksheet.CustomProperties.Add("ReportDate", DateTime.Today.ToShortDateString());

            // 3️⃣ Save workbook as XLSB
            string outputPath = @"C:\Temp\custom_props.xlsb";
            workbook.Save(outputPath, SaveFormat.Xlsb);

            // Optional verification
            Workbook loaded = new Workbook(outputPath);
            string owner = loaded.Worksheets[0].CustomProperties["ReportOwner"].Value.ToString();
            Console.WriteLine($"Report owner verified: {owner}");
        }
    }
}
```

Copy the code into a new console project, replace `C:\Temp\` with a folder you own, and run. The console will output `Report owner verified: Alice`, proving that **create Excel workbook C#**, **set worksheet custom property**, and **save workbook as xlsb** all worked together.

## Conclusion

You now know how to **create Excel workbook C#**, attach a **worksheet custom property**, and **save workbook as XLSB** in a clean, production‑ready pattern. This approach is ideal for automated reporting pipelines, data‑export services, or any scenario where metadata must travel with the Excel file.

Next, you might explore:

* Adding data tables and styling them (`Cells`, `Style` objects).
* Exporting to other formats such as **XLSX** or **CSV** while preserving properties.
* Using **Aspose.Cells** to read custom properties from existing workbooks.

Feel free to experiment with different property names, multiple worksheets, or large data sets. The same three‑step pattern scales from a simple one‑sheet file to enterprise‑level reporting solutions. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook C# – Add Custom Property & Save XLSB](/cells/english/net/document-properties/create-excel-workbook-c-add-custom-property-save-xlsb/)
- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to create Excel workbook C# with custom formatting and save as XLSX](/cells/english/net/excel-formatting-and-styling/how-to-create-excel-workbook-c-with-custom-formatting-and-sa/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}