---
category: general
date: 2026-05-30
description: Vul Excel-sjabloon snel in en leer hoe je Excel kunt vullen met gegevens
  met behulp van Aspose.Cells SmartMarker. Complete C#-gids met uitvoerbare code.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: nl
og_description: Vul een Excel‑sjabloon in en vul Excel met gegevens met behulp van
  Aspose.Cells SmartMarker. Volg deze stapsgewijze C#‑tutorial voor directe resultaten.
og_title: Excel-sjabloon vullen – Excel-gegevens invullen via SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Excel-sjabloon vullen – Excel-gegevens invullen via SmartMarker
url: /nl/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel‑sjabloon vullen – Excel‑gegevens invullen via SmartMarker

Heb je ooit een **Excel‑sjabloon moeten vullen** maar wist je niet hoe je het proces kunt automatiseren? In deze tutorial laten we je zien hoe je **Excel kunt vullen met gegevens** met behulp van Aspose.Cells SmartMarker – een tool die een statische werkmap omzet in een dynamische rapportgenerator.

Stel je voor dat je een vooraf ontworpen factuursjabloon, een verkoopdashboard of een ander herhaalbaar formulier hebt. In plaats van handmatig waarden in te typen, kun je een C#‑object voeden en SmartMarker het zware werk laten doen. Aan het einde van deze gids heb je een volledig uitvoerbaar project dat een sjabloon neemt, rijen, totalen en zelfs voorwaardelijke opmaak invoegt – allemaal zonder de UI aan te raken.

## Wat je zult leren

- Hoe je een gegevensbron voorbereidt die overeenkomt met de markers in je Excel‑sjabloon.  
- Hoe je **SmartMarkerProcessor** instantieert en bereikondersteuning inschakelt.  
- Hoe je **Excel‑sjabloon vult** met geneste collecties, zoals orderitems.  
- Tips voor het omgaan met randgevallen zoals lege collecties of aangepaste getalformaten.  

Geen externe services, geen VBA‑macro’s – alleen pure C# en Aspose.Cells. Alles wat je nodig hebt is .NET 6 (of later) en het Aspose.Cells NuGet‑pakket.

## Vereisten

- Visual Studio 2022 (of een andere IDE naar keuze).  
- .NET 6 SDK geïnstalleerd.  
- Aspose.Cells voor .NET (je kunt een gratis proefversie downloaden van de Aspose‑website).  
- Een basis‑Excel‑sjabloon met SmartMarker‑tags (we maken er zo meteen een).

Als een van deze je onbekend voorkomt, geen paniek; de stappen hieronder leiden je door elk onderdeel.

## Stap 1: Ontwerp de Excel‑sjabloon met SmartMarker‑tags

Open eerst een nieuwe werkmap en leg de statische delen vast – bedrijfslogo, kopteksten, enzovoort. Voeg vervolgens SmartMarker‑plaatsaanduidingen toe waar dynamische gegevens moeten verschijnen.

| Cel | Inhoud |
|------|---------|
| A1   | **Factuur** |
| A3   | `{{CompanyName}}` |
| A5   | **Bestelgegevens** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Waarom dit belangrijk is:** SmartMarker leest de dubbele accolades en koppelt ze aan eigenschappen van het object dat je later doorgeeft. De `Orders.Items`‑collectie vertelt de engine de rij voor elk item in de lijst te herhalen.

> **Pro tip:** Gebruik de `RangeSmartMarker`‑optie (die we later inschakelen) wanneer je wilt dat de engine het bereik automatisch uitbreidt – perfect voor tabellen die groeien of krimpen.

Sla het bestand op als `InvoiceTemplate.xlsx` in de `Resources`‑map van je project.

## Stap 2: Bereid de gegevensbron voor die overeenkomt met de sjabloon‑markers

Nu maken we een anoniem C#‑object (of een sterk getypeerde klasse) waarvan de eigenschapsnamen overeenkomen met de markers. Het is cruciaal de hiërarchie exact te spiegelen.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Waarom dit belangrijk is:** Het `Orders`‑array bevat één order, en elke order heeft een `Items`‑array. SmartMarker zal over `Items` itereren en de rij voor elk element klonen. Als je later meerdere orders nodig hebt, voeg je gewoon meer objecten toe aan het `Orders`‑array – zonder code‑aanpassingen.

## Stap 3: Laad het sjabloon en maak een SmartMarkerProcessor‑instantie

Met de gegevens klaar, laden we de werkmap, maken we de processor en geven we aan dat deze bereik‑markers moet respecteren.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Waarom dit belangrijk is:** `SmartMarkerProcessor` is de engine die de markers parseert, bereiken uitbreidt en waarden schrijft. Door de processor te scheiden van de werkmap houd je de code schoon en herbruikbaar.

## Stap 4: Verwerk het werkblad met RangeSmartMarker ingeschakeld

De magie gebeurt wanneer we `Process` aanroepen. Het instellen van `RangeSmartMarker = true` vertelt SmartMarker het volledige rij‑bereik als een herhaalbaar blok te behandelen, waardoor rijen automatisch worden ingevoegd of verwijderd.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

Op dit moment heeft de engine:

1. Het werkblad gescand op `{{...}}`‑tags.  
2. Elke tag gekoppeld aan een eigenschap van `data`.  
3. Het tabelbereik (A7:D7) gedetecteerd en drie keer gedupliceerd – één keer per item.  
4. De expressie `Price * Qty` berekend voor de kolom totaal.

## Stap 5: Sla de resulterende werkmap op

Schrijf tenslotte de gevulde werkmap naar schijf (of stream deze terug naar een webclient).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Open `InvoicePopulated.xlsx` en je ziet een netjes gevulde tabel:

| Naam      | Aantal | Prijs | Totaal |
|-----------|--------|-------|--------|
| Pen       | 2      | 1.5   | 3.00 |
| Notebook  | 1      | 3.75  | 3.75 |
| Stapler   | 1      | 5.00  | 5.00 |

De **populate Excel template**‑stap is nu voltooid, en je hebt met succes **Excel gevuld met gegevens** voor een willekeurig aantal rijen.

## Veelvoorkomende randgevallen behandelen

### Lege collecties

Als `Items` leeg is, laat SmartMarker de tabelkop intact, maar voegt geen rijen in. Om een lege ruimte te vermijden, kun je een voorwaardelijk blok toevoegen:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Aangepaste getalformaten

Soms heb je valutatekens of duizendtallen‑scheidingstekens nodig. Na het verwerken kun je een stijl programmatisch toepassen:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Grote datasets

Voor duizenden rijen kun je de `UseFastMode`‑optie inschakelen om de prestaties te verbeteren:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Volledig werkend voorbeeld

Hieronder vind je het complete, zelfstandige programma dat je kunt kopiëren‑plakken in een console‑applicatie. Het bevat alle using‑directives, gegevensvoorbereiding, verwerking en opslaan.



## Wat moet je hierna leren?

- [Vul Excel met gegevens met behulp van Aspose.Cells en Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Hoe Excel‑cellen vullen met Aspose.Cells voor .NET: Een stapsgewijze handleiding](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Excel‑gegevens exporteren automatiseren met Aspose.Cells voor .NET: Een stapsgewijze handleiding](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}