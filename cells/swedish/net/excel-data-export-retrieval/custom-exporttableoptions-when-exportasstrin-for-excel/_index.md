---
category: general
date: 2026-10-26
description: Anpassade ExportTableOptions när ExportAsStrin låter dig exportera Excel-data
  som strängar i C#. Följ steg‑för‑steg‑guiden för att konfigurera och köra exporten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: sv
lastmod: 2026-10-26
og_description: Anpassade ExportTableOptions när ExportAsStrin möjliggör Excel‑export
  enbart som sträng. Lär dig de exakta stegen för att konfigurera och köra exporten
  i C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Anpassade ExportTableOptions när ExportAsStrin – exportera Excel som sträng
  i C#
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
title: Anpassade ExportTableOptions vid ExportAsStrin för Excel
url: /sv/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassade ExportTableOptions när ExportAsStrin – exportera Excel som sträng i C#

Om du behöver **Custom ExportTableOptions when ExportAsStrin** för att få varje cellvärde som en ren sträng, visar den här guiden exakt hur du gör det. Oavsett om du bygger en data‑importpipeline eller behöver en ren CSV‑klar dump, kommer du att se varför konfiguration av alternativen på detta sätt undviker överraskningar med typkonvertering.

I den här handledningen kommer du att lära dig **how to export excel as string** med Aspose.Cells‑biblioteket, se den kompletta körbara koden och förstå resonemanget bakom varje inställning. Ingen extern dokumentation krävs – allt du behöver finns här.

## Förutsättningar

* .NET 6.0 SDK eller senare installerat  
* Visual Studio 2022 (eller någon IDE som stödjer .NET)  
* Aspose.Cells for .NET‑paket (installera via NuGet: `Install-Package Aspose.Cells`)  
* En Excel‑arbetsbok (`sample.xlsx`) placerad i projektets rotmapp  

Dessa objekt är de enda beroendena; koden körs på Windows, Linux eller macOS utan ytterligare bibliotek.

## Steg 1: Ladda arbetsboken du vill exportera

Det första du gör när du använder **Custom ExportTableOptions when ExportAsStrin** är att hämta ett `Worksheet`‑objekt från en inläst arbetsbok. Detta objekt ger dig åtkomst till rader, kolumner och export‑API:t.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Varför detta är viktigt:*  
`Workbook` läser filen en gång och behåller all formateringsinformation i minnet. Genom att välja ett specifikt `Worksheet` begränsar du exportens omfattning och undviker onödig bearbetning av dolda blad.

## Steg 2: Konfigurera ExportTableOptions med ExportAsString = true

Kärnan i **Custom ExportTableOptions when ExportAsStrin** är `ExportTableOptions`‑objektet. Att sätta `ExportAsString` tvingar exportören att behandla varje cell som en sträng, oavsett dess ursprungliga datatyp (datum, tal, boolesk osv.). Att aktivera `PreserveFormatting` behåller den visuella stilen (t.ex. valutasymboler) i den resulterande strängen.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Varför detta är viktigt:*  
När du senare anropar `ExportDataTable` försöker biblioteket normalt att härleda .NET‑typen för varje kolumn. Med `ExportAsString = true` hoppas detta härledningssteg över, vilket förhindrar oväntade `DateTime`‑ eller `double`‑konverteringar som kan bryta nedströms CSV‑tolkare.

## Steg 3: Exportera ett område till en DataTable med de anpassade alternativen

Nu kan du exportera ett rektangulärt område (rader 0‑9, kolumner 0‑4) från kalkylbladet. Metoden returnerar en `DataTable` där varje fält är en `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Varför detta är viktigt:*  
`ExportDataTable` är det mest bekväma sättet att flytta Excel‑data till en relationell struktur som många .NET‑API:er redan förstår (t.ex. Entity Framework, Dapper). Genom att skicka **Custom ExportTableOptions when ExportAsStrin** garanterar du att varje `DataColumn.DataType` blir `typeof(string)`.

## Steg 4: Verifiera resultatet – alla värden är strängar

Det är god praxis att bekräfta att exporten fungerade som förväntat. Följande loop skriver ut varje cell och dess körningstyp.

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

**Förväntad output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Varje cell visar `String` som sin typ, vilket bekräftar att **Custom ExportTableOptions when ExportAsStrin** fungerade korrekt.

## Steg 5: Valfritt – skriv DataTable till CSV

Om ditt slutmål är en ren textfil kan du enkelt serialisera `DataTable` till CSV:



## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Exportera HTML‑strängar från Excel till DataTable med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Exportera anpassade egenskaper Excel PDF Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Anpassade laddningsfilter Excel‑export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}