---
category: general
date: 2026-06-27
description: Kopieer draaitabel naar een ander blad in C# met Aspose.Cells. Leer stap
  voor stap hoe je draaitabelgegevens en opmaak behoudt.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: nl
og_description: Kopieer draaitabel naar een ander blad in C# met Aspose.Cells. Deze
  tutorial laat precies zien hoe je een draaitabel dupliceert terwijl de opmaak behouden
  blijft.
og_title: Kopieer draaitabel naar een ander blad – Complete C#-gids
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Kopieer draaitabel naar een ander blad – Complete C#-gids
url: /nl/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel naar een ander blad – Complete C# gids

Heb je ooit **copy pivot table to another sheet** moeten doen, maar was je bang dat je de slicers, berekende velden of opmaak zou verliezen? Je bent niet de enige. Veel ontwikkelaars lopen tegen dit probleem aan bij het automatiseren van Excel‑rapporten, en de frustratie is echt. In deze gids lopen we stap voor stap door een schone, end‑to‑end oplossing die **preserves the pivot table** precies behoudt zoals deze verschijnt.

We gebruiken **Aspose.Cells for .NET**, een krachtige bibliotheek waarmee je Excel‑bestanden kunt manipuleren zonder Excel zelf te openen. Aan het einde van deze tutorial heb je een kant‑klaar C#‑fragment dat een draaitabel van het ene werkblad naar het andere kopieert, waarbij alle onderliggende dataverbindingen behouden blijven.

## Wat deze tutorial behandelt

- Een .NET‑project opzetten en het Aspose.Cells NuGet‑pakket toevoegen.  
- Een bestaand werkboek laden dat al een draaitabel bevat.  
- Zowel het bronbereik (de oorspronkelijke draaitabel) als het doelbereik op een ander blad definiëren.  
- Gebruik van `CopyOptions` om **preserve the pivot table** te behouden tijdens het kopiëren.  
- Het resultaat opslaan en verifiëren dat de draaitabel werkt op de nieuwe locatie.  

Geen externe tools, geen handmatig copy‑paste, en geen verborgen magie—gewoon eenvoudige code die je in elke C# console‑applicatie of service kunt gebruiken.

> **Waarom dit belangrijk is:** Het automatiseren van het dupliceren van draaitabellen bespaart uren handmatig werk, vooral in nachtelijke rapportage‑pijplijnen waar tientallen werkboeken identieke draaitabelstructuren over meerdere bladen nodig hebben.

---

## Stap 1: Het project opzetten en Aspose.Cells toevoegen

Allereerst. Als je dat nog niet hebt gedaan, maak een nieuw .NET console‑project aan:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Voeg nu het Aspose.Cells‑pakket toe:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Gebruik de nieuwste stabiele versie (vanaf juni 2026 v23.12). Deze bevat bugfixes voor de verwerking van `CopyPivotTable`.

## Stap 2: Het werkboek laden en werkbladen benaderen

Open het werkboek dat de bron‑draaivotabel bevat. In de meeste real‑world scenario's staat het bestand op een gedeelde schijf, maar voor deze demo gaan we ervan uit dat het zich in een lokale map bevindt genaamd `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Hier maken we een nieuw blad met de naam **CopyDestination** waar de draaitabel wordt geplaatst. Als je al een doelblad hebt, haal het dan op via index of naam.

## Stap 3: Bron‑ en doelbereiken definiëren

Een draaitabel bevindt zich binnen een rechthoekig blok cellen. Je moet Aspose.Cells vertellen welk blok gekopieerd moet worden. In dit voorbeeld beslaat de draaitabel rijen 0‑20 en kolommen 0‑10 (nul‑gebaseerde indexering).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Let op hoe we de eindrij en -kolom dynamisch berekenen. Op deze manier past de bestemming zich automatisch aan, zelfs als je later de grootte van het bronbereik wijzigt.

## Stap 4: Het kopiëren uitvoeren terwijl de draaitabel behouden blijft

Nu gebeurt de magie. Door een `CopyOptions`‑object met `CopyPivotTable = true` door te geven, weet Aspose.Cells de definitie van de draaitabel intact te houden.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Onder de motorkap recreëert Aspose.Cells de pivot‑cache, ververst de referentie naar de gegevensbron en past eventuele opmaak opnieuw toe. Dit is de **Excel pivot duplication** waar je naar op zoek bent.

## Stap 5: Het resultaat opslaan en verifiëren

Schrijf tenslotte het werkboek terug naar de schijf. Je kunt het originele bestand onaangeroerd laten door onder een nieuwe naam op te slaan.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Open het resulterende `copy-pivot.xlsx` en je zult de draaitabel perfect gerepliceerd zien op het **CopyDestination**‑blad, compleet met slicers, berekende velden en opmaak. De onderliggende gegevensbron wijst nog steeds naar de oorspronkelijke tabel, zodat verversen exact werkt als voorheen.

> **Wat als de bron‑draaivotabel een dynamisch bereik beslaat?**  
> Gebruik `Worksheet.PivotTables[0].CacheDefinition.SourceData` om de werkelijke grenzen op te halen, en bouw vervolgens `sourceRange` op basis van die informatie. Dit behandelt gevallen waarin rijen of kolommen in de loop van de tijd kunnen uitbreiden.

## Bonus: Draaitabelopmaak behouden bij kopieën

Soms verliest de standaardkopie voorwaardelijke opmaak of aangepaste getalnotaties. Om dit te voorkomen, breid je de `CopyOptions` uit:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Het inschakelen van `CopyFormatting` zorgt ervoor dat aan de **preserve pivot formatting**‑vereiste wordt voldaan, waardoor je een pixel‑perfecte duplicaat krijgt.

## Verwachte output

Wanneer je het programma uitvoert, sluit de console stilletjes af (tenzij je logging toevoegt). Het openen van `copy-pivot.xlsx` zou moeten tonen:

- Blad 1: Originele gegevens en draaitabel ongewijzigd.  
- **CopyDestination**: Een exacte replica van de draaitabel, beginnend op rij 31 (aangezien rijen 1‑gebaseerd zijn in de Excel‑UI).  
- Alle slicers en filters functioneel; klikken op “Refresh” werkt beide draaitabellen tegelijk bij.

## Conclusie

We hebben zojuist laten zien hoe je **copy pivot table to another sheet** kunt gebruiken met Aspose.Cells in C#. De stappen—het project opzetten, het werkboek laden, bereiken definiëren, kopiëren met `CopyPivotTable = true`, en opslaan—vormen een betrouwbaar patroon dat je in elke automatiserings‑pijplijn kunt hergebruiken.

Als je verder wilt gaan, overweeg dan:

- **Excel pivot duplication** over meerdere werkboeken (doorloop bestanden).  
- Het gebruik van de **Aspose.Cells copy range with pivot**‑optie om draaitabellen tussen verschillende werkboeken te verplaatsen.  
- Automatiseren van verversingen met `PivotTable.RefreshData()` na het kopiëren.

Voel je vrij om te experimenteren met verschillende bronbereiken, of combineer deze techniek met het genereren van grafieken voor volledig geautomatiseerde rapportagedashboards. Heb je vragen? Laat een reactie achter, en happy coding!

![Screenshot showing copied pivot table in new sheet](copy-pivot-screenshot.png "copy pivot table to another sheet example")

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Master Pivot Table Formatting in .NET Using Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Access Pivot Table External Data Sources in .NET using Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}