---
category: general
date: 2026-10-13
description: Lär dig hur du sparar Excel som TXT med Aspose.Cells. Denna guide täcker
  export av Excel till TXT, skriva värde till en cell och ställa in signifikanta siffror
  på bara några steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: sv
lastmod: 2026-10-13
og_description: Spara Excel som TXT med Aspose.Cells. Lär dig hur du exporterar Excel
  till TXT, skriver ett värde till en cell och anger signifikanta siffror med bara
  några rader C#‑kod.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Spara Excel som TXT – steg‑för‑steg guide för .NET‑utvecklare
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
title: Hur man sparar Excel som TXT med Aspose.Cells i C#
url: /sv/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man sparar Excel som TXT med Aspose.Cells i C#

Om du snabbt behöver **save Excel as TXT**, visar den här handledningen hela processen på under fem minuter. Du kommer att se hur du exporterar Excel till TXT, skriver värde till cell, och anger signifikanta siffror så att textfilen innehåller exakt de data du förväntar dig.

Att exportera ett kalkylblad som TXT är användbart när nedströmsystem endast accepterar ren text‑inmatning, när du behöver generera loggar, eller när du vill ha en människoläsbar dump av beräkningar. Exemplet nedan fungerar med Aspose.Cells v25.10 eller senare och körs på vilken .NET 6+‑runtime som helst.

## Förutsättningar

* En licensierad kopia av **Aspose.Cells for .NET** (gratis provversion fungerar för testning).
* .NET 6 SDK eller senare installerat.
* En IDE såsom Visual Studio 2022, VS Code eller Rider.
* Grundläggande C#‑kunskaper—ingen avancerad Excel‑automatiseringserfarenhet krävs.

Du kan installera Aspose.Cells NuGet‑paketet med:

```bash
dotnet add package Aspose.Cells
```

## Steg 1: Skapa en arbetsbok och få åtkomst till dess första arbetsblad (save excel as txt)

Det första du gör när du vill **save Excel as TXT** är att skapa ett `Workbook`‑objekt. Detta objekt representerar hela Excel‑filen i minnet.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Varför detta är viktigt:** `Workbook`‑klassen är ingångspunkten för alla kalkylbladsoperationer. Genom att börja med en ny arbetsbok undviker du eventuell dold formatering som kan påverka ren‑text‑utdata.

## Steg 2: Skriv ett högprecisionstal i en cell (write value to cell)

Nu behöver du **write value to cell** A1. Metoden `PutValue` upptäcker automatiskt datatypen och lagrar den som ett numeriskt värde.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tips:** Om du senare behöver skriva strängar, datum eller formler fungerar samma `PutValue`‑metod—skicka bara den lämpliga .NET‑typen.

## Steg 3: Konfigurera exportalternativen för att behålla endast den nödvändiga precisionen (set significant digits)

När du exporterar till en TXT‑fil vill du ofta begränsa antalet siffror för att hålla filstorleken liten eller för att matcha en nedströms specifikation. Klassen `TxtSaveOptions` tillhandahåller en egenskap `SignificantDigits` för detta ändamål.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Varför du bör ange signifikanta siffror:** Utan denna inställning skriver Aspose.Cells hela dubbelprecisionvärdet, vilket kan producera långa strängar som `12345.6789012345`. Att sätta `SignificantDigits = 6` kortar ner utdata till `12345.7`, vilket matchar de flesta rapporteringskrav.

## Steg 4: Exportera arbetsboken som en TXT‑fil (export excel to txt)

Slutligen **exporterar du Excel till TXT** genom att anropa `Workbook.Save` med de tidigare konfigurerade alternativen.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

När koden är klar innehåller `LimitedDigits.txt`:

```
12345.7
```

> **Resultatverifiering:** Öppna filen i någon textredigerare (Notepad, VS Code) för att bekräfta att endast sex signifikanta siffror finns och att inga extra kommatecken eller tab‑avgränsare visas.

## Fullt, körbart exempel

Nedan är en fristående konsolapplikation som du kan kopiera, klistra in och köra omedelbart.

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

**Förklaring av varje block**

| Block | Syfte |
|-------|-------|
| `using Aspose.Cells;` | Importerar Aspose.Cells‑namnutrymmet som krävs för `Workbook`, `Worksheet` och `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Instansierar en tom Excel‑arbetsbok i minnet. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 med ett dubbelprecisionstal. |
| `TxtSaveOptions` | Konfigurerar **set significant digits**‑beteendet för TXT‑exporten. |
| `workbook.Save(..., txtOptions);` | Utför **export excel to txt**‑operationen och skapar ren‑text‑filen. |

## Kantfall och ytterligare tips

| Scenario | Hur man hanterar det |
|----------|----------------------|
| **Large worksheets** (many rows/columns) | Använd `txtOptions.Encoding = Encoding.UTF8` om du behöver Unicode‑stöd, och överväg att strömma filen med `Workbook.Save(Stream, txtOptions)` för att undvika hög minnesanvändning. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` exponerar även `Separator`—sätt den till `','` för att producera CSV‑liknande utdata samtidigt som du använder TXT‑formatet. |
| **Preserving formulas** | Sätt `txtOptions.ExportFormulas = true` för att skriva formeltexten istället för det beräknade värdet. |
| **Locale‑specific decimal separators** | Justera `txtOptions.DecimalSeparator` till `','` för europeiska lokaler. |
| **Multiple worksheets** | Loopa igenom `workbook.Worksheets` och anropa `Save` för varje, och lägg till ett arbetsbladsnamn i filnamnet. |

## Vanliga frågor

**Q: Runder `SignificantDigits` eller trunkerar den?**  
A: Den rundar till närmaste värde baserat på det angivna antalet signifikanta siffror, vilket säkerställer att utdata är matematiskt exakt till den precisionen.

**Q: Kan jag exportera direkt till en minnesström?**  
A: Ja. Ersätt filsökvägen med en `MemoryStream`‑instans: `workbook.Save(stream, txtOptions);`. Detta är praktiskt för webb‑API:er som behöver returnera TXT‑innehållet utan att röra filsystemet.

**Q: Vad händer om jag behöver behålla originalformateringen (t.ex. datum)?**  
A: Använd `txtOptions.ExportFormattedValues = true`. Detta tvingar Aspose.Cells att skriva cellens visade text istället för det råa värdet.

## Slutsats

Du vet nu hur du **save Excel as TXT** med full kontroll över precision, formatering och utskriftsplats. Genom att följa de fyra stegen—skapa en arbetsbok, **write value to cell**, **set significant digits** och **export Excel to TXT**—kan du integrera ren‑text‑export i vilken .NET‑applikation som helst.

Nästa, utforska relaterade ämnen som **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, eller **use Aspose.Cells to generate JSON reports**. Var och en av dessa bygger på samma grundläggande koncept som demonstrerats här, och ger dig en mångsidig verktygslåda för datautbyte över plattformar.

Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker nära besläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Spara Excel som text – Komplett C#‑guide för att exportera Excel till TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Skapa ny arbetsbok och exportera Excel till TXT med precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Skapa ny arbetsbok – Exportera Excel till TXT med full precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}