---
category: general
date: 2026-03-18
description: Come esportare i dati di Excel in un DataTable in C# con codice che gestisce
  celle specifiche, converte Excel in DataTable e formatta i numeri. Scopri come esportare
  celle specifiche e altro.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: it
og_description: Come esportare i dati di Excel in una DataTable in C#. Questo tutorial
  mostra come esportare celle specifiche, convertire Excel in DataTable e formattare
  i numeri con facilità.
og_title: Come esportare Excel in una DataTable in C# – Guida completa
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Come esportare Excel in una DataTable in C# – Guida passo passo
url: /it/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel in un DataTable in C# – Guida passo‑passo

Ti sei mai chiesto **come esportare i dati di Excel** in un `DataTable` senza perdere la formattazione? Non sei l'unico—gli sviluppatori hanno costantemente bisogno di estrarre una porzione di un foglio di calcolo in memoria per report, convalida o operazioni di inserimento massivo. La buona notizia? Con poche righe di C# puoi esportare un intervallo preciso (ad esempio *A1:F11*), forzare ogni cella a essere trattata come stringa e persino applicare un formato numerico personalizzato.

In questo tutorial copriremo tutto ciò che devi sapere: dal caricamento della cartella di lavoro, alla configurazione di **export specific cells**, alla conversione dell'intervallo in un `DataTable`, e alla gestione di casi particolari come righe vuote o numeri dipendenti dalla locale. Alla fine avrai un metodo riutilizzabile che funziona con scenari **excel to datatable c#** in codice di produzione.

> **Prerequisiti** – Avrai bisogno della libreria Aspose.Cells per .NET (o di qualsiasi API simile che offra `ExportDataTable`). L'esempio presuppone .NET 6+, ma i concetti si applicano anche alle versioni precedenti.

---

## Cosa imparerai

- Come **convertire Excel in DataTable** usando Aspose.Cells.
- Esportare un intervallo personalizzato (`excel range to datatable`) trattando tutti i valori come stringhe.
- Applicare un formato numerico a due cifre decimali (`#,#00.00`) durante l'esportazione.
- Problemi comuni (righe nulle, colonne nascoste) e come evitarli.
- Un esempio di codice pronto da copiare, completamente eseguibile.

## Prerequisiti e configurazione

Prima di immergerci nel codice, assicurati di avere:

1. **Aspose.Cells for .NET** installato tramite NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. Un file Excel (`input.xlsx`) posizionato in una cartella a cui puoi fare riferimento, ad esempio `YOUR_DIRECTORY/input.xlsx`.
3. Un progetto che targetizza .NET 6 o versioni successive (le istruzioni `using` mostrate di seguito funzionano subito).

> **Consiglio professionale:** Se stai usando una libreria diversa (ad esempio EPPlus o ClosedXML), il concetto rimane lo stesso—carica la cartella di lavoro, seleziona un intervallo e chiama un metodo che restituisce un `DataTable`.

## Passo 1: Carica la cartella di lavoro e ottieni il primo foglio

La prima cosa di cui hai bisogno è un oggetto `Workbook` che rappresenta il tuo file Excel. Una volta ottenuto, puoi accedere a qualsiasi foglio di lavoro tramite indice o nome.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Perché è importante:** Caricare la cartella di lavoro in anticipo ti consente di ispezionarne la struttura (fogli nascosti, protezioni) prima di decidere quali celle esportare. Se il file è grande, considera l'uso di `LoadOptions` per trasmettere solo le parti necessarie.

## Passo 2: Configura le opzioni di esportazione – Tratta tutti i valori come stringhe

Quando esporti dati per l'elaborazione a valle (ad esempio inserimento massivo in SQL), spesso desideri una **rappresentazione stringa coerente**. Questo evita errori di incompatibilità di tipo in seguito.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Spiegazione:**  
- `ExportAsString = true` indica ad Aspose.Cells di ignorare il tipo nativo della cella e restituire il testo formattato.  
- `NumberFormat = "#,##0.00"` assicura che numeri come `1234.5` diventino `"1,234.50"`—utile per report finanziari.

Se ti servono i tipi di dati originali, imposta semplicemente `ExportAsString` a `false` e gestisci la conversione tu stesso.

## Passo 3: Esporta un intervallo specifico (A1:F11) in un DataTable

Adesso arriva il cuore di **export specific cells**. Il metodo `ExportDataTable` accetta gli indici di riga/colonna di inizio/fine (basati su zero) più un flag per l'inclusione dell'intestazione.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**Cosa ottieni:** Un `DataTable` con 11 righe (inclusa l'intestazione) e 6 colonne (`A`‑`F`). Tutti i valori sono stringhe formattate secondo `exportOptions`.

## Passo 4: Verifica il risultato – Stampa su console

È sempre una buona idea verificare la correttezza dell'output prima di passare la tabella a un altro componente.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

Dovresti vedere qualcosa di simile:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Nota come le colonne numeriche mostrano due cifre decimali, esattamente come abbiamo specificato.

## Esempio completo funzionante (pronto per copia‑incolla)

Di seguito trovi il programma completo che collega tutto insieme. Inseriscilo in un nuovo progetto console, regola il percorso del file e avvialo—non è necessaria alcuna configurazione aggiuntiva.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Punti chiave dal codice:**

- L'oggetto `ExportTableOptions` è riutilizzabile; puoi passarlo a più chiamate `ExportDataTable` se devi esportare diversi intervalli.
- L'indicizzazione parte da **0**, quindi `A1` corrisponde a `(0,0)`.
- Impostare `includeColumnNames` a `true` utilizza automaticamente la prima riga come intestazioni di colonna—ideale per operazioni a valle su `DataTable`.

## Gestione dei casi particolari e domande frequenti

### Cosa succede se il foglio di lavoro ha righe o colonne nascoste?

Aspose.Cells rispetta la visibilità per impostazione predefinita. Se devi esportare dati nascosti, imposta `exportOptions.ExportHiddenRows = true` e `ExportHiddenColumns = true`.

### Il mio file Excel contiene formule—otterrò i valori calcolati?

Sì. Per impostazione predefinita `ExportDataTable` restituisce il **valore visualizzato** (il risultato della formula). Se desideri il testo grezzo della formula, imposta `exportOptions.ExportFormulas = true`.

### Come posso saltare le righe completamente vuote?

Dopo l'esportazione, puoi potare il `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Posso esportare un intervallo non contiguo (ad esempio A1:B5 e D1:E5)?

Aspose.Cells non supporta intervalli disgiunti in una singola chiamata. Invece, esporta ogni blocco separatamente e poi unisci manualmente i `DataTable` risultanti.

## Suggerimenti sulle prestazioni

- **Riutilizza `ExportTableOptions`** per più esportazioni; creare una nuova istanza ogni volta aggiunge un sovraccarico trascurabile ma ingombra il codice.
- **Trasmetti file di grandi dimensioni** con `LoadOptions` per evitare di caricare l'intera cartella di lavoro in memoria.
- **Evita `DataTable`** se ti serve solo un'esportazione CSV veloce—`ExportDataTable` è comodo ma non è il più efficiente in termini di memoria per fogli molto grandi.

## Conclusione

Abbiamo illustrato **come esportare i dati di Excel** in un `DataTable` controllando la formattazione, gestendo intervalli di celle specifici e garantendo che ogni valore arrivi come stringa. L'esempio completo dimostra un approccio pulito, pronto per la produzione, che puoi adattare per **convert excel to datatable**, **export specific cells**, o qualsiasi scenario **excel range to datatable** che incontri.

Sentiti libero di sperimentare: cambia l'intervallo, attiva/disattiva `ExportAsString`, o invia il `DataTable` direttamente a Entity Framework per inserimenti massivi. Il cielo è il limite una volta che hai questa solida base.

### Prossimi passi e argomenti correlati

- **Importare un DataTable in Excel** – impara l'operazione inversa con `ImportDataTable`.
- **Inserimento massivo di un DataTable in SQL Server** – usa `SqlBulkCopy` per caricamenti ultra‑veloci.
- **Lavorare con EPPlus o ClosedXML** – scopri come appare lo stesso compito con librerie alternative.
- **Formattare le celle durante l'esportazione** – approfondisci `ExportTableOptions` per formati data, impostazioni culturali personalizzate e altro.

Hai domande o un caso d'uso diverso? Lascia un commento e continuiamo la conversazione. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}