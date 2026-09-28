---
category: general
date: 2026-09-27
description: Leer hoe je een draaitabel in C# kunt kopiëren met Aspose.Cells. Inclusief
  het kopiëren van rijen met opmaak, het kopiëren van de draaitabel naar een ander
  blad en het exporteren van de draaitabel naar een nieuw werkboek.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: nl
lastmod: 2026-09-27
og_description: Hoe een draaitabel te kopiëren in C# met Aspose.Cells. Volg de stapsgewijze
  handleiding om rijen met opmaak te kopiëren, een draaitabel naar een ander blad
  te verplaatsen en deze naar een nieuwe werkmap te exporteren.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Hoe een draaitabel te kopiëren in C# – volledige Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Hoe een draaitabel te kopiëren in C# met Aspose.Cells
url: /nl/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in C# met Aspose.Cells

Als je een **draaitabel** van het ene werkblad naar het andere moet **kopiëren**, kan het leren **hoe een draaitabel te kopiëren** in C# met Aspose.Cells je uren handmatig werk besparen. De aanpak stelt je ook in staat om **rijen met opmaak te kopiëren**, de pivot‑cache intact te houden, en zelfs **de draaitabel te exporteren naar een nieuw werkboek** wanneer je een losstaand bestand nodig hebt.

Deze tutorial leidt je door de volledige workflow:

* maak een werkboek,  
* kopieer het bereik van de draaitabel terwijl je de opmaak behoudt,  
* plaats de gekopieerde gegevens op een nieuw blad, en  
* sla het resultaat op als een apart bestand.

Je zult zien waarom de ingebouwde `CopyRows`‑methode de meest betrouwbare manier is om **een draaitabel naar een ander blad te kopiëren**, en je krijgt tips voor het omgaan met randgevallen zoals verborgen rijen of externe gegevensbronnen.

## Vereisten

Before you start, make sure you have:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| .NET 6.0 or later | Aspose.Cells ondersteunt .NET 6+ en biedt de beste prestaties. |
| Visual Studio 2022 (or any C# IDE) | Je hebt een editor nodig die NuGet‑pakketten kan herstellen. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Deze bibliotheek levert de `CopyRows`‑API die in het voorbeeld wordt gebruikt. |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | De code kopieert dit specifieke bereik; pas het bereik aan als je draaitabel groter is. |

Installeer de bibliotheek met de NuGet‑CLI of Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Stap 1: Laad het werkboek dat de draaitabel bevat

De eerste regel maakt een `Workbook`‑object aan dat het volledige Excel‑bestand vertegenwoordigt. Het laden van het bestand één keer geeft je lees‑/schrijftoegang tot elk werkblad.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Waarom deze stap belangrijk is** – Zonder het werkboek te laden, kunnen geen van de daaropvolgende `CopyRows`‑aanroepen de brongegevens of de pivot‑cache refereren.

## Stap 2: Bereid bron‑ en doel‑werkbladen voor

Je hebt een doelblad nodig waar de gekopieerde draaitabel zal staan. De onderstaande code haalt het eerste werkblad op (waar de originele draaitabel zich bevindt) en voegt een nieuw blad toe met de naam **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tip:** Als het doelblad al bestaat, roep dan eerst `Worksheets.RemoveAt(index)` aan om dubbele namen te voorkomen.

## Stap 3: Definieer het celgebied dat de draaitabel omsluit

Een `CellArea`‑object beschrijft de boven‑linker en onder‑rechter cellen van het bereik dat je wilt verplaatsen. In dit voorbeeld beslaat de draaitabel `A1:G20`. Pas de coördinaten aan voor grotere tabellen.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Stap 4: Kopieer rijen met opmaak en behoud de pivot‑cache

De `CopyRows`‑methode kopieert **rijen** van het bronblad naar het doelblad. Door `CopyOptions.CopyAll` door te geven, zorg je ervoor dat waarden, opmaak, diagrammen en ingesloten objecten — alles wat deel uitmaakt van een draaitabel — worden overgedragen.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Waarom `CopyRows` beter werkt dan `Copy` voor draaitabellen

* `CopyRows` respecteert de interne pivot‑cache, waardoor de gekopieerde draaitabel functioneel blijft.
* Het behoudt **rijen met opmaak kopiëren** precies zoals ze in het originele blad verschijnen.
* In tegenstelling tot een eenvoudige `Copy` van een bereik, verplaatst het ook verborgen rijen en eventuele bijbehorende slicers.

## Stap 5: Sla het werkboek op met de gekopieerde draaitabel

Schrijf tenslotte het aangepaste werkboek naar schijf. Het nieuwe bestand bevat het originele blad plus een **Copy**‑blad dat een volledig functionele duplicaat van de originele draaitabel bevat.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Verwacht resultaat

Wanneer je `pivot_copied.xlsx` opent:

* Blad **Sheet1** bevat nog steeds de originele gegevens en draaitabel.
* Blad **Copy** toont een identieke draaitabel met dezelfde lay-out, filters en opmaak.
* Alle formules en gegevensverbindingen blijven intact omdat de pivot‑cache samen met de rijen is gekopieerd.

## Hoe een draaitabel naar een ander blad in hetzelfde werkboek te kopiëren

Als je de draaitabel alleen in een ander bestaand blad nodig hebt (bijv. “Report”), vervang dan de stap voor het maken van een doelblad door een verwijzing naar het doelblad:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Dit fragment demonstreert **een draaitabel naar een ander blad kopiëren** zonder een nieuw werkblad aan te maken.

## Exporteer draaitabel naar nieuw werkboek

Soms wil je de draaitabel in een volledig apart bestand. Na de kopieerbewerking kun je alle werkbladen verwijderen behalve het blad dat de gekopieerde draaitabel bevat en vervolgens opslaan:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Nu bevat `pivot_only.xlsx` één blad met de gedupliceerde draaitabel, waarmee aan de **export draaitabel naar nieuw werkboek**‑vereiste wordt voldaan.

## Hoe Excel‑rijen te kopiëren zonder opmaak te verliezen

Dezelfde `CopyRows`‑aanroep werkt voor elk bereik, niet alleen voor draaitabellen. Als je **Excel‑rijen wilt kopiëren** die voorwaardelijke opmaak, gegevensvalidatie of samengevoegde cellen bevatten, gebruik dan dezelfde methode:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Omdat `CopyOptions.CopyAll` alles overdraagt, zien de doel‑rijen er precies uit als de bron‑rijen.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Valkuil | Symptoom | Oplossing |
|---------|----------|-----------|
| Bronbereik omvat niet de volledige draaitabel | De gekopieerde draaitabel lijkt afgekapt. | Controleer of de `CellArea` alle rijen/kolommen van de draaitabel omvat. |
| Doelblad bevat al gegevens | Overschreven rijen veroorzaken gegevensverlies. | Kies een nieuw blad of begin met kopiëren op een hogere rij‑index. |
| Draaitabel gebruikt een externe gegevensbron | De kopie verliest de verbinding. | Roep na het kopiëren `pivotTable.RefreshData()` aan om de koppeling te herstellen. |
| Verborgen rijen worden weggelaten | Sommige rijen verdwijnen in de kopie. | `CopyRows` kopieert automatisch verborgen rijen; zorg ervoor dat je niet `CopyOptions.CopyValuesOnly` gebruikt. |

## Volledig, uitvoerbaar voorbeeld

Hieronder staat een zelfstandige programma‑code die je in een nieuw console‑project kunt plakken. Het demonstreert elke stap die hierboven is besproken.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Het uitvoeren van het programma** maakt `pivot_copied.xlsx` aan met een duplicaat van de originele draaitabel op een nieuw blad met de naam **Copy**.

## Conclusie

Je weet nu **hoe je een draaitabel kunt kopiëren** in C# met behulp van

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Nieuw Werkboek Maken – Hoe een Werkblad met een Draaitabel Kopiëren](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Draaitabel Kopiëren in C# – Complete Stapsgewijze Gids](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Hoe een bereik met draaitabellen in C# te kopiëren – Complete Gids](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}