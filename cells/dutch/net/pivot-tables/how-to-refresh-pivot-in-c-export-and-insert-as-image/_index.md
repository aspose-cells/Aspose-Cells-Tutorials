---
category: general
date: 2026-05-04
description: Hoe een draaitabel te vernieuwen in C# en deze als PNG te exporteren,
  vervolgens de afbeelding in een werkblad in te voegen. Volg deze stapsgewijze gids
  met volledige code.
draft: false
keywords:
- how to refresh pivot
- how to export pivot
- insert image into worksheet
- refresh pivot table code
- load excel workbook c#
language: nl
og_description: Hoe ververs je een pivot in C#? Leer hoe je de draaitabel als afbeelding
  exporteert en deze in een werkblad invoegt met volledige codevoorbeelden.
og_title: Hoe een Pivot te vernieuwen in C# – Exporteren en invoegen als afbeelding
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hoe een draaitabel te vernieuwen in C# – Exporteren en invoegen als afbeelding
url: /nl/net/pivot-tables/how-to-refresh-pivot-in-c-export-and-insert-as-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een Pivot te Vernieuwen in C# – Exporteren en Invoegen als Afbeelding

Hoe een pivot vernieuwen in C# is een veelvoorkomend obstakel wanneer je Excel‑rapporten automatiseert. In deze gids zie je precies **hoe je een pivot vernieuwt**, deze exporteert als PNG, en die afbeelding in een werkblad‑placeholder plaatst — alles met één enkel, uitvoerbaar programma.

Als je je ook afvraagt *hoe je een pivot exporteert* of je moet **een afbeelding in een werkblad invoegen**, ben je hier op het juiste adres. We lopen elke regel door, leggen uit waarom het belangrijk is, en behandelen zelfs een paar randgevallen die je in real‑world projecten kunt tegenkomen.

---

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

- **Aspose.Cells for .NET** (de bibliotheek die `Workbook`, `Worksheet`, `ImageOrPrintOptions`, enz. levert). Je kunt het via NuGet halen: `Install-Package Aspose.Cells`.
- .NET 6 of hoger (de code hieronder richt zich op .NET 6, maar elke recente versie werkt).
- Een basisbegrip van C# en bestands‑I/O — niets bijzonders.

Dat is alles. Geen extra DLL’s, geen COM‑interop, gewoon een schone C#‑console‑app.

---

## Stap 1 – Excel‑werkmap laden in C#‑stijl

Eerst moeten we het bronbestand openen. Hier komt het **load excel workbook c#**‑deel.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from disk
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Grab the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Waarom?**  
> Het laden van de werkmap geeft ons toegang tot de werkbladen, draaitabellen en afbeeldings‑placeholders. Als het bestand niet wordt gevonden, gooit Aspose een duidelijke `FileNotFoundException`, die je kunt opvangen voor een vriendelijkere UI.

---

## Stap 2 – Afbeeldingsopties voorbereiden voor het exporteren van de pivot

Nu vertellen we Aspose hoe de geëxporteerde afbeelding eruit moet zien. Dit is de kern van **how to export pivot**.

```csharp
        // Step 2: Set up image export options – PNG is lossless and widely supported
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            // Optional: tweak resolution for sharper images
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

> **Pro tip:**  
> Als je een JPEG wilt voor een kleinere bestandsgrootte, verander `SaveFormat.Png` in `SaveFormat.Jpeg` en pas `Quality` dienovereenkomstig aan.

---

## Stap 3 – Code om de draaitabel te vernieuwen

Een verouderde draaitabel toont oude gegevens. Vernieuwen zorgt ervoor dat de afbeelding de nieuwste cijfers weergeeft.

```csharp
        // Step 3: Refresh the first pivot table in the worksheet
        if (worksheet.PivotTables.Count > 0)
        {
            worksheet.PivotTables[0].Refresh();
        }
        else
        {
            Console.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }
```

> **Waarom vernieuwen?**  
> Draaitabellen cachen brongegevens wanneer ze worden aangemaakt. Als het onderliggende werkblad verandert (bijv. nieuwe rijen worden toegevoegd), wordt de cache verouderd. Het aanroepen van `Refresh()` dwingt Aspose om de bronreeks opnieuw op te vragen, zodat de geëxporteerde afbeelding niet blijft hangen met oude totalen.

---

## Stap 4 – De vernieuwde pivot omzetten naar een afbeelding

Hier is de magische regel die daadwerkelijk **export pivot** naar een byte‑array uitvoert.

```csharp
        // Step 4: Export the refreshed pivot table as an image
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

> **Wat je krijgt:**  
> `pivotImage` bevat nu een PNG‑gecodeerde afbeelding van de draaitabel, klaar om naar schijf te worden geschreven of elders in te sluiten.

---

## Stap 5 – Afbeelding in werkblad invoegen

Dit is waar we **insert image into worksheet** uitvoeren. We plaatsen de afbeelding in de eerste afbeeldings‑placeholder (als die bestaat).

```csharp
        // Step 5: Insert the image into the first picture placeholder
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            // If no placeholder exists, add a new picture at cell A1
            int pictureIndex = worksheet.Pictures.Add(0, 0, pivotImage).Index;
            Console.WriteLine($"Added new picture at index {pictureIndex}.");
        }
```

> **Waarom een placeholder gebruiken?**  
> Veel Excel‑templates worden geleverd met een vooraf opgemaakte afbeeldingsvorm (grootte, rand, positie). Door te richten op `Pictures[0]` behouden we de lay‑out. Als de template geen placeholder heeft, maakt de fallback een nieuwe afbeelding die verankerd is op cel A1.

---

## Stap 6 – Werkmap opslaan (optioneel)

Tot slot persisteren we de wijzigingen. Je kunt het origineel overschrijven of naar een nieuw bestand schrijven.

```csharp
        // Step 6: Save the updated workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **Verwacht resultaat:**  
> Open `output.xlsx` en je ziet de draaitabel vernieuwd, geëxporteerd als een scherpe PNG, en weergegeven in de eerste afbeeldings‑slot. De rest van de werkmap blijft onaangeroerd.

---

## Volledig Werkend Voorbeeld (Klaar om te Kopiëren‑Plakken)

Hieronder staat de complete code‑blok die je in een nieuw console‑project kunt plakken. Er ontbreken geen onderdelen.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);
        Worksheet worksheet = workbook.Worksheets[0];

        // Configure image export options (PNG, 300 DPI)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // Refresh the first pivot table
        if (worksheet.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found.");
            return;
        }
        worksheet.PivotTables[0].Refresh();

        // Export pivot to PNG byte array
        byte[] pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);

        // Insert the image into a picture placeholder or add a new picture
        if (worksheet.Pictures.Count > 0)
        {
            worksheet.Pictures[0].ImageBytes = pivotImage;
        }
        else
        {
            worksheet.Pictures.Add(0, 0, pivotImage);
        }

        // Save the workbook
        string outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Voer het programma uit, open het resulterende bestand, en controleer of de pivot de nieuwste gegevens weergeeft en verschijnt als een afbeelding met hoge resolutie.

---

## Veelgestelde Vragen & Randgevallen

| Vraag | Antwoord |
|----------|--------|
| **Wat als de werkmap meerdere werkbladen heeft?** | Pas `workbook.Worksheets[0]` aan naar de juiste index of naam (`workbook.Worksheets["Sheet2"]`). |
| **Kan ik meerdere draaitabellen exporteren?** | Loop door `worksheet.PivotTables` en herhaal stappen 3‑4 voor elk. Sla elke afbeelding op in een aparte placeholder of combineer ze op één blad. |
| **Wat als grote draaitabellen geheugenbelasting veroorzaken?** | Gebruik `ImageOrPrintOptions` met een lagere DPI of exporteer naar JPEG om de byte‑array‑grootte te verkleinen. |
| **Moet ik iets expliciet vrijgeven?** | Aspose‑objecten worden beheerd; een `using`‑statement is niet vereist, maar je kunt `Workbook` in een `using`‑blok plaatsen voor deterministische opruiming. |
| **Is dit compatibel met .NET Core?** | Ja. Aspose.Cells ondersteunt .NET Core, .NET 5/6 en .NET Framework. Verwijs gewoon naar het juiste NuGet‑pakket. |

---

## Tips & Best Practices

- **Padvalidatie**: Gebruik `Path.Combine` en `Environment.GetFolderPath` om hard‑gecodeerde scheidingstekens te vermijden.
- **Foutafhandeling**: Plaats de volledige `Main`‑body in een `try/catch` en log `Exception.Message` voor productiescripts.
- **Template‑ontwerp**: Plaats een transparante afbeeldingsvorm waar je de pivot‑afbeelding wilt; dit behoudt kolombreedtes en rijhoogtes.
- **Prestaties**: Als je alleen de afbeelding nodig hebt, kun je het opslaan van de werkmap overslaan en `pivotImage` direct naar een apart PNG‑bestand schrijven.

---

## Conclusie

Je weet nu **hoe je een pivot vernieuwt** in C#, die vernieuwde weergave als afbeelding exporteert, en **een afbeelding in een werkblad invoegt** zonder problemen. De volledige oplossing — werkmap laden, exportopties instellen, pivot vernieuwen, omzetten naar PNG, en bestand opslaan — dekt de volledige workflow die je zocht.

Klaar voor de volgende uitdaging? Probeer **how to export pivot** te combineren met batchverwerking van meerdere bestanden, of verken de **refresh pivot table code** voor dynamische gegevensbronnen zoals databases of CSV‑feeds. Hetzelfde patroon geldt: laden, vernieuwen, exporteren, invoegen, opslaan.

Veel programmeerplezier, en moge je Excel‑automatiseringen fris en afbeelding‑perfect blijven!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}