---
category: general
date: 2026-03-21
description: Learn how to save xlsb files in C# while adding a custom property like
  ProjectId. This guide shows how to create an Excel workbook, add custom property,
  and verify it.
draft: false
keywords:
- how to save xlsb
- add custom property
- create excel workbook
- how to add custom property
- add project id
language: en
og_description: Discover how to save xlsb files and add a custom property such as
  ProjectId using C#. Step‑by‑step guide with complete code.
og_title: How to Save XLSB – Add Custom Property in C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: How to Save XLSB – Add Custom Property in C#
url: /net/document-properties/how-to-save-xlsb-add-custom-property-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Save XLSB – Add Custom Property in C#

Ever wondered **how to save xlsb** files while also tucking a piece of metadata inside? Maybe you’re building a reporting engine that needs a hidden ProjectId, or you simply want to tag worksheets for downstream processing. **How to save xlsb** isn’t rocket science, but mixing it with a custom property adds a tiny twist that many developers overlook.

In this tutorial we’ll walk through creating an Excel workbook, adding a custom property (yes, *add custom property*), persisting the file as an **XLSB** binary workbook, and finally loading it back to prove the property stuck around. Along the way we’ll also touch on **how to add custom property** values like a ProjectId, so you’ll leave with a reusable pattern for future projects.

> **Pro tip:** If you’re already using the Aspose.Cells library (the code below does), you get native support for custom properties without any COM interop headaches.

---

## Prerequisites

- .NET 6+ (or .NET Framework 4.6+).  
- Aspose.Cells for .NET – install via NuGet: `Install-Package Aspose.Cells`.  
- Basic C# knowledge – nothing fancy, just a few `using` statements.  

That’s it. No Office installation, no interop, just pure managed code.

---

## Step 1: How to Save XLSB – Create Excel Workbook

The very first thing you need to do is create a fresh workbook object. Think of it as opening a blank Excel file that lives only in memory until you decide to write it to disk.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook workbook = new Workbook();

        // (Optional) Give the first worksheet a friendly name
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Name = "DataSheet";

        // From here we can start adding data or properties…
```

Why start with a workbook? Because **create excel workbook** is the foundation for any further manipulation—whether you later insert formulas, charts, or custom properties. The `Workbook` class abstracts the whole file, while `Worksheets` give you access to individual tabs.

---

## Step 2: Add Custom Property to Worksheet

Now comes the fun part—**add custom property**. In Aspose.Cells you can attach a property directly to a worksheet (or to the workbook itself). Here we’ll store a numeric ProjectId that downstream services can read without touching the visible cells.

```csharp
        // Step 2: Add a custom property called "ProjectId"
        // The value 12345 could come from your database, config, etc.
        sheet.CustomProperties.Add("ProjectId", 12345);

        // You can also add string or date properties:
        // sheet.CustomProperties.Add("Author", "Jane Doe");
        // sheet.CustomProperties.Add("GeneratedOn", DateTime.UtcNow);
```

**How to add custom property**? Just call `CustomProperties.Add(name, value)`. The API automatically handles the underlying XML, so you don’t have to worry about the low‑level details. This is the safest way to embed metadata that isn’t visible to the end‑user.

---

## Step 3: Save the Workbook as XLSB

With the workbook ready and the custom property attached, it’s time to **how to save xlsb**. The XLSB format stores data in a binary representation, which is usually smaller and faster to open than the classic XLSX.

```csharp
        // Step 3: Define the output path – adjust as needed
        string outputPath = @"C:\Temp\WithCustomProp.xlsb";

        // Save the workbook in XLSB format
        workbook.Save(outputPath, SaveFormat.Xlsb);

        Console.WriteLine($"Workbook saved to {outputPath}");
```

Saving as XLSB is as simple as passing `SaveFormat.Xlsb` to the `Save` method. If you’re wondering whether this will strip out the custom property—rest assured, Aspose.Cells preserves both workbook‑level and worksheet‑level properties in the binary file.

---

## Step 4: Verify the Custom Property

A good habit is to reload the file and confirm that the property survived the round‑trip. This also demonstrates **how to add custom property** later on if you need to update it.

```csharp
        // Step 4: Load the saved XLSB to verify the property
        Workbook loaded = new Workbook(outputPath);

        // Retrieve the first worksheet again
        Worksheet loadedSheet = loaded.Worksheets[0];

        // Access the "ProjectId" custom property
        var projectId = loadedSheet.CustomProperties["ProjectId"].Value;

        Console.WriteLine($"Loaded ProjectId: {projectId}"); // Should print 12345
    }
}
```

If the console prints `12345`, you’ve successfully **how to save xlsb** *and* **add project id** in one go. The property lives inside the file’s internal metadata, invisible to the UI but perfectly readable by code.

---

## Additional Tips: Adding Multiple Properties & Edge Cases

### Adding More Than One Property

You can stack as many properties as you like:

```csharp
sheet.CustomProperties.Add("Department", "Finance");
sheet.CustomProperties.Add("IsConfidential", true);
```

### Updating an Existing Property

If a property already exists, just assign a new value:

```csharp
sheet.CustomProperties["ProjectId"].Value = 67890; // Overwrites the old ID
```

### Handling Missing Properties

Attempting to read a non‑existent property throws a `KeyNotFoundException`. Guard against it:

```csharp
if (sheet.CustomProperties.ContainsKey("ClientCode"))
{
    var clientCode = sheet.CustomProperties["ClientCode"].Value;
    // Use clientCode...
}
else
{
    Console.WriteLine("ClientCode property not found.");
}
```

### Cross‑Version Compatibility

XLSB works on Excel 2007 + and on the web version of Excel. However, older Office versions (< 2007) can’t open XLSB files. If you need broader compatibility, consider saving a second copy as XLSX.

### Performance Considerations

Binary XLSB files are typically 30‑50 % smaller than XLSX, and they load faster. For large data‑sets (hundreds of thousands of rows), the speed gain can be noticeable.

---

## Full Working Example

Below is the entire program you can copy‑paste into a console project. It includes all the steps, error handling, and comments you need to get up and running instantly.

```csharp
using Aspose.Cells;
using System;

class SaveXlsbWithCustomProperty
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Name = "DataSheet";

            // 2️⃣ Add a custom property (ProjectId) – this is how to add custom property
            sheet.CustomProperties.Add("ProjectId", 12345);
            sheet.CustomProperties.Add("CreatedBy", Environment.UserName);
            sheet.CustomProperties.Add("GeneratedOn", DateTime.UtcNow);

            // 3️⃣ Save as XLSB – this shows how to save xlsb
            string path = @"C:\Temp\WithCustomProp.xlsb";
            workbook.Save(path, SaveFormat.Xlsb);
            Console.WriteLine($"✅ Workbook saved as XLSB to {path}");

            // 4️⃣ Load the file back and verify the property
            Workbook loaded = new Workbook(path);
            Worksheet loadedSheet = loaded.Worksheets[0];

            if (loadedSheet.CustomProperties.ContainsKey("ProjectId"))
            {
                var projId = loadedSheet.CustomProperties["ProjectId"].Value;
                Console.WriteLine($"🔎 Loaded ProjectId: {projId}"); // Expected: 12345
            }
            else
            {
                Console.WriteLine("❗ ProjectId not found after loading.");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Expected output**

```
✅ Workbook saved as XLSB to C:\Temp\WithCustomProp.xlsb
🔎 Loaded ProjectId: 12345
```

If you see the above, you’ve mastered **how to save xlsb**, **add custom property**, and **add project id**—all in a tidy, reusable snippet.

---

## Frequently Asked Questions

**Q: Does this work with .NET Core?**  
A: Absolutely. Aspose.Cells is .NET Standard‑compatible, so the same code runs on .NET 5/6/7 and on .NET Framework.

**Q: Can I add a custom property to the whole workbook instead of a single sheet?**  
A: Yes. Use `workbook.CustomProperties.Add("Key", value);` to attach it at the workbook level.

**Q: What if I need to store a large string (e.g., JSON) as a property?**  
A: The API accepts strings of any length, but keep in mind that extremely large blobs may increase file size. For massive data, consider a hidden sheet instead.

**Q: Is the custom property visible in Excel’s UI?**  
A: Not directly. Users can view it via **File → Info → Properties → Advanced Properties → Custom**, but it won’t appear in the grid.

---

## Conclusion

We’ve covered **how to save xlsb** files in C# while **adding a custom property** such as a ProjectId. By following the step‑by‑step pattern—**create excel workbook**, **add custom property**, **save as XLSB**, and **verify**—you now have a solid, citation‑worthy reference that works both for search‑engine crawlers and AI assistants.

Next, you might explore:

- **How to add custom property** to multiple worksheets in a loop.  
- Exporting data from a DataTable into the workbook before saving.  
- Encrypting the XLSB file for extra security.

Feel free to experiment, tweak the property names, or swap the binary format for XLSX if you need broader compatibility. Got a tricky scenario? Drop a comment, and we’ll troubleshoot together. Happy coding!  

![how to save xlsb example](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}