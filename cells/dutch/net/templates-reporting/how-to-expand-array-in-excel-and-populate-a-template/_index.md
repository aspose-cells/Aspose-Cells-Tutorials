---
category: general
date: 2026-09-18
description: Leer hoe je een array in Excel kunt uitbreiden met de EXPAND-functie,
  een Excel-sjabloon kunt invullen en een dynamisch bereik in een Excel-werkblad kunt
  maken met C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: nl
lastmod: 2026-09-18
og_description: Hoe een array in Excel uit te breiden met de EXPAND‑functie, een Excel‑sjabloon
  te vullen en een dynamische bereikoplossing in Excel te bouwen met C#‑code.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Hoe een array in Excel uit te breiden en een sjabloon te vullen
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Hoe een array in Excel uit te breiden en een sjabloon te vullen
url: /nl/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een array uit te breiden in Excel en een sjabloon te vullen

Als je **hoe een array uit te breiden** in Excel moet uitvoeren terwijl je een vooraf ontworpen sjabloon invult, laat deze gids je een complete, end‑to‑end oplossing zien. Met de `EXPAND`‑functie samen met de Smart Markers van Aspose.Cells kun je een enkele celreferentie omzetten in een 5 × 5 bereik en automatisch markers zoals `{IsActive}` vervangen door live gegevens.

Je zult zien hoe je **populate excel template** kunt gebruiken, een **dynamic range excel** kunt maken, en correct **use expand function** in een C#‑project. Aan het einde van de tutorial heb je een uitvoerbaar programma dat een `.xlsx`‑bestand laadt, een array‑formule uitbreidt, Smart Markers toepast en het resultaat opslaat.

## Vereisten

* .NET 6.0 of later (de code werkt ook met .NET Core 3.1+)
* Aspose.Cells voor .NET (NuGet‑pakket `Aspose.Cells`)
* Een Excel‑werkmap die een placeholder‑formulecel bevat (bijv. `B2`) en een Smart Marker zoals `{IsActive}`
* Basiskennis van C# en Excel‑formules

> **Pro tip:** De `EXPAND`‑functie is alleen beschikbaar in Excel voor Microsoft 365 en Excel 2021+. Oudere versies geven een `#NAME?`‑fout.

## Stap 1: Hoe een array uit te breiden met de EXPAND‑functie

De eerste stap is het laden van de werkmap en het schrijven van een `EXPAND`‑formule die een enkele broncel omzet in een grotere matrix.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Waarom dit belangrijk is: `EXPAND` maakt het overbodig om formules handmatig te kopiëren over rijen en kolommen. Wanneer de broncel (`A2`) verandert, wordt het volledige 5 × 5‑blok automatisch bijgewerkt, waardoor je een **dynamic range excel** krijgt die reageert op gegevenswijzigingen.

## Stap 2: Excel‑sjabloon vullen met Smart Markers

Smart Markers laten je placeholders in het sjabloon opnemen die worden vervangen door waarden uit een C#‑object. Dit is de meest handige manier om **populate excel template** te vullen zonder cel‑voor‑cel code te schrijven.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

De aanroep `SmartMarkersProcessor().Apply` scant het volledige blad, vindt `{IsActive}` en injecteert de booleaanse waarde. De formule evalueert vervolgens automatisch naar `"Active"` of `"Inactive"`.

## Stap 3: Verifieer het uitgebreide bereik en het gevulde resultaat

Na het toepassen van zowel de `EXPAND`‑formule als Smart Markers, kun je programmatisch enkele cellen lezen om te bevestigen dat alles naar verwachting werkt.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Het uitvoeren van het programma moet de oorspronkelijke waarde van `A2` (of het array‑resultaat) afdrukken en afhankelijk van de `IsActive`‑vlag **Active** of **Inactive** weergeven.

## Stap 4: Werkmap opslaan – de uiteindelijke output

Schrijf tenslotte de aangepaste werkmap naar schijf. Deze stap toont de volledige stroom van laden, uitbreiden, vullen tot het opslaan van het bestand.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

De opgeslagen `output.xlsx` bevat nu een 5 × 5‑matrix die is gegenereerd door de `EXPAND`‑formule en een cel die de waarde van `{IsActive}` weergeeft. Open het bestand in Excel om het dynamische bereik in actie te zien.

## Randgevallen en best practices

| Situatie                              | Aanbeveling                                                                 |
|---------------------------------------|-----------------------------------------------------------------------------|
| Excel‑versie ondersteunt `EXPAND` niet| Val terug op klassieke `=OFFSET`‑ of `=INDEX`‑formules, of upgrade naar Office 365. |
| Noodzaak om uit te breiden naar een variabele grootte | Gebruik `ROWS(source)` en `COLUMNS(source)` binnen `EXPAND` voor echte dynamiek. |
| Meerdere Smart Markers in hetzelfde blad | Roep `SmartMarkersProcessor().Apply` één keer aan met een samengesteld data‑object. |
| Grote werkboeken ( > 10 000 rijen)    | Schakel berekening uit tijdens het schrijven van formules (`workbook.Settings.CheckFormula = false`). |

## Volledig werkend voorbeeld

Hieronder staat het volledige, zelfstandige programma dat je kunt kopiëren‑en‑plakken in een nieuw console‑project.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Verwachte output wanneer je het programma uitvoert** (ervan uitgaande dat `A2` het getal `42` bevat):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Het openen van `output.xlsx` toont een 5 × 5‑blok gevuld met de waarden afgeleid van `A2` en een cel die **Active** weergeeft.

## Conclusie

Je weet nu **how to expand array** in Excel met de `EXPAND`‑functie, hoe je **populate excel template** kunt vullen met Smart Markers, en hoe je een **dynamic range excel** kunt bouwen die automatisch aanpast aan brongegevens. Het voorbeeld toont ook de juiste manier om **use expand function** en de **expand array formula** te gebruiken in een real‑world C#‑automatiseringsscenario.

Vervolgens, overweeg om de oplossing uit te breiden:

* Vervang de vaste `5,5` dimensies door `ROWS(A2:A10), COLUMNS(A2:E2)` voor echt variabele bereiken.
* Combineer meerdere Smart Markers om volledige rapporten te genereren (bijv. werknemerslijsten, verkooptabellen).
* Verken de styling‑API van Aspose.Cells om het uitgebreide blok automatisch op te maken.

Voel je vrij om te experimenteren met verschillende bron‑arrays, marker‑namen en werkmap‑indelingen. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Gegevens exporteren naar Excel: Een sjabloon vullen vanuit een array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [Hoe een array te maken in Excel met C# – Stapsgewijze handleiding](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Gegevens verwerken met de Array‑functie in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}