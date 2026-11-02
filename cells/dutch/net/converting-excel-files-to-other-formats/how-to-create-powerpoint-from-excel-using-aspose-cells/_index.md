---
category: general
date: 2026-09-18
description: Maak PowerPoint van Excel met Aspose.Cells – kopieer draaitabellen, exporteer
  bereiken en sla op als PPTX in een paar regels C#‑code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: nl
lastmod: 2026-09-18
og_description: Maak snel een PowerPoint vanuit Excel. Leer hoe je draaitabellen kunt
  kopiëren, bereiken kunt exporteren en een werkmap kunt opslaan als PPTX met Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: PowerPoint maken vanuit Excel met Aspose.Cells – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Hoe PowerPoint te maken vanuit Excel met Aspose.Cells
url: /nl/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe PowerPoint maken vanuit Excel met Aspose.Cells

Als je PowerPoint wilt maken vanuit Excel, laat deze gids je een beknopte, end‑to‑end oplossing zien. Je ziet hoe je een draaitabel kopieert, een geselecteerd bereik exporteert en het resultaat opslaat als een PPTX‑bestand met slechts een paar regels C#.

Het genereren van een slide‑deck direct vanuit spreadsheet‑gegevens verwijdert de handmatige kopie‑plakstap die rapportage‑workflows vertraagt. De tutorial behandelt alles wat je nodig hebt, van projectconfiguratie tot het uiteindelijke PPTX‑bestand, en werkt met de nieuwste Aspose.Cells voor .NET.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* **Aspose.Cells for .NET** (versie 23.12 of nieuwer). Installeer het via NuGet: `Install-Package Aspose.Cells`.
* Een **.NET 6+** ontwikkelomgeving (Visual Studio 2022 of VS Code werkt).
* Een Excel‑werkmap (`Source.xlsx`) die de gegevens en de draaitabel bevat die je wilt hergebruiken.
* Schrijfrechten op de doelmap.

Er zijn geen extra externe bibliotheken vereist.

## PowerPoint maken vanuit Excel – stap voor stap

Het proces bestaat uit vier logische stappen die direct overeenkomen met het code‑voorbeeld dat je later ziet.

### Stap 1: Laad de bron‑werkmap en definieer het bereik

Je moet de werkmap laden die de brongegevens en de draaitabel bevat. Het selecteren van een precies bereik zorgt ervoor dat alleen de benodigde cellen worden overgebracht, waardoor de resulterende slide licht blijft.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Waarom dit belangrijk is:**  
`CreateRange` maakt een `Range`‑object dat als geheel kan worden gekopieerd. Door het bereik te beperken tot `A1:G20`, voorkom je dat ongewenste cellen worden meegenomen, wat anders het PowerPoint‑bestand zou kunnen opsblazen.

### Stap 2: Bereid de doel‑werkmap voor

Aspose.Cells behandelt een PowerPoint‑slide als een werkmap wanneer je deze opslaat in PPTX‑formaat. Het aanmaken van een nieuwe werkmap geeft je een schoon canvas voor het gekopieerde bereik.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** Als je meerdere slides nodig hebt, kun je extra werkbladen toevoegen en later elk opslaan als een afzonderlijk PPTX‑bestand.

### Stap 3: Kopieer het bereik met behoud van de draaitabel

De `CopyRange`‑methode accepteert een `PasteOptions`‑object. Door `CopyPivotTables = true` in te stellen, vertelt je Aspose.Cells om de structuur van de draaitabel intact te houden, niet alleen de weergegeven waarden.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Hoe het werkt:**  
Wanneer `CopyPivotTables` true is, ontvangt het doelblad zowel de brongegevens als de draaitabel‑cache. Dit betekent dat de draaitabel volledig functioneel blijft en later kan worden vernieuwd als de brongegevens veranderen.

### Stap 4: Sla de werkmap op als een PowerPoint‑bestand

Tot slot exporteer je de werkmap naar PPTX‑formaat. De vlag `SaveFormat.Pptx` vertelt Aspose.Cells om het werkblad als een PowerPoint‑slide te schrijven.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Resultaat:**  
`CopyWithPivot.pptx` opent in Microsoft PowerPoint (of een compatibele viewer) met één slide die het gekopieerde bereik weergeeft, inclusief een live draaitabel die in PowerPoint kan worden bewerkt.

## Volledig uitvoerbaar voorbeeld

Hieronder staat het complete programma dat je kunt plakken in een nieuw console‑project en direct kunt uitvoeren.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Verwachte output:**  
Het uitvoeren van het programma print “PowerPoint file created successfully.” en maakt een bestand genaamd `CopyWithPivot.pptx`. Het openen van het bestand in PowerPoint toont één slide waarop het gekopieerde Excel‑bereik exact verschijnt zoals in het bronwerkblad, met een actieve draaitabel die vanuit PowerPoint kan worden vernieuwd.

## Veelvoorkomende variaties en randgevallen

| Situatie | Wat te wijzigen |
|-----------|----------------|
| **Meerdere draaitabellen** | Definieer aparte `Range`‑objecten voor elke tabel en roep `CopyRange` voor elk aan, of kopieer het volledige blad als ze dezelfde gegevensbron delen. |
| **Grote datasets** | Vergroot het bereik (bijv. `"A1:Z5000"`). Overweeg `PasteOptions.CompressData = true` in te schakelen om de PPTX‑grootte te verkleinen. |
| **Verschillende slide‑lay-outs** | Na het opslaan als PPTX, open het bestand in PowerPoint en pas een aangepast layout of thema toe; de gegevens blijven bewerkbaar. |
| **Opslaan naar een stream** | Gebruik `destinationWorkbook.Save(stream, SaveFormat.Pptx)` wanneer je de PPTX via een web‑API moet retourneren. |
| **Celopmaak behouden** | Stel `PasteOptions.PasteType = PasteType.All` in om lettertypen, kleuren en randen te behouden. |

**Pro‑tip:** Controleer altijd of de doelmap bestaat voordat je `Save` aanroept. Als de map ontbreekt, gooit `Save` een `DirectoryNotFoundException`.

## Conclusie

Je weet nu hoe je PowerPoint maakt vanuit Excel, een draaitabel kopieert en het resultaat exporteert als een PPTX‑bestand met Aspose.Cells. De stappen — het laden van de bron‑werkmap, het definiëren van een bereik, kopiëren met `CopyPivotTables` en opslaan als PPTX — dekken de volledige workflow op een betrouwbare, productie‑klare manier.

Verken vervolgens **hoe je Excel naar PPTX exporteert** voor meerdere werkbladen, of leer **hoe je een bereik tussen werkmappen kopieert** wanneer je gegevens uit verschillende bronnen moet samenvoegen voordat je het slide‑deck genereert. Beide onderwerpen bouwen voort op dezelfde API‑surface en kunnen worden gecombineerd om complexe rapportage‑pijplijnen te automatiseren.

Veel plezier met coderen, en geniet van het omzetten van je spreadsheets naar gepolijste presentaties!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabel te kopiëren in C# – Excel naar PPTX converteren, bereik kopiëren & tekstvak maken](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Nieuwe werkmap maken – Hoe een werkblad met een draaitabel te kopiëren](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Hoe Excel‑bestanden te maken en op te slaan met Aspose.Cells voor .NET: Een volledige gids](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}