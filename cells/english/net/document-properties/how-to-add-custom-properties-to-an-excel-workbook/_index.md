---
category: general
date: 2026-10-01
description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
  This guide also shows how to add project ID and read custom properties.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: en
lastmod: 2026-10-01
og_description: Add custom properties to an Excel workbook with Aspose.Cells. Follow
  this complete tutorial to add a project ID, set reviewer info, and read custom properties
  programmatically.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Add custom properties to Excel workbook – step-by-step guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to add custom properties to an Excel workbook
url: /net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to add custom properties to an Excel workbook

If you need to **add custom properties** to an Excel workbook, this guide shows you exactly how to do it with Aspose.Cells for .NET. You’ll also learn how to add a project ID, set a reviewer name, and later **read custom properties** back from the file.

Working with custom metadata lets you embed business‑specific information directly inside the spreadsheet, making it easy to track ownership, version, or any other context without maintaining a separate database. The steps below cover the complete end‑to‑end workflow, from creating the workbook to persisting the new properties.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* A valid Aspose.Cells for .NET license (or a free trial)  
* Visual Studio 2022 (or any C# IDE)  

No additional NuGet packages are required beyond `Aspose.Cells`.

## Step 1: Set up the project and import namespaces

Create a new console application and add the Aspose.Cells reference:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

The `Aspose.Cells` namespace contains the `Workbook`, `Worksheet`, and `CustomPropertyCollection` classes that we will use.

## Step 2: Load an existing workbook (or create a new one)

You can start with an existing `.xlsb` file or generate a fresh workbook. The example below loads a file named **Data.xlsb** located in a folder called `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

If the file does not exist, replace the code with `new Workbook();` to create a blank workbook.

## Step 3: Add custom properties to the first worksheet

The primary operation is to **add custom properties** to a worksheet. Aspose.Cells stores custom properties in a collection that behaves like a dictionary.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Why we use `CustomProperties.Add` instead of `CustomProperties["Name"] = value` is that the `Add` method creates the entry if it does not exist and guarantees the correct data type is stored. This approach prevents accidental type mismatches that could cause runtime errors when reading the values later.

## Step 4: Save the workbook with the new properties

After you have injected the metadata, persist the changes to a new file so the original remains untouched.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

At this point the Excel file contains the custom metadata you defined. You can verify the properties using the steps in the next section.

## Step 5: Read custom properties from a workbook

Reading **excel custom properties** follows the same collection pattern. This snippet demonstrates how to retrieve the values we just stored.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

The `CustomPropertyCollection` indexer returns a `CustomProperty` object; accessing its `Value` property gives you the stored data in its original type. Checking for `null` before casting avoids `NullReferenceException` if a property is missing.

### Expected console output

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

The timestamp will reflect the exact moment you called `Add` in step 3.

## Pro tip: Updating an existing custom property

If you need to **how to add custom** information later (for example, changing the reviewer), use the `CustomPropertyCollection` setter:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

This pattern ensures that the property is either updated or created, which is useful in iterative workflows such as automated report generation.

## Step 6: Verify the properties inside Excel (optional)

You can also view the custom properties directly in Excel:

1. Open the saved `DataWithProps.xlsb` file in Microsoft Excel.  
2. Go to **File → Info → Properties → Advanced Properties**.  
3. Select the **Custom** tab.  

You’ll see the `ProjectId`, `Reviewer`, and `CreatedOn` entries listed with their respective values.

## Full working example

Below is the complete, self‑contained program that combines all previous snippets. Copy it into `Program.cs` and run it; the console will display the retrieved values.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Running this program produces the console output shown earlier and creates `DataWithProps.xlsb` containing the embedded metadata.

## Common questions and edge cases

| Question | Answer |
|---|---|
| **Can I store non‑primitive types?** | Aspose.Cells supports `string`, `int`, `double`, `DateTime`, and `bool`. For complex objects, serialize them to JSON or XML first and store the string. |
| **What if the workbook is password‑protected?** | Open the workbook with a password (`new Workbook(path, password)`) before accessing `CustomProperties`. The properties are still accessible after decryption. |
| **Do custom properties survive format conversion?** | When saving to a different format (e.g., `.xlsx`), Aspose.Cells preserves custom properties as long as the target format supports them. |
| **How to delete a custom property?** | Use `worksheet.CustomProperties.Remove("PropertyName");`. This removes the entry from the collection. |

## Next steps

Now that you know **add custom properties**, you might explore related topics such as:

* **excel custom properties** for document versioning  
* **read custom properties** from multiple worksheets in a single workbook  
* Using **Aspose.Cells** to create pivot tables that reference custom metadata  
* Exporting the workbook to PDF while preserving custom properties  

Experiment with different data types, combine custom properties with cell comments, or integrate the metadata into a larger document‑management system.

---

**Ready to automate your Excel reporting?** Add the code above to your project, adjust the property names to match your business needs, and you’ll have a self‑describing spreadsheet ready for downstream processing.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}