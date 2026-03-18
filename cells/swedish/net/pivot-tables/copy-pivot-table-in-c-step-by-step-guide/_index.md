---
category: general
date: 2026-03-18
description: Kopiera pivottabell i C# med Aspose.Cells. Lär dig hur du kopierar ett
  Excel‑område, duplicerar en Excel‑pivottabell, kopierar ett område till ett nytt
  blad och kopierar en pivottabell till ett blad på några minuter.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: sv
og_description: Kopiera pivottabell i C# med Aspose.Cells. Lär dig duplicera Excel-pivottabell,
  kopiera Excel-område till en ny plats och kopiera pivottabell till blad med fullständiga
  kodexempel.
og_title: Kopiera pivottabell i C# – Komplett programmeringsguide
tags:
- Aspose.Cells
- C#
- Excel automation
title: Kopiera pivottabell i C# – Steg‑för‑steg‑guide
url: /sv/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopiera pivottabell i C# – Komplett programmeringsguide

Har du någonsin behövt **copy pivot table** från en del av en arbetsbok till en annan, men varit osäker på hur du gör det utan att förlora de underliggande dataanslutningarna? Du är inte ensam. Många utvecklare stöter på detta problem när de automatiserar Excel‑rapporter, särskilt när pivottabellen finns i ett större datablock. Den goda nyheten? Med Aspose.Cells kan du kopiera pivottabellen **exactly as it appears**, och du kommer också att lära dig hur du **copy excel range**, **duplicate excel pivot**, och till och med **copy pivot to sheet** med bara några rader C#.

I den här handledningen går vi igenom ett verkligt scenario: att flytta en pivottabell som upptar *A1:J20* till ett nytt område *M1:V20* i samma kalkylblad. I slutet har du ett körbart program, förstår varför varje steg är viktigt, och vet hur du anpassar koden för andra områden eller till och med separata kalkylblad. Inga externa dokument behövs—allt finns här.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

- **Aspose.Cells for .NET** (version 23.9 eller senare). Du kan hämta det via NuGet: `Install-Package Aspose.Cells`.
- En grundläggande C#‑utvecklingsmiljö (Visual Studio 2022, Rider eller VS Code med C#‑tillägget).
- En Excel‑fil (`source.xlsx`) som innehåller en pivottabell inom området *A1:J20*.

Det är allt. Om du är bekväm med att skapa en konsolapp är du redo att köra.

## Hur man kopierar pivottabell i Aspose.Cells

Kärnan i lösningen är ett enda anrop till `Worksheet.Cells.CopyRange`. Denna metod kopierar inte bara råa cellvärden utan bevarar också pivottabeller, diagram och andra rika objekt automatiskt. Låt oss gå igenom det.

### Steg 1: Ladda källarboken

Först måste vi ladda arbetsboken i minnet.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Varför detta är viktigt:** Att ladda arbetsboken skapar en in‑memory‑representation som Aspose.Cells kan manipulera utan att starta Excel. Det är snabbt, trådsäkert och fungerar på servrar.

### Steg 2: Hämta det första kalkylbladet

De flesta exempel använder det första bladet, men du kan rikta in dig på vilket index eller namn som helst.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tips:** Om du behöver **copy pivot to sheet** istället för samma blad, ändra bara `worksheet`‑referensen till ett annat `Worksheet`‑objekt.

### Steg 3: Definiera käll‑ och målområdena

Vi kommer att använda `CellArea`‑strukturer för att beskriva de block vi flyttar.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Förklaring:** Rad‑ och kolumnindex är nollbaserade. Kolumn 0 = **A**, kolumn 12 = **M**, osv. Justera dessa siffror om din pivottabell finns någon annanstans.

### Steg 4: Utför kopieringsoperationen

Nu händer magin. Att sätta det sista booleska parametern till `true` talar om för Aspose.Cells att kopiera alla objekt—inklusive pivottabellen.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Varför `true`?** Flaggan indikerar “copy all objects”. Om du sätter den till `false` flyttas bara rena cellvärden, och pivottabellen går förlorad.

### Steg 5: Spara arbetsboken

Slutligen, skriv den modifierade arbetsboken tillbaka till disk.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Resultat:** `copy-pivot.xlsx` innehåller nu den ursprungliga pivottabellen på *A1:J20* **och** en identisk kopia på *M1:V20*. Öppna filen i Excel för att verifiera att båda pivottabellerna är funktionella och behåller sina dataanslutningar.

## Kopiera Excel‑område till en ny plats – en snabb variation

Ibland behöver du bara **copy excel range** utan att oroa dig för pivottabeller. Samma `CopyRange`‑metod gör tricket; sätt bara sista argumentet till `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **När du ska använda:** Om du flyttar rådata för ett tillfälligt beräkningsblad, sparar inaktivering av objektkopiering minne och snabbar upp operationen.

## Duplicera excel pivot över flera blad

Vad händer om du vill **duplicate excel pivot** på ett annat kalkylblad? Mönstret är detsamma; du refererar bara ett annat `Worksheet` för destinationen.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Edge case:** Om källpivottabellen använder en tabell som finns på det ursprungliga bladet, kommer Aspose.Cells också att kopiera den underliggande tabelldefinitionen, vilket säkerställer att den nya pivottabellen fungerar direkt.

## Vanliga fallgropar och hur man undviker dem

| Fallgrop | Varför det händer | Lösning |
|----------|-------------------|---------|
| **Pivot förlorar sin cache** | Använder `CopyRange` med `false` eller en anpassad kopieringsrutin som ignorerar objekt. | Skicka alltid `true` när du behöver själva pivottabellen. |
| **Målcellerna innehåller redan data** | Skriver över tyst, vilket kan förstöra befintliga formler. | Rensa målområdet först: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Källområdet inkluderar inte hela pivottabellen** | Pivottabeller sträcker sig över fler rader/kolumner än du förväntar dig (t.ex. dolda rader). | Använd `worksheet.PivotTables[0].DataRange` för att programatiskt hämta de exakta gränserna. |
| **Kopiering mellan arbetsböcker** | `CopyRange` fungerar endast inom samma arbetsbok. | Använd `sourceWorksheet.Cells.CopyRange` till ett temporärt område, sedan `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

## Förväntat resultat & verifiering

Efter att programmet har körts:

1. Öppna `copy-pivot.xlsx`.
2. Du kommer att se två identiska pivottabeller—en på **A1:J20**, en annan på **M1:V20**.
3. Uppdatera någon pivottabell; båda bör återspegla samma underliggande data.
4. Om du duplicerade till ett annat blad, kommer det nya bladet också att innehålla en funktionell kopia.

Ett snabbt sätt att verifiera via kod:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

## Proffstips: Automatisera områdesdetektering

Att hårdkoda `CellArea` fungerar för statiska rapporter, men produktionskod behöver ofta lokalisera pivottabellen dynamiskt.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Varför bry sig?** Detta gör din lösning motståndskraftig mot layoutförändringar—inga fler “Oops, pivottabellen flyttade till B2” fel.

![copy pivot table example](copy-pivot.png){alt="exempel på kopierad pivottabell"}

*Skärmdumpen (platshållare) visar den ursprungliga pivottabellen till vänster och den duplicerade till höger.*

## Sammanfattning

Vi har precis gått igenom hur man **copy pivot table** i C# med Aspose.Cells, utforskat sätt att **copy excel range**, **duplicate excel pivot**, och till och med **copy pivot to sheet** över kalkylblad. De viktigaste slutsatserna är:

- Använd `Worksheet.Cells.CopyRange` med `true`‑flaggan för att bevara rika objekt.
- Definiera käll‑ och mål‑`CellArea`‑objekt med nollbaserade index.
- Justera destinationskalkylbladet om du behöver **copy pivot to sheet**.
- Var uppmärksam på edge cases som befintliga data, dolda rader och scenarier över arbetsböcker.

## Vad blir nästa?

- **Dynamic pivot discovery**: Bygg en hjälpfunktion som skannar en arbetsbok för alla pivottabeller och replikerar dem automatiskt.
- **Export to PDF/HTML**: Efter kopiering kanske du vill rendera bladet till ett rapportformat—Aspose.Cells hanterar det också.
- **Performance tuning**: För enorma arbetsböcker, överväg att inaktivera beräkning innan kopiering och återaktivera den efteråt.

Känn dig fri att experimentera: ändra målkoordinaterna, kopiera till en helt ny arbetsbok, eller till och med loopa över flera kalkylblad för att skapa en samlad rapport. Möjligheterna är oändliga, och med den grund du nu har, kan du anpassa koden till praktiskt taget alla Excel‑automatiseringsuppgifter.

Lycka till med kodandet, och må dina pivottabeller alltid vara perfekt synkroniserade!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}