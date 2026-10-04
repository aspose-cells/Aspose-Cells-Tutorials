---
category: general
date: 2026-10-04
description: Lär dig hur du kopierar en pivottabell från en arbetsbok till en annan
  med C#. Den här guiden täcker också hur du kopierar rader, duplicerar pivottabell
  och kopierar Excel‑område effektivt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: sv
lastmod: 2026-10-04
og_description: Kopiera pivottabell i Excel med C#. Följ den här kompletta handledningen
  för att duplicera pivottabeller, kopiera rader och kopiera Excel‑område med Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Kopiera pivottabell i Excel med C# – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man kopierar pivottabell i Excel med C# och Aspose.Cells
url: /sv/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar pivottabell i Excel med C# och Aspose.Cells

Om du behöver **copy pivot table** från en arbetsbok till en annan, visar den här handledningen en komplett, körbar lösning. Du kommer att se exakt hur du laddar en källfil, definierar området som innehåller pivottabellen, kopierar raderna (inklusive pivottabellens definition) och sparar resultatet. Oavsett om du automatiserar en rapporteringspipeline eller bygger ett migrationsverktyg, låter stegen nedan dig duplicera en pivottabell med bara några rader C#.

Att kopiera en pivottabell är mer än att kopiera cellvärden; den underliggande cachen och fältinställningarna måste följa med. Exemplet använder **Aspose.Cells**-biblioteket eftersom det hanterar pivottabellens metadata automatiskt, så du behöver inte bygga om cachen manuellt. I slutet av den här guiden kommer du att kunna **how to copy pivot**, **copy excel range**, och **how to copy rows** på ett säkert sätt.

## Förutsättningar

- .NET 6.0 eller senare installerat (koden fungerar också med .NET Framework 4.7+).
- En giltig Aspose.Cells för .NET-licens eller en tillfällig utvärderingslicens.
- Två Excel-filer: `Source.xlsx` som innehåller pivottabellen du vill duplicera, och en tom mapp där `CopyWithPivot.xlsx` kommer att skrivas.
- Visual Studio 2022 (eller någon IDE som stödjer C#).

## Steg 1: Ställ in projektet och lägg till Aspose.Cells

Skapa ett nytt konsolprojekt och lägg till Aspose.Cells NuGet-paketet:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

Paketet tillhandahåller klasserna `Workbook`, `Worksheet` och `CellArea` som används i koden nedan.

## Steg 2: Ladda källarboken som innehåller pivottabellen

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Varför detta är viktigt:** Att ladda arbetsboken skapar en in‑memory-representation av alla kalkylblad, inklusive eventuella dolda pivottabellscacher. Utan att ladda filen kan du inte referera till pivottabellens område.

## Steg 3: Definiera cellområdet som täcker pivottabellen

Du måste tala om för Aspose.Cells vilka rader och kolumner som tillhör pivottabellen. `CellArea`-strukturen låter dig specificera ett rektangulärt block.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Tips:** Om du inte är säker på den exakta storleken, öppna källfilen i Excel, markera pivottabellen och notera området som visas i Namnrutan (t.ex. `A1:K31`). Konvertera Excel-koordinaterna till noll‑baserade index för koden.

## Steg 4: Skapa en ny destinationsarbok och hämta dess första kalkylblad

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Varför detta steg krävs:** Destinationsarboken måste finnas innan du kan kopiera rader. Aspose.Cells skapar automatiskt ett standardkalkylblad, som vi kommer att använda som mål.

## Steg 5: Kopiera raderna (inklusive pivottabellen) från källan till destinationen

`CopyRows`-metoden kopierar både cellvärden och den underliggande pivottabellscachen.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **Hur detta fungerar:**  
> - `CopyRows` tar källkalkylbladet, startraden och antalet rader att kopiera.  
> - Den tar också emot destinationskalkylbladet och raden där kopieringen ska börja.  
> - Eftersom källområdet inkluderar pivottabellen, överför metoden pivottabellens cache, fältlista och layout intakt. Detta är kärnan i **how to copy pivot** utan att förlora funktionalitet.

### Kantfall: kopiera en pivottabell som sträcker sig över flera kalkylblad

Om pivottabellens källdata finns på ett annat blad än själva pivottabellen, följer cachen fortfarande kopieringen eftersom Aspose.Cells lagrar cachen i arbetsboken, inte i bladet. Du måste dock säkerställa att destinationsarboken innehåller samma källdataområde; annars kommer pivottabellen att visa `#REF!`-fel. I sådana fall, kopiera först källdataområdet och sedan pivotraderna.

## Steg 6: Spara arbetsboken som nu innehåller den kopierade pivottabellen

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

När programmet körs skapas `CopyWithPivot.xlsx` med en exakt kopia av den ursprungliga pivottabellen, inklusive alla skivare, filter och beräknade fält.

### Förväntat resultat

När du öppnar `CopyWithPivot.xlsx`:

- Pivottabellen visas på samma position (t.ex. A1:K31) som i `Source.xlsx`.
- Alla rad- och kolumnetiketter, totaler och formatering bevaras.
- Uppdatering av pivottabellen visar samma data som källan, vilket bekräftar att cachen kopierades korrekt.

## Hur man kopierar rader utan en pivottabell (copy excel range)

Om du bara behöver **copy excel range** utan någon pivottabelldata, kan du använda samma `CopyRows`-metod men peka på ett område som inte innehåller en pivottabell. Till exempel:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

Detta demonstrerar **how to copy rows** för generiska data, vilket understryker mångsidigheten i samma API.

## Duplicera pivottabell i samma arbetsbok (alternativ metod)

Ibland vill du **duplicate pivot table** inom samma arbetsbok snarare än att skapa en ny fil. Du kan uppnå detta genom att kopiera rader till en annan plats:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

Efter sparning kommer arbetsboken att innehålla två identiska pivottabeller—användbart för jämförelse sida‑vid‑sida eller för att skapa säkerhetskopior.

## Vanliga fallgropar och hur man undviker dem

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Pivot visar `#REF!` efter kopiering | Källdataområdet finns inte i destinationsarboken | Kopiera källdataområdet först, eller använd `CopyRows` på källdatabladsbladet innan du kopierar pivottabellen |
| Formatering förlorad | Endast värden kopierades (t.ex. med `Copy` istället för `CopyRows`) | Använd alltid `CopyRows` som bevarar stil, formatering och pivottabellmetadata |
| Oväntad radförskjutning | Destinations startrad matchar inte källans startrad | Verifiera att `destWorksheet.Cells` startrad matchar den avsedda platsen |
| Stora arbetsböcker ger minnespress | `CopyRows` laddar hela kalkylblad i minnet | Processa kopieringen i delar eller använd streaming‑API:er om du arbetar med >100 000 rader |

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan klistra in i `Program.cs` och köra omedelbart (byt ut `YOUR_DIRECTORY` mot en faktisk sökväg på din maskin).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Kör programmet med `dotnet run`. Efter körning, öppna `CopyWithPivot.xlsx` för att verifiera att pivottabellen visas exakt som i källfilen.

## Slutsats

Du vet nu hur man **copy pivot table** från en Excel-arbetsbok till en annan med C# och Aspose.Cells. Guiden täckte hela arbetsflödet—från att ladda källfilen, definiera pivottabellens cellområde, kopiera rader och spara destinationsarboken. Du har också lärt dig **how to copy rows**, **copy excel range**, och **duplicate pivot table** inom samma fil, samt vanliga fallgropar och bästa praxis‑tips.

Redo för nästa steg? Prova att lägga till kod för att programatiskt uppdatera den kopierade pivottabellen, eller utforska att exportera pivottabellen till PDF med Aspose.Cells. Experimentera med olika källområden, så kommer du snabbt att bemästra Excel‑automation i .NET.

---

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}