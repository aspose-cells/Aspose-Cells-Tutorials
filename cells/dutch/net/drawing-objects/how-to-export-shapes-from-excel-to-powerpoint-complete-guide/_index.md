---
category: general
date: 2026-07-26
description: Hoe je vormen van een Excel‑werkblad naar PowerPoint exporteert in slechts
  een paar stappen – een snelle Excel‑naar‑PPTX exporttutorial voor ontwikkelaars.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: nl
lastmod: 2026-07-26
og_description: Hoe je stap voor stap vormen exporteert van Excel naar PowerPoint.
  Volg deze tutorial over het exporteren van Excel naar PPTX en zie hoe je werkbladen
  veranderen in bewerkbare dia's.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Hoe vormen van Excel naar PowerPoint exporteren – Snel en eenvoudig
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Hoe vormen exporteren van Excel naar PowerPoint – Complete gids
url: /nl/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe shapes vanuit Excel naar PowerPoint exporteren – Complete gids

Heb je je ooit afgevraagd **hoe je shapes** vanuit een Excel‑bestand kunt exporteren en bewerkbaar houdt in een PowerPoint‑presentatie? Je bent niet de enige. Of je nu een rapportage‑pipeline bouwt of gewoon snel een spreadsheet naar een presentatie wilt omzetten, de mogelijkheid om **worksheet to PowerPoint te converteren** zonder de bewerkbaarheid van shapes te verliezen, kan je uren handmatig werk besparen.

In deze **excel to powerpoint tutorial** lopen we een volledig werkend C#‑voorbeeld door dat een werkmap laadt, de juiste exportopties configureert en een PPTX‑bestand schrijft waarin tekstvakken en andere tekenobjecten bewerkbaar blijven. Geen vage verwijzingen—alleen de code die je kunt kopiëren, plakken en vandaag nog uitvoeren.

## Wat je zult leren

- De exacte stappen om **export excel to pptx** uit te voeren terwijl de bewerkbaarheid van shapes behouden blijft.  
- Hoe de `Aspose.Cells`‑bibliotheek’s `PptxSaveOptions` het exportgedrag regelen.  
- Tips voor het verwerken van meerdere werkbladen, ontbrekende bestanden en aangepaste shape‑instellingen.  
- Een compleet, uitvoerbaar programma dat je in elk .NET‑project kunt plaatsen.

### Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7+).  
- Een geldige licentie voor **Aspose.Cells for .NET** (de gratis proefversie werkt voor testen).  
- Een Excel‑werkmap (bijv. `ShapesDemo.xlsx`) die minstens één tekstvak of shape bevat.  
- Een ontwikkelomgeving—Visual Studio, Rider, of VS Code volstaat.

Als je die hebt, laten we beginnen.

## Stap 1: Werkmap laden – Het startpunt voor hoe je shapes exporteert  

Eerst moeten we het Excel‑bestand openen dat de shapes bevat die we bewerkbaar willen houden.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Waarom dit belangrijk is:**  
Het `Workbook`‑object is de toegangspoort tot elke cel, grafiek en tekenobject in het bestand. Door het eerste werkblad (`Worksheets[0]`) te pakken, zorgen we dat we met een bekend blad werken, maar je kunt de index vervangen door een naam (`workbook.Worksheets["Sheet2"]`) als je een specifiek tabblad nodig hebt.

> **Pro tip:** Plaats de laad‑aanroep in een `try / catch`‑blok om een vriendelijke foutmelding te geven als het bestandspad onjuist is.

## Stap 2: PPTX‑exportopties configureren – De kern van hoe je shapes exporteert  

Nu vertellen we Aspose.Cells om shapes bewerkbaar te houden in de resulterende PPTX.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Waarom deze vlaggen?**  
- `ExportEditableTextBoxes` zet Excel‑tekstvakken om in PowerPoint‑tekst‑placeholders die je kunt dubbelklikken en bewerken.  
- `ExportEditableShapes` doet hetzelfde voor shapes zoals pijlen, rechthoeken en SmartArt. Zonder deze worden de objecten statische afbeeldingen, waardoor het doel van een **convert worksheet to powerpoint**‑workflow teniet wordt gedaan.

Je kunt `PptxSaveOptions` ook aanpassen om de dia‑grootte, het thema of het al dan niet insluiten van lettertypen te regelen—handig wanneer je presentatie moet overeenkomen met de huisstijl van het bedrijf.

## Stap 3: Werkblad opslaan als PPTX – Het laatste onderdeel van Export Excel Workbook PowerPoint  

Met de opties ingesteld is opslaan eenvoudig.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Wat er onder de motorkap gebeurt:**  
Aspose.Cells doorloopt elk tekenobject op het blad, mappt het naar de corresponderende PowerPoint‑shape‑klasse en schrijft de XML die PowerPoint leest. Omdat we de bewerkbare vlaggen hebben ingeschakeld, markeert de XML elke shape als een `Shape` in plaats van een `Picture`, zodat PowerPoint het als een live‑object behandelt.

## Stap 4: Export bevestigen – Snelle feedback voor de gebruiker  

Een klein console‑bericht laat je weten dat het proces geslaagd is.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Als je het programma uitvoert en het bericht ziet, open dan `ShapesEditable.pptx` in PowerPoint. Klik op een tekstvak—je zou de tekst direct moeten kunnen bewerken, en het slepen van een shape moet het verplaatsen net als een native PowerPoint‑object.

## Stap 5: Real‑world scenario’s afhandelen  

Hieronder staan veelvoorkomende variaties die je kunt tegenkomen tijdens het werken aan een **excel to powerpoint tutorial**.

### Meerdere werkbladen

Als je meerdere bladen naar één PPTX wilt exporteren, loop dan door `workbook.Worksheets` en roep `worksheet.Save` aan met dezelfde `pptxOptions`. Aspose.Cells voegt automatisch een nieuwe dia toe voor elk blad.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Aangepaste dia‑lay-outs

Je kunt `pptxOptions.SlideSize` (bijv. `SlideSizeType.Widescreen`) opgeven om de afmetingen van je corporate deck te matchen.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### Ontbrekende bestanden of permissies

Plaats de volledige `Main`‑methode in een `try`‑blok:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Dit maakt het **export excel workbook powerpoint**‑proces robuust voor productie‑pipelines.

## Volledig werkend voorbeeld

Hier is het volledige programma dat je direct kunt compileren. Sla het op als `ExportEditableShapes.cs`, pas de bestandspaden aan, en voer `dotnet run` uit.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Verwachte output** wanneer je het programma uitvoert:

```
Exported worksheet with editable shapes.
```

Open de gegenereerde `ShapesEditable.pptx` en je ziet elke Excel‑shape als een volledig bewerkbaar PowerPoint‑object—precies wat je zocht toen je **how to export shapes** opzocht.

## Veelgestelde vragen

- **Werkt dit met oudere Excel‑formaten (.xls)?**  
  Ja. `Workbook` kan `.xls`, `.xlsx` en zelfs CSV‑bestanden openen. De shape‑export werkt op dezelfde manier.

- **Wat als ik grafieken bewerkbaar wil houden?**  
  Grafieken worden al geëxporteerd als native PowerPoint‑grafieken; je hebt geen extra vlaggen nodig.

- **Kan ik exporteren naar PDF in plaats van PPTX?**  
  Zeker—vervang gewoon `SaveFormat.Pptx` door `SaveFormat.Pdf` en laat de `PptxSaveOptions` weg.

## Conclusie

Je hebt nu een solide, end‑to‑end antwoord op **how to export shapes** vanuit Excel naar een bewerkbare PowerPoint‑deck. Door gebruik te maken van `Aspose.Cells`’ `PptxSaveOptions` behoud je elk tekstvak en tekenobject, waardoor een statische spreadsheet wordt omgevormd tot een dynamische presentatie met minimale inspanning.

Klaar voor de volgende uitdaging? Probeer aangepaste slide‑masters toe te voegen, afbeeldingen programmatisch in te voegen, of deze export te koppelen aan een CI/CD‑pipeline die automatisch wekelijks verkoop‑decks genereert. De **export excel workbook powerpoint**‑wereld staat open—ga op ontdekking!

--- 

*Als je deze **excel to powerpoint tutorial** nuttig vond, geef hem een ster op GitHub of deel hem met een collega die nog steeds spreadsheets naar dia’s kopieert‑plakt. Veel plezier met coderen!*

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een Excel‑werkblad exporteren naar PNG met Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Hoe Excel‑cellen exporteren als afbeeldingen met Aspose.Cells voor Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [Hoe Excel‑grafieken exporteren als SVG met Aspose.Cells Java voor schaalbare vectorafbeeldingen](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}