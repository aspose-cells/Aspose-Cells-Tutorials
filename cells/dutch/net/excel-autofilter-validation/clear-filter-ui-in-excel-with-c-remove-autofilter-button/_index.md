---
category: general
date: 2026-02-09
description: Verwijder de AutoFilter-knop in Excel met C# om de filter-UI te wissen.
  Leer hoe je de filterknop verbergt, de koprij weergeeft en je werkbladen netjes
  houdt.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: nl
og_description: Filter-UI in Excel wissen met C#. Deze gids laat zien hoe je de filterknop
  verbergt, de koprij weergeeft en werkbladen schoon houdt.
og_title: Filter UI wissen in Excel met C# – AutoFilter‑knop verwijderen
tags:
- excel
- csharp
- epplus
- automation
title: Filter-UI in Excel wissen met C# – AutoFilter‑knop verwijderen
url: /nl/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Clear filter UI in Excel met C# – Verwijder de AutoFilter‑knop

Heb je ooit de **clear filter UI** in een Excel‑blad moeten verwijderen, maar wist je niet welke regel code die kleine vervolgkeuzepijl verbergt? Je bent niet de enige. De filterknop kan storend zijn wanneer je een rapport naar eindgebruikers stuurt die de weergave nooit hoeven aan te passen.  

In deze tutorial lopen we een compleet, uitvoerbaar voorbeeld door dat **de AutoFilter‑knop** van een tabel verwijdert, ervoor zorgt dat de koprij zichtbaar blijft, en zelfs ingaat op hoe je de *hide filter button* permanent kunt uitschakelen. Aan het einde weet je precies **hoe je AutoFilter verwijdert** in C# en waarom elke stap belangrijk is.

## Wat je nodig hebt

- .NET 6+ (of .NET Framework 4.7.2+) – elke recente runtime werkt.
- Het **EPPlus** NuGet‑pakket (versie 6.x of later) – het levert `ExcelWorksheet`, `ExcelTable`, enz.
- Een simpel Excel‑bestand met een tabel genaamd **SalesTable** (maak er gerust één in een paar klikken).

Dat is alles. Geen COM‑interop, geen extra DLL’s, alleen een handvol `using`‑statements en een paar regels code.

## Clear filter UI: De AutoFilter‑knop verwijderen

De kern van de oplossing bestaat uit drie kleine statements. Laten we ze ontleden zodat je begrijpt *waarom* ze nodig zijn, niet alleen *wat* ze doen.

### Stap 1 – Haal een referentie naar de tabel op

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Waarom dit belangrijk is: EPPlus werkt met **tables** (`ExcelTable`), niet met ruwe bereiken. Door het tabelobject op te halen, krijg je toegang tot de `AutoFilter`‑property, die het UI‑element op het blad regelt. Als je rechtstreeks met het werkblad werkt, beïnvloed je alleen waarden, niet de filterknop.

### Stap 2 – Verwijder de AutoFilter‑knoprij

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Door `AutoFilter` op `null` te zetten, vertelt je EPPlus de onderliggende filterrij te verwijderen. Dit is de *clear filter UI*‑bewerking die de meeste ontwikkelaars zoeken wanneer ze vragen “**how to remove autofilter**”. Het is een nette één‑regelige aanpak die werkt op elke Excel‑versie die EPPlus ondersteunt.

### Stap 3 – Houd de koprij zichtbaar

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

Wanneer je de filter‑UI verwijdert, kan Excel soms de koprij verbergen als de `ShowHeader`‑vlag van de tabel `false` is. Door deze expliciet op `true` te zetten, garanderen we dat de kolomtitels op het scherm blijven – een subtiel maar belangrijk detail voor een gepolijst eindrapport.

### Volledig, uitvoerbaar voorbeeld

Hieronder staat een minimale console‑app die een bestaand werkboek opent, de drie stappen uitvoert en het resultaat opslaat. Kopiëren‑plakken, **F5** indrukken, en zie de filterknop verdwijnen.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Verwacht resultaat:** Open *SalesReport_NoFilter.xlsx* – de filterpijlen zijn weg, maar de kolomkoppen blijven staan. Geen “click‑to‑filter” UI‑rommel meer.

> **Pro tip:** Als je **meerdere tabellen** hebt en de filterknop voor al deze wilt verbergen, loop dan door `worksheet.Tables` en pas dezelfde drie regels toe binnen de lus.

## Hoe AutoFilter verwijderen in Excel met C# – een diepere duik

Je vraagt je misschien af: “Wat als het werkboek al een filter heeft toegepast? Verwijdert `AutoFilter = null` ook de gefilterde rijen?” Het antwoord is **ja**. EPPlus verwijdert zowel de UI als de onderliggende filtercriteria, waardoor de data in de oorspronkelijke volgorde blijft.  

Als je alleen de knop wilt *hide* maar de filter actief wilt laten, kun je in plaats daarvan de `AutoFilter`‑property instellen op een **nieuwe lege filter**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

Die variant is handig wanneer je de *hide filter button* wilt voor een nette uitstraling, maar toch power‑users via VBA of het lint filters wilt laten schakelen.

### Randgeval: Tabellen zonder een koprij

Sommige legacy‑rapporten gebruiken platte bereiken in plaats van tabellen. In dat scenario exposeert EPPlus geen `ExcelTable`‑object, waardoor de bovenstaande code een fout geeft. De oplossing is om **het bereik eerst naar een tabel te converteren**:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Nu heb je de *removed autofilter excel*‑stijl UI zelfs op een bereik dat oorspronkelijk geen formele tabel had.

## Koprij weergeven na verbergen filterknop – waarom het belangrijk is

Een veelgehoorde klacht is dat na het verbergen van de filter‑UI de koprij soms verdwijnt, vooral wanneer het werkboek oorspronkelijk is gemaakt met “Hide Header” ingeschakeld. Door expliciet `salesTable.ShowHeader = true;` te zetten, voorkomen we die verrassing.  

Als je ooit **hide filter button** wilt maar de koprij verborgen wilt houden (bijvoorbeeld bij een ruwe data‑dump), stel dan `salesTable.ShowHeader = false;` in na het wissen van de filter. De code is symmetrisch, waardoor het eenvoudig is om te schakelen op basis van een configuratie‑vlag.

## Hide filter button – praktische tips en valkuilen

- **Versie‑compatibiliteit:** EPPlus 6+ werkt alleen met `.xlsx`‑bestanden. Als je met het oudere `.xls`‑formaat werkt, heb je een andere bibliotheek nodig (bijv. NPOI) omdat de *clear filter UI*‑API niet beschikbaar is.
- **Prestaties:** Het laden van een enorm werkboek alleen om één knop te verbergen kan traag zijn. Overweeg `ExcelPackage.Load(stream, true)` te gebruiken om in **read‑only**‑modus te openen, de wijziging toe te passen en vervolgens op te slaan.
- **Testen:** Valideer het output‑bestand handmatig de eerste keer. Geautomatiseerde UI‑tests kunnen verifiëren dat de filterpijlen echt weg zijn (`worksheet.Tables[0].AutoFilter == null`).
- **Licensing:** EPPlus schakelde over op een dual‑license in versie 5. Voor commerciële projecten heb je een betaalde licentie nodig of moet je overstappen op een alternatieve bibliotheek.

## Volledige broncode voor copy‑paste

Hieronder staat het exacte bestand dat je in een nieuw console‑project kunt plaatsen. Geen verborgen afhankelijkheden, alles staat in één bestand.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Voer `dotnet add package EPPlus --version 6.0.8` (of de nieuwste) uit vóór het bouwen, en je hebt een schoon blad klaar voor distributie.

## Conclusie

We hebben je net laten zien **hoe je AutoFilter verwijdert** en **clear filter UI** toepast in een Excel‑werkboek met C#. De drie‑regelige kern (`AutoFilter = null;`, `ShowHeader = true;`) doet het zware werk, terwijl de omliggende boilerplate de oplossing compleet maakt.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}