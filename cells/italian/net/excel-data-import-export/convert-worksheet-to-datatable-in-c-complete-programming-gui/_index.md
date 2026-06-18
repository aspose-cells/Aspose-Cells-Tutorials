---
category: general
date: 2026-06-17
description: Converti il foglio di lavoro in DataTable in C# rapidamente. Scopri come
  leggere un file Excel in DataTable C# ed esportare Excel in DataTable C# con codice
  reale.
draft: false
keywords:
- convert worksheet to datatable
- read excel file into datatable c#
- load excel workbook c#
- export excel to datatable c#
language: it
og_description: Converti il foglio di lavoro in DataTable in C# velocemente. Questo
  tutorial mostra come leggere un file Excel in DataTable C# ed esportare Excel in
  DataTable C# con un esempio completo.
og_title: Converti foglio di lavoro in DataTable in C# – Guida completa
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Convert worksheet to DataTable in C# quickly. Learn how to read Excel
    file into DataTable C# and export Excel to DataTable C# with real code.
  headline: Convert Worksheet to DataTable in C# – Complete Programming Guide
  type: TechArticle
tags:
- C#
- Excel
- DataTable
title: Converti foglio di lavoro in DataTable in C# – Guida completa alla programmazione
url: /it/net/excel-data-import-export/convert-worksheet-to-datatable-in-c-complete-programming-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convert Worksheet to DataTable in C# – Complete Programming Guide

Hai mai dovuto **convertire un foglio di lavoro in DataTable** ma non sapevi quale API chiamare? Non sei l'unico: molti sviluppatori incontrano questo ostacolo quando automatizzano report o importano dati Excel in un database. La buona notizia? Con poche righe di C# puoi leggere un file Excel in un `DataTable` e essere pronto a eseguire query LINQ, inserimenti massivi o qualsiasi altra operazione successiva.

In questa guida vedremo come caricare una cartella di lavoro Excel, estrarre il primo foglio e **export excel to DataTable C#**—niente magia, solo codice chiaro. Alla fine avrai un metodo riutilizzabile che trasforma qualsiasi foglio di lavoro in un `DataTable` tipizzato. (E sì, copriremo anche lo scenario “read Excel file into DataTable C#” per chi preferisce una soluzione in una sola riga.)

## Prerequisiti – Cosa ti serve

Prima di iniziare, assicurati di avere:

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.6+)
- Un riferimento a **Aspose.Cells** (o qualsiasi altra libreria che offra `ExportDataTable`; l’esempio usa Aspose perché è semplice)
- Un file Excel (`.xlsx`) che vuoi elaborare
- Un IDE C# di base (Visual Studio, Rider o VS Code)

Questo è tutto—nessun pacchetto NuGet aggiuntivo oltre alla libreria Excel stessa. Pronto? Iniziamo.

## Step 1: Load Excel Workbook C# – Getting the File into Memory

Prima di tutto: dobbiamo **load excel workbook c#**. Pensa al workbook come al contenitore che ospita tutti i fogli, gli stili e i metadati. Aprirlo correttamente evita di bloccare il file o di perdere risorse.

```csharp
using Aspose.Cells;
using System.Data;

// Path to your input file – change as needed
string excelPath = @"C:\Data\input.xlsx";

// Load the workbook; the constructor reads the file into memory
Workbook workbook = new Workbook(excelPath);
```

> **Perché è importante:** La classe `Workbook` astrae il formato di file a basso livello, così non devi analizzare XML manualmente. Inoltre rilascia lo stream sottostante quando l'oggetto esce dallo scope, prevenendo errori di file‑in‑use.

### Pro tip
Se lavori con fogli di calcolo enormi, considera l'uso di `LoadOptions` per abilitare **memory‑optimized loading**:

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook workbook = new Workbook(excelPath, options);
```

## Step 2: Access the Desired Worksheet – Usually the First One

La maggior parte degli script rapidi prende semplicemente il primo foglio, ma puoi scegliere qualsiasi foglio per nome o indice. Ecco l'approccio classico “primo foglio”, che copre il caso d'uso **convert worksheet to DataTable** per file semplici.

```csharp
// Grab the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Optional: verify the sheet isn’t empty
if (sheet.Cells.MaxDataRow < 0 || sheet.Cells.MaxDataColumn < 0)
{
    throw new InvalidOperationException("The worksheet appears to be empty.");
}
```

> **Caso limite:** Se il tuo workbook contiene fogli nascosti o ti serve una scheda specifica, sostituisci `0` con `workbook.Worksheets["MySheet"]`.

## Step 3: Configure Export Options – Export As String for Predictable Types

Quando converti in un `DataTable`, spesso vuoi che ogni cella sia una stringa per evitare problemi di conversione di tipo in seguito. Questo è esattamente ciò che fa il flag **export excel to datatable c#**.

```csharp
// Set up options so every cell is treated as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true   // forces string output for all cells
};
```

Perché forzare le stringhe? Perché le celle Excel possono contenere date, numeri o formule. Esportando tutto come testo eviti incongruenze di tipo colonna quando successivamente inserisci i dati in una tabella SQL.

## Step 4: Perform the Export – The Core Convert Worksheet to DataTable Logic

Ora avviene la magia. Chiamiamo `ExportDataTable` sull'oggetto `Worksheet`, passando riga/colonna di partenza, numero totale di righe/colonne, un flag per includere le intestazioni di colonna e le nostre opzioni.

```csharp
// Determine the used range
int totalRows = sheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int totalCols = sheet.Cells.MaxDataColumn + 1;   // +1 for the same reason

// Export the used range to a DataTable
DataTable dataTable = sheet.ExportDataTable(
    0,                 // start row (0‑based)
    0,                 // start column (0‑based)
    totalRows,
    totalCols,
    true,              // include column names as first row
    exportOptions);
```

### Cosa ottieni
`dataTable` ora rispecchia il foglio di lavoro:

| Column1 | Column2 | Column3 |
|---------|---------|---------|
| Row1‑A  | Row1‑B  | Row1‑C  |
| Row2‑A  | Row2‑B  | Row2‑C  |
| …       | …       | …       |

Tutti i valori sono stringhe, rendendo prevedibile l'elaborazione successiva.

## Step 5: Verify the Result – Quick sanity check (read excel file into datatable c#)

Un modo veloce per confermare che la conversione sia riuscita è stampare le prime righe sulla console. Questo dimostra anche il pattern **read excel file into datatable c#** in pratica.

```csharp
Console.WriteLine("First 5 rows of the imported DataTable:");
for (int i = 0; i < Math.Min(5, dataTable.Rows.Count); i++)
{
    var row = dataTable.Rows[i];
    Console.WriteLine(string.Join(" | ", row.ItemArray));
}
```

Se vedi i valori separati da pipe come previsto, hai completato con successo il **convert worksheet to DataTable**.

## Step 6: Wrap It Up – A Reusable Helper Method

La maggior parte dei progetti avrà bisogno di questa conversione in più punti, quindi raccogliamo tutto in un unico metodo statico. Così la chiamata **read excel file into datatable c#** diventa semplice come una riga.

```csharp
public static DataTable WorksheetToDataTable(string filePath, int sheetIndex = 0, bool exportAsString = true)
{
    // Load the workbook
    Workbook wb = new Workbook(filePath);

    // Grab the requested sheet
    Worksheet ws = wb.Worksheets[sheetIndex];

    // Prepare export options
    ExportTableOptions opts = new ExportTableOptions
    {
        ExportAsString = exportAsString
    };

    // Determine used range
    int rows = ws.Cells.MaxDataRow + 1;
    int cols = ws.Cells.MaxDataColumn + 1;

    // Export and return
    return ws.ExportDataTable(0, 0, rows, cols, true, opts);
}
```

Esempio d'uso:

```csharp
DataTable myTable = WorksheetToDataTable(@"C:\Data\input.xlsx");
```

Questa è tutta la storia—niente loop extra, niente interop COM, solo dati tipizzati e puliti.

## Common Pitfalls & How to Avoid Them

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| **File locked by another process** | Opening the workbook without `LoadOptions` can keep the file handle open. | Use `LoadOptions` with `MemorySetting.MemoryPreference` or wrap the `Workbook` in a `using` block. |
| **Missing column headers** | If the first row contains data instead of headers, `ExportDataTable` will treat it as data. | Pass `false` for the `includeColumnNames` parameter and add column names manually. |
| **Mixed data types cause exceptions** | When `ExportAsString` is `false`, numeric cells become `double`, dates become `DateTime`. | Keep `ExportAsString = true` unless you need strong typing, then handle conversions yourself. |
| **Very large sheets cause OutOfMemory** | Exporting millions of rows at once can blow the heap. | Export in chunks: loop over row blocks and concatenate `DataTable`s. |

## Bonus: Export Multiple Sheets at Once

Se devi **export excel to datatable c#** per ogni foglio, basta iterare su `workbook.Worksheets`:

```csharp
var tables = new Dictionary<string, DataTable>();
foreach (Worksheet ws in workbook.Worksheets)
{
    tables[ws.Name] = ws.ExportDataTable(
        0, 0,
        ws.Cells.MaxDataRow + 1,
        ws.Cells.MaxDataColumn + 1,
        true,
        exportOptions);
}
```

Ora `tables` contiene un `DataTable` per foglio, indicizzato dal nome del foglio—utile per importazioni batch.

## Conclusion

Ti abbiamo guidato da un file Excel vuoto a un `DataTable` completamente popolato usando un flusso di lavoro conciso **convert worksheet to DataTable**. I passaggi hanno coperto il caricamento del workbook, la selezione del foglio, la configurazione delle opzioni di esportazione e infine il trasferimento dei dati in un `DataTable`. Con il metodo helper riutilizzabile ora puoi **read excel file into datatable c#** ovunque nel tuo codice, e disponi anche di un pattern per **export excel to datatable c#** su più fogli.

Cosa fare dopo? Prova a inserire il `DataTable` risultante in un `BulkInsert` di Entity Framework, genera report CSV o applica filtri LINQ per estrarre insight. Il cielo è il limite una volta che i dati Excel vivono in memoria come una tabella vera e propria.

Hai domande o un file Excel ostinato che non riesci a gestire? Lascia un commento qui sotto, e buona programmazione!

## What Should You Learn Next?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci alternativi nei tuoi progetti.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Export Excel Data to DataTable Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}