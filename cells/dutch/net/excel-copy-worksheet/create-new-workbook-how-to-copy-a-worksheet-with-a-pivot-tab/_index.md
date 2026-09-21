---
category: general
date: 2026-03-01
description: Maak een nieuw werkboek en kopieer een werkblad naar een werkboek met
  een draaitabel. Leer hoe je een draaitabel exporteert, een blad kopieert en een
  draaitabel kopieert in C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: nl
og_description: Maak een nieuw werkboek in C# en kopieer een werkblad naar het werkboek
  terwijl je de draaitabel behoudt. Stapsgewijze handleiding met volledige code.
og_title: Nieuw werkboek maken – Werkblad en draaitabel kopiëren in C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Nieuw werkboek maken – Hoe een werkblad met een draaitabel kopiëren
url: /nl/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe Werkmap Maken – Werkblad & Pivottabel Kopiëren in C#

Heb je ooit moeten **create new workbook** die een kant‑klare pivottabel bevat zonder deze vanaf nul op te bouwen? Je bent niet de enige. In veel rapportagescenario's heb je een masterbestand (`src.xlsx`) met een complexe pivottabel, en wil je een schone kopie (`dest.xlsx`) naar een klant of een ander systeem sturen. Het goede nieuws? Je kunt het in slechts twee regels C# doen — en deze gids laat je precies zien hoe.

We lopen het hele proces door: het laden van de bronwerkmap, het kopiëren van het eerste werkblad (dat de pivottabel bevat), en het opslaan als een gloednieuwe werkmap. Aan het einde weet je **how to copy sheet** die een pivottabel bevat, hoe je **export pivot table** gegevens kunt exporteren indien nodig, en zelfs een paar trucjes voor randgevallen zoals kopiëren naar een bestaand bestand.

## Vereisten

- .NET 6.0 of later (any recent version works)
- Aspose.Cells for .NET (free trial or licensed version) – deze bibliotheek levert de `Workbook`‑klasse die hieronder wordt gebruikt.
- Een bron‑Excel‑bestand (`src.xlsx`) dat al een pivottabel bevat op het eerste werkblad.

Als je Aspose.Cells nog niet hebt, voeg het toe via NuGet:

```bash
dotnet add package Aspose.Cells
```

Dat is alles—geen extra COM‑interop, geen Excel geïnstalleerd op de server.

## Wat Deze Tutorial Behandelt

- **Create new workbook** van een bestaand werkblad dat een pivottabel bevat.
- **Copy worksheet to workbook** terwijl alle pivottabeldefinities behouden blijven.
- **Export pivot table** gegevens naar een DataTable (optioneel).
- Veelvoorkomende valkuilen bij het gebruik van **how to copy pivot** in verschillende omgevingen.
- Een compleet, uitvoerbaar voorbeeld dat je in een console‑app kunt plaatsen.

---

## Stap 1: Laad de Bronwerkmap (How to Copy Sheet)

Het eerste wat je doet is de werkmap openen die de pivottabel bevat. Het gebruik van Aspose.Cells maakt dit moeiteloos omdat het het bestand in het geheugen leest zonder Excel te starten.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Why this matters:** Het laden van het bestand valideert dat de pivottabel bestaat en geeft je toegang tot de werkbladcollectie. Als het bestand corrupt is, gooit `Workbook` een duidelijke uitzondering, waardoor je later geen mysterieuze output krijgt.

## Stap 2: Kopieer het Werkblad naar een Nieuwe Werkmap (Copy Worksheet to Workbook)

Nu **copy worksheet to workbook** we daadwerkelijk. De `CopyTo`‑methode van Aspose.Cells kloont het volledige blad—incl. formules, opmaak en pivottabelcache—naar een nieuw bestand.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Pro tip:** `CopyTo` maakt een gloednieuwe werkmap op de achtergrond, zodat je geen extra `Workbook`‑object hoeft te instantieren. Dit houdt het geheugenverbruik laag en garandeert dat de pivottabeldefinitie intact blijft.

## Stap 3: Verifieer de Gekopieerde Pivottabel (How to Copy Pivot)

Nadat de kopie voltooid is, is het een goed idee om het nieuwe bestand te openen en te bevestigen dat de pivottabel nog werkt. Je kunt dit programmatisch doen of gewoon in Excel openen.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

Running the program prints something like:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Als je die waarden ziet, is de **how to copy pivot** stap geslaagd.

## Stap 4: (Optioneel) Export Pivottabelgegevens naar een DataTable

Soms heb je de ruwe cijfers uit de pivottabel nodig zonder Excel te openen. Aspose.Cells laat je de pivottabelgegevens naar een `DataTable` halen — perfect voor verdere verwerking of API‑reacties.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Why you might want this:** Exporteren stelt je in staat om **export pivot table** inhoud naar een database, JSON‑payload, of een ander formaat te sturen zonder handmatig kopiëren‑plakken.

## Stap 5: Randgevallen & Veelvoorkomende Valkuilen

### Kopiëren Naar een Bestaande Werkmap

Als je **copy worksheet to workbook** moet naar een werkmap die al andere bladen bevat, gebruik dan de overload die een doel‑`Workbook`‑instantie accepteert:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Behouden van Externe Gegevensbronnen

Pivottabellen die gegevens halen uit externe verbindingen (bijv. Power Query) kunnen hun koppeling verliezen na het kopiëren. In dat geval stel je `pivot.RefreshDataOnOpen = true` in vóór het opslaan:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### Grote Bestanden & Prestaties

Voor bestanden groter dan 50 MB, overweeg `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` in te schakelen om de geheugenbelasting te verminderen.

---

![Create new workbook example](https://example.com/images/create-new-workbook.png "Nieuwe werkmap")

*Afbeeldingsalttekst: nieuwe werkmap – een werkblad met een pivottabel kopiëren*

## Volledig Werkend Voorbeeld (Alle Stappen Gecombineerd)

Hieronder staat de volledige, kant‑klaar console‑applicatie. Kopieer‑plak het in een nieuw `.csproj` en druk op **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Verwacht Resultaat

- `dest.xlsx` verschijnt in `YOUR_DIRECTORY`.
- Het eerste blad ziet er precies uit als het origineel, compleet met de pivottabel.
- Het uitvoeren van de console drukt pivottabel‑metadata en een kleine gegevenspreview af, wat bevestigt dat de kopie geslaagd is.

---

## Conclusie

Je weet nu hoe je **create new workbook** kunt maken door een werkblad met een pivottabel te kopiëren, hoe je **copy worksheet to workbook** kunt uitvoeren, en zelfs hoe je **export pivot table** gegevens kunt exporteren voor downstream verwerking. Of je nu een rapportageservice bouwt, Excel‑distributie automatiseert, of gewoon een snelle manier nodig hebt om een pivottabel te dupliceren, de bovenstaande stappen bieden een betrouwbare, productie‑klare oplossing.

**Next steps** die je kunt verkennen:

- Combineer meerdere bladen (gebruik `CopyTo` herhaaldelijk) – perfect voor het samenstellen van een volledig rapport.
- Pas de refresh‑instellingen van de pivottabelcache aan wanneer de brongegevens veranderen.
- Gebruik **how to copy sheet** technieken om grafieken, afbeeldingen of VBA‑modules te dupliceren.
- Duik in Aspose.Cells’ `WorkbookDesigner` voor sjabloon‑gebaseerde rapportgeneratie.

Probeer het, pas de paden aan, en zie hoe eenvoudig het is om schone, pivottabel‑klare werkmappen te verzenden. Heb je vragen over randgevallen of licenties? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}