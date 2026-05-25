---
category: general
date: 2026-03-29
description: Leer hoe je een bereik kopieert, draaitabellen kopieert, hoe je een werkmap
  opslaat en hoe je een werkmap laadt in C#. Verplaats draaitabellen eenvoudig met
  stapsgewijze code.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: nl
og_description: Hoe een bereik te kopiëren, draaitabellen te kopiëren, een werkmap
  op te slaan en een werkmap te laden in C#. Verplaats draaitabellen moeiteloos met
  duidelijke code.
og_title: Hoe een bereik met draaitabellen te kopiëren in C# – Complete gids
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hoe een bereik met draaitabellen te kopiëren in C# – Complete gids
url: /nl/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een bereik met draaitabellen te kopiëren in C# – Complete gids

Heb je je ooit afgevraagd **hoe je een bereik** dat een draaitabel bevat kunt kopiëren zonder de koppeling met de brongegevens te verbreken? Je bent niet de enige. In veel real‑world projecten ben ik op dit exacte probleem gestuit—Excel‑bestanden komen met geavanceerde draaitabellen, en de eis is om ze te verplaatsen of de gegevens ergens anders te dupliceren.  

Het goede nieuws? De oplossing is vrij eenvoudig zodra je weet **hoe je een werkmap laadt**, een kopie maakt, en vervolgens **hoe je een werkmap opslaat**. In deze tutorial lopen we het volledige proces door, inclusief hoe je **draaitabellen kopieert**, en zelfs een snelle tip over **draaitabel verplaatsen** als je die ergens anders in hetzelfde blad nodig hebt.

Aan het einde van deze gids heb je een volledig functioneel C#‑fragment dat:

1. Laadt een bestaand Excel‑bestand.  
2. Kopieert een bereik (inclusief de draaitabel) naar een nieuwe locatie.  
3. Slaat de aangepaste werkmap op in een nieuw bestand.

Geen externe scripts, geen handmatig geknoei—alleen schone, herhaalbare code.

---

## Vereisten

- **.NET 6+** (elke recente versie werkt).  
- **Aspose.Cells for .NET** – de bibliotheek die `Workbook`, `WorksheetCopyOptions`, enz. levert. Je kunt het installeren via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Een invoer‑werkmap (`input.xlsx`) die al een draaitabel bevat in het bereik `A1:G20`.  
- Basiskennis van C# en Visual Studio (of je favoriete IDE).

> **Pro tip:** Als je een andere Excel‑bibliotheek gebruikt (bijv. EPPlus), zijn de concepten hetzelfde—vervang gewoon de API‑aanroepen.

## Stap 1 – Hoe je een werkmap laadt (Primaire setup)

Voordat we iets kunnen kopiëren, moeten we het Excel‑bestand in het geheugen laden.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Waarom dit belangrijk is:**  
Het laden van de werkmap geeft je een objectmodel dat je kunt manipuleren. Zonder **hoe je een werkmap laadt** correct, zou elke daaropvolgende kopie‑operatie een *FileNotFound* of *InvalidOperation*‑exception veroorzaken.

> **Let op:** Als het bestand groot is, overweeg dan `LoadOptions` met `MemorySetting` te gebruiken om het geheugenverbruik te regelen.

## Stap 2 – Hoe je een bereik kopieert (inclusief de draaitabel)

Nu komt de ster van de show: het kopiëren van een bereik dat een draaitabel bevat. De `CopyRange`‑methode, gecombineerd met `WorksheetCopyOptions`, doet het zware werk.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Waarom we `CopyPivotTables = true` instellen:**  
Standaard verplaatst het kopiëren van een bereik alleen de ruwe cellen. De draaitabel‑cache blijft achter, en de gekopieerde draaitabel wordt een statische tabel. Het instellen van `CopyPivotTables` behoudt de live‑verbinding, zodat de gedupliceerde draaitabel nog steeds wordt vernieuwd wanneer de brongegevens veranderen.

**Randgeval:** Als het doelbereik overlapt met de bron, zal Aspose.Cells een `ArgumentException` gooien. Kies altijd een niet‑overlappend doel, of maak eerst een nieuw werkblad.

## Stap 3 – Hoe je een werkmap opslaat (De wijzigingen behouden)

Na het kopiëren wil je de wijzigingen terug naar de schijf schrijven. Hier komt **hoe je een werkmap opslaat** in beeld.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**Wat er onder de motorkap gebeurt:**  
`Save` serialiseert de werkmap in het geheugen, inclusief de nieuw gekopieerde draaitabel, naar een standaard `.xlsx`‑pakket. Als je een ander formaat nodig hebt (CSV, PDF, enz.), wijzig dan simpelweg de bestandsextensie of gebruik de overload die `SaveFormat` accepteert.

> **Tip:** Gebruik `Workbook.Save(string, SaveOptions)` als je het bestand met een wachtwoord wilt beveiligen of andere exportopties wilt instellen.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het volledige, kant‑klaar programma:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Verwacht resultaat:**  
Open `output.xlsx`. Je ziet de originele draaitabel nog steeds in `A1:G20`, en een identieke, volledig functionele kopie die start bij `A25`. Beide draaitabellen wijzen naar dezelfde brongegevens, dus het vernieuwen van de ene werkt de andere bij.

## Veelgestelde vragen & Variaties

### Kan ik **draaitabel verplaatsen** in plaats van deze te kopiëren?

Absoluut. Na het kopiëren, wis je simpelweg het oorspronkelijke bereik (of gebruik `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) en hernoem je vervolgens het doelbereik indien nodig. Dit verplaatst de draaitabel effectief.

### Wat als de draaitabel een externe gegevensbron gebruikt?

`CopyPivotTables = true` kopieert alleen de draaitabeldefinitie, niet de externe verbinding zelf. Zorg ervoor dat de doel‑werkmap toegang heeft tot dezelfde gegevensbron, of maak de verbinding opnieuw na het kopiëren.

### Hoe kopieer ik naar een **ander werkblad**?

Geef simpelweg het doel‑werkbladobject door in plaats van `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Is er een manier om **meerdere bereiken** tegelijk te kopiëren?

Je kunt `CopyRange` herhaaldelijk aanroepen of `CopyRows`/`CopyColumns` gebruiken voor grotere blokken. Over een lijst van adres‑strings itereren is een nette aanpak.

## Veelvoorkomende valkuilen & Pro‑tips

- **Grootte van de draaitabel‑cache:** Grote draaitabel‑caches kunnen de grootte van de werkmap doen toenemen. Als je alleen de weergegeven gegevens nodig hebt, overweeg dan `CopyPivotTables = false` en gebruik vervolgens `PivotTable.RefreshData()` op het doel.  
- **Bestandspaden:** Gebruik `Path.Combine` om hard‑gecodeerde scheidingstekens te vermijden, vooral op cross‑platform .NET.  
- **Prestaties:** Voor enorme werkmappen, wikkel de kopie in een `using (var stream = new MemoryStream())` en sla eerst op naar de stream, daarna naar de schijf. Dit vermindert I/O‑overhead.

## Conclusie

Je weet nu **hoe je een bereik kopieert** dat een draaitabel bevat, hoe je **draaitabellen kopieert**, en de exacte stappen om **een werkmap te laden** en **een werkmap op te slaan** na de bewerking. Of je nu een **draaitabel moet verplaatsen** binnen hetzelfde blad of naar een ander werkblad, het patroon blijft hetzelfde—laden, kopiëren met de juiste opties, en opslaan.

Probeer het met je eigen bestanden, pas het doeladres aan, en experimenteer met verschillende draaitabel‑configuraties. Hoe meer je ermee speelt, hoe zekerder je wordt in het automatiseren van Excel‑taken in C#.

![Diagram dat het bronbereik A1:G20 wordt gekopieerd naar A25 in hetzelfde werkblad – hoe een bereik met draaitabellen te kopiëren](/images/how-to-copy-range-diagram.png "hoe een bereik met draaitabellen te kopiëren")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}