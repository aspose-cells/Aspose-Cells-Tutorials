---
category: general
date: 2026-07-29
description: Kopieer rijen van het ene werkblad naar het andere en leer hoe je een
  Excel‑werkmap programmatisch kunt laden met Aspose.Cells in een stapsgewijze tutorial.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: nl
lastmod: 2026-07-29
og_description: Kopieer rijen van het ene werkblad naar het andere met Aspose.Cells.
  Leer hoe je een Excel‑werkmap programmeerbaar laadt en draaitabellen behoudt in
  slechts een paar regels C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Rijen kopiëren van het ene werkblad naar het andere – C# Excel Automatiseringsgids
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Rijen kopiëren van het ene werkblad naar het andere – Complete C#‑gids
url: /nl/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rijen kopiëren van het ene werkblad naar het andere – Complete C# Gids

Heb je ooit moeten **rijen kopiëren van het ene werkblad naar het andere**, maar wist je niet hoe je de formules en draaitabellen intact kon houden? Je bent niet de enige. In veel rapportage‑pijplijnen moeten we een deel van de gegevens uit een hoofdbestand halen en in een nieuw werkboek plaatsen voor verdere verwerking. Het goede nieuws? Met Aspose.Cells kun je dit programmatisch doen, en de hele bewerking kost slechts een handvol regels.

In deze tutorial lopen we stap voor stap door het programmatisch laden van een Excel‑werkboek, het selecteren van een bereik, en vervolgens het kopiëren van die rijen naar een gloednieuw werkboek terwijl eventuele ingesloten draaitabellen behouden blijven. Aan het einde heb je een herbruikbare code‑snippet die je in elk C#‑project kunt plaatsen — zonder handmatig kopiëren‑plakken.

## Wat je zult bereiken

- **Excel‑werkboek programmatisch laden** met de `Workbook`‑klasse van Aspose.Cells.  
- Definieer een **celgebied** dat de rijen bevat die je wilt verplaatsen.  
- **Rijen kopiëren van het ene werkblad naar het andere** met één methode‑aanroep die draaitabellen actief houdt.  
- Sla het resultaat op in een nieuw bestand, klaar voor distributie of verdere verwerking.

### Vereisten

- .NET 6.0 of later (de code werkt zowel op .NET Core als .NET Framework).  
- Een geldige Aspose.Cells‑licentie (of een tijdelijke evaluatiesleutel).  
- Twee mappen op schijf: één voor het bron‑werkboek (`Source.xlsx`) en één voor de bestemming (`Destination.xlsx`).  

Als je dat hebt, laten we dan beginnen.

## Stap 1: Excel‑werkboek programmatisch laden

Allereerst—voordat je iets kunt kopiëren, moet je het bronbestand in het geheugen laden. Aspose.Cells maakt dit een fluitje van een cent:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Why this matters:** Het programmatisch laden van het werkboek geeft je volledige controle over de inhoud van het bestand zonder ooit Excel op de server te openen. Het voorkomt bovendien COM‑interop‑problemen en werkt in headless‑omgevingen zoals CI‑pijplijnen.

## Stap 2: Definieer het bronbereik dat de rijen bevat

Vervolgens bepaal je precies welke rijen je wilt overzetten. Het `CellArea`‑object laat je een rechthoekig blok specificeren met behulp van de boven‑linker‑ en onder‑rechter‑celadressen:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Pro tip:** Als de grootte van je gegevens dynamisch verandert, kun je `EndRow` berekenen met `sourceWorksheet.Cells.MaxDataRow` om altijd de volledige tabel vast te leggen.

## Stap 3: Maak een nieuw werkboek voor de bestemming

Maak nu een leeg werkboek aan dat de gekopieerde rijen zal ontvangen. Dit werkboek start standaard met één werkblad:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Why a new workbook?** Een schone start zorgt ervoor dat je per ongeluk geen bestaande gegevens overschrijft en geeft je een voorspelbare omgeving voor testen.

## Stap 4: Rijen kopiëren van het ene werkblad naar het andere (draaientabellen behouden)

Hier is het hart van de tutorial. De `CopyRows`‑methode kopieert de geselecteerde rijen en wanneer je `true` als laatste argument doorgeeft, kopieert deze ook eventuele draaitabellen die zich binnen het bereik bevinden:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Wat gebeurt er onder de motorkap?

- **Source worksheet**: `sourceWorkbook.Worksheets[0]` wijst naar het eerste blad in het bronbestand.  
- **Row indices**: Aspose.Cells gebruikt nul‑gebaseerde indexering, dus `StartRow` en `EndRow` komen overeen met de rijen die je in `sourceRange` hebt gedefinieerd.  
- **Destination start row**: We beginnen bij rij 0 in het nieuwe blad, waardoor het gekopieerde blok direct bovenaan wordt geplaatst.  
- **`true` flag**: Dit is de magische schakel die Aspose.Cells vertelt om alle draaitabellen binnen de gekopieerde rijen te klonen, waardoor hun cache en verbindingen behouden blijven.

> **Edge case warning:** Als het bronbereik samengevoegde cellen bevat die buiten het gedefinieerde gebied uitstrekken, worden die samenvoegingen afgekapt. Om ze intact te houden, breid je het bereik uit zodat het de volledige samengevoegde regio dekt.

## Stap 5: Sla het bestemmings‑werkboek op

Schrijf tenslotte het nieuwe bestand naar schijf. Je kunt elke gewenste map kiezen; zorg er alleen voor dat het proces schrijfrechten heeft:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Wanneer je `Destination.xlsx` opent, zie je rijen A1‑H20 gedupliceerd, compleet met eventuele draaitabellen die oorspronkelijk waren ingesloten. De rest van het werkboek blijft leeg, klaar om later meer bladen of gegevens toe te voegen.

## Volledig werkend voorbeeld

Alles bij elkaar genomen, hier is het complete, uitvoerbare programma:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Expected output** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Open het bestemmingsbestand en controleer of de gegevens, opmaak en draaitabellen er precies zo uitzien als in de bron. Als je ontbrekende gegevens ziet, controleer dan of `sourceRange` de relevante rijen volledig omvat.

## Veelgestelde vragen & tips

- **Kan ik kopiëren naar een specifiek werkblad in plaats van het eerste?**  
  Zeker. Vervang `destinationWorkbook.Worksheets[0]` door `destinationWorkbook.Worksheets["TargetSheet"]` (maak het blad eerst aan als het nog niet bestaat).

- **Wat als ik alleen waarden wil kopiëren, niet formules?**  
  Gebruik `CopyRows` met de overload die een `CopyRowsOptions`‑object accepteert en stel `PasteType` in op `PasteType.Values`.

- **Hoe ga ik om met grote bestanden zonder het geheugen te overbelasten?**  
  Aspose.Cells ondersteunt **streaming** via `LoadOptions` met `MemorySetting.MemoryPreference`. Laad het bron‑werkboek met een lagere geheugenvoetafdruk en de kopieerbewerking blijft efficiënt.

- **Blijven draaitabellen gekoppeld aan de oorspronkelijke gegevensbron?**  
  Wanneer je de `true`‑vlag instelt, wordt de draaitabel‑cache gedupliceerd, zodat de draaitabellen in het nieuwe werkboek naar de gekopieerde gegevens verwijzen, niet naar het originele bestand.

## Afronden

Je weet nu hoe je **rijen kunt kopiëren van het ene werkblad naar het andere** terwijl je eventuele draaitabellen intact houdt, en je hebt gezien hoe je **Excel‑werkboek programmatisch kunt laden** met Aspose.Cells. Dit patroon vormt een solide basis voor het bouwen van geautomatiseerde rapportage‑pijplijnen, datamigratiescripts of elke situatie waarin je Excel‑gegevens on‑the‑fly moet splitsen.

Wat nu? Probeer de snippet uit te breiden naar:

- Een lus over meerdere bronbereiken en deze samenvoegen in één bestemmingsbestand.  
- Voorwaardelijke opmaak toepassen na het kopiëren om belangrijke statistieken te markeren.  
- Het uiteindelijke werkboek exporteren naar PDF of CSV voor downstream‑consumptie.

Voel je vrij om te experimenteren, en als je tegen een probleem aanloopt, laat dan een reactie achter. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe rijen te kopiëren in Excel met Aspose.Cells voor .NET: Een C#‑gids](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Werkblad kopiëren van het ene werkboek naar het andere met Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Hoe zichtbare Excel‑rijen te exporteren met Aspose.Cells voor .NET: Een stapsgewijze gids](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}