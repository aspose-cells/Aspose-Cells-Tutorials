---
category: general
date: 2026-03-29
description: Lär dig hur du kopierar ett område, kopierar pivottabeller, hur du sparar
  en arbetsbok och hur du laddar en arbetsbok i C#. Flytta pivottabeller enkelt med
  steg‑för‑steg‑kod.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: sv
og_description: Hur man kopierar ett område, kopierar pivottabeller, hur man sparar
  en arbetsbok och hur man laddar en arbetsbok i C#. Flytta pivottabeller utan ansträngning
  med tydlig kod.
og_title: Hur man kopierar område med pivottabeller i C# – Komplett guide
tags:
- C#
- Aspose.Cells
- Excel automation
title: Hur man kopierar område med pivottabeller i C# – Komplett guide
url: /sv/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar område med pivottabeller i C# – Komplett guide

Har du någonsin undrat **hur man kopierar område** som innehåller en pivottabell utan att bryta länken till dess källdata? Du är inte ensam. I många verkliga projekt har jag stött på exakt detta problem—Excel‑filer kommer med avancerade pivottabeller, och kravet är att flytta dem eller duplicera datan någon annanstans.  

Den goda nyheten? Lösningen är ganska enkel när du vet **how to load workbook**, gör en kopia och sedan **how to save workbook** igen. I den här handledningen går vi igenom hela processen, inklusive hur man **copy pivot tables**, och till och med ett snabbt tips om **move pivot table** om du behöver den någon annanstans i samma blad.

Vid slutet av den här guiden har du ett fullt fungerande C#‑exempel som:

1. Laddar en befintlig Excel‑fil.  
2. Kopierar ett område (inklusive pivottabellen) till en ny plats.  
3. Sparar den modifierade arbetsboken till en ny fil.

Inga externa skript, ingen manuell hackning—bara ren, repeterbar kod.

---

## Förutsättningar

- **.NET 6+** (någon nyare version fungerar).  
- **Aspose.Cells for .NET** – biblioteket som tillhandahåller `Workbook`, `WorksheetCopyOptions` osv. Du kan installera det via NuGet:

```bash
dotnet add package Aspose.Cells
```

- En inmatningsarbetsbok (`input.xlsx`) som redan innehåller en pivottabell i området `A1:G20`.  
- Grundläggande kunskap om C# och Visual Studio (eller din föredragna IDE).

> **Pro tip:** Om du använder ett annat Excel‑bibliotek (t.ex. EPPlus) är koncepten desamma—byt bara ut API‑anropen.

## Steg 1 – How to load workbook (Primär setup)

Innan vi kan kopiera någonting måste vi läsa in Excel‑filen i minnet.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Varför detta är viktigt:**  
Att ladda arbetsboken ger dig en objektmodell som du kan manipulera. Utan att `how to load workbook` korrekt skulle någon efterföljande kopieringsoperation kasta ett *FileNotFound* eller *InvalidOperation*‑undantag.  

> **Se upp:** Om filen är stor, överväg att använda `LoadOptions` med `MemorySetting` för att kontrollera minnesanvändning.

## Steg 2 – How to copy range (inklusive pivottabellen)

Nu kommer stjärnan i showen: att kopiera ett område som innehåller en pivottabell. Metoden `CopyRange`, i kombination med `WorksheetCopyOptions`, gör det tunga arbetet.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Varför vi sätter `CopyPivotTables = true`:**  
Som standard flyttar en kopiering av ett område bara de råa cellerna. Pivot‑cachen blir kvar, och den kopierade pivottabellen blir en statisk tabell. Genom att sätta `CopyPivotTables` bevaras den levande anslutningen, så den duplicerade pivottabellen fortfarande uppdateras när dess källdata ändras.

**Edge case:** Om målområdet överlappar källområdet kommer Aspose.Cells att kasta ett `ArgumentException`. Välj alltid ett icke‑överlappande mål, eller skapa ett nytt arbetsblad först.

## Steg 3 – How to save workbook (Spara ändringarna)

Efter kopieringen vill du skriva tillbaka ändringarna till disk. Det är här **how to save workbook** kommer in i bilden.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**Vad som händer under huven:**  
`Save` serialiserar den in‑memory‑arbetsboken, inklusive den nykopierade pivottabellen, till ett standard `.xlsx`‑paket. Om du behöver ett annat format (CSV, PDF osv.) ändrar du bara filändelsen eller använder den överlagrade metoden som accepterar `SaveFormat`.  

> **Tips:** Använd `Workbook.Save(string, SaveOptions)` om du behöver skydda filen med ett lösenord eller ställa in andra exportalternativ.

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta, färdiga programmet att köra:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Förväntat resultat:**  
Öppna `output.xlsx`. Du kommer att se den ursprungliga pivottabellen fortfarande i `A1:G20`, och en identisk, fullt funktionell kopia som börjar på `A25`. Båda pivottabellerna pekar på samma källdata, så att uppdatera en uppdaterar den andra.

## Vanliga frågor & variationer

### Kan jag **move pivot table** istället för att kopiera den?

Absolut. Efter kopieringen rensar du helt enkelt det ursprungliga området (eller använder `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) och sedan byter namn på målområdet om det behövs. Detta flyttar i praktiken pivottabellen.

### Vad händer om pivottabellen använder en extern datakälla?

`CopyPivotTables = true` kopierar bara pivottabellens definition, inte den externa anslutningen i sig. Se till att målarbetsboken har åtkomst till samma datakälla, eller återskapa anslutningen efter kopieringen.

### Hur kopierar jag till ett **different worksheet**?

Just pass the destination worksheet object instead of `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Finns det ett sätt att kopiera **multiple ranges** på en gång?

Du kan anropa `CopyRange` upprepade gånger eller använda `CopyRows`/`CopyColumns` för större block. Att loopa över en lista med adresssträngar är ett rent tillvägagångssätt.

## Vanliga fallgropar & Pro Tips

- **Pivot cache size:** Stora pivot‑cacher kan blåsa upp arbetsbokens storlek. Om du bara behöver den visade datan, överväg `CopyPivotTables = false` och använd sedan `PivotTable.RefreshData()` på målet.  
- **File paths:** Använd `Path.Combine` för att undvika hårdkodade separatorer, särskilt på tvärplattform .NET.  
- **Performance:** För enorma arbetsböcker, omslut kopieringen i en `using (var stream = new MemoryStream())` och spara först till strömmen, sedan skriv till disk. Detta minskar I/O‑belastningen.  

## Slutsats

Du vet nu **how to copy range** som innehåller en pivottabell, hur man **copy pivot tables**, och de exakta stegen för **how to load workbook** och **how to save workbook** efter operationen. Oavsett om du behöver **move pivot table** inom samma blad eller till ett annat arbetsblad, förblir mönstret detsamma—ladda, kopiera med rätt alternativ och spara.

Prova det med dina egna filer, justera måladressen och experimentera med olika pivottabellskonfigurationer. Ju mer du leker runt, desto säkrare blir du på att automatisera Excel‑uppgifter i C#.

![Diagram som visar källområdet A1:G20 som kopieras till A25 i samma arbetsblad – hur man kopierar område med pivottabeller](/images/how-to-copy-range-diagram.png "hur man kopierar område med pivottabeller")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}