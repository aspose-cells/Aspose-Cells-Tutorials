---
category: general
date: 2026-03-22
description: Stel het afdrukgebied in Excel in en converteer Excel naar PowerPoint
  met bewerkbare vormen. Leer hoe je de titelrij kunt herhalen, PowerPoint vanuit
  Excel kunt maken en Excel kunt exporteren naar pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: nl
og_description: Stel het afdrukgebied in Excel in en zet het om naar een PowerPoint-dia
  met bewerkbare vormen. Volg deze volledige gids om de titelrij te herhalen en Excel
  naar pptx te exporteren.
og_title: Afdrukgebied instellen in Excel – Exporteren naar PowerPoint tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Printgebied instellen in Excel en exporteren naar PowerPoint – Stapsgewijze
  handleiding
url: /nl/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stel afdrukgebied in Excel in en exporteer naar PowerPoint – Complete programmeertutorial

Heb je ooit moeten **set print area** in een Excel-werkblad en vervolgens dat deel omzetten naar een PowerPoint-dia? Je bent niet de enige. In veel rapportage‑pipelines moet dezelfde data die mooi afgedrukt wordt, ook in een presentatie verschijnen, vaak met de eerste rij herhaald als titel. Het goede nieuws? Met een paar regels C# kun je **convert excel to powerpoint**, alle tekstvakken bewerkbaar houden, en zelfs **repeat title row** automatisch.

In deze gids lopen we alles door wat je moet weten: van het configureren van het afdrukgebied tot het maken van een PPTX‑bestand dat je direct in PowerPoint kunt bewerken. Aan het einde kun je **create powerpoint from excel** uitvoeren, het resultaat exporteren als **export excel to pptx**, en dezelfde code hergebruiken in elk .NET‑project. Geen magie, alleen duidelijke stappen en een volledig uitvoerbaar voorbeeld.

## Wat je nodig hebt

- **.NET 6.0** of later (de API werkt ook met .NET Framework)
- **Aspose.Cells for .NET** (de bibliotheek die `Workbook`, `ImageOrPrintOptions`, enz. levert)
- Een eenvoudige C#‑IDE (Visual Studio, Rider, of VS Code met de C#‑extensie)
- Een Excel‑bestand (`input.xlsx`) dat de gegevens bevat die je wilt exporteren

Dat is alles—geen extra NuGet‑pakketten naast Aspose.Cells. Als je de bibliotheek nog niet hebt toegevoegd, voer dan uit:

```bash
dotnet add package Aspose.Cells
```

Nu zijn we klaar om te beginnen.

## Stap 1: Laad de werkmap – het startpunt voor export

Het eerste wat je moet doen is de werkmap laden die het blad bevat dat je wilt omzetten naar een dia. Beschouw de werkmap als het bron‑document; zonder deze is niets anders van belang.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Waarom dit belangrijk is:** Het laden van de werkmap geeft je toegang tot de werkbladcollectie, pagina‑instellingen en de exportengine. Als je deze stap overslaat kun je het **print area** niet instellen of rijen herhalen.

> **Pro tip:** Gebruik een absoluut pad tijdens het testen, schakel daarna over naar een relatief pad of een configuratie‑gebaseerd pad voor productie.

## Stap 2: Configureer exportopties – houd tekstvakken en vormen bewerkbaar

Wanneer je exporteert naar PowerPoint wil je waarschijnlijk dat de resulterende dia bewerkbaar is. Aspose.Cells laat je dat regelen met `ImageOrPrintOptions`. Door `ExportTextBoxes` en `ExportShapeObjects` op `true` te zetten, vertel je de bibliotheek die objecten te behouden als native PowerPoint‑elementen in plaats van ze te rasteren tot een afbeelding.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Waarom dit belangrijk is:** Als je ooit **convert excel to powerpoint** moest uitvoeren en vervolgens de dia handmatig wilt aanpassen, bespaart deze instelling je het opnieuw maken van tekstvakken vanaf nul. Het zorgt er ook voor dat vormen (zoals pijlen of grafieken) als vectorobjecten blijven die je kunt schalen.

## Stap 3: Stel afdrukgebied in en herhaal de titelrij

Nu komen we bij het hart van de tutorial: **set print area** en de eerste rij laten herhalen op elke afgedrukte pagina (of, in ons geval, op de geëxporteerde dia). Het afdrukgebied vertelt Excel welke cellen moeten worden beschouwd voor afdrukken — of exporteren in ons scenario.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Waarom dit belangrijk is:** Door de export te beperken tot `A1:G20` vermijd je het ophalen van enorme lege bereiken, wat de conversie versnelt en de dia overzichtelijk houdt. De regel `PrintTitleRows` laat de eerste rij fungeren als koptekst — precies wat je wilt wanneer je **repeat title row** in een presentatie.

> **Randgeval:** Als je gegevens beginnen op rij 2, pas dan het bereik dienovereenkomstig aan (bijv. `PrintTitleRows = "$2:$2"`).

## Stap 4: Sla het werkblad op als PowerPoint‑bestand

Ten slotte schrijven we de dia naar schijf. De `Save`‑methode neemt de doel‑bestandsnaam en de opties die we eerder hebben geconfigureerd. Het resultaat is een PPTX‑bestand met bewerkbare tekstvakken en vormen, klaar om te openen in PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Wat je zult zien:** Open `SheetWithEditableShapes.pptx` in PowerPoint. De eerste rij verschijnt als titel, alle cellen van `A1:G20` worden weergegeven, en alle vormen die je in Excel hebt toegevoegd zijn nog steeds verplaatsbaar en bewerkbaar. Geen gerasterde afbeeldingen — alleen native PowerPoint‑objecten.

## Volledig werkend voorbeeld – alle stappen gecombineerd

Hieronder staat het volledige, kant‑klaar te kopiëren programma. Voer het uit als een console‑applicatie of embed het in een grotere oplossing.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Verwachte output:** Na het uitvoeren van het programma print de console het succesbericht, en verschijnt het PPTX‑bestand op de opgegeven locatie. Het openen van het bestand toont één dia met het geselecteerde bereik, bewerkbare tekstvakken en eventuele oorspronkelijke vormen.

## Veelgestelde vragen & valkuilen

| Vraag | Antwoord |
|----------|--------|
| **Werkt dit met meerdere werkbladen?** | Ja. Loop door `workbook.Worksheets` en herhaal dezelfde stappen voor elk blad, waarbij je elke keer de output‑bestandsnaam wijzigt. |
| **Wat als ik meer dan één dia moet exporteren?** | Roep `workbook.Save` meerdere keren aan met verschillende `ImageOrPrintOptions`‑objecten, elk geconfigureerd met een andere `PageSetup` indien nodig. |
| **Kan ik de dia‑grootte aanpassen?** | Gebruik `exportOptions.ImageFormat` om de DPI in te stellen, of pas `sheet.PageSetup.PaperSize` aan vóór het opslaan. |
| **Is Aspose.Cells gratis?** | Het biedt een gratis evaluatie met watermerken. Voor productie is een licentie vereist. |
| **Wat betreft Excel‑formules?** | De geëxporteerde waarden zijn de **berekende resultaten** op het moment van export. Als je live‑formules in PowerPoint nodig hebt, heb je een andere aanpak nodig. |

## Tips voor een soepele workflow

- **Pro tip:** Stel `Workbook.Settings.CalcMode = CalculationModeType.Automatic` in vóór export om te garanderen dat alle formules up‑to‑date zijn.
- **Let op:** Zeer grote bereiken kunnen geheugenbelasting veroorzaken. Snijd het afdrukgebied bij tot het kleinste noodzakelijke bereik.
- **Performance tip:** Hergebruik één `ImageOrPrintOptions`‑instantie als je veel bladen exporteert; elke keer een nieuwe maken voegt overhead toe.
- **Versie‑opmerking:** De bovenstaande code richt zich op Aspose.Cells 23.10 (uitgebracht november 2023). Latere versies behouden dezelfde API, maar controleer altijd de release‑notes op breaking changes.

## Conclusie

We hebben behandeld hoe je **set print area** in een Excel‑werkblad instelt, de eerste rij als titel herhaalt, en vervolgens **export excel to pptx** uitvoert terwijl bewerkbare tekstvakken en vormen behouden blijven. Kortom, je kent nu een betrouwbare manier om **convert excel to powerpoint**, **repeat title row**, en **create powerpoint from excel** te doen met slechts een paar regels C#.

Klaar voor de volgende stap? Probeer een batch‑conversie van tientallen rapporten te automatiseren, of voeg aangepaste dia‑lay-outs toe met de PowerPoint‑SDK na de export. De mogelijkheden zijn eindeloos — experimenteer, breek dingen, en geniet van de kracht van programmatische documentgeneratie.

Als je deze tutorial nuttig vond, deel hem, laat een reactie achter met je eigen aanpassingen, of bekijk onze andere gidsen over **export excel to pptx** en gerelateerde automatiseringsthema's. Veel plezier met coderen!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}