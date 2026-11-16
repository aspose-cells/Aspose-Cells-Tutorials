---
category: general
date: 2026-11-16
description: Leer hoe je Excel opslaat als PowerPoint en Excel programmatically naar
  PowerPoint converteert. Deze stapsgewijze gids behandelt ook het exporteren van
  Excel naar PPTX en het opslaan van een werkmap als PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: nl
lastmod: 2026-11-16
og_description: Sla Excel op als PowerPoint met Aspose.Cells. Volg deze gids om Excel
  naar PowerPoint te converteren, Excel naar PPTX te exporteren en een werkmap in
  enkele minuten als PPTX op te slaan.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Excel opslaan als PowerPoint – Complete C#‑gids
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Hoe Excel opslaan als PowerPoint met Aspose.Cells in C#
url: /nl/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel opslaan als PowerPoint met Aspose.Cells in C#

Als je programmatically **Excel als PowerPoint wilt opslaan**, biedt deze tutorial een complete, kant‑klaar oplossing. Of je nu een rapportage‑engine bouwt of een geautomatiseerde slide‑generator, de onderstaande stappen laten je een Excel-werkblad omzetten naar een bewerkbare PPTX‑slide in slechts een paar regels code.

Je leert hoe je **Excel naar PowerPoint kunt converteren**, het blad exporteert naar een PPTX‑bestand, en tekstvakken en vormen bewerkbaar houdt – alles zonder de .NET‑omgeving te verlaten.

## Vereisten

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7.2+)
* Een geldige Aspose.Cells‑licentie (de gratis proefversie werkt voor evaluatie)
* Visual Studio 2022 (of een andere C#‑IDE)
* Een Excel‑werkmap die de gegevens en vormen bevat die je wilt exporteren

## Stap 1: Installeer Aspose.Cells

Add the Aspose.Cells NuGet package to your project:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Gebruik de `-v`‑vlag om een specifieke versie te targeten, bijv. `Aspose.Cells.24.5`.

## Stap 2: Laad de werkmap die je wilt exporteren

De eerste bewerking in de **save Excel as PowerPoint**‑workflow is het laden van de bron‑werkmap.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Waarom dit belangrijk is:* Het laden van de werkmap geeft je toegang tot de werkbladen, paginainstellingen en de tekenobjecten die bewerkbare PowerPoint‑vormen worden.

## Stap 3: Configureer exportopties voor een bewerkbare PPTX‑slide

Om **Excel naar PowerPoint te converteren** terwijl je de bewerkbaarheid behoudt, moet je een paar eigenschappen instellen op `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Uitleg:*  
* `SaveFormat = SaveFormat.Pptx` vertelt Aspose.Cells om een PowerPoint‑bestand te produceren.  
* `ExportEditableText` en `ExportEditableShapes` zorgen ervoor dat de resulterende slide zich gedraagt als een native PowerPoint‑slide — je kunt op een tekstvak of vorm klikken en deze direct in PowerPoint bewerken.

## Stap 4: Definieer het exportgebied en pas het aan één slide aan

Wanneer je **Excel naar PPTX exporteert**, wil je meestal een specifiek bereik op de slide laten verschijnen. Het instellen van het printgebied en de aanpassingsopties garandeert een nette, één‑slide output.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Waarom dit belangrijk is:* De `PrintArea` beperkt de export tot cellen A1 tot en met G30, terwijl `FitToPagesTall` en `FitToPagesWide` alles comprimeren tot één slide, waardoor ongewenste extra pagina's worden voorkomen.

## Stap 5: Sla het werkblad op als een bewerkbaar PPTX‑bestand

Nu kun je eindelijk **workbook as PPTX opslaan** en het **save Excel as PowerPoint**‑proces voltooien.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Na het uitvoeren van het programma, open `EditableShapes.pptx` in Microsoft PowerPoint. Je ziet een slide die de geselecteerde Excel‑range weerspiegelt, en alle tekstvakken en vormen zijn volledig bewerkbaar.

### Verwachte output

* Een bestand genaamd `EditableShapes.pptx` in `C:\Output\`.
* Eén PowerPoint‑slide met de range A1:G30.
* Tekstvakken, grafieken en vormen die je kunt dubbelklikken en direct in PowerPoint kunt bewerken.

## Volledige broncode (klaar om te kopiëren)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Veelgestelde vragen en edge‑case handling

| Vraag | Antwoord |
|----------|--------|
| **Wat als ik meerdere werkbladen heb?** | Loop door `workbook.Worksheets` en herhaal stappen 3‑5 voor elk blad, waarbij je de bestandsnaam van de output wijzigt (bijv. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Kan ik de hele werkmap exporteren naar één PowerPoint‑deck?** | Ja. Stel `ExportAllSheets = true` in op `ImageOrPrintOptions`. Elk werkblad wordt een aparte slide. |
| **Mijn vormen verschijnen als afbeeldingen, niet als bewerkbare objecten.** | Zorg ervoor dat `ExportEditableShapes = true` is en dat je Aspose.Cells 24.5+ gebruikt (eerdere versies missen deze functie). |
| **De gegenereerde PPTX is te groot.** | Verklein het printgebied, of verlaag de beeldresolutie via `exportOptions.ImageResolution`. |
| **Heb ik een licentie nodig voor productiegebruik?** | Een betaalde licentie verwijdert het evaluatiewatermerk en ontgrendelt volledige prestaties. De gratis proefversie werkt voor testen. |

## Tips voor robuuste productiecode

* **Valideer bestands‑paden** voordat je `Workbook` of `Save` aanroept om `FileNotFoundException` te voorkomen.  
* **Plaats de export in een try/catch‑blok** om licentiefouten (`Aspose.Cells.LicenseException`) af te handelen.  
* **Dispose de werkmap** (`workbook.Dispose()`) wanneer klaar om ongebeheerste resources vrij te geven.  
* **Gebruik async I/O** (`FileStream` met `await`) als je veel grote bladen exporteert in een webservice.

## Volgende stappen

Nu je weet hoe je **Excel als PowerPoint kunt opslaan**, kun je gerelateerde onderwerpen verkennen:

* **Export Excel naar PPTX met aangepaste slide‑lay-outs** – pas `SlideSize` aan en voeg een masterslide toe.  
* **Converteer Excel‑slide naar PDF** – gebruik `SaveFormat.Pdf` voor een afdrukbare versie.  
* **Batch‑conversie van een map met werkmappen** – combineer de bovenstaande lus met `Directory.GetFiles`.  

Experimenteer met verschillende printgebieden, schaalopties en PowerPoint‑thema's om de output af te stemmen op de huisstijl van je organisatie.

---

*Veel plezier met coderen! Als deze gids je heeft geholpen **Excel naar PowerPoint te converteren**, deel hem dan gerust met teamgenoten of open een issue in de Aspose.Cells GitHub‑repository voor verdere ondersteuning.*

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel opslaan als PowerPoint met C# en Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Hoe PPTX opslaan vanuit Excel – Complete gids om Excel‑blad naar PowerPoint te exporteren](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Excel naar PowerPoint converteren – Volledige stap‑voor‑stap gids](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}