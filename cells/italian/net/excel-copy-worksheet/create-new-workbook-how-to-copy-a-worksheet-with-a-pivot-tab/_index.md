---
category: general
date: 2026-03-01
description: Crea una nuova cartella di lavoro e copia il foglio di lavoro in una
  cartella di lavoro con una tabella pivot. Impara come esportare la tabella pivot,
  copiare il foglio e copiare la pivot in C#.
draft: false
keywords:
- create new workbook
- copy worksheet to workbook
- export pivot table
- how to copy sheet
- how to copy pivot
language: it
og_description: Crea una nuova cartella di lavoro in C# e copia il foglio di lavoro
  nella cartella mantenendo la tabella pivot. Guida passo passo con codice completo.
og_title: Crea nuova cartella di lavoro – Copia foglio di lavoro e tabella pivot in
  C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Crea nuova cartella di lavoro – Come copiare un foglio di lavoro con una tabella
  pivot
url: /it/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea nuovo workbook – Copia foglio di lavoro e tabella pivot in C#

Hai mai avuto bisogno di **creare un nuovo workbook** che contenga una tabella pivot pronta all'uso senza ricrearla da zero? Non sei l'unico. In molti scenari di reporting hai un file master (`src.xlsx`) con una pivot complessa, e vuoi inviare una copia pulita (`dest.xlsx`) a un cliente o a un altro sistema. La buona notizia? Puoi farlo in sole due righe di C# — e questa guida ti mostrerà esattamente come.

Passeremo in rassegna l'intero processo: caricare il workbook di origine, copiare il primo foglio di lavoro (che contiene la pivot) e salvarlo come un nuovo workbook. Alla fine saprai **come copiare un foglio** che contiene una pivot, come **esportare i dati della tabella pivot** se ne hai bisogno, e anche alcuni trucchi per casi particolari come copiare in un file esistente.

## Prerequisiti

- .NET 6.0 o versioni successive (qualsiasi versione recente va bene)
- Aspose.Cells per .NET (versione di prova gratuita o licenziata) – questa libreria fornisce la classe `Workbook` utilizzata di seguito.
- Un file Excel di origine (`src.xlsx`) che contiene già una tabella pivot nel suo primo foglio di lavoro.

Se non hai ancora Aspose.Cells, aggiungilo tramite NuGet:

```bash
dotnet add package Aspose.Cells
```

È tutto—nessun COM interop aggiuntivo, nessun Excel installato sul server.

## Cosa copre questo tutorial

- **Create new workbook** da un foglio di lavoro esistente che contiene una pivot.
- **Copy worksheet to workbook** preservando tutte le definizioni della pivot.
- **Export pivot table** dati in un DataTable (opzionale).
- Problemi comuni quando si utilizza **how to copy pivot** in ambienti diversi.
- Un esempio completo e eseguibile che puoi inserire in un'app console.

---

## Passo 1: Carica il workbook di origine (Come copiare un foglio)

La prima cosa da fare è aprire il workbook che contiene la tabella pivot. Usare Aspose.Cells rende questo processo indolore perché legge il file in memoria senza avviare Excel.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the pivot
        string srcPath = @"YOUR_DIRECTORY\src.xlsx";

        // Load the workbook – this is where we **create new workbook** later
        Workbook sourceWorkbook = new Workbook(srcPath);
```

> **Perché è importante:** Caricare il file verifica che la pivot esista e ti dà accesso alla collezione di fogli di lavoro. Se il file è corrotto, `Workbook` lancia un'eccezione chiara, risparmiandoti output misteriosi in seguito.

## Passo 2: Copia il foglio di lavoro in un nuovo workbook (Copia foglio di lavoro in workbook)

Ora effettuiamo realmente **copy worksheet to workbook**. Il metodo `CopyTo` di Aspose.Cells clona l'intero foglio—incluse formule, formattazione e cache della pivot—in un nuovo file.

```csharp
        // Destination path for the new workbook
        string destPath = @"YOUR_DIRECTORY\dest.xlsx";

        // Copy the first worksheet (index 0) which contains the pivot
        sourceWorkbook.Worksheets[0].CopyTo(destPath);
```

> **Consiglio professionale:** `CopyTo` crea un nuovo workbook dietro le quinte, quindi non è necessario istanziare un altro oggetto `Workbook`. Questo mantiene basso l'uso della memoria e garantisce che la definizione della pivot rimanga intatta.

## Passo 3: Verifica la pivot copiata (Come copiare la pivot)

Dopo che la copia è terminata, è una buona idea aprire il nuovo file e confermare che la pivot funzioni ancora. Puoi farlo programmaticamente o semplicemente aprirlo in Excel.

```csharp
        // Optional: Load the destination workbook to verify
        Workbook destWorkbook = new Workbook(destPath);
        Worksheet copiedSheet = destWorkbook.Worksheets[0];

        // Find the first pivot table on the copied sheet
        PivotTable pivot = copiedSheet.PivotTables[0];

        Console.WriteLine($"Pivot name: {pivot.Name}");
        Console.WriteLine($"Data source range: {pivot.DataSource}");
        Console.WriteLine($"Number of rows in pivot cache: {pivot.CacheDefinition.RecordCount}");
    }
}
```

Eseguendo il programma stampa qualcosa del genere:

```
Pivot name: PivotTable1
Data source range: A1:D100
Number of rows in pivot cache: 100
```

Se vedi questi valori, il passo **how to copy pivot** è riuscito.

## Passo 4: (Opzionale) Esporta i dati della tabella pivot in un DataTable

A volte hai bisogno dei numeri grezzi della pivot senza aprire Excel. Aspose.Cells ti consente di estrarre i dati della pivot in un `DataTable`—perfetto per ulteriori elaborazioni o risposte API.

```csharp
        // Export pivot data to a DataTable
        DataTable pivotData = pivot.ExportDataTable(pivot.RowFields[0].Name, 
                                                   pivot.ColumnFields[0].Name,
                                                   true);

        // Display a few rows in the console
        foreach (DataRow row in pivotData.Rows)
        {
            Console.WriteLine(string.Join("\t", row.ItemArray));
        }
```

> **Perché potresti volerlo:** L'esportazione ti permette di **export pivot table** contenuti in un database, payload JSON, o qualsiasi altro formato senza copia‑incolla manuale.

## Passo 5: Casi limite e problemi comuni

### Copiare in un workbook esistente

Se devi **copy worksheet to workbook** che contiene già altri fogli, usa la sovraccarico che accetta un'istanza `Workbook` di destinazione:

```csharp
        Workbook targetWorkbook = new Workbook(); // empty workbook
        sourceWorkbook.Worksheets[0].CopyTo(targetWorkbook);
        targetWorkbook.Save(@"YOUR_DIRECTORY\combined.xlsx");
```

### Preservare le fonti dati esterne

Le tabelle pivot che si collegano a connessioni esterne (ad es., Power Query) possono perdere il collegamento dopo la copia. In questi casi, imposta `pivot.RefreshDataOnOpen = true` prima di salvare:

```csharp
        pivot.RefreshDataOnOpen = true;
```

### File di grandi dimensioni e prestazioni

Per file più grandi di 50 MB, considera di abilitare `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;` per ridurre la pressione sulla memoria.

---

![Esempio di creazione nuovo workbook](https://example.com/images/create-new-workbook.png "Crea nuovo workbook")

*Testo alternativo immagine: crea nuovo workbook – copia di un foglio di lavoro con una tabella pivot*

## Esempio completo funzionante (Tutti i passi combinati)

Di seguito trovi l'applicazione console completa, pronta per l'esecuzione. Copia‑incolla in un nuovo `.csproj` e premi **F5**.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace CopyPivotDemo
{
    class Program
    {
        static void Main()
        {
            // ==============================
            // 1️⃣ Load the source workbook
            // ==============================
            string srcPath = @"YOUR_DIRECTORY\src.xlsx";
            Workbook sourceWorkbook = new Workbook(srcPath);

            // ==============================
            // 2️⃣ Copy the first worksheet (pivot) to a new workbook
            // ==============================
            string destPath = @"YOUR_DIRECTORY\dest.xlsx";
            sourceWorkbook.Worksheets[0].CopyTo(destPath);

            // ==============================
            // 3️⃣ Verify the copied pivot (how to copy pivot)
            // ==============================
            Workbook destWorkbook = new Workbook(destPath);
            Worksheet copiedSheet = destWorkbook.Worksheets[0];
            PivotTable pivot = copiedSheet.PivotTables[0];

            Console.WriteLine($"Pivot name: {pivot.Name}");
            Console.WriteLine($"Data source range: {pivot.DataSource}");
            Console.WriteLine($"Cache rows: {pivot.CacheDefinition.RecordCount}");

            // ==============================
            // 4️⃣ (Optional) Export pivot data
            // ==============================
            if (pivot.RowFields.Count > 0 && pivot.ColumnFields.Count > 0)
            {
                DataTable dt = pivot.ExportDataTable(
                    pivot.RowFields[0].Name,
                    pivot.ColumnFields[0].Name,
                    true);

                Console.WriteLine("\n--- Pivot Data Preview ---");
                foreach (DataRow row in dt.Rows)
                {
                    Console.WriteLine(string.Join("\t", row.ItemArray));
                }
            }

            Console.WriteLine("\nDone! New workbook created at: " + destPath);
        }
    }
}
```

### Risultato atteso

- `dest.xlsx` appare in `YOUR_DIRECTORY`.
- Il primo foglio appare esattamente come l'originale, completo di tabella pivot.
- L'esecuzione della console stampa i metadati della pivot e un piccolo anteprima dei dati, confermando che la copia è riuscita.

## Conclusione

Ora sai come **create new workbook** copiando un foglio di lavoro che contiene una tabella pivot, come **copy worksheet to workbook**, e anche come **export pivot table** dati per l'elaborazione a valle. Che tu stia costruendo un servizio di reporting, automatizzando la distribuzione di Excel, o abbia semplicemente bisogno di un modo rapido per duplicare una pivot, i passaggi sopra ti offrono una soluzione affidabile e pronta per la produzione.

**Prossimi passi** che potresti esplorare:

- Combina più fogli (usa `CopyTo` ripetutamente) – perfetto per impacchettare un report completo.
- Regola le impostazioni di aggiornamento della cache della pivot quando i dati di origine cambiano.
- Usa le tecniche **how to copy sheet** per duplicare grafici, immagini o moduli VBA.
- Approfondisci `WorkbookDesigner` di Aspose.Cells per la generazione di report basati su template.

Provalo, modifica i percorsi, e vedrai quanto è facile distribuire workbook puliti e pronti per le pivot. Hai domande su casi limite o licenze? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}