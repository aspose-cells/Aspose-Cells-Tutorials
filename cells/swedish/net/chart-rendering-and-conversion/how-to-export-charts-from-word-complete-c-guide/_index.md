---
category: general
date: 2026-03-25
description: Hur man exporterar diagram från Word med Aspose.Words C# – lär dig hur
  du inkluderar diagram och exporterar diagram från Word på några minuter.
draft: false
keywords:
- how to export charts
- how to include charts
- export charts from word
- Aspose.Words export
- C# document automation
language: sv
og_description: Hur man exporterar diagram från Word med Aspose.Words C#. Den här
  guiden visar hur du inkluderar diagram och snabbt exporterar diagram från Word.
og_title: Hur man exporterar diagram från Word – Komplett C#‑guide
tags:
- C#
- Aspose.Words
- Word Automation
- Charts
title: Hur man exporterar diagram från Word – Komplett C#‑guide
url: /sv/net/chart-rendering-and-conversion/how-to-export-charts-from-word-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man exporterar diagram från Word – Komplett C#‑guide

Har du någonsin behövt **how to export charts** från ett Word‑dokument men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på detta problem när de automatiserar rapporter. I den här tutorialen går vi igenom en praktisk, end‑to‑end‑lösning som inte bara visar dig **how to export charts**, utan också förklarar **how to include charts** i den exporterade filen. I slutet kommer du att kunna exportera diagram från Word med bara några rader C#.

Vi kommer att använda det populära **Aspose.Words for .NET**‑biblioteket eftersom det hanterar diagramobjekt nativt och fungerar med .docx, .doc och även äldre format. Ingen krångel med Office Interop, inga COM‑mardrömmar. Stegen nedan förutsätter att du har ett grundläggande C#‑projekt och att Aspose.Words‑NuGet‑paketet är installerat. Om du är ny på biblioteket, oroa dig inte—vi går snabbt igenom förutsättningarna.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+)
- Visual Studio 2022 eller någon IDE du föredrar
- Aspose.Words for .NET (installera via `dotnet add package Aspose.Words`)

> **Pro tip:** Håll din Aspose.Words‑version uppdaterad; den senaste utgåvan (från mars 2026) ger bättre diagramhantering och prestandaförbättringar.

## Steg 1: Läs in källdokumentet i Word

Det första du behöver göra är att öppna `.docx`‑filen som innehåller diagrammen du vill extrahera. Aspose.Words gör detta till en enradare.

```csharp
using Aspose.Words;

// Load the source document (replace with your actual path)
Document document = new Document(@"C:\Docs\input.docx");
```

*Varför detta är viktigt:* Att läsa in dokumentet skapar en minnesrepresentation av varje element—paragrafer, tabeller och, avgörande, diagramobjekten. Utan detta steg kan du inte komma åt eller manipulera diagrammen.

## Steg 2: Konfigurera sparalternativ för att bevara diagram

Som standard kommer ett enkelt `document.Save("output.docx")` att behålla allt, men om du någonsin ändrar `ExportImages` eller liknande flaggor kan du förlora inbäddade diagram. För att vara tydlig—och för att svara på “**how to include charts**”-delen av frågan—sätter vi `DocxSaveOptions` med `ExportCharts = true`.

```csharp
// Create save options that ensure charts are included
DocxSaveOptions saveOptions = new DocxSaveOptions
{
    ExportCharts = true          // Guarantees charts are part of the saved file
};
```

*Förklaring:* `ExportCharts` instruerar motorn att serialisera varje diagram som en inbyggd Office Open XML‑diagramdel. Detta är avgörande när du senare öppnar filen i Word eller andra redigerare; diagrammen visas exakt som de gjorde i källdokumentet.

## Steg 3: Spara dokumentet med de konfigurerade alternativen

Nu skriver vi dokumentet tillbaka till disk, med de alternativ vi just definierade. Utdatafilen kommer att innehålla allt ursprungligt innehåll **och** diagrammen.

```csharp
// Save the document with charts preserved
document.Save(@"C:\Docs\charts.docx", saveOptions);
```

Vid detta tillfälle har du en ny Word‑fil (`charts.docx`) som är en trogen kopia av originalet, komplett med alla diagramgrafiker. Öppna den i Microsoft Word för att verifiera—dina diagram bör vara fullt funktionella, redigerbara och se exakt likadana ut som tidigare.

## Fullt fungerande exempel

Nedan är det kompletta, färdiga programmet. Kopiera det till en konsolapp, justera sökvägarna och tryck **F5**.

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Saving;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the source document containing charts
            string inputPath = @"C:\Docs\input.docx";
            Document document = new Document(inputPath);
            Console.WriteLine($"Loaded document: {inputPath}");

            // 2️⃣ Set save options to explicitly include charts
            DocxSaveOptions saveOptions = new DocxSaveOptions
            {
                ExportCharts = true   // This ensures charts are not stripped out
            };
            Console.WriteLine("Configured DocxSaveOptions to export charts.");

            // 3️⃣ Save the new file
            string outputPath = @"C:\Docs\charts.docx";
            document.Save(outputPath, saveOptions);
            Console.WriteLine($"Document saved with charts at: {outputPath}");

            // Verification hint
            Console.WriteLine("Open the output file in Word to confirm charts are present.");
        }
    }
}
```

**Förväntat resultat:** När du öppnar `charts.docx` i Microsoft Word visas varje diagram från `input.docx` oförändrat. Inga saknade bilder, inga brutna referenser.

## Hantera vanliga kantfall

| Situation | Vad man bör vara uppmärksam på | Rekommenderad åtgärd |
|-----------|-------------------------------|----------------------|
| **Dokumentet innehåller inbäddade Excel‑arbetsblad** | Diagram kan vara länkade till extern Excel‑data. | Använd `DocxSaveOptions.ExportEmbeddedExcelData = true` (tillgängligt i nyare versioner) för att behålla data intakt. |
| **Stora dokument (> 100 MB)** | Minnesanvändning skjuter i höjden under inläsning. | Aktivera `LoadOptions.LoadFormat = LoadFormat.Docx` och överväg streaming med `DocumentBuilder` för inkrementell bearbetning. |
| **Du behöver bara specifika diagram** | Att exportera hela filen är överdrivet. | Iterera `document.GetChildNodes(NodeType.Shape, true)` och filtrera på `Shape.IsChart`. Klona sedan dessa former till ett nytt `Document` innan du sparar. |
| **Målet är PDF** | Diagram kan renderas annorlunda. | Använd `PdfSaveOptions` med `ExportCharts = true` (flaggan fungerar även för PDF). |

Dessa variationer svarar på frågan “**export charts from word**” i olika sammanhang, så att du är täckt oavsett om du sparar tillbaka till DOCX eller konverterar till ett annat format.

## Vanliga frågor

**Q: Fungerar detta med äldre `.doc`‑filer?**  
A: Ja. Aspose.Words konverterar automatiskt det äldre binära formatet till den moderna Open XML‑strukturen i minnet, så `ExportCharts` gäller fortfarande.

**Q: Vad händer om jag bara vill exportera diagrambilderna, inte hela dokumentet?**  
A: Du kan extrahera varje diagram som en bild med `ChartRenderer`. Exempel: `chartRenderer.Save("chart.png", ImageFormat.Png);` Detta uppfyller ett snävare “how to export charts”-behov.

**Q: Finns det några licensfrågor?**  
A: Aspose.Words är ett kommersiellt bibliotek. För utvärdering kan du använda en tillfällig licens; för produktion behöver du en riktig licens för att undvika utvärderingsvattentecknet.

## Visuell översikt

Nedan är ett snabbt schema över flödet—lägg märke till det primära nyckelordet i alt‑texten.

![Exempel på hur man exporterar diagram – diagram som visar steg: läs in → konfigurera → spara](https://example.com/images/export-charts-diagram.png)

*Alt text:* **how to export charts-diagram som illustrerar laddning, konfiguration och sparsteg**

## Sammanfattning

Vi har precis gått igenom **how to export charts** från ett Word‑dokument med Aspose.Words, demonstrerat **how to include charts** vid sparning, och berört flera scenarier för **export charts from word** i olika format. Det trestegs‑mönstret—läs in, konfigurera, spara—är enkelt, pålitligt och skalar från små rapporter till massiva företagsdokument.

Vad blir nästa steg? Prova att extrahera endast utvalda diagram, konvertera dem till PNG för webbbruk, eller automatisera en batch‑process som går igenom en mapp med Word‑filer och exporterar deras diagram i ett svep. Varje av dessa utökningar bygger på den grundläggande tekniken du just har lärt dig.

Känn dig fri att lämna en kommentar om du stöter på problem, eller dela hur du har anpassat detta mönster för dina egna projekt. Lycka till med kodandet, och må dina diagram alltid renderas perfekt!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}