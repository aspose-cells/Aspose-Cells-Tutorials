---
category: general
date: 2026-10-26
description: Aangepaste ExportTableOptions wanneer ExportAsStrin je toestaat Excel‑gegevens
  als strings te exporteren in C#. Volg de stapsgewijze handleiding om de export te
  configureren en uit te voeren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: nl
lastmod: 2026-10-26
og_description: Aangepaste ExportTableOptions wanneer ExportAsStrin string‑only Excel-export
  mogelijk maakt. Leer de exacte stappen om de export te configureren en uit te voeren
  in C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Aangepaste ExportTableOptions bij ExportAsString – exporteer Excel als string
  in C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Aangepaste ExportTableOptions bij ExportAsStrin voor Excel
url: /nl/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aangepaste ExportTableOptions bij ExportAsStrin – exporteer Excel als string in C#

Als je **Custom ExportTableOptions when ExportAsStrin** nodig hebt om elke celwaarde als een platte string te krijgen, laat deze gids je precies zien hoe je dit doet. Of je nu een data‑importpipeline bouwt of een schone CSV‑klare dump nodig hebt, je zult zien waarom het zo configureren van de opties type‑conversie verrassingen voorkomt.

In deze tutorial leer je **hoe je Excel als string exporteert** met behulp van de Aspose.Cells‑bibliotheek, zie de volledige, uitvoerbare code, en begrijp de reden achter elke instelling. Er is geen externe documentatie nodig – alles wat je nodig hebt staat hier.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 SDK of later geïnstalleerd  
* Visual Studio 2022 (of een IDE die .NET ondersteunt)  
* Aspose.Cells voor .NET‑pakket (installeren via NuGet: `Install-Package Aspose.Cells`)  
* Een Excel‑werkmap (`sample.xlsx`) geplaatst in de hoofdmap van het project  

Dit zijn de enige afhankelijkheden; de code draait op Windows, Linux of macOS zonder extra bibliotheken.

## Stap 1: Laad de werkmap die je wilt exporteren

Het eerste wat je doet bij het gebruik van **Custom ExportTableOptions when ExportAsStrin** is een `Worksheet`‑object verkrijgen uit een geladen werkmap. Dit object geeft je toegang tot rijen, kolommen en de export‑API.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Waarom dit belangrijk is:*  
`Workbook` leest het bestand één keer en houdt alle opmaakinformatie in het geheugen. Door een specifieke `Worksheet` te selecteren, beperk je de exportreikwijdte en vermijd je onnodige verwerking van verborgen bladen.

## Stap 2: Configureer ExportTableOptions met ExportAsString = true

De kern van **Custom ExportTableOptions when ExportAsStrin** is het `ExportTableOptions`‑object. Het instellen van `ExportAsString` dwingt de exporter om elke cel als een string te behandelen, ongeacht het oorspronkelijke gegevenstype (datum, getal, boolean, enz.). Het inschakelen van `PreserveFormatting` behoudt de visuele stijl (bijv. valutasymbolen) in de resulterende string.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Waarom dit belangrijk is:*  
Wanneer je later `ExportDataTable` aanroept, probeert de bibliotheek normaal gesproken het .NET‑type van elke kolom af te leiden. Met `ExportAsString = true` wordt die afleidingsstap overgeslagen, waardoor onverwachte `DateTime`‑ of `double`‑conversies die downstream CSV‑parsers kunnen breken, worden voorkomen.

## Stap 3: Exporteer een bereik naar een DataTable met de aangepaste opties

Nu kun je een rechthoekig bereik (rijen 0‑9, kolommen 0‑4) uit het werkblad exporteren. De methode retourneert een `DataTable` waarbij elk veld een `string` is.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Waarom dit belangrijk is:*  
`ExportDataTable` is de meest handige manier om Excel‑gegevens naar een relationele structuur te verplaatsen die veel .NET‑API's al begrijpen (bijv. Entity Framework, Dapper). Door de **Custom ExportTableOptions when ExportAsStrin** door te geven, garandeer je dat elke `DataColumn.DataType` `typeof(string)` zal zijn.

## Stap 4: Verifieer het resultaat – alle waarden zijn strings

Het is een goede gewoonte om te bevestigen dat de export zich gedraagt zoals verwacht. De volgende lus drukt elke cel en zijn runtime‑type af.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Verwachte output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Elke cel toont `String` als type, wat bevestigt dat **Custom ExportTableOptions when ExportAsStrin** correct heeft gewerkt.

## Stap 5: Optioneel – schrijf de DataTable naar CSV

Als je uiteindelijke doel een platte‑tekstbestand is, kun je de `DataTable` eenvoudig naar CSV serialiseren:



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Exporteer HTML‑strings van Excel naar DataTable met Aspose.Cells voor .NET: Een stapsgewijze gids](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Exporteer aangepaste eigenschappen Excel PDF Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java aangepaste laadfilters Excel export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}