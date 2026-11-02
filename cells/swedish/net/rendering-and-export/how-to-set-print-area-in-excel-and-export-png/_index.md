---
category: general
date: 2026-09-27
description: Ställ in utskriftsområde i Excel och lär dig hur du exporterar PNG‑bilder
  av markerade celler. Denna guide täcker också hur du sparar ett område som bild
  och lägger till en bild i kalkylbladet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: sv
lastmod: 2026-09-27
og_description: Ställ in utskriftsområde i Excel och exportera PNG med Aspose.Cells.
  Följ den här steg‑för‑steg‑guiden för att spara ett område som bild och lägga till
  en bild i kalkylbladet.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Ställ in utskriftsområde i Excel – exportera PNG i C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Hur man anger utskriftsområde i Excel och exporterar PNG
url: /sv/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man ställer in utskriftsområde i Excel och exporterar PNG

Om du behöver **set print area excel** innan du skapar en bild, visar den här guiden exakt hur du gör det. Du kommer också att lära dig **how to export png** filer från ett specifikt område, **save range as image**, och **add picture to worksheet** i ett enda, repeterbart arbetsflöde.

Att arbeta med Excel programatiskt innebär ofta att du bara vill ha en delmängd av celler — till exempel en pivottabell eller ett diagram — att bli en bild. Genom att först definiera ett utskriftsområde säkerställer du att den exporterade PNG-filen exakt innehåller de celler du förväntar dig, varken mer eller mindre. Denna handledning guidar dig genom varje steg, från att ladda arbetsboken till att spara den slutliga PNG-filen, och förklarar varför varje inställning är viktig.

## Förutsättningar

* .NET 6.0 eller senare installerat  
* Visual Studio 2022 (eller någon C#-IDE)  
* NuGet-paketet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* En Excel-fil (`input.xlsx`) som ligger i en känd katalog  

Dessa krav säkerställer att koden körs utan ytterligare konfiguration.

## Steg 1: Ladda arbetsboken du vill arbeta med

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook`-klassen representerar hela Excel-filen. Att ladda den först ger dig åtkomst till arbetsblad, celler och sidinställningsalternativ.

## Steg 2: **Set print area excel** för målområdet

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Att ange **print area** talar om för Excel (och Aspose.Cells) vilka celler som tillhör den utskrivbara sidan. När du senare exporterar bladet som en bild renderas endast detta område, vilket är avgörande för en ren **export selected cells image**.

## Steg 3: Konfigurera bildexportalternativ – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` styr utdataformatet. Genom att välja `ImageFormat.Png` garanterar du en högupplöst bild med transparent bakgrund som fungerar bra i webb- och skrivbordssammanhang.

## Steg 4: Skapa en bild från det definierade området och **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add`-metoden infogar en ny bild i arbetsbladet. Genom att skicka in området som skapades i Steg 2, **save range as image** direkt på bladet, vilket är användbart om du senare behöver referera till bilden i andra delar av arbetsboken.

## Steg 5: **Save the picture as an image file** – slutför **export selected cells image**-arbetsflödet

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Genom att anropa `Save` skrivs bilden till filsystemet med de alternativ som definierades i Steg 3. Den resulterande `selected_range.png` innehåller exakt de celler som definierades av kommandot **set print area excel**.

## Fullt, körbart exempel

Genom att sätta ihop alla bitar får du ett kompakt program som du kan lägga in i vilken konsolapplikation som helst:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Förväntat resultat

När programmet körs skrivs:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Och du hittar en `selected_range.png`-fil som endast visar cellerna A1 till G20 från `input.xlsx`.

## Vanliga fallgropar och hur man undviker dem

| Problem | Varför det händer | Lösning |
|-------|----------------|-----|
| Den exporterade bilden innehåller hela bladet | Inget utskriftsområde definierades | Se till att **set print area excel** innan du skapar bilden |
| PNG är suddig | Standard‑DPI är låg | Ställ in `imageOptions.DpiX` och `imageOptions.DpiY` till ett högre värde (t.ex. 300) |
| Filen hittades inte‑fel | Fel katalogsökväg | Använd `Path.Combine` eller dubbelkolla att mappen finns |
| Bilden visas förskjuten | Fel rad‑/kolumnindex | De två första parametrarna i `Pictures.Add` är den övre‑vänstra cellen där bilden placeras; håll dem på `0,0` för en ren export |

## Proffstips: Exportera flera områden i ett kör

Om du behöver **export selected cells image** för flera områden, upprepa Steg 2‑5 i en loop och ändra `printArea` för varje iteration. Kom ihåg att ge varje bild ett unikt filnamn, annars kommer den senare sparningen att skriva över den föregående filen.

## Slutsats

Du vet nu hur man **set print area excel**, konfigurerar **how to export png**, **save range as image**, och **add picture to worksheet** med Aspose.Cells. Denna helhetslösning låter dig omvandla vilket cellblock som helst till en högkvalitativ PNG med bara några rader C#‑kod.

Nästa steg kan vara att utforska:

* Lägg till ramar eller vattenstämplar i den exporterade PNG:n (sök efter *add picture to worksheet* med styling)
* Exportera direkt till PDF för utskrivbara rapporter (*export selected cells image* → PDF‑arbetsflöde)
* Automatisera processen för flera arbetsböcker i ett batchjobb

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}