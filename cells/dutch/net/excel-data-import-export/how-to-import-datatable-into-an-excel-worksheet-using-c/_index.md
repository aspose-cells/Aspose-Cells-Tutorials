---
category: general
date: 2026-10-26
description: Leer hoe je een DataTable importeert in een Excel-werkblad met C# en
  Aspose.Cells, waarbij je stijlen en kopteksten behoudt in slechts een paar regels
  code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: nl
lastmod: 2026-10-26
og_description: hoe een datatable te importeren in een Excel-werkblad met C# en Aspose.Cells.
  Volg deze volledige gids om stijlen, kopteksten en opmaak te behouden.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: Hoe een DataTable importeren in een Excel-werkblad – C# stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Hoe een DataTable importeren in een Excel-werkblad met C#
url: /nl/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een DataTable importeren in een Excel-werkblad met C#

Als je **hoe je een datatable importeert** in een Excel-werkblad, laat deze gids de exacte stappen in C# zien. Of je nu een rapportage‑engine bouwt of rastergegevens exporteert, je ziet hoe je kolomkoppen en celstijlen intact houdt met Aspose.Cells. De oplossing werkt met .NET 6+ en vereist slechts een paar regels code.

Het importeren van een DataTable is een veelvoorkomende taak bij het werken met spreadsheets, maar ontwikkelaars vergeten vaak om stijloverdracht in te schakelen of de header‑vlag correct door te geven. In deze tutorial leer je hoe je **ImportTableOptions** configureert, **ImportDataTableStyle** inschakelt en `ImportDataTable` veilig aanroept. Aan het einde heb je een kant‑klaar‑te‑gebruiken methode die je in elk C#‑project kunt plaatsen.

## Prerequisites

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6 SDK of later geïnstalleerd.
* Een gelicentieerde kopie van **Aspose.Cells for .NET** (de gratis proefversie werkt voor testen).
* Basiskennis van `DataTable` en Excel‑concepten.
* Een IDE zoals Visual Studio 2022 (elke editor die C# ondersteunt is voldoende).

Er zijn geen extra NuGet‑pakketten nodig naast `Aspose.Cells`.

## Stap 1: Haal de brongegevens op in een DataTable

Het eerste wat je doet wanneer je **hoe je een datatable importeert** beantwoordt, is de gegevens klaar hebben. In de meeste real‑world scenario's komt de `DataTable` van een database‑query, een CSV‑parser of een in‑memory collectie. Hier is een minimaal voorbeeld dat een tabel met een paar rijen maakt:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Waarom dit belangrijk is*: Door eerst de `DataTable` te construeren, bepaal je de kolomvolgorde, gegevenstypen en header‑namen — alles wordt behouden wanneer je later de tabel in een Excel‑werkblad importeert.

## Stap 2: Maak `ImportTableOptions` aan en schakel stijlimport in

Wanneer je **hoe je een datatable importeert** beantwoordt, is de volgende beslissing of je de visuele stijl (lettertypen, kleuren, randen) wilt behouden die al op de bron‑`DataTable` is gedefinieerd. Aspose.Cells biedt de `ImportTableOptions`‑klasse voor fijnmazige controle. Het instellen van `ImportDataTableStyle = true` kopieert de stijl‑informatie naar het doel‑werkblad.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Waarom dit belangrijk is*: Zonder `ImportDataTableStyle` in te schakelen, zouden de geïmporteerde cellen de standaard werkbladstijl gebruiken, waardoor aangepaste opmaak die je op de `DataTable` hebt toegepast verloren gaat. Deze vlag is essentieel voor een gepolijste export.

## Stap 3: Importeer de DataTable in het werkblad, inclusief headers

Nu heb je alles wat je nodig hebt om **hoe je een datatable importeert** in een Excel‑bestand te beantwoorden. Je maakt een workbook, kiest een werkblad en roept `ImportDataTable` aan. Het tweede argument van de methode (`true`) vertelt Aspose.Cells om kolomkoppen als eerste rij te schrijven.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

Het uitvoeren van `ExportDataTableToExcel("Employees.xlsx")` produceert een `Employees.xlsx`‑bestand waarbij de eerste rij **Id**, **Name** en **Department** bevat, en elke cel behoudt de stijl die in de oorspronkelijke `DataTable` is gedefinieerd.

### Volledig uitvoerbaar voorbeeld

Hieronder staat een compleet, zelfstandig console‑programma dat **hoe je een datatable importeert** demonstreert en het resultaat opslaat in de huidige map. Kopieer‑plak het in een nieuw console‑project en voer het uit.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Verwachte output**  
Wanneer je `Employees.xlsx` opent, zie je:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Alle cellen behouden de standaard DataTable‑stijl (lettertype, uitlijning). Als je aangepaste stijlen op de `DataTable` hebt toegepast vóór het importeren, verschijnen die stijlen identiek in het werkblad omdat `ImportDataTableStyle` op `true` staat.

## Veelvoorkomende valkuilen en best‑practice tips

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Headers missing** | Passing `false` as the second argument to `ImportDataTable` skips column names. | Always use `true` when you need headers, or manually write them before the import. |
| **Style not transferred** | Forgetting to enable `ImportDataTableStyle`. | Set `ImportDataTableStyle = true` in `ImportTableOptions`. |
| **Large tables cause performance lag** | Importing millions of rows without paging. | Import in batches or use `ImportDataTable` with the `startRow` overload to stream data. |
| **Incorrect worksheet reference** | Using `workbook.Worksheets[1]` when only one sheet exists. | Use `workbook.Worksheets[0]` or create a new sheet with `workbook.Worksheets.Add()`. |
| **License expiration** | Aspose.Cells trial throws a watermark after 30 days. | Apply a valid license with `License license = new License(); license.SetLicense("Aspose.Cells.lic");`. |

**Pro tip**: Als je na het importeren een aangepast thema wilt toepassen, roep dan `ws.Cells.ApplyStyle(style)` aan waarbij `style` een `Style`‑object is dat je één keer configureert en hergebruikt over rijen.

## De oplossing uitbreiden

Nu je **hoe je een datatable importeert** kent, kun je gerelateerde scenario’s verkennen:

* **Meerdere tabellen importeren** – herhaal de import op verschillende werkbladen.
* **Voorwaardelijke opmaak** – voeg na het importeren regels toe met `ws.Cells.ApplyConditionalFormatting`.
* **Exporteren naar CSV** – gebruik `workbook.Save("file.csv", SaveFormat.Csv)` als een platte‑tekstindeling vereist is.
* **Teruglezen naar een DataTable** – gebruik `ws.Cells.ExportDataTable` om round‑trip integriteit te verifiëren.

Al deze uitbreidingen bouwen voort op het kernpatroon dat hierboven is gedemonstreerd: haal gegevens op, configureer importopties en roep één enkele Aspose.Cells‑methode aan.

## Conclusie

Je hebt nu een volledige, productie‑klare oplossing voor **hoe je een datatable importeert** in een Excel‑werkblad met C#. De tutorial besprak het ophalen van brongegevens, het configureren van `ImportTableOptions` met `ImportDataTableStyle`, en het uitvoeren van de import met `ImportDataTable`. Door de code‑voorbeeld te volgen, behoud je automatisch headers en stijlen, en kun je het patroon aanpassen voor grotere datasets, meerdere bladen of extra opmaakbehoeften.

Klaar om je rapportage‑workflow te automatiseren? Vervang de voorbeeld‑`DataTable` door een echte database‑query, experimenteer met aangepaste celstijlen, en integreer de methode in je bestaande servicelaag. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Import Arrays into Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [How to Import XML Data into Excel with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [How to Import HTML-Formatted DataTables into Excel Using Aspose.Cells for .NET](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}