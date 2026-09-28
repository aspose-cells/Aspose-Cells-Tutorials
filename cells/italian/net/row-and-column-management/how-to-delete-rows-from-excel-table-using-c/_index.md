---
category: general
date: 2026-09-27
description: Scopri come eliminare righe da una tabella Excel in C# con una guida
  passo‑passo che mostra anche come caricare rapidamente un workbook Excel in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: it
lastmod: 2026-09-27
og_description: Elimina righe da una tabella Excel in C# con un esempio chiaro. Questo
  tutorial copre anche come caricare un workbook Excel in C# e gestire i casi limite
  più comuni.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Elimina righe da una tabella Excel in C# – guida completa al codice
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: Come eliminare righe da una tabella Excel usando C#
url: /it/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eliminare righe da una tabella Excel in C# – guida completa di programmazione

Se hai bisogno di **eliminare righe da una tabella Excel** in un file .xlsx, questo tutorial ti mostra esattamente come farlo con C#. Vedrai un esempio conciso e eseguibile che carica una cartella di lavoro Excel, rimuove righe specifiche dalla prima tabella e salva il risultato. L'approccio funziona con la popolare libreria Aspose.Cells e può essere adattato ad altre API Excel per .NET.

Rimuovere righe da una tabella è un'operazione comune quando si puliscono dati importati, si riducono sezioni di report o si automatizzano gli aggiornamenti dei fogli di calcolo. Alla fine di questa guida sarai in grado di **caricare una cartella di lavoro Excel C#**, individuare una tabella (ListObject), eliminare le righe che desideri e scrivere il file modificato su disco.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate (il codice funziona anche con .NET Framework 4.7+).
* Un riferimento al pacchetto NuGet **Aspose.Cells** (o a qualsiasi libreria compatibile che espone i tipi `Workbook`, `Worksheet` e `ListObject`).
* Un file di input chiamato `input.xlsx` posizionato in una cartella a cui puoi fare riferimento dal tuo progetto.
* Familiarità di base con la sintassi C# e Visual Studio (o il tuo IDE preferito).

> **Suggerimento:** Se preferisci un'alternativa open‑source, la stessa logica può essere applicata con **ClosedXML** – basta sostituire le classi specifiche di Aspose con `XLWorkbook`, `IXLWorksheet` e `IXLTable`.

## Passo 1: Caricare la cartella di lavoro Excel in C#

La prima operazione è leggere il file sorgente in memoria. Caricare la cartella di lavoro è poco costoso per le dimensioni tipiche dei fogli di calcolo e ti offre pieno accesso a fogli, tabelle e valori delle celle.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Perché è importante:* `Workbook` analizza la struttura Open XML del file .xlsx, esponendo una collezione di oggetti `Worksheet`. Se il file non viene trovato, Aspose genera una `FileNotFoundException`, quindi assicurati che il percorso sia corretto.

## Passo 2: Accedere al foglio di lavoro target

La maggior parte dei fogli di calcolo contiene più fogli; devi scegliere quello che contiene la tabella che vuoi modificare. Qui usiamo il primo foglio (`Worksheets[0]`), che è un valore predefinito sicuro per file semplici.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Perché è importante:* `Worksheet` è il contenitore per le tabelle (`ListObjects`). Accedere al foglio corretto previene modifiche accidentali a dati non correlati.

## Passo 3: Eliminare righe da una tabella Excel

Le tabelle Excel sono rappresentate da oggetti `ListObject`. La prima tabella sul foglio è `ListObjects[0]`. Il metodo `DeleteRows(startIndex, rowCount)` rimuove le righe **relative all'area dati della tabella**, non ai numeri di riga assoluti del foglio.  

In questo esempio eliminiamo la seconda e la terza riga della tabella (l'intestazione è la riga 0, quindi iniziamo dall'indice 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### E se la tabella ha un nome o una posizione diversa?

* **Tabella con nome:** Usa `ws.ListObjects["MyTableName"]` invece dell'indice.  
* **Tabelle multiple:** Scorri `ws.ListObjects` e scegli quella che corrisponde a una condizione (ad es., nomi delle intestazioni di colonna).  
* **Conteggio righe dinamico:** Puoi calcolare `rowCount` a runtime ispezionando `ws.ListObjects[0].DataRange.RowCount`.

### Gestione dei casi limite

| Situazione                              | Modifica di codice consigliata                                      |
|----------------------------------------|---------------------------------------------------------------------|
| La tabella è vuota o ha meno righe      | Verifica `ws.ListObjects[0].DataRange.RowCount` prima di eliminare. |
| Le righe da eliminare superano la dimensione della tabella       | Limita `rowCount` a `DataRange.RowCount - startIndex`.               |
| È necessario eliminare righe in base a una condizione (ad es., valore nella colonna C) | Itera `DataRange.Rows` e raccogli gli indici corrispondenti, quindi elimina in ordine inverso per mantenere gli indici stabili. |

## Passo 4: Salvare la cartella di lavoro modificata

Dopo l'eliminazione, scrivi la cartella di lavoro su un nuovo file (o sovrascrivi l'originale se preferisci). Il salvataggio crea un nuovo .xlsx che riflette la tabella aggiornata.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Perché è importante:* `Save` serializza la rappresentazione in memoria su disco. Se devi preservare il file originale, scrivi sempre su un percorso diverso.

## Esempio completo e eseguibile

Unendo tutti i passaggi ottieni un programma autonomo che puoi copiare, incollare ed eseguire.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Output previsto** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Apri `output.xlsx` – la prima tabella ora non contiene le righe che hai rimosso, mentre la riga di intestazione rimane intatta.

## Domande frequenti e variazioni

### Come elimino righe da **tutte** le tabelle in una cartella di lavoro?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Posso eliminare righe in base a un **valore di cella**?

Sì. Scansiona il `DataRange` per le celle corrispondenti, raccogli i loro indici a base zero, quindi elimina in ordine decrescente:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### E se devo **preservare la formattazione**?

`DeleteRows` rimuove l'intera riga dalla tabella ma mantiene lo stile della tabella per le righe rimanenti. Se devi conservare una formattazione specifica su una riga che stai eliminando, copia lo stile su un'altra riga prima dell'eliminazione.

### Funziona con i file **.xls** (Excel 97‑2003)?

Sì. Aspose.Cells rileva automaticamente il formato del file, quindi lo stesso codice funziona con `.xls`. Basta cambiare l'estensione del file nel costruttore `Workbook`.

## Suggerimenti sulle prestazioni

* **Eliminazioni batch:** Eliminare molte righe una alla volta può essere più lento. Usa una singola chiamata `DeleteRows(start, count)` quando possibile.  
* **Evitare il blocco del thread UI:** Se integri questo in un'app desktop, esegui la manipolazione della cartella di lavoro su un thread in background per mantenere l'interfaccia reattiva.  
* **Gestire correttamente le risorse:** Sebbene Aspose.Cells utilizzi memoria gestita, avvolgi il `Workbook` in un blocco `using` se lavori con file di grandi dimensioni per liberare le risorse tempestivamente.

## Conclusione

Ora hai un esempio completo e pronto per la produzione che **elimina righe da una tabella Excel** usando C#. La guida ha mostrato come **caricare una cartella di lavoro Excel C#**, individuare il `ListObject` desiderato, rimuovere le righe in modo sicuro e salvare il file aggiornato. Con la gestione dei casi limite e i consigli sulle prestazioni inclusi, puoi adattare questo modello a scenari più complessi come eliminazioni condizionali, tabelle multiple o librerie Excel .NET alternative.

### Prossimi passi

* Esplora **ClosedXML** o **EPPlus** se preferisci uno stack completamente open‑source.  
* Combina l'eliminazione di righe con la **validazione dei dati** per pulire i fogli prima di importarli in un database.  
* Automatizza il processo per una cartella di cartelle di lavoro usando `Directory.GetFiles` e un ciclo.

Sentiti libero di sperimentare con diversi intervalli di righe, nomi di tabelle e logica condizionale. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Caricare file Excel C# – Come eliminare righe e rimuovere righe specifiche](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Come inserire ed eliminare righe in Excel con Aspose.Cells per .NET: Guida completa](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Come eliminare righe vuote in Excel usando Aspose.Cells .NET per la pulizia dei dati](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}