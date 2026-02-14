---
category: general
date: 2026-02-14
description: Maak een masterdata-object in C# en genereer moeiteloos een detailblad.
  Leer de volledige SmartMarker-werkstroom met praktische codevoorbeelden.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: nl
og_description: Maak een masterdata‑object in C# en genereer een detailblad met SmartMarker.
  Volg onze gedetailleerde tutorial voor een kant‑klaar oplossing.
og_title: Maak Master Data Object – Complete gids
tags:
- C#
- SmartMarker
- Excel Automation
title: Maak Master Data‑object – Stapsgewijze gids voor het genereren van een detailsheet
url: /nl/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

, should be translated to Dutch. Keep URL unchanged.

Also translate "The illustration shows the flow from the C# master object → SmartMarker options → worksheet processing → new detail sheet." to Dutch.

Also translate "Full Working Example", "Expected Output", etc.

Make sure to keep code block fences and placeholders unchanged.

Let's produce final translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Master‑gegevensobject maken – Complete tutorial

Heb je ooit een **master‑gegevensobject** moeten maken voor een Excel‑werkblad, maar wist je niet hoe je het moet koppelen aan een SmartMarker‑detailblad? Je bent niet de enige. In veel rapportagescenario's stuurt het master‑object een dynamisch detailblad aan, en de juiste bekabeling kan aanvoelen als een puzzel zonder afbeelding.  

In deze gids lopen we het volledige proces door – het bouwen van het master‑gegevensobject, het configureren van de SmartMarker‑opties om een **detailblad te genereren**, en tenslotte het starten van de processor. Aan het einde heb je een uitvoerbaar fragment dat je in elk .NET‑project kunt plakken dat de GrapeCity Documents for Excel (GcExcel)‑bibliotheek gebruikt.

## Wat je nodig hebt

- .NET 6+ (of .NET Framework 4.7.2) met een referentie naar `GcExcel.dll`
- Basiskennis van C# (variabelen, anonieme types, object‑initializers)
- Een Excel‑werkmap die al SmartMarker‑tags bevat zoals `{{OrderId}}` en een tabel voor regelitems
- Visual Studio, Rider of een andere editor naar keuze

Dat is alles – geen extra NuGet‑pakketten naast de core‑distributie van GcExcel.

## Stap 1: Het master‑gegevensobject maken

Het eerste wat je moet doen is een **master‑gegevensobject** maken dat de structuur weerspiegelt die de SmartMarker‑tags verwachten. Zie het als een klein in‑memory rapportmodel.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Waarom hier een anoniem type gebruiken? Omdat het je een lichtgewicht container laat definiëren zonder een volledige klasse te declareren – perfect voor snelle demo’s of wanneer de vorm waarschijnlijk niet verandert. Als je later een herbruikbaar model nodig hebt, vervang je `var` gewoon door een juiste POCO.

> **Pro tip:** Houd de eigenschapsnamen (`OrderId`, `Product`, `Quantity`) exact gelijk aan de placeholders in je werkblad; SmartMarker vergelijkt ze hoofdletter‑ongevoelig.

## Stap 2: SmartMarker‑opties configureren om een detailblad te genereren

Nu vertellen we SmartMarker dat we een apart werkblad willen voor de regel‑item‑tabel. Hier komt het **generate detail sheet**‑keyword van pas.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Het `DetailSheetNewName`‑patroon gebruikt accolades‑placeholders die tijdens runtime worden vervangen. In ons voorbeeld heet het blad `Order_1`. Als je later over meerdere orders iterereert, krijgt elke order zijn eigen tab – precies wat de meeste accountants verwachten.

## Stap 3: De SmartMarker‑processor uitvoeren

Met data en opties klaar, is de laatste stap om de processor aan te roepen op het doel‑werkblad.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Achter de schermen scant SmartMarker het werkblad op tags, injecteert de waarden van `orderData`, en omdat `DetailSheet` `true` is, kloont het de sjabloon naar een nieuw blad met de naam `Order_1`. Alle regelitems verschijnen in het detailgebied, met behoud van alle opmaak die je in de sjabloon hebt toegepast.

### Volledig werkend voorbeeld

Hieronder staat een zelfstandige console‑applicatie die een sjabloon‑werkmap (`Template.xlsx`) opent, de drie stappen uitvoert, en het resultaat opslaat als `Result.xlsx`. Je kunt dit kopiëren‑plakken in een nieuw console‑project en **F5** indrukken.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Verwachte output

- **Result.xlsx** bevat een blad genaamd `Order_1`.
- Cel `A1` (of waar je ook `{{OrderId}}` hebt geplaatst) toont nu `1`.
- Een tabel die begint bij het SmartMarker‑blok bevat twee rijen:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Als je het bestand opent, zie je dat de opmaak uit de sjabloon behouden blijft – randen, lettertypen, voorwaardelijke opmaak – alles intact.

## Veelgestelde vragen & randgevallen

### Wat als ik meerdere orders heb?

Wikkel het master‑object in een collectie en laat SmartMarker automatisch itereren:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Elke order genereert zijn eigen blad (`Order_1`, `Order_2`, …). De processor behandelt de buitenste array als de master‑collectie.

### Hoe regel ik de positie van het blad?

Stel `smartMarkerOptions.DetailSheetInsertIndex = 2;` in om het nieuwe blad na het tweede tabblad te plaatsen, of gebruik `DetailSheetInsertAfter = "Summary"` om na een blad met die naam in te voegen.

### Kan ik het detailblad voor een specifieke uitvoering uitschakelen?

Zet simpelweg `DetailSheet = false;`. SmartMarker schrijft dan de regelitems in hetzelfde blad waar de master‑tags staan.

### Wat als ik met grote datasets werk?

SmartMarker streamt data efficiënt, maar als je enkele honderden duizenden rijen overschrijdt, kun je tegen de limiet van 1.048.576 rijen in Excel aanlopen. Splits in dat geval de data over meerdere master‑records of overweeg export naar CSV.

## Visueel overzicht

![Diagram dat laat zien hoe een master‑gegevensobject te maken en een detailblad te genereren met SmartMarker](/images/smartmarker-flow.png)

*De illustratie toont de stroom van het C#‑master‑object → SmartMarker‑opties → werkbladverwerking → nieuw detailblad.*

## Conclusie

Je weet nu hoe je een **master‑gegevensobject** in C# maakt en SmartMarker configureert om automatisch een **detailblad** te **genereren**. Het drie‑stappen‑patroon – data, opties, processor – dekt het merendeel van Excel‑automatiseringsscenario's met GcExcel.  

Vanaf hier kun je verder verkennen:

- Header/footer‑data toevoegen aan elk detailblad
- Voorwaardelijke opmaak gebruiken op basis van orderstatus
- De gegenereerde werkmap exporteren naar PDF met `workbook.SaveAsPdf(...)`

Voel je vrij om te experimenteren, dingen kapot te maken en ze daarna weer in elkaar te zetten. Dat is de snelste manier om werkblad‑automatisering onder de knie te krijgen. Veel programmeerplezier!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}