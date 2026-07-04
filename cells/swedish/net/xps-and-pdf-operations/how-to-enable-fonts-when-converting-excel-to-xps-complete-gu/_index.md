---
category: general
date: 2026-07-03
description: Hur du aktiverar teckensnitt när du konverterar Excel till XPS med Aspose.Cells.
  Lär dig steg‑för‑steg‑inställning, kod och tips för felfri teckensnittspreservation.
draft: false
keywords:
- how to enable fonts
- convert excel to xps
- Aspose.Cells XPS export
- preserve font variations
- C# Excel automation
language: sv
og_description: Hur du aktiverar teckensnitt i din Excel‑till‑XPS‑konvertering. Följ
  den här guiden för ett fungerande C#‑exempel som behåller teckensnittsvariationerna
  intakta.
og_title: Hur du aktiverar teckensnitt när du konverterar Excel till XPS – Fullständig
  handledning
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  headline: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  type: TechArticle
- description: How to enable fonts while you convert Excel to XPS using Aspose.Cells.
    Learn step‑by‑step setup, code, and tips for flawless font preservation.
  name: How to Enable Fonts When Converting Excel to XPS – Complete Guide
  steps:
  - name: What Does `FontVariationSelectors = true` Actually Do?
    text: '- **Preserves custom weight & style variations** (e.g., a font that supports
      multiple thicknesses via OpenType features). - **Ensures the XPS viewer renders
      the exact glyphs** you see in Excel, rather than falling back to a generic font.
      - **Adds a small overhead** to the file size because the selec'
  - name: Expected Result
    text: '- The file `WithSelectors.xps` will appear in the target folder. - Open
      it in any XPS viewer (e.g., Windows XPS Viewer or Edge). - You should see the
      same font weights, italics, and any custom OpenType variations that were present
      in the original Excel file.'
  - name: Next Steps
    text: '- Experiment with other `XpsSaveOptions` properties like `Compress` or
      `EmbedStandardFonts`. - Try converting to PDF first, then to XPS, to compare
      file sizes and fidelity. - Dive into Aspose.Cells’ **image handling** (`ImageOrPrintOptions`)
      if your workbook contains charts or pictures you also need'
  type: HowTo
tags:
- Aspose.Cells
- C#
- XPS
- Excel
title: Hur man aktiverar teckensnitt vid konvertering av Excel till XPS – Komplett
  guide
url: /sv/net/xps-and-pdf-operations/how-to-enable-fonts-when-converting-excel-to-xps-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så aktiverar du teckensnitt vid konvertering av Excel till XPS – Komplett guide

Har du någonsin undrat **hur man aktiverar teckensnitt** så att din Excel‑till‑XPS‑konvertering ser exakt ut som den ursprungliga arbetsboken? Du är inte ensam. Många utvecklare stöter på problem när den resulterande XPS‑filen tappar anpassade teckensnittsvarianter, vilket får dokumentet att se tråkigt ut.  

I den här handledningen går vi igenom en praktisk lösning som inte bara visar **hur man aktiverar teckensnitt** utan också demonstrerar det bästa sättet att **konvertera Excel till XPS** med Aspose.Cells. I slutet har du ett färdigt C#‑kodexempel, en tydlig förklaring av varje inställning och några pro‑tips för att hålla ditt XPS‑resultat pixel‑perfekt.

## Vad du behöver

Innan vi dyker ner, se till att du har:

- **Aspose.Cells for .NET** (senaste versionen per 2026‑07).  
- En .NET‑utvecklingsmiljö (Visual Studio 2022 eller VS Code med C#‑tillägget fungerar bra).  
- En Excel‑arbetsbok (`VariationFont.xlsx`) som innehåller teckensnittsvariationsväljare du vill bevara.  

Det är allt—inga extra NuGet‑paket, ingen krånglig COM‑interop, bara ren C#.

![Diagram som visar flödet från Excel‑arbetsbok till XPS‑dokument – hur man aktiverar teckensnitt under konvertering](https://example.com/images/enable-fonts-xps.png "hur man aktiverar teckensnitt i Excel till XPS‑konvertering")

## Steg 1: Ställ in projektet och importera namnrymder

Först, skapa en ny konsolapp (eller integrera i en befintlig lösning). Lägg till Aspose.Cells‑referensen via NuGet:

```bash
dotnet add package Aspose.Cells
```

Sedan, importera de nödvändiga namnrymderna:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // optional, for advanced graphics handling
```

> **Pro tip:** Om du riktar dig mot .NET 6+ kan du använda den implicita `global using`‑funktionen för att hålla dina filer prydliga.

## Steg 2: Läs in Excel‑arbetsboken

Att läsa in arbetsboken är grunden; utan en korrekt `Workbook`‑instans kan du inte justera några sparalternativ.

```csharp
// Step 2: Load the Excel workbook you want to convert
Workbook workbook = new Workbook("YOUR_DIRECTORY/VariationFont.xlsx");

// Quick sanity check – make sure at least one worksheet is present
if (workbook.Worksheets.Count == 0)
{
    throw new InvalidOperationException("The workbook contains no worksheets.");
}
```

> **Varför detta är viktigt:** När du senare aktiverar teckensnittsvariationsväljare behöver Aspose.Cells en fullständigt initierad arbetsbok; annars ignoreras alternativet tyst.

## Steg 3: Skapa och konfigurera XPS‑spara‑alternativ – Här **aktiverar du teckensnitt**

Kärnan i handledningen finns i detta steg. Som standard tar Aspose.Cells bort teckensnittsvariationsväljare för att hålla XPS‑filens storlek liten. För att bevara dem, sätt `FontVariationSelectors` till `true`.

```csharp
// Step 3: Create XPS save options and enable font variation selectors
XpsSaveOptions xpsOptions = new XpsSaveOptions
{
    // This flag tells Aspose.Cells to keep any OpenType font variation selectors
    FontVariationSelectors = true,

    // Optional: keep the original DPI for sharper rendering (default is 96)
    Dpi = 300
};
```

### Vad gör `FontVariationSelectors = true` egentligen?

- **Bevarar anpassade vikt‑ och stilvariationer** (t.ex. ett teckensnitt som stödjer flera tjocklekar via OpenType‑funktioner).  
- **Säkerställer att XPS‑visaren renderar exakt samma glyfer** som du ser i Excel, istället för att falla tillbaka på ett generiskt teckensnitt.  
- **Lägger till en liten overhead** i filstorleken eftersom selector‑data lagras i XPS‑paketet.

Om du någonsin behöver **konvertera Excel till XPS** utan att bevara dessa väljare, sätt helt enkelt egenskapen till `false` (eller utelämna den, då `false` är standard).

## Steg 4: Spara arbetsboken som XPS med de konfigurerade alternativen

Nu när alternativen är klara, anropa `Save` med `SaveFormat.Xps`‑enumet och skicka med options‑objektet.

```csharp
// Step 4: Save the workbook as an XPS document with the font‑preserving options
string outputPath = "YOUR_DIRECTORY/WithSelectors.xps";
workbook.Save(outputPath, SaveFormat.Xps, xpsOptions);

Console.WriteLine($"Workbook successfully saved to XPS at: {outputPath}");
```

### Förväntat resultat

- Filen `WithSelectors.xps` kommer att visas i mål‑mappen.  
- Öppna den i någon XPS‑visare (t.ex. Windows XPS Viewer eller Edge).  
- Du bör se samma teckensnittsvikter, kursiver och eventuella anpassade OpenType‑variationer som fanns i den ursprungliga Excel‑filen.

Om teckensnitten ser annorlunda ut, dubbelkolla att käll‑Excel‑filen faktiskt använder ett teckensnitt med variationsväljare och att den visare du använder stödjer dem.

## Vanliga fallgropar & hur du undviker dem

| Symptom | Trolig orsak | Lösning |
|---------|--------------|-----|
| Text visas i ett generiskt reservteckensnitt | `FontVariationSelectors` lämnades på standard (`false`) | Sätt `xpsOptions.FontVariationSelectors = true`. |
| XPS‑filens storlek ökar oväntat | Hög DPI‑inställning kombinerad med teckensnittsväljare | Sänk `Dpi` till 150 eller 96 om storlek är viktigare än noggrannhet. |
| Undantag “File not found” vid `Workbook`‑skapande | Fel sökväg eller fil saknas | Använd en absolut sökväg eller `Path.Combine(Environment.CurrentDirectory, "VariationFont.xlsx")`. |

## Steg 5: Verifiera konverteringen (valfritt automatiserat test)

Om du automatiserar byggen kan du vilja påstå att XPS‑filen finns och inte är tom:

```csharp
if (!System.IO.File.Exists(outputPath) || new System.IO.FileInfo(outputPath).Length == 0)
{
    throw new Exception("XPS conversion failed – file is missing or empty.");
}
```

Att köra denna kontroll som en del av en CI‑pipeline garanterar att **hur man aktiverar teckensnitt** fungerar varje gång du pushar kod.

## Sammanfattning: Vad vi gick igenom

- **Hur man aktiverar teckensnitt** under en Excel‑till‑XPS‑konvertering genom att växla `FontVariationSelectors`.  
- Det kompletta C#‑kodexemplet som läser in en arbetsbok, konfigurerar `XpsSaveOptions` och sparar resultatet.  
- Tips för felsökning och verifiering av det slutliga dokumentet.  

Nu kan du med självförtroende **konvertera Excel till XPS** samtidigt som du behåller varje typografisk nyans intakt.  

### Nästa steg

- Experimentera med andra `XpsSaveOptions`‑egenskaper som `Compress` eller `EmbedStandardFonts`.  
- Prova att först konvertera till PDF och sedan till XPS för att jämföra filstorlekar och noggrannhet.  
- Fördjupa dig i Aspose.Cells **bild‑hantering** (`ImageOrPrintOptions`) om din arbetsbok innehåller diagram eller bilder som du också behöver bevara.

Har du frågor om mer avancerade scenarier—t.ex. inbäddning av anpassade teckensnitt som inte är installerade på målmaskinen? Lämna en kommentar nedan, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man ställer in teckenstilar i Excel med Aspose.Cells för .NET (Steg‑för‑steg‑guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Hur man extraherar teckensnitt från Excel‑filer med Aspose.Cells för .NET](/cells/english/net/formatting/extract-fonts-excel-aspose-cells-dotnet-guide/)
- [Hur man konverterar Excel‑ark till bilder med Aspose.Cells .NET (Steg‑för‑steg‑guide)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}