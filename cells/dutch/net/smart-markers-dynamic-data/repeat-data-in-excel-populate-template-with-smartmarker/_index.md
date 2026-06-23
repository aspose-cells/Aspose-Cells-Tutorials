---
category: general
date: 2026-02-21
description: Herhaal gegevens in Excel snel met SmartMarker—leer hoe je een Excel-sjabloon
  vult en rijen moeiteloos herhaalt.
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: nl
og_description: herhaal gegevens in Excel met SmartMarker. Leer hoe je een Excel-sjabloon
  vult, rijen herhaalt en je spreadsheets automatiseert.
og_title: Gegevens herhalen in Excel – Sjabloon vullen met SmartMarker
tags:
- excel
- csharp
- smartmarker
- automation
title: Gegevens herhalen in Excel – Sjabloon vullen met SmartMarker
url: /nl/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# gegevens herhalen in Excel – Sjabloon vullen met SmartMarker

Heb je ooit **gegevens moeten herhalen in Excel** maar wist je niet hoe je handmatig kopiëren‑plakken kon vermijden? Je bent niet de enige. In veel rapportagescenario's heb je een lijst items die automatisch in rijen moet worden uitgebreid, en dit handmatig doen leidt snel tot fouten.

Het punt is: met de **SmartMarkerProcessor** uit de **GemBox.Spreadsheet**‑bibliotheek kun je **een Excel‑sjabloon vullen** met één regel C# en laten de rijen voor elk item in je collectie herhalen. In deze gids lopen we stap voor stap de exacte procedure door, laten we de volledige code zien en leggen we uit waarom elk onderdeel belangrijk is, zodat je zonder moeite rijen in Excel kunt herhalen.

## Wat je gaat leren

* Hoe je de datastructuur definieert die de herhaaloperatie aandrijft.  
* Hoe je een `SmartMarkerProcessor` koppelt aan een werkmap die een verborgen sjabloonsheet bevat.  
* Hoe de marker `${Repeat:Item}` automatisch in meerdere rijen wordt uitgebreid.  
* Tips voor het omgaan met randgevallen zoals lege collecties of aangepaste opmaak.  

Aan het einde van deze tutorial kun je **Excel vullen vanuit data** op een manier die schaalbaar is, makkelijk te onderhouden, en werkt met elk .NET‑project.

---

## Vereisten

* .NET 6.0 of hoger (de code maakt gebruik van moderne C#‑features).  
* Het **GemBox.Spreadsheet** NuGet‑pakket (de gratis versie werkt tot 150 rijen).  
* Een basis‑Excel‑sjabloonbestand (`Template.xlsx`) met een verborgen sheet genaamd `HiddenTemplate`.  
* Basiskennis van C#‑objecten en LINQ is handig maar niet vereist.

---

## Stap 1 – Definieer de herhaal‑datastructuur

Eerst heb je een gegevensbron nodig waar de SmartMarker‑engine over kan itereren. In de meeste real‑world apps komt dit uit een database, een API of een CSV‑bestand. Voor de duidelijkheid gebruiken we een anonieme type met één eigenschap `Item` die een array van strings bevat.

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Waarom dit belangrijk is:** De marker `${Repeat:Item}` in het Excel‑sjabloon zoekt naar een eigenschap met de naam `Item`. Als je de eigenschap hernoemt, moet je de marker overeenkomstig aanpassen. Deze strakke koppeling zorgt ervoor dat het sjabloon synchroon blijft met je code, waardoor je makkelijker **excel‑sjabloon kunt vullen** zonder te gokken naar kolomnamen.

### Veelvoorkomende variaties

* **Complexe objecten:** In plaats van een eenvoudige string‑array kun je een lijst van objecten leveren (`new[] { new { Name = "A", Qty = 10 } }`). De marker zal rijen herhalen en je kunt `${Item.Name}` en `${Item.Qty}` in het blad gebruiken.  
* **Lege collecties:** Als `Item` leeg is, verwijdert SmartMarker simpelweg het herhaal‑blok, waardoor het sjabloon ongewijzigd blijft – ideaal voor optionele secties.

---

## Stap 2 – Maak de SmartMarkerProcessor voor het verborgen sjabloonsheet

Laad vervolgens je werkmap en maak een `SmartMarkerProcessor` aan. Verwijs deze naar de werkmap die het verborgen sjabloonsheet bevat; SmartMarker kopieert dat sheet naar een zichtbaar sheet en breidt de herhaal‑markers uit.

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** Als je meerdere sjablonen in hetzelfde bestand hebt, kun je de bron‑sheetnaam opgeven bij het aanroepen van `processor.Process`. Dit helpt wanneer je **rijen moet herhalen in excel** voor verschillende delen van een rapport.

### Afhandeling van randgevallen

* **Ontbrekend sjabloonsheet:** Plaats de load in een try/catch en log een duidelijke fout – dit voorkomt stille fouten wanneer het bestandspad onjuist is.  
* **Grote datasets:** Voor duizenden rijen kun je overwegen de output te streamen naar een bestand (`processor.Save`) in plaats van alles in het geheugen te houden.

---

## Stap 3 – Pas de data toe en breid de `${Repeat:Item}`‑marker uit

Nu volgt de magische regel die daadwerkelijk de rijen herhaalt. Geef het object dat je in Stap 1 hebt gemaakt door aan `processor.Process`. SmartMarker zoekt elke `${Repeat:Item}`‑marker, dupliceert de rij voor elk element en vervangt de placeholders door de werkelijke waarden.

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### Wat je zou moeten zien

Wanneer je `Result.xlsx` opent, is het verborgen sjabloonsheet gekopieerd naar een nieuw zichtbaar sheet (standaard `Sheet1`). De rij die `${Repeat:Item}` bevat, verschijnt nu drie keer, met in de cellen respectievelijk **A**, **B** en **C**.

| Item |
|------|
| A    |
| B    |
| C    |

Als je extra kolommen toevoegt zoals `${Item.Price}`, worden die automatisch ingevuld vanuit de gegevensbron.

---

## Hoe rijen in Excel te herhalen zonder SmartMarker (snelle vergelijking)

| Benadering               | Codecomplexiteit | Onderhoud | Prestaties |
|--------------------------|-------------------|-----------|------------|
| Handmatig kopiëren‑plakken| Hoog              | Laag      | Slecht     |
| VBA‑macro                | Gemiddeld         | Gemiddeld | Goed       |
| **SmartMarkerProcessor** | Laag              | Hoog      | Uitstekend |

Zoals je ziet, levert het gebruik van SmartMarker om **gegevens te herhalen in excel** de schoonste scheiding tussen sjabloondesign en bedrijfslogica. Het is bovendien taal‑agnostisch – vergelijkbare concepten bestaan in Java, Python en JavaScript‑bibliotheken.

---

## Geavanceerde tips & veelvoorkomende valkuilen

### 1. Opmaak van de herhaalde rijen

SmartMarker kopieert de volledige rij – inclusief celstijlen, randen en voorwaardelijke opmaak. Als je een andere stijl nodig hebt voor de eerste of laatste rij, voeg dan extra markers toe zoals `${If:Item.IsFirst}` en gebruik voorwaardelijke formules in Excel.

### 2. Werken met grote datasets

Bij > 10 000 rijen kun je de automatische berekening van Excel uitschakelen vóór het verwerken:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

Schakel deze daarna weer in na het opslaan om de prestaties soepel te houden.

### 3. Excel vullen vanuit data in een echte database

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

Gebruik vervolgens `${Repeat:Order}` in het sjabloon om elke order te vermelden. Dit patroon laat zien hoe eenvoudig het is om **excel vanuit data te vullen** direct vanuit Entity Framework.

### 4. Meerdere herhaal‑blokken gebruiken

Je kunt meerdere `${Repeat:...}`‑markers op hetzelfde sheet of op verschillende sheets hebben. SmartMarker verwerkt ze opeenvolgend, dus de volgorde is alleen van belang als een blok afhankelijk is van de output van een ander blok.

---

## Volledig uitvoerbaar voorbeeld

Hieronder vind je een zelfstandige console‑applicatie die je in Visual Studio kunt plakken en direct kunt uitvoeren. Het demonstreert alle drie de stappen plus het opslaan van het bestand.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**Verwachte output:** `Result.xlsx` bevat een sheet waarin de rij met `${Repeat:Item}` drie keer verschijnt, met A, B en C. Geen handmatige aanpassingen nodig.

---

## Conclusie

Je weet nu hoe je **gegevens efficiënt kunt herhalen in excel** door gebruik te maken van de SmartMarkerProcessor. Door een eenvoudige data‑object te definiëren, een sjabloon‑werkmap te laden en `Process` aan te roepen, kun je **excel‑sjabloon vullen**, **rijen herhalen in excel**, en over het algemeen **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}