---
category: general
date: 2026-03-22
description: Create Excel workbook, add custom properties, set worksheet name, and
  save as XLSB binary file using C#.
draft: false
keywords:
- create excel workbook
- add custom properties
- save as xlsb
- set worksheet name
- write binary excel file
language: en
og_description: Create Excel workbook, add custom properties, set worksheet name,
  and save as XLSB binary file using C#.
og_title: Create Excel Workbook – Add Custom Properties and Save as XLSB
tags:
- C#
- Aspose.Cells
- Excel automation
title: Create Excel Workbook – Add Custom Properties and Save as XLSB
url: /net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook – Add Custom Properties and Save as XLSB

Ever needed to **create Excel workbook** programmatically but also keep some metadata attached? Maybe you’re building a reporting engine that tags each file with a report ID, author name, or version number. In that case, learning how to **add custom properties** while you **set worksheet name** and finally **save as XLSB** will save you a lot of manual post‑processing.

In this tutorial we’ll walk through a complete, runnable example that shows exactly how to **write binary Excel file** using C#. You’ll see why the XLSB format is the right choice for transporting custom properties, how to avoid the most common pitfalls, and what to do if you need to support older Excel versions.

---

## What You’ll Need

- **.NET 6+** (or .NET Framework 4.6+). The code works on any recent runtime.
- **Aspose.Cells for .NET** (free trial or licensed). It provides the `Workbook`, `Worksheet`, and `CustomProperties` classes used below.
- An IDE you’re comfortable with – Visual Studio, Rider, or even VS Code will do.
- Write access to a folder where the generated file will be saved.

No other third‑party libraries are required.

---

## Step 1: Install Aspose.Cells

To start, add the Aspose.Cells NuGet package to your project:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** If you’re on a CI server, store the license key in an environment variable and load it at runtime – this prevents the “evaluation” watermark from sneaking into your output.

---

## Step 2: Create Excel Workbook – Overview

The first real action is to **create Excel workbook**. This object represents the whole file in memory and gives you access to worksheets, styles, and custom properties.

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2.1: Instantiate a new workbook (empty by default)
            Workbook workbook = new Workbook();

            // The rest of the steps follow...
```

Why instantiate a fresh `Workbook` instead of loading a template? A blank workbook guarantees no hidden styles or leftover custom properties, which is especially important when you intend to **write binary excel file** for downstream systems that expect a clean slate.

---

## Step 3: Set Worksheet Name (and Why It Matters)

Excel sheets default to “Sheet1”, “Sheet2”, etc. Giving a sheet a meaningful name makes downstream processing—like Power Query or VBA macros—much easier to read.

```csharp
            // Step 3.1: Grab the first worksheet (index 0) and rename it
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data"; // clear, concise, and self‑describing
```

If you try to assign a duplicate name, Aspose.Cells will throw an `ArgumentException`. To be safe, you can check `Worksheets.Exists("Data")` before renaming.

---

## Step 4: Add Custom Properties

Custom properties are stored in the workbook’s internal XML and travel with the file regardless of format. They’re perfect for embedding things like `ReportId` or `GeneratedBy`.

```csharp
            // Step 4.1: Add a numeric property
            workbook.CustomProperties.Add("ReportId", 12345);

            // Step 4.2: Add a string property
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");
```

> **Why use custom properties?**  
> • They’re accessible via Excel’s “File → Info → Properties” panel.  
> • Code that consumes the workbook can read them without scanning cell contents.  
> • They survive format conversions (XLSX ↔ XLSB) because they’re part of the file’s metadata.

You can also store dates, booleans, or even binary blobs, but keep the payload small—Excel isn’t a database.

---

## Step 5: Save as XLSB (Write Binary Excel File)

The XLSB format stores data in a binary structure, which makes the file smaller and faster to open. More importantly for this tutorial, **custom properties are baked into the binary stream**, guaranteeing they travel with the file.

```csharp
            // Step 5.1: Define the output path
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // Step 5.2: Save the workbook as a binary XLSB file
            workbook.Save(outputPath, SaveFormat.Xlsb);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

### Expected Result

After running the program, you’ll find `WithCustomProps.xlsb` on your desktop. Open it in Excel, go to **File → Info → Properties**, and you’ll see `ReportId` and `GeneratedBy` listed under *Custom*.

---

## Step 6: Edge Cases & Common Questions

### What if the target folder is read‑only?

Wrap the `Save` call in a `try/catch` block and fall back to a user‑writable location, such as `%TEMP%`. This prevents the application from crashing on permission errors.

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsb);
}
catch (UnauthorizedAccessException)
{
    string fallback = Path.GetTempFileName().Replace(".tmp", ".xlsb");
    workbook.Save(fallback, SaveFormat.Xlsb);
    Console.WriteLine($"Saved to fallback location: {fallback}");
}
```

### Can I **save as XLSX** and still keep custom properties?

Yes—just change `SaveFormat.Xlsb` to `SaveFormat.Xlsx`. The properties are stored in the same XML part, so they survive the format switch. However, XLSX files are larger because they’re zipped XML, whereas XLSB offers better performance for large data sets.

### How do I read the custom properties later?

```csharp
Workbook loaded = new Workbook(outputPath);
foreach (CustomProperty prop in loaded.CustomProperties)
{
    Console.WriteLine($"{prop.Name} = {prop.Value}");
}
```

This snippet prints every custom property, making it trivial for downstream services to verify the file’s provenance.

---

## Full Working Example

Below is the complete program you can copy‑paste into a new console project. No pieces are missing—everything from `using` statements to the final `Console.WriteLine` is included.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook instance
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet and give it a meaningful name
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "Data";

            // 3️⃣ Add custom properties (they travel with the file)
            workbook.CustomProperties.Add("ReportId", 12345);
            workbook.CustomProperties.Add("GeneratedBy", "MyApp");

            // 4️⃣ Define where to save the binary XLSB file
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "WithCustomProps.xlsb");

            // 5️⃣ Save the workbook as a binary XLSB file
            try
            {
                workbook.Save(outputPath, SaveFormat.Xlsb);
                Console.WriteLine($"✅ Workbook saved to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ Failed to save workbook: {ex.Message}");
            }
        }
    }
}
```

Run the program, open the resulting file, and verify the custom properties. That’s the whole process of **create excel workbook**, **add custom properties**, **set worksheet name**, and **save as xlsb** in one tidy flow.

---

## Conclusion

You now know exactly how to **create Excel workbook**, give its sheet a clear **set worksheet name**, embed useful metadata with **add custom properties**, and finally **save as XLSB** to produce a compact, binary Excel file. This workflow is reliable, works across .NET versions, and scales nicely whether you’re generating one report or a thousand.

What’s next? Try adding a data table to the “Data” sheet, experiment with different property types (dates, booleans), or switch the output to **save as xlsb** for massive data sets. You might also explore protecting the workbook with a password—Aspose.Cells makes that a one‑liner as well.

Feel free to drop a comment if you hit any snags, or share how you’ve extended this pattern in your own projects. Happy coding!  

---  

![Create Excel workbook screenshot](image.png){alt="Create Excel workbook with custom properties"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}