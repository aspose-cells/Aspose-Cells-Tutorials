---
category: general
date: 2026-10-26
description: Ställ in utskriftsområde och exportera ett Excel‑ark till PNG i C#. Lär
  dig bildexportalternativ, hur du exporterar PNG och får en utskrivbar bild från
  en arbetsbok.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: sv
lastmod: 2026-10-26
og_description: Ställ in utskriftsområde och exportera ett Excel‑ark till PNG i C#.
  Denna steg‑för‑steg‑handledning täcker bildexportalternativ och hur du exporterar
  PNG från en arbetsbok.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Ställ in utskriftsområde och exportera Excel‑ark till PNG – C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Ställ in utskriftsområde och exportera Excel‑ark till PNG i C#
url: /sv/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in utskriftsområde och exportera Excel‑blad till PNG i C#

Om du behöver **set print area** innan du exporterar ett Excel‑blad till PNG, visar den här guiden hur du gör. Du får se ett komplett C#‑exempel som konfigurerar bildexportalternativ, justerar bladets utskriftsområde och sparar resultatet som en bild.

Att exportera ett Excel‑blad till PNG är ett vanligt behov när du vill bädda in en ögonblicksbild av ett kalkylblad i en rapport, ett e‑postmeddelande eller en webbsida. Koden nedan fungerar med alla arbetsböcker som innehåller en pivottabell, men tekniken gäller även för vanliga dataområden. Inga externa verktyg krävs – bara Aspose.Cells för .NET‑biblioteket.

## Förutsättningar

- .NET 6.0 eller senare (exemplet riktar sig mot .NET 6, men alla nyare .NET‑versioner fungerar)
- Aspose.Cells för .NET (installera via NuGet: `Install-Package Aspose.Cells`)
- Grundläggande kunskap om C# och Excel‑koncept som kalkylblad och utskriftsområden

## Steg 1: Konfigurera bildexportalternativ

Det första du gör är att skapa en instans av `ImageOrPrintOptions`. Detta objekt talar om för Aspose.Cells hur bladet ska renderas som en bild.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Varför detta är viktigt:** `ImageOrPrintOptions` styr utdataformat, upplösning och andra renderingsdetaljer. Att använda PNG ger förlustfri kvalitet, vilket är idealiskt för rapporter som kräver skarp text och grafik.

## Steg 2: Läs in arbetsboken och få åtkomst till mål‑kalkylbladet

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Varför detta är viktigt:** Du måste arbeta med ett specifikt `Worksheet`‑objekt eftersom utskriftsområdet är en inställning på kalkylbladsnivå.

## Steg 3: Identifiera det område du vill skriva ut

I många scenarier finns den data du är intresserad av i en pivottabell. Följande kod extraherar dataområdet för den första pivottabellen på bladet.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Om ditt kalkylblad inte innehåller en pivottabell kan du ersätta `pivotDataRange` med någon `CellArea` du skapar manuellt, t.ex.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Steg 4: **Set print area** för att matcha det valda området

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Varför detta är viktigt:** Utskriftsområdet talar om för Excel (och Aspose.Cells) vilka celler som ska inkluderas när bladet renderas till en bild. Genom att anpassa utskriftsområdet till pivottabellens dataområde undviker du tomma marginaler och säkerställer att den exporterade PNG‑filen bara innehåller den relevanta datan.

## Steg 5: Exportera kalkylbladet till en PNG‑bild

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Varför detta är viktigt:** `worksheet.ToImage` respekterar det tidigare angivna utskriftsområdet, så PNG‑filen innehåller exakt de celler du definierat. Att tilldela bilden till en bildform möjliggör att du kan bädda in den tillbaka i arbetsboken om så behövs, medan sparandet till disk ger dig en fristående fil.

## Fullständigt fungerande exempel

När du sätter ihop alla steg får du ett självständigt program som du kan köra omedelbart.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Förväntat resultat

När programmet körs skapas `C:\Temp\WorksheetExport.png`. När du öppnar filen visas en skarp PNG‑bild som bara innehåller de celler som definierats av **set print area** (pivottabellens data i detta exempel). Bilden kan infogas i Word‑dokument, PowerPoint‑bilder eller webbsidor utan ytterligare konverteringssteg.

## Hantera flera kalkylblad eller pivottabeller

- **Flera kalkylblad:** Loopa igenom `wb.Worksheets` och upprepa steg 3‑5 för varje blad du behöver exportera.
- **Flera pivottabeller:** Välj rätt `PivotTables[index]` eller iterera över `worksheet.PivotTables` för att exportera varje tabell individuellt.
- **Ingen pivottabell:** Skapa en `CellArea` manuellt (se kommentaren i Steg 3) och tilldela den till `PrintArea`.

## Praktiska tips (E‑E‑A‑T)

- **Proffstips:** Sätt `HorizontalResolution` och `VerticalResolution` till 300 DPI för utskriftsklara PNG‑filer; lägre värden minskar filstorleken för webbbruk.
- **Var uppmärksam på tomma bildformer:** Om kalkylbladet saknar bildformer, lägg till en innan du tilldelar bilden:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Prestanda:** Återanvänd en enda `ImageOrPrintOptions`‑instans för flera kalkylblad för att undvika onödiga allokeringar.
- **Kompatibilitet:** Aspose.Cells 23.9+ stöder fullt ut .NET 6 och senare; äldre versioner kan kräva justeringar av API‑namnen.

## Slutsats

Du vet nu hur du **set print area** och exporterar ett Excel

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på de tekniker som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man exporterar Excel till PNG – fullständig steg‑för‑steg‑guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Hur man exporterar Excel‑område som bild med C# och Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel‑blad till png – Exportera en pivottabell som PNG i C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}