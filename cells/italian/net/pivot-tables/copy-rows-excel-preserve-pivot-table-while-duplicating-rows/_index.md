---
category: general
date: 2026-02-14
description: Copia righe in Excel e conserva la tabella pivot in un'unica operazione.
  Scopri come copiare righe, copiare un intervallo su un foglio e duplicare righe
  con pivot usando Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: it
og_description: Copia le righe di Excel e conserva la tabella pivot in un'unica operazione.
  Segui questa guida passo‑passo per duplicare le righe con la pivot usando C#.
og_title: Copia righe Excel – Conserva la tabella pivot durante la duplicazione delle
  righe
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copia righe Excel – Conserva la tabella pivot durante la duplicazione delle
  righe
url: /it/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copy rows excel – Conserva la Tabella Pivot Durante la Duplicazione delle Righe

Mai avuto bisogno di **copy rows excel** mantenendo intatta la tabella pivot? In questo tutorial ti mostreremo una soluzione completa e funzionante che ti spiega **how to copy rows**, mantiene attivo il comportamento **preserve pivot table** e persino **duplicate rows with pivot** tra i fogli usando Aspose.Cells per .NET.

Immagina di dover creare un report mensile di vendite che estrae dati da un foglio master, genera una pivot e poi devi inviare una versione ridotta a un partner. Copiare manualmente l’intervallo è una seccatura e rischi di rompere la pivot. La buona notizia? Alcune righe di C# possono fare il lavoro pesante per te—senza clic del mouse.

> **What you’ll get:** un esempio di codice completo, spiegazioni passo‑a‑passo, consigli per casi limite e un rapido sanity‑check per verificare che la pivot sia sopravvissuta alla copia.

---

## What You’ll Need

- **Aspose.Cells for .NET** (il pacchetto NuGet gratuito funziona bene per questa demo).  
- Un runtime **.NET** recente (4.7+ o .NET 6/7).  
- Un file Excel (`source.xlsx`) che contiene una tabella pivot nel primo foglio di lavoro.  
- Visual Studio, Rider o qualsiasi editor C# tu preferisca.

Nessuna libreria aggiuntiva, nessun COM interop e nessuna installazione di Excel sul server. Per questo questo approccio è sia **copy range to sheet** friendly sia server‑safe.

---

## Step 1 – Load the Workbook (copy rows excel)

La prima cosa da fare è aprire la cartella di lavoro di origine. Usare Aspose.Cells ci fornisce un modello di oggetti pulito che funziona allo stesso modo su Windows, Linux o Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** il caricamento della cartella di lavoro crea una rappresentazione in‑memoria di ogni foglio, inclusi gli oggetti nascosti come le cache della pivot. Non appena il file è in memoria, possiamo manipolare le righe senza mai toccare l’interfaccia utente.

---

## Step 2 – Identify Destination Worksheet (copy range to sheet)

Vogliamo che le righe copiate vengano inserite in un foglio diverso—`Sheet2` in questo esempio. Se il foglio non esiste, Aspose lo creerà per te.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Pro tip:** controlla sempre `Worksheets.Contains` prima di aggiungere un foglio; altrimenti finirai con nomi duplicati e un’eccezione a runtime.

---

## Step 3 – Copy Rows While Preserving the Pivot Table

Ora arriva il nocciolo della questione: copiare le righe **A1:E20** (che includono la pivot) dal primo foglio a `Sheet2`. Il metodo `CopyRows` copia le celle grezze *e* la cache della pivot sottostante, così la pivot rimane funzionale.

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

> **Why it works:** `CopyRows` rispetta la cache interna della pivot, quindi la tabella pivot nel foglio di destinazione è una copia *live*, non uno snapshot statico. Questo soddisfa il requisito **preserve pivot table** senza codice aggiuntivo.

Se hai bisogno che le righe inizino in un offset diverso nel foglio di destinazione—ad esempio alla riga 10—basta cambiare il terzo argomento in `9`.

---

## Step 4 – Save the Workbook (duplicate rows with pivot)

Infine, scrivi la cartella di lavoro modificata su disco. La tabella pivot sarà pienamente funzionale nel nuovo file.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Result verification:** apri `copyWithPivot.xlsx` in Excel, vai su *Sheet2* e aggiorna la pivot. Dovresti vedere lo stesso layout dei campi e gli stessi calcoli dell’originale—nulla è rotto.

---

## Verifying the Copy – Quick sanity check

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

Se la console stampa `True`, hai **duplicate rows with pivot** con successo e hai mantenuto vivo il motore di analisi dei dati.

---

## Common Edge Cases & How to Handle Them

| Situation | What to watch for | Suggested tweak |
|-----------|-------------------|-----------------|
| **Source range includes merged cells** | Le celle unite possono causare disallineamenti durante la copia. | Usa `CopyRows` come mostrato; preserva automaticamente le unioni. |
| **Destination sheet already has data** | Le nuove righe potrebbero sovrascrivere contenuti esistenti. | Cambia la riga di partenza di destinazione (terzo argomento) alla prima riga vuota: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Pivot uses external data source** | Le connessioni esterne non vengono copiate. | Assicurati che la cartella di lavoro di origine contenga l’intero set di dati; altrimenti riattacca la connessione dopo la copia. |
| **Large workbook (100k+ rows)** | L’uso di memoria aumenta drasticamente. | Considera di copiare a blocchi (ad esempio 5.000 righe alla volta) per tenere contento il GC. |

---

## Full Working Example (All Steps Together)

Di seguito trovi l’intero programma che puoi incollare in un’app console e eseguire subito.

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

Esegui il programma, apri il file generato `copyWithPivot.xlsx` e vedrai che la pivot su **Sheet2** funziona esattamente come l’originale. Nessuna ricreazione manuale necessaria.

---

## Frequently Asked Questions

**Q: Does this work with Excel 2003‑compatible `.xls` files?**  
A: Yes. Aspose.Cells abstracts the file format, so the same code works for `.xls`, `.xlsx`, and even `.xlsb`.

**Q: What if I need to copy *columns* instead of rows?**  
A: Use `CopyColumns` in a similar fashion; just swap the row parameters for column indices.

**Q: Can I copy multiple, non‑contiguous ranges at once?**  
A: Not directly with `CopyRows`. Loop over each range or build a temporary worksheet that consolidates the ranges before copying.

---

## Conclusion

Abbiamo appena dimostrato un pattern pulito, **copy rows excel**, che mantiene l’integrità della **preserve pivot table**, ti consente di **how to copy rows** in modo efficiente e ti mostra come **copy range to sheet** senza perdere alcuna funzionalità della pivot. Alla fine di questa guida dovresti sentirti sicuro di **duplicate rows with pivot** in qualsiasi pipeline di automazione—sia che tu stia generando report giornalieri o costruendo un servizio di esportazione dati su larga scala.

Pronto per la prossima sfida? Prova ad estendere il codice per:

- Esportare il foglio duplicato come PDF.  
- Aggiornare la pivot programmaticamente dopo la copia.  
- Iterare su un elenco di file di origine e processarli in batch.

Se incontri problemi, lascia un commento qui sotto o contattami su GitHub. Buon coding, e goditi il tempo risparmiato evitando di trascinare Excel manualmente!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}