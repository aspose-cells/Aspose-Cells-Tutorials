---
category: general
date: 2026-07-13
description: Hoe een celbereik als tabel te exporteren met C# en ExportTableOptions.
  Leer stap‑voor‑stap de werkmapinstelling, opmaak en tabelexport.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: nl
lastmod: 2026-07-13
og_description: Hoe een celbereik exporteren als tabel in C# met ExportTableOptions.
  Volg deze gids om cellen te formatteren, een werkmap te maken en moeiteloos een
  tabel te exporteren.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Hoe een celbereik exporteren als tabel – volledige C# walkthrough
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Hoe een celbereik exporteren als tabel – Complete C#‑gids
url: /nl/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een celbereik als tabel exporteren – Complete C#-gids

Heb je je ooit afgevraagd **hoe je een celbereik als tabel kunt exporteren** zonder je haar uit te trekken door formatteringsproblemen? Je bent niet de enige. Of je nu gegevens voedt in een rapportage‑pipeline of gewoon een snelle CSV‑achtige dump nodig hebt, het beheersen van het exportproces kan je uren handmatig kopiëren‑plakken besparen.

In deze tutorial lopen we de exacte stappen door om een numerieke cel te nemen, wetenschappelijke notatie toe te passen en deze als tabel te exporteren met **ExportTableOptions**. Aan het einde heb je een uitvoerbare code‑fragment, begrijp je het *waarom* achter elke aanroep, en weet je hoe je de code kunt aanpassen voor grotere bereiken of andere formaten.

## Vereisten

- .NET 6 of later (de API werkt hetzelfde op .NET Framework 4.7+)
- Aspose.Cells for .NET geïnstalleerd (`Install-Package Aspose.Cells`)
- Een basisbegrip van C#-syntaxis; geen diepgaande Excel‑interne kennis vereist

Heb je die? Geweldig—laten we erin duiken.

## Stap 1: Exportopties instellen – Hoe een celbereik als tabel exporteren

Het eerste wat je nodig hebt is een **ExportTableOptions**-instantie die de bibliotheek vertelt hoe de celinhoud behandeld moet worden. Zonder dit standaard exporteert de bibliotheek ruwe numerieke waarden, wat downstream‑consumenten die tekst verwachten kan breken.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Waarom dit belangrijk is:**  
- `ExportAsString = true` dwingt de bibliotheek om de weergegeven tekst van de cel te schrijven, niet de onderliggende double.  
- `CustomFormat` stelt je in staat een **wetenschappelijke notatie‑export** af te dwingen, handig bij zeer grote of zeer kleine getallen.

> **Pro tip:** Als je een datum‑ of valutanaam nodig hebt, vervang dan `"0.00E+00"` door `"yyyy‑MM‑dd"` of respectievelijk `"$#,##0.00"`.

## Stap 2: Een Workbook maken en het eerste Worksheet ophalen – Workbook‑ en Worksheet‑beheer

Een **Workbook** vertegenwoordigt het volledige Excel‑bestand, terwijl een **Worksheet** een enkel tabblad is. Voor een eenvoudige export blijven we bij het eerste blad, dat altijd aanwezig is op index 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Waarom dit belangrijk is:**  
Het aanmaken van een nieuwe `Workbook` zorgt voor een schone lei—geen verborgen stijlen of overgebleven gegevens die je kunnen hinderen. Toegang tot `Worksheets[0]` is de snelste manier om een referentie naar het actieve blad te krijgen zonder je zorgen te maken over bladnamen.

## Stap 3: Doelcel vullen – Celwaarde‑opmaak C#

Nu voegen we een numerieke waarde in cel **A1** (rij 0, kolom 0) in. De waarde die we kiezen is bewust lang‑decimaal zodat je de wetenschappelijke notatie in actie kunt zien.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Waarom dit belangrijk is:**  
Het aanroepen van `PutValue` bepaalt automatisch het gegevenstype van de cel. Omdat we later als string exporteren, wordt de ruwe double geconverteerd met het formaat dat we eerder hebben ingesteld, waardoor we een nette `"1.23E+04"`‑output krijgen.

## Stap 4: Het gedefinieerde celbereik als tabel exporteren – Het celbereik als tabel exporteren

Met de opties en gegevens op hun plaats is de laatste stap om Aspose.Cells te laten weten dat het bereik moet worden weggeschreven. De `ExportTable`‑methode verwacht de start‑rij/kolom, de grootte van het bereik, en het opties‑object dat we hebben opgebouwd.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Waarom dit belangrijk is:**  
- `totalRows = 1` en `totalColumns = 1` beperken de export tot één cel, maar je kunt deze getallen uitbreiden om grotere blokken te dekken (bijv. `5, 3` voor een bereik van 5 rijen × 3 kolommen).  
- De methode schrijft de gegevens naar een interne tabelstructuur die kan worden opgeslagen als CSV, HTML, of zelfs direct gestreamd naar een client.

### Het resultaat opslaan (optioneel)

Als je de geëxporteerde tabel wilt opslaan op schijf, kun je deze naar een CSV‑bestand schrijven:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Het uitvoeren van bovenstaande genereert een bestand met:

```
1.23E+04
```

## Randgevallen & Veelvoorkomende Variaties

| Situatie | Wat te wijzigen | Reden |
|-----------|----------------|--------|
| **Meerdere rijen exporteren** | Pas `totalRows` aan en loop over rijen indien nodig | Staat batch‑export toe zonder `ExportTable` herhaaldelijk aan te roepen |
| **Formules behouden** | Stel `ExportAsString = false` in | Behoudt de oorspronkelijke formule in plaats van de weergegeven waarde |
| **Verschillende scheidingstekens** | Gebruik de overload `ExportTableToCSV(..., ',', ...)` | Schakelt van komma‑gescheiden naar tab‑gescheiden of pipe‑gescheiden waarden |
| **Grote werkbladen** | Stream de export om `OutOfMemoryException` te vermijden | Werkt goed voor >10 000 rijen |

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar‑om‑te‑kopiëren‑en‑plakken programma. Het compileert met elk .NET‑consoleproject dat Aspose.Cells referereert.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Verwachte output:**  
Een bestand genaamd `ExportedTable.csv` met één regel:

```
1.23E+04
```

Als je de CSV opent in een teksteditor zie je de wetenschappelijke notatie precies zoals gedefinieerd.

## Conclusie

We hebben **hoe je een celbereik als tabel exporteert** van begin tot eind behandeld: het instellen van `ExportTableOptions`, het maken van een `Workbook`, het invoegen van gegevens, en uiteindelijk het aanroepen van `ExportTable`. Door elk onderdeel te begrijpen, kun je nu de aanpak opschalen naar grotere bereiken, andere formaten, of zelfs integreren in een web‑API die Excel‑afgeleide gegevens on‑the‑fly levert.

Vooruitkijkend wil je misschien verkennen:

- **ExportTableToHTML** voor web‑klare previews  
- **ExportTableToDataTable** om direct te voeden in ADO.NET‑pijplijnen  
- Geavanceerde **aangepaste formaten** voor datums, valuta's of percentages  

Probeer ze uit, en je verandert een eenvoudige cel‑export in een veelzijdige data‑leveringsengine. Heb je vragen of een eigenzinnige use‑case? Laat een reactie achter—veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe zichtbare Excel‑rijen exporteren met Aspose.Cells voor .NET: een stapsgewijze gids](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Hoe Excel‑bestanden exporteren in .NET met Aspose.Cells: een uitgebreide gids](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Hoe een Excel‑cel op naam benaderen met Aspose.Cells voor .NET: een stapsgewijze gids](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}