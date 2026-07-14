---
category: general
date: 2026-07-13
description: Come esportare un intervallo di celle come tabella usando C# e ExportTableOptions.
  Scopri passo‑passo la configurazione della cartella di lavoro, la formattazione
  e l’esportazione della tabella.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: it
lastmod: 2026-07-13
og_description: Come esportare un intervallo di celle come tabella in C# con ExportTableOptions.
  Segui questa guida per formattare le celle, creare una cartella di lavoro ed esportare
  una tabella senza sforzo.
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: Come esportare un intervallo di celle come tabella – Guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: Come esportare l'intervallo di celle come tabella – Guida completa a C#
url: /it/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare un intervallo di celle come tabella – Guida completa in C#

Ti sei mai chiesto **come esportare un intervallo di celle come tabella** senza impazzire per i problemi di formattazione? Non sei l'unico. Che tu stia alimentando un pipeline di reporting o abbia semplicemente bisogno di un dump in stile CSV, padroneggiare il processo di esportazione può farti risparmiare ore di copia‑incolla manuale.

In questo tutorial percorreremo passo passo le operazioni necessarie per prendere una cella numerica, applicare la notazione scientifica e esportarla come tabella usando **ExportTableOptions**. Alla fine avrai uno snippet eseguibile, comprenderai il *perché* di ogni chiamata e saprai come modificare il codice per intervalli più grandi o formati diversi.

## Prerequisiti

- .NET 6 o successivo (l'API funziona allo stesso modo su .NET Framework 4.7+)
- Aspose.Cells per .NET installato (`Install-Package Aspose.Cells`)
- Una conoscenza di base della sintassi C#; non servono approfondimenti su Excel

Hai tutto? Ottimo—iniziamo.

## Passo 1: Configurare le opzioni di esportazione – Come esportare un intervallo di celle come tabella

La prima cosa di cui hai bisogno è un'istanza **ExportTableOptions** che dica alla libreria come trattare il contenuto delle celle. Senza di essa, l'esportazione usa i valori numerici grezzi, il che può rompere i consumatori a valle che si aspettano del testo.

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**Perché è importante:**  
- `ExportAsString = true` costringe la libreria a scrivere il testo visualizzato nella cella, non il valore double sottostante.  
- `CustomFormat` ti permette di imporre un **esportazione in notazione scientifica**, utile quando si trattano numeri molto grandi o molto piccoli.

> **Consiglio esperto:** Se ti serve un formato data o valuta, sostituisci `"0.00E+00"` con `"yyyy‑MM‑dd"` o `"$#,##0.00"` rispettivamente.

## Passo 2: Creare un Workbook e prendere il primo Worksheet – Gestione di Workbook e Worksheet

Un **Workbook** rappresenta l'intero file Excel, mentre un **Worksheet** è una singola scheda. Per un'esportazione semplice ci limiteremo al primo foglio, che è sempre presente all'indice 0.

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**Perché è importante:**  
Creare un nuovo `Workbook` garantisce una base pulita—nessuno stile nascosto o dati residui che possano creare problemi. Accedere a `Worksheets[0]` è il modo più veloce per ottenere il foglio attivo senza preoccuparsi dei nomi.

## Passo 3: Popolare la cella di destinazione – Formattazione del valore della cella in C#

Ora inseriamo un valore numerico nella cella **A1** (riga 0, colonna 0). Il valore scelto è deliberatamente a decimali lunghi così potrai vedere la notazione scientifica in azione.

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**Perché è importante:**  
Chiamare `PutValue` inferisce automaticamente il tipo di dato della cella. Poiché in seguito esportiamo come stringa, il double grezzo verrà convertito usando il formato impostato prima, producendo un output pulito come `"1.23E+04"`.

## Passo 4: Esportare l'intervallo di celle definito come tabella – Esportare l'intervallo di celle come tabella

Con le opzioni e i dati pronti, l'ultimo passo è dire ad Aspose.Cells di scrivere l'intervallo. Il metodo `ExportTable` richiede la riga/colonna di partenza, la dimensione dell'intervallo e l'oggetto opzioni che abbiamo creato.

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**Perché è importante:**  
- `totalRows = 1` e `totalColumns = 1` limitano l'esportazione a una singola cella, ma puoi aumentare questi numeri per coprire blocchi più grandi (es. `5, 3` per un intervallo 5 righe × 3 colonne).  
- Il metodo scrive i dati in una struttura tabellare interna che può essere salvata come CSV, HTML o persino trasmessa direttamente a un client.

### Salvataggio del risultato (opzionale)

Se vuoi persistere la tabella esportata su disco, puoi scriverla in un file CSV:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

Eseguendo quanto sopra verrà generato un file contenente:

```
1.23E+04
```

## Casi limite e variazioni comuni

| Situazione | Cosa modificare | Motivo |
|------------|-----------------|--------|
| **Esportare più righe** | Regolare `totalRows` e iterare sulle righe se necessario | Consente l'esportazione batch senza invocare ripetutamente `ExportTable` |
| **Preservare le formule** | Impostare `ExportAsString = false` | Mantiene la formula originale invece del valore visualizzato |
| **Delimiter diversi** | Usare la sovraccarico `ExportTableToCSV(..., ',', ...)` | Passa da valori separati da virgola a valori separati da tabulazione o pipe |
| **Fogli di lavoro molto grandi** | Trasmettere lo stream di esportazione per evitare `OutOfMemoryException` | Funziona bene per >10 000 righe |

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per il copia‑incolla. Compila con qualsiasi progetto console .NET che faccia riferimento ad Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**Output previsto:**  
Un file chiamato `ExportedTable.csv` contenente una singola riga:

```
1.23E+04
```

Se apri il CSV in un editor di testo vedrai la notazione scientifica applicata esattamente come definita.

## Conclusione

Abbiamo coperto **come esportare un intervallo di celle come tabella** dall'inizio alla fine: configurare `ExportTableOptions`, creare un `Workbook`, inserire i dati e infine invocare `ExportTable`. Capendo ogni singola parte, ora puoi scalare l'approccio a intervalli più ampi, formati diversi o persino integrarlo in una web API che fornisce dati derivati da Excel al volo.

Guardando al futuro, potresti voler esplorare:

- **ExportTableToHTML** per anteprime pronte per il web  
- **ExportTableToDataTable** per alimentare direttamente pipeline ADO.NET  
- Formati **personalizzati avanzati** per date, valute o percentuali  

Provali e trasformerai una semplice esportazione di cella in un motore versatile di consegna dati. Hai domande o un caso d'uso particolare? Lascia un commento qui sotto—buona programmazione!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}