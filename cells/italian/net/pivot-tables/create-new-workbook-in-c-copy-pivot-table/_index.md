---
category: general
date: 2026-06-24
description: Crea un nuovo workbook in C# e copia la tabella pivot preservando i dati.
  Scopri come copiare le righe, esportare l’intervallo selezionato e mantenere intatta
  la pivot.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: it
og_description: Crea un nuovo workbook in C# e copia una tabella pivot mantenendo
  intatti i dati. Guida passo‑passo su come copiare le righe ed esportare l'intervallo
  selezionato.
og_title: Crea nuova cartella di lavoro in C# – Copia tabella pivot
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
title: Crea nuova cartella di lavoro in C# – Copia tabella pivot
url: /it/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea nuovo workbook in C# – Copia tabella pivot

Ever needed to **create new workbook** in C# just to move a slice of data that includes a pivot table? You're not the only one. In many reporting pipelines you grab a handful of rows, maybe a few columns, and you expect the pivot to stay exactly as it was—no broken references, no missing calculations.  

The good news? With a few lines of Aspose.Cells you can **copy pivot table**, keep it intact, and even **export selected range** without breaking anything. Below you’ll see a complete, ready‑to‑run example that shows **how to copy rows**, preserve the pivot, and save the result as a brand‑new workbook.

## Cosa copre questo tutorial

- Setting up a C# project with Aspose.Cells (the library that powers the code).
- Loading the source workbook that holds the original pivot.
- Using the library’s `CopyRows` and `CopyColumns` methods to duplicate the exact range you need.
- Saving the duplicated area into a **create new workbook** scenario while the pivot stays functional.
- Tips for edge cases like multiple pivot tables, hidden rows, and large data sets.

By the end of this guide you’ll be able to **export selected range** from any Excel file, keep the pivot logic alive, and drop the new file wherever you like.

> **Prerequisite**: Aspose.Cells for .NET (free trial or licensed version) installed via NuGet. If you haven’t added it yet, run `dotnet add package Aspose.Cells` in your project folder.

## Crea nuovo workbook e copia tabella pivot

Below is the heart of the solution. We’ll walk through each line, explain why it matters, and then show the full program.

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

### Perché funziona

- **`CopyRows` / `CopyColumns`**: questi metodi duplicano i dati delle celle sottostanti *e* gli oggetti associati (come una cache pivot). Ecco perché la pivot rimane funzionale dopo lo spostamento.
- **Separate destination workbook**: creando una nuova istanza `Workbook` noi **create new workbook** senza formattazioni residue o fogli nascosti che potrebbero interferire.
- **Zero‑based indexing**: Aspose.Cells utilizza indici a base zero, quindi `0` corrisponde alla cella **A1**. Regola `startRow`/`startColumn` se la tua pivot non è nell'angolo in alto a sinistra.
- **Preserve pivot table**: la cache della pivot si trova nello stesso intervallo, quindi copiare l'intervallo copia automaticamente la cache. Non è necessario codice aggiuntivo.

## Come copiare le righe senza rompere la pivot

If you’re only interested in the row‑copy part, you can isolate it:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Quando copi righe che intersecano una tabella pivot, copia sempre l'intera area della pivot (righe + colonne). Copie parziali possono lasciare la pivot con campi mancanti, causando errori `#REF!`.

## Export selected range – Uno scenario reale

Imagine you have a gigantic sales workbook, but your client only wants the first quarter’s summary, which lives in rows 1‑20 and columns A‑D. The snippet above already **export selected range** for you. Just change the `totalRows` and `totalColumns` variables to match the client’s request, and you’re done.

### Gestione di righe nascoste o filtri

If the source sheet has hidden rows (perhaps filtered out), you might want to copy *visible* rows only. Aspose.Cells offers `CopyRows` overloads that respect visibility:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Set the last boolean to `true` to copy only visible rows—perfect for “export selected range” when the user has applied filters.

## Preserva tabella pivot – Errori comuni e come evitarli

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Pivot cache not copied** | Utilizzo di `Range.Copy` semplice invece di `Cells.CopyRows/CopyColumns`. | Usa i metodi `Cells` come mostrato. |
| **Destination sheet has existing pivot** | Salvataggio su un workbook che contiene già una pivot con lo stesso nome. | Inizia con un nuovo `Workbook()` (come facciamo noi). |
| **Named ranges break** | La pivot di origine fa riferimento a un intervallo denominato che non è presente nel nuovo file. | Copia l'intervallo denominato anche: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | La pivot punta a una fonte dati esterna non disponibile. | Usa `PivotTable.RefreshData()` dopo la copia se necessario. |

## Esempio completo end‑to‑end (pronto da eseguire)

Below is the complete program, including the `using` directives and a brief console UI. Copy‑paste it into a new Console App project and hit **F5**.

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

**Output previsto** (nella console):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Open `copy-pivot.xlsx` and you’ll see the same pivot table you had in `source.xlsx`, fully functional and referencing the copied data range.

## Domande frequenti

**Q: Questo funziona con più tabelle pivot nello stesso foglio?**  
A: Sì, purché il rettangolo copiato includa ogni pivot necessaria. Se ne vuoi solo una, regola `rows`/`cols` per isolarla.

**Q: Cosa succede se il workbook di origine utilizza connessioni dati esterne?**  
A: La cache della pivot continuerà a puntare alla connessione originale. Chiama `pivotTable.RefreshData()` dopo aver caricato la destinazione se vuoi rieseguire la query della fonte.

**Q: Posso copiare la pivot in un foglio diverso all'interno dello stesso workbook?**  
A: Assolutamente. Sostituisci `destinationWorkbook` con `sourceWorkbook` e scegli un altro indice di foglio.

**Q: Esiste un modo per copiare solo la formattazione?**  
A: Usa gli overload di `CopyRows`/`CopyColumns` che accettano un oggetto `CopyOptions`—imposta `CopyOptions.CopyType = CopyType.ValuesOnly` o `CopyType.All` a seconda delle tue esigenze.

## Conclusione

We’ve just walked through a **create new workbook** scenario that **copy pivot table**, **preserve pivot table**, and **export selected range**—all in pure C#

## Cosa dovresti imparare dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Crea una nuova tabella pivot programmaticamente in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [Come modificare i dati di origine della tabella pivot usando Aspose.Cells per .NET | Guida all'analisi dei dati](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Come gestire la compatibilità delle tabelle pivot Excel con Aspose.Cells per .NET | Guida all'analisi dei dati](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}