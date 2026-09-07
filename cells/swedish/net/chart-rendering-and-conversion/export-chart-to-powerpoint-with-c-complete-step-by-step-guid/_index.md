---
category: general
date: 2026-02-26
description: Exportera diagram till PowerPoint från Excel med C#. Lär dig hur du konverterar
  Excel till PowerPoint, sparar Excel som PowerPoint och behåller former redigerbara.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: sv
og_description: Exportera diagram till PowerPoint från Excel med C#. Den här guiden
  visar hur du konverterar Excel till PowerPoint, sparar arbetsboken som PPTX och
  behåller former redigerbara.
og_title: Exportera diagram till PowerPoint med C# – Fullständig programmeringshandledning
tags:
- Aspose.Cells
- C#
- Office Automation
title: Exportera diagram till PowerPoint med C# – Komplett steg‑för‑steg‑guide
url: /sv/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

Now produce final output with all content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera diagram till PowerPoint – Komplett programmeringshandledning

Har du någonsin undrat hur man **exporterar diagram till PowerPoint** utan att förlora redigerbarheten? I många rapporteringsscenarier behöver du ett levande diagram i en bildspelspresentation, men att kopiera och klistra in manuellt är besvärligt. Den goda nyheten är att du kan göra det programatiskt med några få rader C#.

I den här guiden går vi igenom hela processen: från att ladda en Excel-arbetsbok som innehåller ett diagram med en textruta, konfigurera exporten så att textrutor och former förblir redigerbara, och slutligen spara resultatet som en **PowerPoint**-fil. I slutet kommer du också att veta hur man **konverterar Excel till PowerPoint**, **sparar Excel som PowerPoint**, och till och med justerar alternativen för kantfallsscenarier.

## Vad du behöver

- **Aspose.Cells for .NET** (version 23.10 eller senare). Det är biblioteket som gör konverteringen smärtfri.
- **.NET 6+** runtime – någon nyare SDK fungerar.
- En enkel Excel-fil (`ChartWithTextbox.xlsx`) som innehåller minst ett diagram och en textruta.
- Visual Studio eller din favorit‑IDE.

Inga ytterligare NuGet‑paket krävs utöver Aspose.Cells, men att ha en grundläggande förståelse för C#‑syntax hjälper definitivt.

## Exportera diagram till PowerPoint – Steg för steg

Nedan delar vi upp lösningen i separata, lättföljda steg. Varje steg innehåller den exakta koden du behöver, samt ett kort “varför”‑avsnitt som förklarar resonemanget bakom det.

### Steg 1: Ladda Excel‑arbetsboken som innehåller diagrammet

Först måste vi läsa in källfilen i minnet. Att använda `Workbook` från Aspose.Cells läser in hela kalkylbladet, inklusive diagram, bilder och inbäddade objekt.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Varför detta är viktigt:* Om arbetsboken öppnas utan att ange sökvägen korrekt får du ett `FileNotFoundException`. Den snabba kontrollen förhindrar att du senare exporterar en tom bild.

### Steg 2: Förbered presentationsalternativ för att behålla former redigerbara

Aspose.Cells låter dig bestämma om textrutor, former och till och med diagrammet självt förblir **redigerbara** efter exporten. Genom att sätta `ExportTextBoxes` och `ExportShapes` till `true` bevaras dessa objekt som inbyggda PowerPoint‑element istället för att de plattas ut till en statisk bild.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Varför detta är viktigt:* Om du lämnar dessa flaggor på sina standardvärden (`false`) kommer den resulterande bilden att innehålla en bitmap av diagrammet, vilket gör det omöjligt att redigera serierna eller ändra rubriken senare. Att aktivera båda alternativen ger dig ett riktigt PowerPoint‑diagram som beter sig exakt som ett du skulle rita manuellt.

### Steg 3: Konvertera Excel till PowerPoint och spara filen

Nu anropar vi `Save`‑metoden och skickar med `SaveFormat.Pptx`‑enumet samt de alternativ vi just konfigurerat. Biblioteket tar hand om att översätta Excel‑diagramobjektet till en PowerPoint‑diagramform.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Varför detta är viktigt:* `Save`‑anropet gör allt tungt arbete – det mappar Excel‑serier till PowerPoint‑serier, bevarar axelformatering och kopierar över eventuella länkade textrutor. Efter att den här raden har körts har du en fullt redigerbar `.pptx`‑fil som är klar att öppnas i Microsoft PowerPoint.

### Verifiera resultatet

Öppna `Result.pptx` i PowerPoint. Du bör se en bild som innehåller:

- Det ursprungliga diagrammet, fortfarande länkat till sina data (du kan dubbelklicka för att redigera serierna).
- Eventuell textruta som fanns i Excel‑arket, nu en inbyggd PowerPoint‑textruta.
- Bildlayouten väljs automatiskt (vanligtvis en tom bild).

Om du märker några saknade element, dubbelkolla att källarbetsboken faktiskt hade synliga objekt och att `ExportTextBoxes` / `ExportShapes` var satta till `true`.

### Konvertera Excel till PowerPoint: Hantera flera arbetsblad

Ofta innehåller en arbetsbok mer än ett blad, varje med sitt eget diagram. Som standard exporterar Aspose.Cells **alla** diagram från **alla** arbetsblad till separata bilder. Om du bara behöver en delmängd kan du filtrera dem innan du sparar:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Proffstips:* Att sätta `chart.IsVisible = false` är billigare än att ta bort diagrammet helt, och det låter dig växla inkludering utan att ändra källfilen.

### Spara Excel som PowerPoint – Anpassa bildstorlek

PowerPoint har som standard en bild på 10 tum gånger 5,63 tum. Om ditt diagram ser trångt ut kan du ändra bildens dimensioner via `PresentationOptions`‑objektet:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Nu får det exporterade diagrammet mer utrymme, och eventuella textrutor behåller sin ursprungliga layout.

### Hur man konverterar Excel till PPT: Hantera dolda objekt

Dolda rader, kolumner eller former kan ibland smyga in i exporten. För att ta bort dem, kör en snabb städning innan du sparar:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Detta steg är inte alltid nödvändigt, men det förhindrar oväntade luckor i din slutliga bildspelsuppsättning.

### Spara arbetsbok som PPTX – Fullt fungerande exempel

När vi sätter ihop allt, här är ett färdigt konsolprogram som demonstrerar hela flödet:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Att köra detta program skapar `Result.pptx` med ett redigerbart diagram och en textruta, exakt vad du kan förvänta dig när du **sparar arbetsbok som pptx** manuellt.

![Exempel på export av diagram till PowerPoint](/images/export-chart-to-powerpoint.png "Exportera diagram till PowerPoint – redigerbar bild")

## Vanliga frågor & kantfall

**Vad händer om Excel‑filen innehåller ett diagram med en länkad extern datakälla?**  
Aspose.Cells kopierar de *aktuella* datavärdena till PowerPoint‑diagrammet. Det bevarar **inte** den externa länken, eftersom PowerPoint inte kan referera till en Excel‑datakoppling på samma sätt. Om du behöver live‑uppdateringar, överväg att bädda in den ursprungliga Excel‑filen i PPTX som ett OLE‑objekt istället.

**Kan jag exportera ett diagram som använder ett anpassat tema?**  
Ja. Biblioteket försöker mappa Excel‑temafärger till PowerPoint‑temaplatser. För mycket anpassade paletter kan du behöva justera färgerna efter export med PowerPoints eget API (t.ex. Aspose.Slides).

**Finns det någon gräns för antalet diagram?**  
I praktiken ingen—Aspose.Cells strömmar data, så även en arbetsbok med dussintals diagram exporteras, även om den resulterande PPTX‑filens storlek växer linjärt.

**Behöver jag en licens för Aspose.Cells?**  
En gratis utvärdering fungerar, men den lägger till ett vattenmärke på den första bilden. För produktionsbruk, skaffa en riktig licens för att ta bort vattenmärket och låsa upp full prestanda.

## Sammanfattning

Vi har gått igenom hur man **exporterar diagram till PowerPoint** med C#, demonstrerat den exakta koden för att ladda en Excel‑arbetsbok, konfigurera `PresentationOptions` för att behålla textrutor och former redigerbara, och slutligen spara resultatet som en `.pptx`. Du har också lärt dig hur man **konverterar Excel till PowerPoint**, **sparar Excel som PowerPoint**, och svarat på frågan “**hur man konverterar Excel till ppt**” med ett komplett, körbart exempel.

## Vad blir nästa steg?

- **Spara arbetsbok som PPTX** med flera bilder: loopa igenom varje arbetsblad och anropa `Save` med `PresentationOptions` för varje.
- Utforska **Aspose.Slides** om du behöver programatiskt modifiera den genererade PPTX‑filen ytterligare (lägga till övergångar, talarnoter osv.).
- Prova att exportera **pivotdiagram** eller **3‑D‑diagram**—samma alternativ gäller, men du kan behöva justera axelformatering efteråt.

Om du stöter på problem, lämna en kommentar nedan eller kolla den officiella Aspose.Cells‑dokumentationen för de senaste API‑ändringarna. Lycka till med kodandet, och njut av att förvandla dina Excel‑diagram till polerade PowerPoint‑presentationer med bara några rader C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}