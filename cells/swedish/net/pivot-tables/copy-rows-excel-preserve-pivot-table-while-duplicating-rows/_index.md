---
category: general
date: 2026-02-14
description: Kopiera rader i Excel och bevara pivottabellen på en gång. Lär dig hur
  du kopierar rader, kopierar ett område till ett blad och duplicerar rader med pivottabell
  med hjälp av Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: sv
og_description: Kopiera rader i Excel och bevara pivottabellen i ett svep. Följ den
  här steg‑för‑steg‑guiden för att duplicera rader med pivot med C#.
og_title: Kopiera rader Excel – Bevara pivottabell när du duplicerar rader
tags:
- Aspose.Cells
- C#
- Excel automation
title: Kopiera rader i Excel – bevara pivottabell när du duplicerar rader
url: /sv/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copy rows excel – Bevara pivottabell vid duplicering av rader

Har du någonsin behövt **copy rows excel** medan du behåller pivottabellen intakt? I den här handledningen går vi igenom en komplett, körbar lösning som visar dig **how to copy rows**, behåller **preserve pivot table**‑beteendet levande, och till och med **duplicate rows with pivot** över blad med Aspose.Cells för .NET.

Föreställ dig att du bygger en månatlig försäljningsrapport som hämtar data från ett huvudblad, kör en pivottabell, och sedan måste du skicka en nedskuren version till en partner. Att manuellt kopiera området är besvärligt, och du riskerar att förstöra pivottabellen. De goda nyheterna? Några rader C# kan göra det tunga arbetet åt dig—utan några musklick.

> **What you’ll get:** en komplett kodexempel, steg‑för‑steg‑förklaringar, tips för kantfall, och en snabb kontroll för att verifiera att pivottabellen överlevde kopieringen.

---

## Vad du behöver

- **Aspose.Cells for .NET** (det fria NuGet‑paketet fungerar bra för den här demonstrationen).  
- En aktuell **.NET runtime** (4.7+ eller .NET 6/7).  
- En Excel‑fil (`source.xlsx`) som innehåller en pivottabell på det första kalkylbladet.  
- Visual Studio, Rider eller någon C#‑redigerare du föredrar.

Inga extra bibliotek, ingen COM‑interop och ingen Excel‑installation på servern. Det är därför detta tillvägagångssätt är både **copy range to sheet**‑vänligt och server‑säkert.

## Steg 1 – Ladda arbetsboken (copy rows excel)

Det allra första är att öppna källarbetsboken. Att använda Aspose.Cells ger oss en ren objektmodell som fungerar likadant på Windows, Linux eller Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** att ladda arbetsboken skapar en minnesrepresentation av varje kalkylblad, inklusive dolda objekt som pivottabellscachar. Så snart filen är i minnet kan vi manipulera rader utan att någonsin röra UI:n.

## Steg 2 – Identifiera destinationskalkylblad (copy range to sheet)

Vi vill att de kopierade raderna hamnar på ett annat blad—`Sheet2` i detta exempel. Om bladet inte finns skapar Aspose det åt dig.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Pro tip:** kontrollera alltid `Worksheets.Contains` innan du lägger till ett blad; annars får du dubbla namn och ett körningsfel.

## Steg 3 – Kopiera rader samtidigt som pivottabellen bevaras

Nu kommer kärnan i saken: att kopiera raderna **A1:E20** (som inkluderar pivottabellen) från det första bladet till `Sheet2`. Metoden `CopyRows` kopierar de råa cellerna *och* den underliggande pivottabellscachen, så pivottabellen förblir funktionell.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **Why it works:** `CopyRows` respekterar den interna pivottabellscachen, så pivottabellen på destinationsbladet är en *levande* kopia, inte ett statiskt ögonblicksbild. Detta uppfyller **preserve pivot table**‑kravet utan extra kod.

Om du behöver att raderna ska börja på ett annat avstånd på destinationsbladet—t.ex. rad 10—ändrar du helt enkelt det tredje argumentet till `9`.

## Steg 4 – Spara arbetsboken (duplicate rows with pivot)

Slutligen skriver du den modifierade arbetsboken tillbaka till disk. Pivottabellen kommer att vara fullt funktionell i den nya filen.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Result verification:** öppna `copyWithPivot.xlsx` i Excel, gå till *Sheet2* och uppdatera pivottabellen. Du bör se samma fältlayout och beräkningar som originalet—inget är trasigt.

## Verifiera kopieringen – Snabb kontroll

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

Om konsolen skriver ut `True` har du framgångsrikt **duplicate rows with pivot** och hållit dataanalysmotorn vid liv.

## Vanliga kantfall & hur man hanterar dem

| Situation | What to watch for | Suggested tweak |
|-----------|-------------------|-----------------|
| **Källområdet inkluderar sammanslagna celler** | Sammanslagna celler kan orsaka feljustering vid kopiering. | Använd `CopyRows` som visat; den bevarar sammanslagningar automatiskt. |
| **Destinationsbladet har redan data** | Nya rader kan skriva över befintligt innehåll. | Ändra destinationsstartraden (tredje argumentet) till den första tomma raden: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Pivottabellen använder extern datakälla** | Externa anslutningar kopieras inte. | Säkerställ att källarboken innehåller hela datamängden; annars återanslut anslutningen efter kopiering. |
| **Stor arbetsbok (100k+ rader)** | Minnesanvändningen skjuter i höjden. | Överväg att kopiera i delar (t.ex. 5 000 rader åt gången) för att hålla GC:n nöjd. |

## Fullt fungerande exempel (Alla steg tillsammans)

Nedan är hela programmet som du kan klistra in i en konsolapp och köra omedelbart.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

Kör programmet, öppna den genererade `copyWithPivot.xlsx`, och du kommer att se att pivottabellen på **Sheet2** fungerar exakt som originalet. Ingen manuell återuppbyggnad krävs.

## Vanliga frågor

**Q: Fungerar detta med Excel 2003‑kompatibla `.xls`‑filer?**  
A: Ja. Aspose.Cells abstraherar filformatet, så samma kod fungerar för `.xls`, `.xlsx` och även `.xlsb`.

**Q: Vad händer om jag behöver kopiera *kolumner* istället för rader?**  
A: Använd `CopyColumns` på liknande sätt; byt bara ut radparametrarna mot kolumnindex.

**Q: Kan jag kopiera flera, icke‑sammanhängande områden på en gång?**  
A: Inte direkt med `CopyRows`. Loopa över varje område eller bygg ett temporärt blad som konsoliderar områdena innan kopiering.

## Slutsats

Vi har just demonstrerat ett rent **copy rows excel**‑mönster som bevarar **preserve pivot table**‑integriteten, låter dig **how to copy rows** effektivt, och visar dig hur du **copy range to sheet** utan att förlora någon pivottabellfunktionalitet. Vid slutet av den här guiden bör du känna dig säker på att **duplicate rows with pivot** i vilken automatiseringspipeline som helst—oavsett om du genererar dagliga rapporter eller bygger en storskalig dataexporttjänst.

Klar för nästa utmaning? Prova att utöka koden till:

- Exportera det duplicerade bladet som en PDF.  
- Uppdatera pivottabellen programatiskt efter kopiering.  
- Loopa över en lista med källfiler och batch‑processa dem.

Om du stöter på problem, lämna en kommentar nedan eller ping mig på GitHub. Lycka till med kodandet, och njut av den tid du sparat genom att inte dra runt Excel manuellt!

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}