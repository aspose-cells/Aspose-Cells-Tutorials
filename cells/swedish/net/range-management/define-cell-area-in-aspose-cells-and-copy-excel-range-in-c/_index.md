---
category: general
date: 2026-08-04
description: Definiera cellområde i Aspose.Cells och lär dig hur du kopierar pivottabeller,
  kopierar Excel‑område i C# och kopierar område i samma blad effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: sv
lastmod: 2026-08-04
og_description: Definiera cellområde i Aspose.Cells och kopiera Excel‑område i C#
  samtidigt som pivottabeller bevaras. Följ den här steg‑för‑steg‑guiden för pålitliga
  resultat.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Definiera cellområde i Aspose.Cells – kopiera Excel‑område i C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Definiera cellområde i Aspose.Cells och kopiera Excel‑område i C#
url: /sv/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definiera cellområde i Aspose.Cells och kopiera Excel‑intervall i C#

Om du behöver **definiera cellområde** för ett intervall och sedan kopiera det intervallet på samma kalkylblad, visar den här guiden exakt hur du gör det med Aspose.Cells för .NET. Oavsett om du flyttar en pivottabell‑driven rapport eller duplicerar ett datablock, lär du dig hela processen på bara några steg.

Du får också reda på **hur man kopierar pivottabeller** utan att förlora deras anslutningar, och ser ett rent exempel på **copy excel range c#** som fungerar i scenariot **copy range same sheet**. Inga externa verktyg behövs – bara Aspose.Cells och några rader C#.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
- Aspose.Cells för .NET (NuGet‑paket `Aspose.Cells`)
- En Excel‑arbetsbok (`input.xlsx`) som innehåller en pivottabell i intervallet A1:J50
- En utvecklingsmiljö som Visual Studio 2022

## Steg 1: Definiera cellområdet för källintervallet

Den första uppgiften är att **definiera cellområde** som representerar blocket du vill kopiera. Aspose.Cells använder strukturen `CellArea`, som lagrar noll‑baserade rad‑ och kolumnindex.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Varför detta är viktigt:** `CellArea` talar om för Aspose.Cells exakt vilka celler som ska bearbetas. Genom att använda noll‑baserade index undviker du off‑by‑one‑fel som ofta uppstår när man översätter Excels A1‑notation till kod.

## Steg 2: Definiera destinations‑cellområdet på samma kalkylblad

För att **copy range same sheet** måste du också ange var data ska placeras. Destinationen kan börja på vilken rad som helst; här börjar vi på rad 61 (noll‑baserat index 60) för att lämna ett tomt mellanrum.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Varför detta är viktigt:** Genom att spegla källans dimensioner säkerställer du att det kopierade blocket passar perfekt utan avklippning.

## Steg 3: Kopiera intervallet samtidigt som pivottabeller bevaras

Nu kan du **how to copy pivot** på ett säkert sätt. Klassen `CopyOptions` innehåller flaggan `CopyPivotTables` som behåller pivottabellens definition, datakälla och formatering.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Varför detta är viktigt:** Utan att sätta `CopyPivotTables = true` blir pivottabellen en statisk ögonblicksbild och förlorar interaktiviteten. Detta alternativ kopierar den underliggande cachen och anslutningarna, så den nya pivottabellen beter sig exakt som originalet.

## Steg 4: Spara arbetsboken

Till sist skriver du tillbaka ändringarna till disk. Utdatafilen visar att pivottabellen har duplicerats på samma blad.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Proffstips:** Använd `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` om du måste tvinga fram ett specifikt format, särskilt när du arbetar med äldre Excel‑versioner.

## Steg 5: Verifiera den kopierade pivottabellen

Öppna `CopyWithPivot.xlsx` i Excel och kontrollera följande:

1. Intervallet A61:J110 innehåller en kopia av de ursprungliga data.
2. En ny pivottabell visas högst upp i det kopierade intervallet.
3. När du uppdaterar pivottabellen reflekteras förändringar i källdata, vilket bekräftar att **how to copy pivot** lyckades.

Om pivottabellen inte uppdateras, kontrollera att källdata‑intervallet i pivottabellens definition fortfarande pekar på det ursprungliga arbetsboksområdet. Aspose.Cells uppdaterar automatiskt källreferensen när `CopyPivotTables` är true.

## Kantfall och variationer

| Situation | Vad som ska ändras |
|-----------|--------------------|
| **Kopiera till ett annat kalkylblad** | Byt ut `srcWorkbook.Worksheets[0]` mot mål‑kalkylbladets index eller namn, och justera `destinationRange` därefter. |
| **Kopiera ett sammanslaget cellblock** | Sätt `CopyOptions.PasteType = PasteType.All` för att bevara sammanslagna celler och formatering. |
| **Kopiera endast värden, inte formler** | Använd `CopyOptions.PasteType = PasteType.Values` för att undvika att överföra formler som refererar till originalbladet. |
| **Stora intervall ( > 10 000 rader )** | Överväg att använda `Workbook.Copy` för hela kalkylblad för att förbättra prestanda, och radera sedan oönskade rader. |

Dessa variationer visar att samma **aspose.cells copy range**‑logik kan anpassas till många verkliga scenarier.

## Fullständigt fungerande exempel

Nedan finns hela, färdiga programmet. Byt ut `YOUR_DIRECTORY` mot en faktisk mapp‑sökväg på din maskin.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Förväntad utdata:** Efter att programmet har körts innehåller `CopyWithPivot.xlsx` de ursprungliga data plus ett identiskt block som startar på rad 61, komplett med en fungerande pivottabell.

## Slutsats

Du vet nu hur du **definierar cellområde** i Aspose.Cells, **copy excel range c#**, och **copy range same sheet** samtidigt som all pivottabellsfunktionalitet bevaras. Denna teknik eliminerar manuella kopierings‑ och klistra‑fel och fungerar även för stora arbetsböcker.

Utforska nästa steg, som **how to copy pivot** över flera kalkylblad, eller använd **aspose.cells copy range** för att duplicera hela blad med formatering. Experimentera med olika `CopyOptions`‑inställningar för att skräddarsy kopieringsbeteendet efter ditt projekts behov.

Lycka till med kodandet!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra fler API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}