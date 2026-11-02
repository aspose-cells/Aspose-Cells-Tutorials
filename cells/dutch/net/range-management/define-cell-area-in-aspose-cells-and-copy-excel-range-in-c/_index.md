---
category: general
date: 2026-08-04
description: Definieer celgebied in Aspose.Cells en leer hoe je draaitabellen kunt
  kopiëren, een Excel‑bereik in C# kunt kopiëren en een bereik op hetzelfde blad efficiënt
  kunt kopiëren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: nl
lastmod: 2026-08-04
og_description: Definieer celgebied in Aspose.Cells en kopieer een Excel-bereik in
  C# terwijl je draaitabellen behoudt. Volg deze stapsgewijze gids voor betrouwbare
  resultaten.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Definieer celgebied in Aspose.Cells – kopieer Excel-bereik in C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Definieer celgebied in Aspose.Cells en kopieer Excel-bereik in C#
url: /nl/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definieer celgebied in Aspose.Cells en kopieer Excel-bereik in C#

Als je een **define cell area** moet definiëren voor een bereik en vervolgens dat bereik op hetzelfde werkblad wilt kopiëren, laat deze gids je precies zien hoe je dat doet met Aspose.Cells voor .NET. Of je nu een pivot‑gedreven rapport verplaatst of een datablock dupliceert, je leert het volledige proces in slechts een paar stappen.

Je ontdekt ook **how to copy pivot** tabellen zonder hun verbindingen te verliezen, en ziet een helder voorbeeld van **copy excel range c#** dat werkt in het **copy range same sheet** scenario. Er zijn geen externe tools nodig—alleen Aspose.Cells en een paar regels C#.

## Wat je nodig hebt

- .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+)
- Aspose.Cells for .NET (NuGet‑pakket `Aspose.Cells`)
- Een Excel‑werkmap (`input.xlsx`) die een pivot‑tabel bevat in het bereik A1:J50
- Een ontwikkelomgeving zoals Visual Studio 2022

## Stap 1: Definieer het celgebied voor het bronbereik

De eerste taak is om **define cell area** die het blok vertegenwoordigt dat je wilt kopiëren. Aspose.Cells gebruikt de `CellArea` struct, die nul‑gebaseerde rij‑ en kolomindexen opslaat.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Waarom dit belangrijk is:** `CellArea` vertelt Aspose.Cells precies op welke cellen moet worden gewerkt. Het gebruik van nul‑gebaseerde indexen voorkomt off‑by‑one fouten die vaak voorkomen bij het vertalen van Excel’s A1-notatie naar code.

## Stap 2: Definieer het bestemmingscelgebied op hetzelfde werkblad

Om **copy range same sheet** uit te voeren, moet je ook aangeven waar de gegevens moeten terechtkomen. De bestemming kan op elke rij beginnen; hier beginnen we bij rij 61 (nul‑gebaseerde index 60) om een lege buffer te laten.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Waarom dit belangrijk is:** Door de bronafmetingen te spiegelen, garandeer je dat het gekopieerde blok perfect past zonder afkapping.

## Stap 3: Kopieer het bereik terwijl je pivot‑tabellen behoudt

Nu kun je **how to copy pivot** veilig uitvoeren. De `CopyOptions`‑klasse bevat een `CopyPivotTables`‑vlag die de pivot‑definitie, gegevensbron en opmaak behoudt.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Waarom dit belangrijk is:** Zonder `CopyPivotTables = true` in te stellen, zou de pivot een statisch momentopname worden, waardoor interactiviteit verloren gaat. Deze optie kopieert de onderliggende cache en verbindingen, zodat de nieuwe pivot zich precies gedraagt als de originele.

## Stap 4: Sla de werkmap op

Tot slot schrijf je de wijzigingen terug naar de schijf. Het uitvoerbestand toont aan dat de pivot‑tabel is gedupliceerd op hetzelfde blad.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Pro tip:** Gebruik `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` als je een specifiek formaat moet afdwingen, vooral bij het werken met oudere Excel‑versies.

## Stap 5: Verifieer de gekopieerde pivot‑tabel

Open `CopyWithPivot.xlsx` in Excel en controleer het volgende:

1. Het bereik A61:J110 bevat een kopie van de oorspronkelijke gegevens.
2. Een nieuwe pivot‑tabel verschijnt bovenaan het gekopieerde bereik.
3. Het vernieuwen van de pivot weerspiegelt wijzigingen in de brongegevens, wat bevestigt dat **how to copy pivot** geslaagd is.

Als de pivot niet ververst, zorg er dan voor dat het brongegevensbereik in de definitie van de pivot nog steeds naar het oorspronkelijke werkmapgebied wijst. Aspose.Cells werkt de bronreferentie automatisch bij wanneer `CopyPivotTables` true is.

## Randgevallen en variaties

| Situatie | Wat te wijzigen |
|-----------|----------------|
| **Copy to a different worksheet** | Vervang `srcWorkbook.Worksheets[0]` door de doelwerkblad‑index of -naam, en pas `destinationRange` dienovereenkomstig aan. |
| **Copy a merged cell block** | Stel `CopyOptions.PasteType = PasteType.All` in om samengevoegde cellen en opmaak te behouden. |
| **Copy only values, not formulas** | Gebruik `CopyOptions.PasteType = PasteType.Values` om te voorkomen dat formules die naar het originele blad verwijzen worden overgebracht. |
| **Large ranges ( > 10,000 rows )** | Overweeg `Workbook.Copy` te gebruiken voor volledige werkbladen om de prestaties te verbeteren, en verwijder vervolgens ongewenste rijen. |

Deze variaties tonen aan dat dezelfde **aspose.cells copy range**‑logica kan worden aangepast aan veel real‑world scenario's.

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma. Vervang `YOUR_DIRECTORY` door een daadwerkelijk mappad op jouw machine.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Verwachte output:** Na het uitvoeren van het programma bevat `CopyWithPivot.xlsx` de oorspronkelijke gegevens plus een identiek blok dat begint bij rij 61, compleet met een functionele pivot‑tabel.

## Conclusie

Je weet nu hoe je **define cell area** in Aspose.Cells, **copy excel range c#**, en **copy range same sheet** kunt uitvoeren terwijl je alle pivot‑functionaliteit behoudt. Deze techniek elimineert handmatige copy‑paste fouten en schaalt naar grote werkmappen.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **how to copy pivot** over meerdere werkbladen, of **aspose.cells copy range** gebruiken om volledige bladen met opmaak te dupliceren. Experimenteer met verschillende `CopyOptions`‑instellingen om het kopieergedrag af te stemmen op de behoeften van jouw project.

Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}