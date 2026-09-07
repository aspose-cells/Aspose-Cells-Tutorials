---
category: general
date: 2026-02-26
description: Exportera arbetsboken till PDF med inbäddade teckensnitt och exportera
  även diagram till PowerPoint i C#. Lär dig att kopiera pivottabellsbladet och spara
  arbetsboken som PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: sv
og_description: Exportera arbetsboken till PDF med inbäddade teckensnitt och exportera
  även diagram till PowerPoint i C#. Följ steg‑för‑steg‑guiden för att kopiera pivottabeller
  och spara som PPTX.
og_title: Exportera arbetsbok till PDF – Komplett C#-guide
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Exportera arbetsbok till PDF – Komplett C#‑guide
url: /sv/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

. We'll translate as is: "**Advanced PDF Styling** – Explore `" but keep as is. Probably we keep the line as is. Since it's incomplete, we keep it.

We need to keep the shortcodes after that: {{< /blocks/products/pf/tutorial-page-section >}} etc.

Now ensure we didn't miss any text.

Check after "Explore `" there is a blank line then closing shortcodes. We'll keep that line as is.

Now produce final content with all translations and unchanged parts.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera arbetsbok till PDF – Komplett C#-guide

Att exportera en arbetsbok till PDF är ett vanligt krav när du behöver dela rapporter med intressenter som kanske inte har Excel installerat. I den här handledningen visar vi också hur du **exporterar diagram till PowerPoint**, kopierar ett **pivot‑tabellblad**, och bäddar in teckensnitt så att PDF-filen ser exakt ut som din skärm‑design.  

Har du någonsin undrat varför vissa PDF-filer förlorar den ursprungliga layouten eller varför PowerPoint‑bilder slutar med saknade former? Svaret ligger oftast i saknade alternativ under exportprocessen. I slutet av den här guiden har du en enda, återanvändbar C#‑metod som hanterar alla dessa smärtpunkter—slut på manuellt kopier‑och‑klistra eller krångliga exportinställningar.

## Vad du kommer att lära dig

- Hur du skapar en arbetsbok, lägger till Smart Marker‑uttryck och bearbetar dem.  
- Hur du **kopierar ett pivot‑tabellblad** utan att bryta datakällan.  
- Hur du **exporterar diagram, former och textrutor** till en PowerPoint‑presentation samtidigt som de förblir redigerbara.  
- Hur du **bäddar in standardteckensnitt** vid PDF‑export för konsekvent rendering på vilken maskin som helst.  
- Hur du **sparar arbetsboken som PPTX** med hjälp av `save workbook as pptx`‑metoden.  

Allt detta fungerar med de senaste Aspose.Cells‑ och Aspose.Slides .NET‑biblioteken (version 23.11 vid skrivtillfället). Inga externa verktyg, inga efterbearbetnings‑skript—bara ren C#.

> **Proffstips:** Om du redan använder Aspose i ditt projekt kan du klistra in kodsnuttarna som de är; annars lägger du först till NuGet‑paketen `Aspose.Cells` och `Aspose.Slides`.

## Förutsättningar

- .NET 6.0 eller senare (koden körs även på .NET Framework 4.7.2).  
- Visual Studio 2022 (eller någon annan IDE du föredrar).  
- Aspose.Cells .NET och Aspose.Slides .NET installerade via NuGet.  
- Grundläggande kunskap om C# och Excel‑koncept som Smart Markers och PivotTables.

---

![Diagram för export av arbetsbok till PDF](export-workbook-to-pdf.png "Arbetsflöde för export av arbetsbok till PDF som visar PDF- och PPTX-utdata")

## Exportera arbetsbok till PDF – Steg‑för‑steg‑implementation

Nedan är det kompletta, färdiga exemplet. Det bygger en arbetsbok, injicerar Smart Marker‑uttryck, bearbetar dem, kopierar ett pivot‑tabellområde och sparar slutligen både en PDF‑ och en PowerPoint‑fil.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Varför detta fungerar

1. **Smart Marker‑bearbetning** låter dig fylla arbetsboken från vilken datakälla som helst (JSON, DataTables osv.) utan att skriva loopar.  
2. **DetailSheetNewName** skapar ett separat blad för varje avdelning, vilket ger dig en ren flik per avdelning.  
3. **Kopiering av området** (`sourceRange.Copy`) duplicerar pivot‑tabellen *inklusive* dess cache, så det kopierade bladet beter sig exakt som originalet.  
4. **PresentationOptions** med `ExportCharts`, `ExportShapes` och `ExportTextBoxes` instruerar Aspose att rendera dessa objekt som inbyggda PowerPoint‑element, vilket bevarar redigerbarheten.  
5. **PdfSaveOptions.EmbedStandardFonts** säkerställer att PDF‑filen ser identisk ut på maskiner som inte har de ursprungliga teckensnitten installerade.

Resultatet blir två filer—`FinalReport.pdf` och `FinalPresentation.pptx`—som kan e‑postas, arkiveras eller visas i vilken visare som helst utan att förlora kvalitet.

## Exportera diagram till PowerPoint (Spara arbetsbok som PPTX)

Om din rapport innehåller diagram vill du sannolikt ha dem redigerbara i PowerPoint. Klassen `PresentationOptions` är nyckeln. Här är ett fokuserat kodexempel som bara visar diagram‑exportdelen:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Vad händer under huven?** Aspose översätter varje Excel‑diagram till ett inbyggt PowerPoint‑diagram, vilket bevarar serier, axeltitlar och formatering. Detta är mycket bättre än att exportera diagrammet som en statisk bild, eftersom din publik kan justera datapunkter senare.

## Kopiera pivot‑tabellblad utan att förlora data

Pivot‑tabeller är ofta den svåraste delen av en export eftersom de förlitar sig på en dold cache. Den enkla `Copy`‑metoden fungerar eftersom Aspose kopierar både det synliga området **och** det underliggande cache‑objektet.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Obs:** Om du bara behöver pivot‑tabellen på ett nytt blad i samma arbetsbok är den tidigare `sourceRange.Copy`‑metoden lättare och undviker att skapa en helt ny arbetsbok.

## Bädda in teckensnitt för PDF‑export – Varför det är viktigt

När du öppnar en PDF på en maskin som saknar de ursprungliga teckensnitten kan texten flyttas, radbrytningar ändras eller tecken försvinna. Genom att sätta `EmbedStandardFonts = true` instruerar du Aspose att bädda in de vanligaste teckensnitten (Arial, Times New Roman osv.) direkt i PDF‑strömmen.

Om du använder anpassade teckensnitt, byt till `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Här är ett exempel:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Nu ser varje mottagare exakt samma layout som du designade—inga överraskningar.

## Sammanfattning av komplett fungerande exempel

När allt sätts ihop gör det kompletta programmet (visat tidigare) följande:

1. **Skapar** en arbetsbok med Smart Marker‑platshållare.  
2. **Bearbetar** markörerna och genererar ett detaljblad namngivet efter avdelningen.  
3. **Kopierar** ett område som innehåller en pivot‑tabell till ett nytt arbetsblad, vilket bevarar dess funktionalitet.  
4. **Exporterar** arbetsboken till PowerPoint, med diagram, former och textrutor redigerbara.  
5. **Exporterar** samma arbetsbok till PDF samtidigt som standardteckensnitt bäddas in för pålitlig rendering.

Kör programmet, öppna de genererade filerna, och du kommer att se:

- **PDF**: Skarpa tabeller, inbäddade teckensnitt och samma visuella stil som Excel‑källan.  
- **PowerPoint**: Redigerbara diagram som du kan högerklicka → *Edit Data* i PowerPoint, och former som förblir fullt manipulerbara.

---

## Vanliga frågor (FAQ)

**Q: Fungerar detta med .NET Core?**  
Ja—Aspose.Cells och Aspose.Slides är plattformsoberoende. Rikta bara in på .NET 6 eller senare så körs samma kod på Windows, Linux eller macOS.

**Q: Vad händer om jag bara behöver exportera en delmängd av blad?**  
Använd `Workbook.Save` med `SaveOptions` som låter dig specificera `SheetNames`. Exempel: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Kan jag kryptera PDF‑filen?**  
Absolut. Ställ in `PdfSaveOptions.EncryptionDetails` med ett lösenord innan du anropar `Save`.

**Q: Min pivot‑tabell använder en extern datakälla—kommer kopieringen att bryta länken?**  
Kopieringsoperationen inkluderar cachen, inte den externa anslutningen. Pivot‑tabellen fungerar fortfarande offline, men den uppdateras inte mot den ursprungliga källan. Om du behöver live‑uppdatering, exportera källdata tillsammans med arbetsboken.

## Nästa steg & relaterade ämnen

- **Dynamiska datakällor** – Lär dig hur du matar JSON eller en DataTable i Smart Markers för realtidsrapportering.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}