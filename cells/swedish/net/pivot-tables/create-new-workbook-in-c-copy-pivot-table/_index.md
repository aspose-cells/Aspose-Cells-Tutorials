---
category: general
date: 2026-06-24
description: Skapa en ny arbetsbok i C# och kopiera pivottabellen samtidigt som du
  bevarar dess data. Lär dig hur du kopierar rader, exporterar ett markerat område
  och behåller pivottabellen intakt.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: sv
og_description: Skapa en ny arbetsbok i C# och kopiera en pivottabell samtidigt som
  du bevarar dess data. Steg‑för‑steg‑guide som täcker hur du kopierar rader och exporterar
  ett valt område.
og_title: Skapa ny arbetsbok i C# – Kopiera pivottabell
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Skapa ny arbetsbok i C# – Kopiera pivottabell
url: /sv/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa ny arbetsbok i C# – Kopiera pivottabell

Har du någonsin behövt **create new workbook** i C# bara för att flytta ett utdrag av data som inkluderar en pivottabell? Du är inte ensam. I många rapporteringspipeline tar du ett fåtal rader, kanske några kolumner, och du förväntar dig att pivottabellen förblir exakt som den var—inga brutna referenser, inga saknade beräkningar.  

Den goda nyheten? Med några rader Aspose.Cells kan du **copy pivot table**, behålla den intakt, och till och med **export selected range** utan att bryta något. Nedan ser du ett komplett, färdigt‑att‑köra exempel som visar **how to copy rows**, bevarar pivottabellen och sparar resultatet som en helt ny arbetsbok.

## Vad den här handledningen täcker

- Att sätta upp ett C#-projekt med Aspose.Cells (biblioteket som driver koden).
- Ladda källarbetsboken som innehåller den ursprungliga pivottabellen.
- Använda bibliotekets `CopyRows` och `CopyColumns`-metoder för att duplicera det exakta område du behöver.
- Spara det duplicerade området i ett **create new workbook**-scenario medan pivottabellen förblir funktionell.
- Tips för kantfall som flera pivottabeller, dolda rader och stora datamängder.

I slutet av den här guiden kommer du att kunna **export selected range** från vilken Excel-fil som helst, hålla pivottabellens logik levande, och släppa den nya filen var du än vill.

> **Förutsättning**: Aspose.Cells för .NET (gratis provversion eller licensierad version) installerad via NuGet. Om du ännu inte har lagt till den, kör `dotnet add package Aspose.Cells` i din projektmapp.

---

## Skapa ny arbetsbok och kopiera pivottabell

Nedan är hjärtat i lösningen. Vi går igenom varje rad, förklarar varför den är viktig, och visar sedan hela programmet.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Varför detta fungerar

- **`CopyRows` / `CopyColumns`**: Dessa metoder duplicerar den underliggande celldata *och* de associerade objekten (som en pivotcache). Det är därför pivottabellen förblir funktionell efter flytten.
- **Separate destination workbook**: Genom att skapa en ny `Workbook`-instans **create new workbook** utan någon kvarvarande formatering eller dolda blad som kan störa.
- **Zero‑based indexing**: Aspose.Cells använder nollbaserade index, så `0` pekar på cellen **A1**. Justera `startRow`/`startColumn` om din pivottabell inte är i det övre‑vänstra hörnet.
- **Preserve pivot table**: Pivotens cache finns i samma område, så när du kopierar området kopieras cachen automatiskt. Ingen extra kod behövs.

---

## Hur man kopierar rader utan att bryta pivottabellen

Om du bara är intresserad av rad‑kopieringsdelen kan du isolera den:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: När du kopierar rader som skär en pivottabell, kopiera alltid hela pivottabellens område (*alla* rader + kolumner). Partiella kopior kan lämna pivottabellen med saknade fält, vilket orsakar `#REF!`-fel.

## Exportera valt område – ett verkligt scenario

Föreställ dig att du har en gigantisk försäljningsarbetsbok, men din kund bara vill ha första kvartalets sammanfattning, som finns i rader 1‑20 och kolumner A‑D. Kodsnutten ovan **export selected range** redan åt dig. Ändra bara variablerna `totalRows` och `totalColumns` så att de matchar kundens begäran, så är du klar.

### Hantera dolda rader eller filter

Om källbladet har dolda rader (kanske filtrerade), kan du vilja kopiera endast *synliga* rader. Aspose.Cells erbjuder `CopyRows`-överladdningar som respekterar synlighet:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Sätt den sista booleska till `true` för att kopiera endast synliga rader—perfekt för “export selected range” när användaren har applicerat filter.

## Bevara pivottabell – vanliga fallgropar & hur man undviker dem

| Fallgropar | Varför det händer | Lösning |
|-----------|-------------------|--------|
| **Pivot cache not copied** | Använder vanlig `Range.Copy` istället för `Cells.CopyRows/CopyColumns`. | Håll dig till `Cells`-metoderna som visas. |
| **Destination sheet has existing pivot** | Sparar över en arbetsbok som redan innehåller en pivottabell med samma namn. | Börja med en ny `Workbook()` (som vi gör). |
| **Named ranges break** | Källpivottabellen refererar ett namngivet område som inte finns i den nya filen. | Kopiera även det namngivna området: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Pivottabellen pekar på en extern datakälla som inte är tillgänglig. | Använd `PivotTable.RefreshData()` efter kopiering om behövs. |

## Fullständigt end‑to‑end‑exempel (klart att köra)

Nedan är hela programmet, inklusive `using`-direktiven och ett kort konsol‑UI. Kopiera‑klistra in det i ett nytt Console App‑projekt och tryck **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Förväntad output** (i konsolen):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Öppna `copy-pivot.xlsx` så kommer du att se samma pivottabell som du hade i `source.xlsx`, fullt funktionell och refererande till det kopierade dataområdet.

## Vanliga frågor

**Q: Fungerar detta med flera pivottabeller på samma blad?**  
A: Ja, så länge den kopierade rektangeln omger varje pivottabell du behöver. Om du bara vill ha en, justera `rows`/`cols` för att isolera den.

**Q: Vad händer om källarbetsboken använder externa datakopplingar?**  
A: Pivotcachen kommer fortfarande att peka på den ursprungliga anslutningen. Anropa `pivotTable.RefreshData()` efter att ha laddat destinationen om du vill göra om‑frågan mot källan.

**Q: Kan jag kopiera pivottabellen till ett annat blad i samma arbetsbok?**  
A: Absolut. Ersätt `destinationWorkbook` med `sourceWorkbook` och välj ett annat arbetsbladsindex.

**Q: Finns det ett sätt att bara kopiera formatering?**  
A: Använd `CopyRows`/`CopyColumns`‑överladdningar som accepterar ett `CopyOptions`-objekt—sätt `CopyOptions.CopyType = CopyType.ValuesOnly` eller `CopyType.All` beroende på dina behov.

## Slutsats

Vi har just gått igenom ett **create new workbook**-scenario som **copy pivot table**, **preserve pivot table**, och **export selected range**—allt i ren C#

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa en ny pivottabell programatiskt i .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [Hur man ändrar pivottabellens källdata med Aspose.Cells för .NET | Dataanalysguide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Hur man hanterar Excel-pivottabellens kompatibilitet med Aspose.Cells för .NET | Dataanalysguide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}