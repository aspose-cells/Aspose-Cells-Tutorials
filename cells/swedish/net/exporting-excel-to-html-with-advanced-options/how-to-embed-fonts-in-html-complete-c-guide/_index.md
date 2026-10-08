---
category: general
date: 2026-01-14
description: Hur man bäddar in typsnitt i HTML och tvingar formelberäkning vid konvertering
  av Excel till HTML. Lär dig att ange utskriftsområde och exportera diagram.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: sv
og_description: Hur man bäddar in typsnitt i HTML, tvingar formelberäkning och konverterar
  Excel till HTML med utskriftsområdesinställningar—allt i C#.
og_title: Hur man bäddar in teckensnitt i HTML – Komplett C#‑guide
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hur man bäddar in teckensnitt i HTML – Komplett C#‑guide
url: /sv/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man bäddar in typsnitt i HTML – Komplett C#‑guide

Har du någonsin funderat **hur man bäddar in typsnitt i HTML** när du exporterar en Excel‑arbetsbok? Du är inte ensam. Många utvecklare stöter på problem när den genererade HTML‑filen ser bra ut på deras maskin men förlorar sin typografi på en annan enhet. Den goda nyheten? Med Aspose.Cells för .NET kan du bädda in de exakta typsnittsfilerna direkt i HTML‑utdata—inga saknade tecken längre.

I den här handledningen går vi igenom ett full‑stack‑exempel som inte bara visar **hur man bäddar in typsnitt i HTML**, utan också demonstrerar **force formula calculation**, **convert Excel to HTML** och till och med **how to set print area** innan ett diagram exporteras till en redigerbar PPTX. I slutet har du ett enda körbart C#‑program som du kan slänga in i vilket .NET‑projekt som helst.

---

## Vad du kommer att bygga

- Skapa en ny arbetsbok, skriv ett par array‑formler och **force formula calculation** så att resultaten lagras i filen.
- Spara arbetsboken som HTML samtidigt som du **embeds fonts** och deras variation selectors.
- Ladda en andra arbetsbok som innehåller ett diagram, definiera ett **print area** och exportera det bladet till en redigerbar PowerPoint‑presentation.
- Allt detta med bara några få rader ren, välkommenterad C#‑kod.

Inga externa verktyg, ingen manuell kopiering‑och‑klistring av typsnittsfiler—Aspose.Cells sköter det tunga lyftet åt dig.

---

## Förutsättningar

| Krav | Orsak |
|------|-------|
| .NET 6.0 eller senare | Moderna språkfunktioner och bättre prestanda |
| Aspose.Cells för .NET (NuGet‑paket `Aspose.Cells`) | Tillhandahåller `Workbook`, `HtmlSaveOptions`, `ImageOrPrintOptions`, osv. |
| Ett par TrueType/OpenType‑typsnittsfiler (t.ex. `Arial.ttf`) placerade i projektmappen | Behövs för inbäddning; Aspose hämtar dem automatiskt om de är installerade på värd‑OS‑en |
| Grundläggande C#‑kunskaper | För att följa koden och anpassa den till dina egna scenarier |

---

## Steg 1 – Skapa en arbetsbok och skriv array‑formler  

Först startar vi en ny `Workbook`‑instans och lägger två array‑formler i cellerna **A1** och **A3**. Dessa formler (`WRAPCOLS` och `WRAPROWS`) producerar en liten 2‑kolumn/2‑rad‑array som vi senare kommer att se renderas i HTML‑utdata.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **Why this matters:** Genom att infoga formler får du dynamiskt innehåll som kommer att utvärderas när vi tvingar beräkning senare. Det visar också att HTML‑exporten kan hantera array‑resultat korrekt.

---

## Steg 2 – Tvinga formelberäkning  

Aspose.Cells beräknar formler lat. För att garantera att vår HTML innehåller de beräknade värdena (istället för råa formler) anropar vi `CalculateFormula()`.

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **Pro tip:** Om du hoppar över detta steg kommer HTML att visa formeltexten (`=WRAPCOLS...`) istället för siffrorna, vilket undergräver syftet med en polerad export.

---

## Steg 3 – Konfigurera HTML‑spara‑alternativ för att bädda in typsnitt  

Nu kommer stjärnan i showen: inbäddning av typsnitt. Att sätta `EmbedFonts` till `true` instruerar Aspose att inkludera typsnittsdata som Base64‑kodade strömmar i den genererade HTML‑filen. Att aktivera `EmbedFontVariationSelectors` säkerställer att eventuella OpenType‑variations‑selectorer (används för avancerad typografi) också bevaras.

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **How it works:** När HTML skrivs injicerar Aspose ett `<style>`‑block med `@font-face`‑regler som refererar de inbäddade data‑URI:erna. Webbläsare renderar exakt samma typsnitt oavsett vilka typsnitt som är installerade på klienten.

---

## Steg 4 – Spara arbetsboken som HTML  

Vi sparar arbetsboken först till en `.xlsx`‑fil (för säkerhets skull) och exporterar sedan till HTML med de alternativ vi just definierat.

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **Result:** Öppna `fontDemo.html` i någon modern webbläsare så ser du array‑värdena renderade med det inbäddade typsnittet, även om typsnittet inte är installerat på din maskin.

---

## Steg 5 – Ladda en arbetsbok med ett diagram och ange utskriftsområdet  

Nästa steg demonstrerar **how to set print area** innan ett blad som innehåller ett diagram exporteras. Utskriftsområdet begränsar vad som renderas, vilket är praktiskt när du bara vill ha ett specifikt område i den slutgiltiga PPTX‑filen.

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **Why set a print area?** Utan ett utskriftsområde skulle Aspose exportera hela bladet, eventuellt med tomma rader/kolumner och göra PPTX‑filen onödigt stor.

---

## Steg 6 – Exportera arbetsbladet till en redigerbar PPTX  

Till sist exporterar vi arbetsbladet till en redigerbar PowerPoint‑fil. Genom att sätta `ExportChartAsEditable = true` sparas diagrammet som inbyggda PowerPoint‑former, så slutanvändare kan modifiera det direkt i PowerPoint.

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **What you get:** `editableChart.pptx` innehåller diagrammet från `chartEditable.xlsx` som redigerbara PowerPoint‑objekt, begränsade till området `A1:G20`.

---

## Förväntat resultat‑översikt  

| Fil | Beskrivning |
|-----|-------------|
| `fontDemo.xlsx` | Ursprunglig arbetsbok med beräknade array‑formler. |
| `fontDemo.html` | HTML‑fil som **bäddar in typsnitt**, visar array‑resultaten och fungerar offline. |
| `editableChart.pptx` | PowerPoint‑presentation med ett redigerbart diagram, som respekterar det **utskriftsområde** du angav. |

Öppna `fontDemo.html` i Chrome eller Edge; du kommer märka att texten använder exakt det typsnitt du bäddade in (t.ex. Arial) även om ditt system saknar det. Diagrammet i `editableChart.pptx` kan dubbelklickas och redigeras precis som vilket inbyggt PowerPoint‑diagram som helst.

---

## Vanliga frågor och edge‑fall  

### Vad händer om mitt typsnitt inte är installerat på servern?  
Aspose.Cells kommer bara att bädda in de typsnitt som är *tillgängliga* för körmiljön. Om ett specifikt typsnitt saknas faller HTML tillbaka till webbläsarens standardsnitt. För att garantera inbäddning, kopiera de nödvändiga `.ttf`/`.otf`‑filerna till din applikationsmapp och referera dem via `FontInfo` (avancerat scenario).

### Kan jag bara bädda in en delmängd av tecken för att minska filstorleken?  
Ja. Använd `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. Detta får Aspose att inkludera endast de glyfer som faktiskt används i arbetsboken, vilket kraftigt minskar HTML‑payloaden.

### Fungerar **tvinga formelberäkning** också för volatila funktioner som `NOW()`?  
Absolut. `CalculateFormula()` utvärderar alla formler, inklusive volatila, i det ögonblick du anropar den. Om du vill att beräkningen ska spegla ett specifikt datum/tid, sätt workbookens `CalculationOptions` i förväg.

### Hur är det med stora arbetsböcker – kommer inbäddning av typsnitt att göra HTML-filen onödigt stor?  
Inbäddning av typsnitt lägger till ungefär 100‑200 KB per typsnitt (beroende på storlek). För mycket stora rapporter kan du överväga att länka till webb‑hostade typsnitt istället för att bädda in dem, eller använda subset‑läget som nämnts ovan.

---

## Pro‑tips och bästa praxis  

- **Batch saves:** Om du genererar dussintals HTML‑filer, återanvänd en enda `HtmlSaveOptions`‑instans för att undvika onödiga allokeringar.  
- **Cache print areas:** När du exporterar många blad, lagra önskat utskriftsområde i en konfigurationsfil för att hålla koden DRY.  
- **Validate output:** Efter att ha sparat HTML, kör en snabb headless‑browser‑kontroll (t.ex. Puppeteer) för att säkerställa att typsnitten renderas korrekt innan du levererar till användare.  
- **Version lock:** Koden ovan riktar sig mot Aspose.Cells 23.12+. Nyare versioner kan introducera ytterligare alternativ som `FontEmbeddingMode`. Kontrollera alltid release‑noterna.

---

## Slutsats  

Vi har gått igenom **hur man bäddar in typsnitt i HTML** med Aspose.Cells, visat vikten av **force formula calculation**, demonstrerat ett rent **convert Excel to HTML**‑flöde och förklarat **how to set print area** innan ett diagram exporteras till en redigerbar PPTX. Det kompletta, körbara exemplet finns i en enda `Program.cs`‑fil, så du kan kopiera‑klistra, justera sökvägar och köra det redan idag.

Redo för nästa steg? Prova att byta ut det inbäddade typsnittet mot ett eget varumärkes‑typsnitt, eller experimentera med `Subset`‑läget för att hålla HTML‑filen lätt. Samma mönster fungerar för PDF, bilder och till och med CSV‑export—byt bara ut `SaveOptions`‑klassen.

Har du fler frågor om inbäddning av typsnitt, formelhantering eller utskriftsområden? Kommentera nedan eller hör av dig i Aspose‑community‑forumen. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}