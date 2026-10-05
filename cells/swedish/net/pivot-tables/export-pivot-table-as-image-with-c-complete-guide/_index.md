---
category: general
date: 2026-05-23
description: Lär dig hur du exporterar pivottabell som bild och sparar pivottabell
  som foto med Aspose.Cells i C#. Steg‑för‑steg‑kod och tips.
draft: false
keywords:
- export pivot table as image
- save pivot table as picture
language: sv
og_description: Exportera pivottabell som bild och spara pivottabell som bild med
  Aspose.Cells. Fullständig kod, förklaring och bästa praxis.
og_title: Exportera pivottabell som bild med C# – Komplett guide
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  headline: Export Pivot Table as Image with C# – Complete Guide
  type: TechArticle
- description: Learn how to export pivot table as image and save pivot table as picture
    using Aspose.Cells in C#. Step‑by‑step code and tips.
  name: Export Pivot Table as Image with C# – Complete Guide
  steps:
  - name: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
    text: '**.NET 6+** (or .NET Framework 4.6+ if you prefer classic) installed.'
  - name: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
    text: A **license** for Aspose.Cells — the free evaluation works fine for testing,
      but a license removes the evaluation watermark.
  - name: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
    text: An Excel file (`Sample.xlsx`) that contains at least one pivot table on
      a sheet named *Sheet1* (you can rename it later).
  - name: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
    text: '**Dispose Resources:** Wrap the `Workbook` in a `using` block or call `workbook.Dispose()`
      to free memory, especially when processing large files.'
  - name: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
    text: '**Thread Safety:** Each thread should have its own `Workbook` instance;
      Aspose.Cells objects are not thread‑safe.'
  - name: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
    text: '**Logging:** Log the export path and any exceptions to a central log file
      for easier troubleshooting.'
  - name: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
    text: '**Batch Processing:** If you need to generate images for dozens of workbooks,
      consider a queue system (e.g., Azure Queue) to spread the load.'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel automation
- PivotTable
- Image export
title: Exportera pivottabell som bild med C# – Komplett guide
url: /sv/net/pivot-tables/export-pivot-table-as-image-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera pivottabell som bild med C# – Komplett guide

Har du någonsin undrat hur man **exportera pivottabell som bild** direkt från en Excel-arbetsbok utan att ta en skärmdump? Du är inte ensam. I många rapporteringsscenarier—tänk automatiska instrumentpaneler eller e‑postbilagor—är det mycket bekvämare att ha en skarp bild av en pivottabell än en rå `.xlsx`‑fil.  

I den här handledningen går vi igenom de exakta stegen för att **exportera pivottabell som bild** och täcker även den subtila konsten att **spara pivottabell som bild** med det kraftfulla Aspose.Cells‑biblioteket. I slutet har du ett självständigt, körbart C#‑program som sparar en PNG‑fil precis där du behöver den.

## Vad den här guiden täcker

- Att sätta upp ett .NET‑projekt med Aspose.Cells  
- Att ladda en befintlig arbetsbok och hitta den önskade pivottabellen  
- Att konfigurera bildexportalternativ (upplösning, format osv.)  
- Att faktiskt exportera pivottabellen som en PNG‑bildfil  
- Vanliga fallgropar—t.ex. hantering av dolda kalkylblad eller flera pivoter—och hur man undviker dem  

Inga externa skript, ingen manuell hackning, bara ren kod du kan kopiera‑klistra och köra.

## Förutsättningar

Innan vi dyker ner, se till att du har:

1. **.NET 6+** (eller .NET Framework 4.6+ om du föredrar klassisk) installerat.  
2. En **licens** för Aspose.Cells — den fria utvärderingen fungerar bra för testning, men en licens tar bort vattenstämpeln.  
3. En Excel‑fil (`Sample.xlsx`) som innehåller minst en pivottabell på ett blad som heter *Sheet1* (du kan byta namn senare).  

Om du saknar någon av dessa, hämta det senaste Aspose.Cells‑NuGet‑paketet:

```bash
dotnet add package Aspose.Cells
```

Nu när vi är redo, låt oss sätta igång.

## Steg 1: Ladda arbetsboken och hämta kalkylbladet

Först och främst: vi måste öppna arbetsboken och peka på kalkylbladet som innehåller pivottabellen. Detta steg är grunden för **exportera pivottabell som bild** eftersom biblioteket utan ett giltigt `Worksheet`‑objekt inte kan hitta pivoten.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // Path to the Excel file containing the pivot table
        string workbookPath = @"C:\Data\Sample.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(workbookPath);

        // Obtain the worksheet that contains the pivot table
        // Replace "Sheet1" with your actual sheet name if different
        Worksheet ws = workbook.Worksheets["Sheet1"];
```

> **Varför detta är viktigt:** Aspose.Cells läser in hela arbetsboken i minnet, så varje stavfel i bladnamnet kastar ett `ArgumentException`. Verifiera alltid att bladet finns innan du fortsätter.

## Steg 2: Åtkomst till önskad pivottabell

En arbetsbok kan innehålla flera pivoter, men för de flesta enkla scenarier räcker den första. Om du har flera kan du iterera över `ws.PivotTables` och välja efter namn.

```csharp
        // Access the first pivot table in the worksheet
        // If you know the pivot's name, you can use ws.PivotTables["MyPivot"]
        PivotTable pivot = ws.PivotTables[0];
```

> **Proffstips:** När du har mer än en pivot, använd `ws.PivotTables["PivotName"]` för att undvika att av misstag exportera fel tabell.

## Steg 3: Konfigurera bildexportalternativ

Aspose.Cells ger dig finjusterad kontroll över bildutdata. Här sätter vi formatet till PNG, men du kan byta till JPEG eller BMP genom att ändra `ImageFormat`. Du kan också justera DPI, skalning och om du vill inkludera rutnätslinjer.

```csharp
        // Set up image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: increase resolution for sharper output
            // HorizontalResolution = 300,
            // VerticalResolution = 300,
            // Transparent = true   // if you need a transparent background
        };
```

> **Varför vi använder PNG:** PNG bevarar textens klarhet och stödjer transparens, vilket gör det idealiskt för inbäddning i rapporter eller webbsidor.

## Steg 4: Exportera pivottabellen som en bildfil

Nu händer magin. Metoden `ToImage` skriver pivottabellen till disk i det format vi konfigurerat. Detta är kärnan i **spara pivottabell som bild**.

```csharp
        // Define the output path – make sure the directory exists
        string outputPath = @"C:\Exports\pivot.png";

        // Export the pivot table as an image file
        pivot.ToImage(outputPath, imageOptions);

        System.Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

> **Edge case:** Om målkatalogen inte finns, kastar `ToImage` ett `DirectoryNotFoundException`. Skapa mappen först eller använd `Directory.CreateDirectory(Path.GetDirectoryName(outputPath))`.

## Steg 5: Verifiera resultatet

Kör programmet (F5 i Visual Studio eller `dotnet run` från kommandoraden). Navigera till `C:\Exports\pivot.png` och du bör se en skarp avbildning av din pivottabell, identisk med vad du ser i Excel.

![exempel på export av pivottabell som bild](https://example.com/images/pivot-export.png "exempel på export av pivottabell som bild")

*Bildens alt‑text: exportera pivottabell som bild exempel*

Om bilden ser avklippt ut, justera `ImageOrPrintOptions`‑egenskaperna `HorizontalResolution`, `VerticalResolution` eller `OnePagePerSheet`. Dessa justeringar låter dig **spara pivottabell som bild** med exakt de dimensioner du behöver.

## Vanliga frågor & fallgropar

| Question | Answer |
|----------|--------|
| **Kan jag exportera flera pivoter samtidigt?** | Iterera över `ws.PivotTables` och anropa `ToImage` för varje, och ändra utdatafilnamnet varje gång. |
| **Vad händer om pivoten innehåller diagram?** | Diagram är inte en del av pivotens dataområde, så de visas inte. Exportera diagrammet separat med `Chart.ToImage`. |
| **Fungerar detta med lösenordsskyddade arbetsböcker?** | Ja—ladda arbetsboken med `Workbook(workbookPath, new LoadOptions { Password = "secret" })`. |
| **Hur ändrar jag bakgrundsfärgen?** | Sätt `imageOptions.BackgroundColor = Color.White;` (eller någon `System.Drawing.Color`). |
| **Finns det ett sätt att exportera till JPEG för mindre filstorlek?** | Ändra `ImageFormat = ImageFormat.Jpeg` och sätt eventuellt `imageOptions.JpegQuality = 80`. |

## Proffstips för produktionsklar export

- **Dispose Resources:** Stäng resurser: Wrappa `Workbook` i ett `using`‑block eller anropa `workbook.Dispose()` för att frigöra minne, särskilt vid bearbetning av stora filer.  
- **Thread Safety:** Varje tråd bör ha sin egen `Workbook`‑instans; Aspose.Cells‑objekt är inte trådsäkra.  
- **Logging:** Logga exportvägen och eventuella undantag till en central loggfil för enklare felsökning.  
- **Batch Processing:** Om du behöver generera bilder för dussintals arbetsböcker, överväg ett kö‑system (t.ex. Azure Queue) för att fördela belastningen.  

## Komplett fungerande exempel

Här är hela programmet igen, redo att kopiera‑klistra:

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;
using System.IO;

class ExportPivotImage
{
    static void Main()
    {
        // 1️⃣ Load workbook
        string workbookPath = @"C:\Data\Sample.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // 2️⃣ Get worksheet containing the pivot
        Worksheet ws = workbook.Worksheets["Sheet1"]; // adjust if needed

        // 3️⃣ Grab the first pivot table
        if (ws.PivotTables.Count == 0)
        {
            Console.WriteLine("No pivot tables found on the sheet.");
            return;
        }
        PivotTable pivot = ws.PivotTables[0];

        // 4️⃣ Set image export options (PNG is default)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Uncomment to increase DPI for sharper images
            // HorizontalResolution = 300,
            // VerticalResolution = 300
        };

        // 5️⃣ Ensure output directory exists
        string outputDir = @"C:\Exports";
        Directory.CreateDirectory(outputDir);
        string outputPath = Path.Combine(outputDir, "pivot.png");

        // 6️⃣ Export pivot table as image
        pivot.ToImage(outputPath, imageOptions);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

Att köra den här koden kommer att producera en PNG‑fil med namnet `pivot.png` i `C:\Exports`. Öppna den med någon bildvisare så ser du en exakt visuell kopia av pivottabellen—perfekt för rapporter, e‑post eller webbsidor.

## Slutsats

Vi har precis gått igenom allt du behöver för att **exportera pivottabell som bild** och **spara pivottabell som bild** med C# och Aspose.Cells. Från att ladda arbetsboken till finjustering av bildalternativ är processen enkel och fullt skriptbar.  

Nästa steg? Prova att experimentera med andra format (JPEG, BMP), öka DPI för utskriftskvalitet, eller batch‑processa en mapp med arbetsböcker. Du kan också utforska att exportera hela kalkylbladet som en bild om du behöver omgivande kontext.  

Har du fler frågor eller ett knepigt scenario? Lämna en kommentar nedan, och lycka till med kodningen!

## Relaterade handledningar

- [Skapa en pivottabell i Excel med Aspose.Cells för .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Hur man ändrar pivottabellens källdata med Aspose.Cells för .NET | Dataanalysguide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Behärska pivottabellformatering i .NET med Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}