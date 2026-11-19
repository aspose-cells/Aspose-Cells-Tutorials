---
category: general
date: 2026-11-19
description: Scopri come copiare un intervallo usando CopyOptions in Aspose.Cells,
  preservando la formattazione e le tabelle pivot durante la copia di un intervallo
  Excel con formattazione.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: it
lastmod: 2026-11-19
og_description: Copia un intervallo con CopyOptions in Aspose.Cells permette di duplicare
  i dati di Excel mantenendo intatta tutta la formattazione e le tabelle pivot, consentendo
  una manipolazione affidabile della cartella di lavoro.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Copia intervallo usando CopyOptions in Aspose.Cells – guida passo passo
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come copiare un intervallo usando CopyOptions in Aspose.Cells
url: /it/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare un intervallo usando CopyOptions in Aspose.Cells

Se devi **copiare un intervallo usando CopyOptions** in Aspose.Cells, questa guida ti mostra esattamente come duplicare un blocco di celle mantenendo intatti tutti i formati e le tabelle pivot incorporate. Molti sviluppatori incontrano difficoltà nel preservare lo stile quando spostano dati tra fogli di lavoro, e la classe `CopyOptions` risolve questo problema senza passaggi manuali aggiuntivi.

In questo tutorial imparerai a:

* Definire le aree di origine e destinazione in una cartella di lavoro Excel.  
* Usare `CopyOptions` per mantenere la formattazione delle celle, le larghezze delle colonne e le tabelle pivot.  
* Salvare il risultato in un nuovo file pronto per l'elaborazione successiva.

L'esempio funziona con qualsiasi file `.xlsx` e richiede solo la libreria Aspose.Cells per .NET.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate.  
* Una licenza valida di Aspose.Cells per .NET (o una chiave di valutazione gratuita).  
* Visual Studio 2022 o qualsiasi IDE C# tu preferisca.  

Non sono necessari pacchetti NuGet aggiuntivi oltre a `Aspose.Cells`.

## Passo 1: Configura il progetto e importa i namespace

Crea una nuova applicazione console e aggiungi il riferimento a Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

La direttiva `using Aspose.Cells;` ti dà accesso a `Workbook`, `CellArea` e `CopyOptions`.

## Passo 2: Carica la cartella di lavoro che vuoi modificare

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` rappresenta l'intero file Excel. Sostituisci `YOUR_DIRECTORY` con la cartella che contiene il tuo file di origine.

## Passo 3: Definisci gli intervalli di origine e destinazione

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` crea un'area rettangolare basata sugli indirizzi della cella in alto‑a‑sinistra e in basso‑a‑destra. Puoi regolare le coordinate per corrispondere alle dimensioni del blocco che desideri copiare.

## Passo 4: Copia l'intervallo preservando formattazione e tabelle pivot

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

L'oggetto `CopyOptions` indica ad Aspose.Cells esattamente cosa mantenere. Impostare `CopyPivotTables = true` è la chiave per **copiare un intervallo usando CopyOptions** quando la tua origine contiene tabelle pivot. Le altre flag assicurano che **copiare un intervallo Excel con formattazione** venga eseguita automaticamente—non è necessario alcun codice aggiuntivo per riapplicare gli stili dopo la copia.

### Perché `CopyOptions` è importante

* **Prestazioni** – La libreria esegue un'unica operazione interna anziché copiare le celle una per una.  
* **Precisione** – Tutti gli aspetti visivi (font, colori, bordi) sopravvivono allo spostamento, eliminando le discrepanze visive nei report generati.  
* **Affidabilità** – Le tabelle pivot rimangono funzionali perché la loro cache e i riferimenti di origine vengono duplicati.

## Passo 5: Salva la cartella di lavoro modificata

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Dopo aver chiamato `Save`, il file `output.xlsx` contiene i dati originali più il blocco duplicato nella posizione di destinazione, completo di formattazione e tabelle pivot.

## Codice sorgente completo per riferimento

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Eseguendo questo programma otterrai:

```
Range copied successfully. Output saved to output.xlsx
```

Apri `output.xlsx` in Excel – vedrai il blocco A1:H30 duplicato in A35:H64, con tutti i colori delle celle, i bordi, i formati numerici e le eventuali tabelle pivot intatti.

## Domande frequenti e gestione dei casi limite

### E se l'area di destinazione si sovrappone a quella di origine?

Aspose.Cells genera un'`ArgumentException`. Per evitarlo, calcola una destinazione che non intersechi l'origine, oppure copia su un foglio di lavoro diverso:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Come copiare tra cartelle di lavoro diverse?

Crea una seconda istanza `Workbook` per il file di destinazione e utilizza lo stesso oggetto `CopyOptions`:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions` copia anche le celle unite?

Sì. La flag `CopyStyle` include le informazioni sulle celle unite. Se ti serve un controllo più fine, imposta `options.CopyMergedCells = true` (disponibile nelle versioni più recenti).

### E per intervalli molto grandi (migliaia di righe)?

L'operazione è efficiente in termini di memoria, ma potresti voler aumentare la proprietà `WorkbookSettings` `MemorySetting` a `MemorySetting.MemoryPreference` per file molto grandi.

## Consigli professionali

* **Riutilizza la stessa istanza di `CopyOptions`** per più operazioni di copia – riduce l'overhead di allocazione degli oggetti.  
* **Convalida gli intervalli** prima di copiare: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` aiuta a intercettare errori di battitura in anticipo.  
* **Disattiva il calcolo** (`workbook.Settings.CalcMode = CalculationMode.Manual`) durante la copia di grandi set di dati per velocizzare il processo, quindi chiama `workbook.CalculateFormula()` dopo la copia se hai bisogno di risultati aggiornati.

## Conclusione

Ora sai come **copiare un intervallo usando CopyOptions** in Aspose.Cells, ottenendo un completo **copiare un intervallo Excel con formattazione** mantenendo le tabelle pivot e altre funzionalità avanzate. Questo approccio elimina la riapplicazione manuale degli stili e garantisce che la tua automazione Excel rimanga robusta e manutenibile.

Passi successivi che potresti esplorare:

* Usa `CopyOptions` per duplicare interi fogli di lavoro.  
* Combina l'operazione di copia con `WorksheetCollection.AddCopy` per la generazione di report basati su template.  
* Integra il codice in un'API ASP.NET Core per fornire trasformazioni Excel on‑the‑fly.

Sentiti libero di sperimentare con diverse coordinate di origine/destinazione e condividi i tuoi risultati nei commenti!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}