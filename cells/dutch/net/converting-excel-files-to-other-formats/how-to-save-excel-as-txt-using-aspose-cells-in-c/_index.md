---
category: general
date: 2026-10-13
description: Leer hoe u Excel als TXT kunt opslaan met Aspose.Cells. Deze gids behandelt
  het exporteren van Excel naar TXT, het schrijven van een waarde naar een cel en
  het instellen van significante cijfers in slechts een paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: nl
lastmod: 2026-10-13
og_description: Sla Excel op als TXT met Aspose.Cells. Leer hoe je Excel naar TXT
  exporteert, een waarde naar een cel schrijft en het aantal significante cijfers
  instelt in slechts een paar regels C#‑code.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Excel opslaan als TXT – stapsgewijze handleiding voor .NET‑ontwikkelaars
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Hoe Excel als TXT opslaan met Aspose.Cells in C#
url: /nl/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe Excel opslaan als TXT met Aspose.Cells in C#

Als je snel **Excel als TXT wilt opslaan**, laat deze tutorial het volledige proces zien in minder dan vijf minuten. Je ziet hoe je Excel naar TXT exporteert, een waarde in een cel schrijft en significante cijfers instelt zodat het tekstbestand precies de gegevens bevat die je verwacht.

Een spreadsheet exporteren als TXT is handig wanneer downstream‑systemen alleen platte‑tekst invoer accepteren, wanneer je logbestanden moet genereren, of wanneer je een mens‑leesbare dump van berekeningen wilt. Het voorbeeld hieronder werkt met Aspose.Cells v25.10 of later en draait op elke .NET 6+ runtime.

## Prerequisites

Voordat je begint, zorg dat je het volgende hebt:

* Een gelicentieerde kopie van **Aspose.Cells for .NET** (de gratis proefversie werkt voor testen).
* .NET 6 SDK of later geïnstalleerd.
* Een IDE zoals Visual Studio 2022, VS Code, of Rider.
* Basiskennis van C# — geen geavanceerde Excel‑automatiseringservaring vereist.

Je kunt het Aspose.Cells NuGet‑pakket installeren met:

```bash
dotnet add package Aspose.Cells
```

## Stap 1: Maak een werkmap en krijg toegang tot het eerste werkblad (save excel as txt)

Het eerste wat je doet wanneer je **Excel als TXT wilt opslaan** is een `Workbook`‑object aanmaken. Dit object vertegenwoordigt het volledige Excel‑bestand in het geheugen.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Waarom dit belangrijk is:** De `Workbook`‑klasse is het toegangspunt voor alle spreadsheet‑bewerkingen. Door met een lege werkmap te beginnen, vermijd je verborgen opmaak die de platte‑tekstuitvoer zou kunnen beïnvloeden.

## Stap 2: Schrijf een hoog‑precisie getal in een cel (write value to cell)

Nu moet je **write value to cell** A1. De `PutValue`‑methode detecteert automatisch het gegevenstype en slaat het op als een numerieke waarde.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** Als je later strings, datums of formules moet schrijven, werkt dezelfde `PutValue`‑methode — geef gewoon het juiste .NET‑type door.

## Stap 3: Configureer de exportopties om alleen de benodigde precisie te behouden (set significant digits)

Bij het exporteren naar een TXT‑bestand wil je vaak het aantal cijfers beperken om de bestandsgrootte klein te houden of om te voldoen aan een downstream‑specificatie. De `TxtSaveOptions`‑klasse biedt een `SignificantDigits`‑eigenschap voor dit doel.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Waarom je significante cijfers moet instellen:** Zonder deze instelling schrijft Aspose.Cells de volledige double‑precisie waarde, wat lange strings kan opleveren zoals `12345.6789012345`. Het instellen van `SignificantDigits = 6` verkort de uitvoer tot `12345.7`, wat aan de meeste rapportage‑eisen voldoet.

## Stap 4: Exporteer de werkmap als een TXT‑bestand (export excel to txt)

Tot slot **exporteer je Excel naar TXT** door `Workbook.Save` aan te roepen met de eerder geconfigureerde opties.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

Wanneer de code klaar is, bevat `LimitedDigits.txt`:

```
12345.7
```

> **Resultaatverificatie:** Open het bestand in een willekeurige teksteditor (Notepad, VS Code) om te bevestigen dat er precies zes significante cijfers aanwezig zijn en dat er geen extra komma’s of tab‑scheidingstekens verschijnen.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat een zelfstandige console‑applicatie die je kunt kopiëren, plakken en direct kunt uitvoeren.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Uitleg van elk blok**

| Blok | Doel |
|------|------|
| `using Aspose.Cells;` | Importeert de Aspose.Cells‑namespace die nodig is voor `Workbook`, `Worksheet` en `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Instantieert een lege Excel‑werkmap in het geheugen. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 met een double‑precisie getal. |
| `TxtSaveOptions` | Configureert **set significant digits** gedrag voor de TXT‑export. |
| `workbook.Save(..., txtOptions);` | Voert de **export excel to txt**‑operatie uit en maakt het platte‑tekstbestand aan. |

## Randgevallen en extra tips

| Scenario | Hoe te handelen |
|----------|-----------------|
| **Grote werkbladen** (veel rijen/kolommen) | Gebruik `txtOptions.Encoding = Encoding.UTF8` als je Unicode‑ondersteuning nodig hebt, en overweeg het bestand te streamen met `Workbook.Save(Stream, txtOptions)` om hoog geheugenverbruik te vermijden. |
| **Aangepaste scheidingstekens** (komma‑gescheiden waarden) | `TxtSaveOptions` biedt ook `Separator` — stel deze in op `','` om CSV‑achtige uitvoer te produceren terwijl je toch het TXT‑formaat gebruikt. |
| **Formules behouden** | Stel `txtOptions.ExportFormulas = true` in om de formule‑tekst te schrijven in plaats van de berekende waarde. |
| **Locale‑specifieke decimale scheidingstekens** | Pas `txtOptions.DecimalSeparator` aan naar `','` voor Europese locales. |
| **Meerdere werkbladen** | Loop door `workbook.Worksheets` en roep `Save` aan voor elk, waarbij je de werkbladnaam aan de bestandsnaam toevoegt. |

## Veelgestelde vragen

**Q: Rondt `SignificantDigits` af of wordt het afgekapt?**  
A: Het rondt af naar de dichtstbijzijnde waarde op basis van het opgegeven aantal significante cijfers, waardoor de uitvoer wiskundig nauwkeurig is tot die precisie.

**Q: Kan ik direct naar een memory stream exporteren?**  
A: Ja. Vervang het bestandspad door een `MemoryStream`‑instantie: `workbook.Save(stream, txtOptions);`. Dit is handig voor web‑API’s die de TXT‑inhoud moeten retourneren zonder het bestandssysteem aan te raken.

**Q: Wat als ik de oorspronkelijke opmaak (bijv. datums) wil behouden?**  
A: Gebruik `txtOptions.ExportFormattedValues = true`. Hiermee dwingt je Aspose.Cells om de weergegeven tekst van de cel te schrijven in plaats van de ruwe waarde.

## Conclusie

Je weet nu hoe je **Excel als TXT kunt opslaan** met volledige controle over precisie, opmaak en uitvoerlocatie. Door de vier stappen te volgen — een werkmap maken, **write value to cell**, **set significant digits**, en **export Excel to TXT** — kun je platte‑tekst‑export integreren in elke .NET‑applicatie.

Verken vervolgens gerelateerde onderwerpen zoals **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, of **use Aspose.Cells to generate JSON reports**. Elk van deze bouwt voort op dezelfde kernconcepten die hier worden getoond, waardoor je een veelzijdige toolkit krijgt voor gegevensuitwisseling tussen platformen.

Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}