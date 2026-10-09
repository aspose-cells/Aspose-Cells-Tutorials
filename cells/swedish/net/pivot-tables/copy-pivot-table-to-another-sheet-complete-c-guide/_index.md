---
category: general
date: 2026-06-27
description: Kopiera pivottabell till ett annat blad i C# med Aspose.Cells. Lär dig
  steg för steg hur du bevarar pivottabellens data och formatering.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: sv
og_description: Kopiera pivottabell till ett annat blad i C# med Aspose.Cells. Denna
  handledning visar exakt hur du duplicerar en pivottabell samtidigt som du behåller
  dess formatering intakt.
og_title: Kopiera pivottabell till ett annat blad – komplett C#-guide
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Kopiera pivottabell till ett annat blad – Komplett C#‑guide
url: /sv/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell till ett annat blad – Komplett C#-guide

Har du någonsin behövt **kopiera pivottabell till ett annat blad** men oroat dig för att du skulle förlora slicers, beräknade fält eller formatering? Du är inte ensam. Många utvecklare stöter på detta problem när de automatiserar Excel‑rapporter, och frustrationen är verklig. I den här guiden går vi igenom en ren, end‑to‑end‑lösning som **bevarar pivottabellen** exakt som den visas.

Vi kommer att använda **Aspose.Cells for .NET**, ett kraftfullt bibliotek som låter dig manipulera Excel‑filer utan att någonsin öppna Excel själv. I slutet av den här tutorialen har du ett färdigt C#‑kodexempel som kopierar en pivottabell från ett kalkylblad till ett annat, och behåller alla underliggande datakopplingar intakta.

## Vad den här tutorialen täcker

- Att sätta upp ett .NET‑projekt och lägga till Aspose.Cells‑paketet via NuGet.  
- Ladda en befintlig arbetsbok som redan innehåller en pivottabell.  
- Definiera både källintervallet (den ursprungliga pivottabellen) och målintervallet på ett annat blad.  
- Använda `CopyOptions` för att **bevara pivottabellen** vid kopiering.  
- Spara resultatet och verifiera att pivottabellen fungerar på sin nya plats.  

Inga externa verktyg, ingen manuell kopiera‑och‑klistra, och ingen dold magi—bara enkel kod som du kan slänga in i vilken C#‑konsolapp eller tjänst som helst.

> **Varför du bör bry dig:** Att automatisera duplicering av pivottabeller sparar timmar av manuellt arbete, särskilt i nattliga rapporteringspipelines där dussintals arbetsböcker behöver identiska pivottabellstrukturer över flera blad.

---

## Steg 1: Sätt upp projektet och lägg till Aspose.Cells

Först och främst. Om du inte redan har gjort det, skapa ett nytt .NET‑konsolprojekt:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Lägg nu till Aspose.Cells‑paketet:

```bash
dotnet add package Aspose.Cells
```

> **Proffstips:** Använd den senaste stabila versionen (från juni 2026 v23.12). Den innehåller buggfixar för hantering av `CopyPivotTable`.

## Steg 2: Ladda arbetsboken och få åtkomst till kalkylblad

Öppna arbetsboken som innehåller källpivottabellen. I de flesta verkliga scenarier ligger filen på en gemensam enhet, men för den här demonstrationen antar vi att den finns i en lokal mapp som heter `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Här skapar vi ett nytt blad med namnet **CopyDestination** där pivottabellen kommer att placeras. Om du redan har ett målblad, hämta det bara via index eller namn.

## Steg 3: Definiera käll- och målintervall

En pivottabell finns i ett rektangulärt cellblock. Du måste tala om för Aspose.Cells vilket block som ska kopieras. I det här exemplet sträcker sig pivottabellen över rader 0‑20 och kolumner 0‑10 (nollbaserad indexering).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Observera hur vi beräknar slutraden och -kolumnen dynamiskt. På så sätt justeras målet automatiskt även om du senare ändrar storleken på källintervallet.

## Steg 4: Utför kopieringen samtidigt som pivottabellen bevaras

Nu händer magin. Genom att skicka ett `CopyOptions`‑objekt med `CopyPivotTable = true` vet Aspose.Cells att behålla pivottabellens definition intakt.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Bakom kulisserna återskapar Aspose.Cells pivottabellscachen, uppdaterar referensen till datakällan och återapplicerar all formatering. Detta är den **Excel‑pivottabellduplicering** du har letat efter.

## Steg 5: Spara och verifiera resultatet

Till sist skriver du arbetsboken tillbaka till disk. Du kan låta originalfilen förbli orörd genom att spara under ett nytt namn.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Öppna den resulterande `copy-pivot.xlsx` så ser du att pivottabellen är perfekt replikerad på bladet **CopyDestination**, komplett med slicers, beräknade fält och formatering. Den underliggande datakällan pekar fortfarande på den ursprungliga tabellen, så uppdatering fungerar exakt som tidigare.

> **Vad händer om källpivottabellen sträcker sig över ett dynamiskt område?**  
> Använd `Worksheet.PivotTables[0].CacheDefinition.SourceData` för att hämta de faktiska gränserna, och bygg sedan `sourceRange` utifrån den informationen. Detta hanterar fall där rader eller kolumner kan expandera över tid.

## Bonus: Bevara pivottabellens formatering över kopior

Ibland förlorar standardkopieringen villkorsstyrd formatering eller anpassade talformat. För att skydda mot detta, utöka `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Genom att aktivera `CopyFormatting` säkerställs att kravet **bevara pivottabellens formatering** uppfylls, vilket ger dig en pixel‑perfekt kopia.

## Förväntat resultat

När du kör programmet avslutas konsolen tyst (såvida du inte lägger till loggning). Att öppna `copy-pivot.xlsx` bör visa:

- Blad 1: Ursprungliga data och pivottabell oförändrade.  
- **CopyDestination**: En exakt kopia av pivottabellen, placerad med start på rad 31 (eftersom rader är 1‑baserade i Excels UI).  
- Alla slicers och filter fungerar; genom att klicka på “Refresh” uppdateras båda pivottabellerna samtidigt.

## Slutsats

Vi har just demonstrerat hur man **kopierar pivottabell till ett annat blad** med Aspose.Cells i C#. Stegen—att sätta upp projektet, ladda arbetsboken, definiera intervall, kopiera med `CopyPivotTable = true` och spara—utgör ett pålitligt mönster som du kan återanvända i vilken automatiseringspipeline som helst.

Om du vill gå längre, överväg:

- **Excel‑pivottabellduplicering** över flera arbetsböcker (loopa igenom filer).  
- Att använda **Aspose.Cells kopieringsintervall med pivottabell**‑alternativet för att flytta pivottabeller mellan olika arbetsböcker.  
- Automatisera uppdateringar med `PivotTable.RefreshData()` efter kopiering.

Känn dig fri att experimentera med olika källintervall, eller kombinera denna teknik med diagramgenerering för helt automatiserade rapporteringsdashboards. Har du frågor? Lämna en kommentar, och lycka till med kodandet!

![Skärmbild som visar kopierad pivottabell i nytt blad](copy-pivot-screenshot.png "exempel på kopiera pivottabell till ett annat blad")

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man ändrar pivottabellens källdata med Aspose.Cells för .NET | Dataanalysguide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Behärska pivottabellformatering i .NET med Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Åtkomst till pivottabellens externa datakällor i .NET med Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}