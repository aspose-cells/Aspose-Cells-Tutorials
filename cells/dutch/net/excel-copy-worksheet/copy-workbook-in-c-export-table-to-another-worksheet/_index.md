---
category: general
date: 2026-06-21
description: Kopieer werkmap in C# en exporteer tabel naar een ander werkblad met
  Aspose.Cells. Volg deze stapsgewijze handleiding voor een schone, herbruikbare oplossing.
draft: false
keywords:
- copy workbook in c#
- export table to another worksheet
language: nl
og_description: Kopieer een werkmap in C# en exporteer een tabel naar een ander werkblad
  met een volledig, uitvoerbaar voorbeeld. Ontdek waarom deze aanpak het beste werkt.
og_title: Werkmap kopiëren in C# – Tabel exporteren naar een ander werkblad
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  headline: Copy Workbook in C# – Export Table to Another Worksheet
  type: TechArticle
- description: Copy workbook in C# and export table to another worksheet using Aspose.Cells.
    Follow this step‑by‑step guide for a clean, reusable solution.
  name: Copy Workbook in C# – Export Table to Another Worksheet
  steps:
  - name: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
    text: '**`Workbook.Copy()`** performs a deep clone of every worksheet, style,
      and formula. It’s the cleanest way to **copy workbook in C#** without manually
      iterating over sheets.'
  - name: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
    text: '**`ExportTableOptions.ExportAsString = true`** tells Aspose.Cells to give
      us a CSV‑style string rather than a binary block. This makes it trivial to drop
      the data into any cell using `PutValue`.'
  - name: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
    text: By exporting from the **source workbook** and inserting into the **destination
      workbook**, we keep the two files completely independent—no accidental cross‑contamination
      of references.
  type: HowTo
tags:
- csharp
- aspose.cells
- excel automation
title: Werkmap kopiëren in C# – Tabel exporteren naar een ander werkblad
url: /nl/net/excel-copy-worksheet/copy-workbook-in-c-export-table-to-another-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkmap kopiëren in C# – Tabel exporteren naar een ander werkblad

Heb je je ooit afgevraagd hoe je **werkmap kopieert in C#** terwijl je ook een specifiek gegevensbereik naar een nieuw blad verplaatst? Je bent niet de enige. Veel ontwikkelaars lopen tegen dit probleem aan bij het automatiseren van rapporten, facturen of datamigraties. Het goede nieuws? Met een paar regels Aspose.Cells‑code kun je zowel de werkmap dupliceren als **tabel exporteren naar een ander werkblad** in één nette workflow.

In deze tutorial lopen we het volledige proces door – van het laden van het bronbestand, het klonen ervan, en het exporteren van een bereik als string, tot het plakken van die string in het bestemmingsblad. Aan het einde heb je een zelfstandige, productie‑klare code‑fragment dat je in elk .NET‑project kunt gebruiken.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

- **Aspose.Cells for .NET** (versie 23.12 of later). Het is een krachtige bibliotheek die Excel‑bestanden verwerkt zonder dat Office geïnstalleerd hoeft te zijn.
- Een .NET‑ontwikkelomgeving (Visual Studio, Rider, of VS Code met de C#‑extensie).
- Een voorbeeld‑werkmap met de naam `Formatted.xlsx` in een bekende map (we verwijzen ernaar als `YOUR_DIRECTORY/Formatted.xlsx`).

Er zijn geen extra NuGet‑pakketten nodig naast Aspose.Cells, en de code werkt op .NET 6+, .NET Framework 4.7+ of .NET Core.

## Stapsgewijze implementatie

Hieronder staat het volledige, uitvoerbare programma. Kopieer‑en‑plak het gerust in een console‑app‑project en druk op **F5**.

```csharp
using System;
using Aspose.Cells;

namespace WorkbookCopyExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load the source workbook
            // -------------------------------------------------
            // Adjust the path to point at your actual file location.
            string sourcePath = @"YOUR_DIRECTORY/Formatted.xlsx";
            Workbook sourceWorkbook = new Workbook(sourcePath);
            Console.WriteLine("Source workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Set up export options – we want the range as a string
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true   // This forces the export to return CSV‑style text.
            };
            Console.WriteLine("Export options configured (ExportAsString = true).");

            // -------------------------------------------------
            // Step 3: Copy workbook in C# – creates an isolated clone
            // -------------------------------------------------
            // Using the Copy method ensures the original stays untouched.
            Workbook destinationWorkbook = sourceWorkbook.Copy();
            Console.WriteLine("Destination workbook created as a copy of the source.");

            // -------------------------------------------------
            // Step 4: Export the specified range (B2:B10) from the source sheet
            // -------------------------------------------------
            // The range is taken from the first worksheet (index 0).
            // ExportTable returns a string that can be written directly.
            string exportedTable = sourceWorkbook.Worksheets[0]
                .Cells.ExportTable(sourceWorkbook.Worksheets[0].Cells["B2:B10"],
                                   exportOptions);
            Console.WriteLine("Range B2:B10 exported as string:");
            Console.WriteLine(exportedTable);

            // -------------------------------------------------
            // Step 5: Paste the exported string into the destination sheet
            // -------------------------------------------------
            // We start at cell A1 of the first worksheet in the destination.
            destinationWorkbook.Worksheets[0].Cells["A1"]
                .PutValue(exportedTable);
            Console.WriteLine("Exported data placed at A1 in the destination workbook.");

            // -------------------------------------------------
            // Step 6: Save the result so you can verify it
            // -------------------------------------------------
            string resultPath = @"YOUR_DIRECTORY/Copy_With_ExportedTable.xlsx";
            destinationWorkbook.Save(resultPath);
            Console.WriteLine($"Result saved to {resultPath}");
        }
    }
}
```

### Waarom deze aanpak werkt

1. **`Workbook.Copy()`** maakt een diepe kloon van elk werkblad, elke stijl en elke formule. Het is de meest eenvoudige manier om **werkmap kopieert in C#** zonder handmatig over bladen te itereren.
2. **`ExportTableOptions.ExportAsString = true`** vertelt Aspose.Cells ons een CSV‑achtige string te geven in plaats van een binair blok. Hierdoor kun je de gegevens eenvoudig in elke cel plaatsen met `PutValue`.
3. Door te exporteren vanuit de **bron‑werkmap** en in te voegen in de **doel‑werkmap**, blijven de twee bestanden volledig onafhankelijk – er ontstaat geen onbedoelde kruis‑verwijzing.

## Randgevallen & Veelvoorkomende valkuilen

| Situatie | Waar je op moet letten | Oplossing / Aanbeveling |
|-----------|------------------------|------------------------|
| **Verschillende werkblad‑indexen** | Als de bron‑ of doel‑werkmap meerdere bladen heeft, kan een hard‑gecodeerde index `0` het verkeerde blad selecteren. | Gebruik `Worksheets["SheetName"]` of loop door `Worksheets` om het gewenste blad te vinden. |
| **Grote bereiken** | Het exporteren van een enorm bereik als string kan geheugenlimieten raken. | Overweeg om in delen te exporteren of gebruik `ExportTable` met `ExportAsString = false` en verwerk binaire streams. |
| **Verlies van opmaak** | `ExportAsString` verwijdert alle opmaak; alleen ruwe waarden blijven behouden. | Als je stijlen nodig hebt, exporteer dan als een `IEnumerable<CellArea>` en kopieer cellen één voor één. |
| **Bestandspad‑problemen** | Relatieve paden kunnen breken wanneer de app vanuit een andere werkmap wordt uitgevoerd. | Gebruik `Path.Combine(Environment.CurrentDirectory, "Formatted.xlsx")` of sla paden op in configuratie. |

### Pro Tip

Als je de geëxporteerde gegevens in meerdere werkmappen wilt hergebruiken, verpak dan de export‑en‑plak‑logica in een hulpfunctie:

```csharp
static void ExportRangeToWorkbook(Workbook src, string range, Workbook dest, string destCell)
{
    var opts = new ExportTableOptions { ExportAsString = true };
    string data = src.Worksheets[0].Cells.ExportTable(src.Worksheets[0].Cells[range], opts);
    dest.Worksheets[0].Cells[destCell].PutValue(data);
}
```

Nu kun je `ExportRangeToWorkbook(sourceWorkbook, "B2:B10", destinationWorkbook, "A1");` aanroepen waar je maar wilt.

## Het resultaat verifiëren

Open `Copy_With_ExportedTable.xlsx` in Excel of een andere spreadsheet‑viewer:

- Het eerste werkblad zou identiek moeten zijn aan `Formatted.xlsx` **behalve** voor het nieuwe gegevensblok dat begint bij **A1**.
- Cellen A1 tot en met A9 (of hoeveel rijen B2:B10 ook beslaat) bevatten de geëxporteerde waarden, gescheiden door de standaard‑scheidingsteken (komma voor CSV). Als je een ander scheidingsteken nodig hebt, stel dan `exportOptions.Separator` in vóór het exporteren.

Die visuele controle bevestigt dat zowel de **werkmap kopieert in C#**‑operatie als de **tabel exporteren naar een ander werkblad** succesvol zijn uitgevoerd.

## Afronding

We hebben zojuist een schone, herhaalbare patroon laten zien voor **werkmap kopieert in C#** terwijl we tegelijkertijd **een tabel exporteren naar een ander werkblad**. De belangrijkste leerpunten zijn:

- Gebruik `Workbook.Copy()` voor een veilige, diepe kloon.
- Maak gebruik van `ExportTableOptions.ExportAsString` om een bereik om te zetten in een draagbare string.
- Plaats de string waar je maar wilt met `PutValue`.

Vanaf hier kun je verder gaan met:

- Het exporteren van meerdere, niet‑aaneengesloten bereiken.
- Het omzetten van de string naar een 2‑D‑array voor uitgebreidere gegevensmanipulatie.
- Het automatiseren van het proces over een map met werkmappen (batch‑verwerking).

Probeer het, pas het bereik aan, en zie hoe deze techniek je Excel‑automatiseringspijplijnen vereenvoudigt. Als je tegen problemen aanloopt of ideeën hebt voor uitbreidingen, laat dan gerust een reactie achter. Veel programmeerplezier!

![Copy workbook in C# example diagram](https://example.com/images/copy-workbook-diagram.png "Copy workbook in C# example showing source, export, and destination steps")

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Copy Worksheet from One Workbook to Another using Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data Within Workbook using Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-data-within-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}