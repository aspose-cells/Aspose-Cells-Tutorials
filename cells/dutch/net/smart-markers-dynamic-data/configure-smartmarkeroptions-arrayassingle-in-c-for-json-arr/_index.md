---
category: general
date: 2026-09-21
description: Configureer SmartMarkerOptions ArrayAsSingle in C# om JSON‑arrays als
  één celwaarde te exporteren in een Excel‑werkmap.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: nl
lastmod: 2026-09-21
og_description: Configureer SmartMarkerOptions ArrayAsSingle in C# om JSON‑arrays
  als één celwaarde te exporteren. Leer de volledige stap‑voor‑stap‑oplossing.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Configureer SmartMarkerOptions ArrayAsSingle in C# – volledige gids
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Configureer SmartMarkerOptions ArrayAsSingle in C# voor JSON‑arrays
url: /nl/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays

If you need to **configure SmartMarkerOptions ArrayAsSingle** while generating Excel files with Aspose.Cells, this guide shows you exactly how to do it. You’ll see how to keep a JSON array intact in one cell instead of spreading its elements across multiple rows.

Working with JSON data in spreadsheets often means choosing between a flattened view and a compact representation. In many reporting scenarios—like storing a list of tags or a set of identifiers—you want the whole JSON string to stay in a single cell. The **ArrayAsSingle** flag in `SmartMarkerOptions` makes that possible.

In this tutorial you will:

* Create a `DataTable` that holds a JSON array in a column.
* Place Smart Markers in an Excel worksheet.
* **Configure SmartMarkerOptions ArrayAsSingle** so the JSON array is treated as a single cell value.
* Process the markers and save the workbook.
* Verify the output.

> **Voorvereisten** – Je hebt de Aspose.Cells for .NET library (v23.12 of later) en een .NET‑ontwikkelomgeving (Visual Studio 2022 aanbevolen) nodig. Basiskennis van C# en DataTables wordt verondersteld.

---

## Stap 1: Bereid de gegevensbron voor met een JSON‑array

First, build a `DataTable` that mimics the data you would receive from a service or a database. The **Names** column contains a JSON‑encoded string representing an array of names.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Waarom deze stap?*  
Smart Markers read data directly from .NET objects. By placing the JSON array in a string column, you preserve the exact JSON syntax, which later can be written to a cell unchanged.

---

## Stap 2: Voeg Smart Markers toe aan een nieuw werkboek

Create a fresh workbook, select the first worksheet, and write Smart Markers that reference the whole table and the specific **Names** column.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

The marker `&=dataTable.Names` tells Aspose.Cells to replace the cell with the value of the **Names** column for each row in `dataTable`. Because we have only one row, the marker will be processed once.

---

## Stap 3: **Configure SmartMarkerOptions ArrayAsSingle**

By default, Aspose.Cells expands an array‑like string into separate rows. Setting `ArrayAsSingle` to `true` overrides that behavior, forcing the whole JSON string to stay in a single cell.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Waarom `ArrayAsSingle` inschakelen?*  
When `ArrayAsSingle` is `false`, the engine interprets `["Alice","Bob"]` as two separate values and writes them to adjacent rows. Setting it to `true` treats the string as an atomic value, which is essential for preserving JSON format inside Excel.

---

## Stap 4: Verwerk de Smart Markers met de geconfigureerde opties

Now run the Smart Marker engine, passing the options object you just configured.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

During processing, Aspose.Cells reads the `dataTable`, applies the markers, and respects the `ArrayAsSingle` flag, leaving the JSON array untouched.

---

## Stap 5: Sla het werkboek op en controleer het resultaat

Finally, write the workbook to disk. Open the generated file in Excel or any spreadsheet viewer to confirm that cell **A2** contains the exact JSON string.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Verwacht resultaat

| A   |
|-----|
| **["Alice","Bob"]** |

Cell **A2** shows the JSON array as a single text value, exactly as stored in the `DataTable`. No extra rows are created.

---

## Veelvoorkomende variaties en edge‑case handling

| Situatie | Hoe aan te passen |
|-----------|--------------|
| **Meerdere rijen met JSON‑arrays** | Dezelfde `ArrayAsSingle`‑instelling werkt; elke rij‑JSON‑array blijft in zijn eigen cel. |
| **Verschillende JSON‑structuren (objecten, geneste arrays)** | Zolang de JSON een string is, houdt `ArrayAsSingle` deze intact. Voor complexe objecten moet je mogelijk aanhalingstekens escapen. |
| **Een andere gegevensbron gebruiken (bijv. List\<T\>)** | Vervang de `DataTable` door een willekeurige enumerable collectie; de marker‑syntaxis (`&=myList.Property`) blijft gelijk. |
| **Exporteren naar CSV in plaats van XLSX** | `ArrayAsSingle` blijft van toepassing, maar onthoud dat CSV geen celopmaak behoudt; je moet de JSON mogelijk tussen aanhalingstekens plaatsen. |

**Pro tip:** Always set `ArrayAsSingle` *before* calling `ProcessSmartMarkers`. Changing the flag after processing has no effect on already‑generated cells.

---

## Volledig, uitvoerbaar voorbeeld

Below is the complete program you can copy‑paste into a console application. It includes all `using` directives and comments for clarity.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Run the program, open `SmartMarkerJson.xlsx`, and you’ll see the JSON array preserved in cell **A2**.

---

## Conclusie

You now know how to **configure SmartMarkerOptions ArrayAsSingle** in C# to keep a JSON array as a single cell value when using Aspose.Cells smart markers. The steps—preparing a `DataTable`, inserting markers, setting the `ArrayAsSingle` flag, processing, and saving—form a repeatable pattern you can apply to any scenario where compact JSON representation inside Excel is required.

Next, you might explore:

* **Aspose.Cells smart markers** for looping over collections.
* Exporting **nested JSON objects** by customizing cell formatting.
* Combining **conditional formatting** with smart markers for richer reports.

Feel free to experiment with different data structures and share your findings. Happy coding!

## Wat moet je hierna leren?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}