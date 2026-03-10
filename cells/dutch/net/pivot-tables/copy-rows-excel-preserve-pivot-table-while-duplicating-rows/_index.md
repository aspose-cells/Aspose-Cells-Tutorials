---
category: general
date: 2026-02-14
description: Rijen kopiëren in Excel en de draaitabel in één keer behouden. Leer hoe
  je rijen kopieert, een bereik naar een blad kopieert en rijen dupliceert met een
  draaitabel met behulp van Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: nl
og_description: Kopieer rijen in Excel en behoud de draaitabel in één keer. Volg deze
  stapsgewijze handleiding om rijen te dupliceren met een draaitabel met behulp van
  C#.
og_title: Rijen kopiëren Excel – Draaitabel behouden bij het dupliceren van rijen
tags:
- Aspose.Cells
- C#
- Excel automation
title: Rijen kopiëren Excel – Behoud draaitabel bij het dupliceren van rijen
url: /nl/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copy rows excel – Preserveer draaitabel tijdens het dupliceren van rijen

Ever needed to **copy rows excel** while keeping the pivot table intact? In this tutorial we’ll walk through a complete, runnable solution that shows you **how to copy rows**, keep the **preserve pivot table** behavior alive, and even **duplicate rows with pivot** across sheets using Aspose.Cells for .NET.

Imagine you’re building a monthly sales report that pulls data from a master sheet, runs a pivot, and then you have to ship a trimmed‑down version to a partner. Manually copying the range is a pain, and you risk breaking the pivot. The good news? A few lines of C# can do the heavy lifting for you—no mouse clicks required.

> **What you’ll get:** a full code sample, step‑by‑step explanations, tips for edge cases, and a quick sanity‑check to verify that the pivot survived the copy.

---

## Wat je nodig hebt

- **Aspose.Cells for .NET** (the free NuGet package works fine for this demo).  
- A recent **.NET runtime** (4.7+ or .NET 6/7).  
- An Excel file (`source.xlsx`) that contains a pivot table on the first worksheet.  
- Visual Studio, Rider, or any C# editor you like.

No additional libraries, no COM interop, and no Excel installation on the server. That’s why this approach is both **copy range to sheet** friendly and server‑safe.

---

## Stap 1 – Laad de werkmap (copy rows excel)

The very first thing is to open the source workbook. Using Aspose.Cells gives us a clean object model that works the same on Windows, Linux, or Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** loading the workbook creates an in‑memory representation of every worksheet, including hidden objects like pivot caches. As soon as the file is in memory, we can manipulate rows without ever touching the UI.

---

## Stap 2 – Identificeer doelwerkblad (copy range to sheet)

We want the copied rows to land on a different sheet—`Sheet2` in this example. If the sheet doesn’t exist, Aspose will create it for you.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Pro tip:** always check `Worksheets.Contains` before adding a sheet; otherwise you’ll end up with duplicate names and a runtime exception.

---

## Stap 3 – Kopieer rijen terwijl de draaitabel behouden blijft

Now comes the heart of the matter: copying rows **A1:E20** (which include the pivot) from the first sheet to `Sheet2`. The `CopyRows` method copies the raw cells *and* the underlying pivot cache, so the pivot stays functional.

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

> **Why it works:** `CopyRows` respects the internal pivot cache, so the pivot table on the destination sheet is a *live* copy, not a static snapshot. This satisfies the **preserve pivot table** requirement without extra code.

If you need the rows to start at a different offset on the destination sheet—say row 10—you’d simply change the third argument to `9`.

---

## Stap 4 – Sla de werkmap op (duplicate rows with pivot)

Finally, write the modified workbook back to disk. The pivot table will be fully functional in the new file.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Result verification:** open `copyWithPivot.xlsx` in Excel, go to *Sheet2*, and refresh the pivot. You should see the same field layout and calculations as the original—nothing broken.

---

## Verifying the Copy – Quick sanity check

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

If the console prints `True`, you’ve successfully **duplicate rows with pivot** and kept the data analysis engine alive.

---

## Veelvoorkomende randgevallen & hoe ze op te lossen

| Situatie | Waar op te letten | Aanbevolen aanpassing |
|-----------|-------------------|-----------------|
| **Bronbereik bevat samengevoegde cellen** | Samengevoegde cellen kunnen bij het kopiëren voor misalignement zorgen. | Gebruik `CopyRows` zoals getoond; het behoudt automatisch de samenvoegingen. |
| **Doelblad bevat al gegevens** | Nieuwe rijen kunnen bestaande inhoud overschrijven. | Verander de startrij van het doel (derde argument) naar de eerste lege rij: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Draaitabel gebruikt externe gegevensbron** | Externe verbindingen worden niet gekopieerd. | Zorg ervoor dat de bronwerkmap de volledige dataset bevat; anders koppel je de verbinding opnieuw na het kopiëren. |
| **Grote werkmap (100k+ rijen)** | Geheugengebruik piekt. | Overweeg om in delen te kopiëren (bijv. 5.000 rijen per keer) om de GC tevreden te houden. |

---

## Volledig werkend voorbeeld (Alle stappen samen)

Below is the entire program you can paste into a console app and run immediately.

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

Run the program, open the generated `copyWithPivot.xlsx`, and you’ll see that the pivot on **Sheet2** works exactly like the original. No manual re‑creation required.

---

## Veelgestelde vragen

**Q: Werkt dit met Excel 2003‑compatibele `.xls` bestanden?**  
A: Ja. Aspose.Cells abstracteert het bestandsformaat, dus dezelfde code werkt voor `.xls`, `.xlsx`, en zelfs `.xlsb`.

**Q: Wat als ik *kolommen* in plaats van rijen moet kopiëren?**  
A: Gebruik `CopyColumns` op een vergelijkbare manier; vervang gewoon de rij‑parameters door kolomindices.

**Q: Kan ik meerdere, niet‑aaneengesloten bereiken in één keer kopiëren?**  
A: Niet direct met `CopyRows`. Loop over elk bereik of bouw een tijdelijke werkblad die de bereiken consolideert vóór het kopiëren.

---

## Conclusie

We’ve just demonstrated a clean, **copy rows excel** pattern that **preserve pivot table** integrity, lets you **how to copy rows** efficiently, and shows you how to **copy range to sheet** without losing any pivot functionality. By the end of this guide you should feel confident to **duplicate rows with pivot** in any automation pipeline—whether you’re generating daily reports or building a large‑scale data‑export service.

Ready for the next challenge? Try extending the code to:

- Export the duplicated sheet as a PDF.  
- Refresh the pivot programmatically after copying.  
- Loop over a list of source files and batch‑process them.

If you hit any snags, drop a comment below or ping me on GitHub. Happy coding, and enjoy the time you saved by not dragging Excel around manually!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}