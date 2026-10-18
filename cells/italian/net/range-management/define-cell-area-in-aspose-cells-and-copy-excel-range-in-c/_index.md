---
category: general
date: 2026-08-04
description: Definisci l'area della cella in Aspose.Cells e impara come copiare le
  tabelle pivot, copiare un intervallo Excel in C# e copiare l'intervallo nello stesso
  foglio in modo efficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: it
lastmod: 2026-08-04
og_description: Definisci l'area della cella in Aspose.Cells e copia l'intervallo
  Excel in C# preservando le tabelle pivot. Segui questa guida passo passo per risultati
  affidabili.
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: Definire l'area della cella in Aspose.Cells – copiare l'intervallo Excel
  in C#
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: Definire l'area della cella in Aspose.Cells e copiare l'intervallo Excel in
  C#
url: /it/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Definire l'area della cella in Aspose.Cells e copiare l'intervallo Excel in C#

Se hai bisogno di **definire l'area della cella** per un intervallo e poi copiare quell'intervallo nello stesso foglio di lavoro, questa guida ti mostra esattamente come farlo con Aspose.Cells per .NET. Che tu stia spostando un report basato su pivot o duplicando un blocco di dati, imparerai l'intero processo in pochi passaggi.

Scoprirai anche **come copiare pivot** senza perdere le loro connessioni, e vedrai un esempio chiaro di **copy excel range c#** che funziona nello scenario **copy range same sheet**. Non sono necessari strumenti esterni—solo Aspose.Cells e qualche riga di C#.

## Cosa ti servirà

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+)
- Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`)
- Un workbook Excel (`input.xlsx`) che contiene una tabella pivot nell'intervallo A1:J50
- Un ambiente di sviluppo come Visual Studio 2022

## Passo 1: Definire l'area della cella per l'intervallo di origine

Il primo compito è **definire l'area della cella** che rappresenta il blocco da copiare. Aspose.Cells utilizza la struttura `CellArea`, che memorizza gli indici di riga e colonna basati su zero.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**Perché è importante:** `CellArea` indica ad Aspose.Cells esattamente su quali celle operare. L'uso di indici basati su zero evita errori di tipo off‑by‑one comuni quando si traduce la notazione A1 di Excel in codice.

## Passo 2: Definire l'area della cella di destinazione nello stesso foglio

Per **copy range same sheet**, devi anche specificare dove devono atterrare i dati. La destinazione può iniziare in qualsiasi riga; qui iniziamo dalla riga 61 (indice basato su zero 60) per lasciare un buffer vuoto.

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**Perché è importante:** Riflettendo le dimensioni dell'origine, garantisci che il blocco copiato si adatti perfettamente senza troncamenti.

## Passo 3: Copiare l'intervallo preservando le tabelle pivot

Ora puoi **how to copy pivot** in modo sicuro. La classe `CopyOptions` include un flag `CopyPivotTables` che mantiene la definizione della pivot, la fonte dei dati e la formattazione.

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**Perché è importante:** Senza impostare `CopyPivotTables = true`, la pivot diventerebbe un'istantanea statica, perdendo l'interattività. Questa opzione copia la cache sottostante e le connessioni, così la nuova pivot si comporta esattamente come l'originale.

## Passo 4: Salvare il workbook

Infine, scrivi le modifiche su disco. Il file di output dimostra che la tabella pivot è stata duplicata nello stesso foglio.

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**Pro tip:** Usa `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)` se devi forzare un formato specifico, soprattutto quando lavori con versioni più vecchie di Excel.

## Passo 5: Verificare la tabella pivot copiata

Apri `CopyWithPivot.xlsx` in Excel e controlla quanto segue:

1. L'intervallo A61:J110 contiene una copia dei dati originali.
2. Una nuova tabella pivot appare nella parte superiore dell'intervallo copiato.
3. Aggiornare la pivot riflette le modifiche nei dati di origine, confermando che **how to copy pivot** è riuscito.

Se la pivot non si aggiorna, assicurati che l'intervallo dei dati di origine nella definizione della pivot punti ancora all'area originale del workbook. Aspose.Cells aggiorna automaticamente il riferimento di origine quando `CopyPivotTables` è true.

## Casi limite e variazioni

| Situazione | Cosa cambiare |
|------------|----------------|
| **Copy to a different worksheet** | Sostituisci `srcWorkbook.Worksheets[0]` con l'indice o il nome del foglio di destinazione, e regola `destinationRange` di conseguenza. |
| **Copy a merged cell block** | Imposta `CopyOptions.PasteType = PasteType.All` per preservare le celle unite e la formattazione. |
| **Copy only values, not formulas** | Usa `CopyOptions.PasteType = PasteType.Values` per evitare di trasferire formule che fanno riferimento al foglio originale. |
| **Large ranges ( > 10,000 rows )** | Considera l'uso di `Workbook.Copy` per interi fogli di lavoro per migliorare le prestazioni, poi elimina le righe indesiderate. |

Queste variazioni dimostrano che la stessa logica di **aspose.cells copy range** può essere adattata a molte situazioni reali.

## Esempio completo funzionante

Di seguito trovi il programma completo, pronto per l'esecuzione. Sostituisci `YOUR_DIRECTORY` con un percorso di cartella reale sul tuo computer.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**Output previsto:** Dopo aver eseguito il programma, `CopyWithPivot.xlsx` contiene i dati originali più un blocco identico a partire dalla riga 61, completo di una tabella pivot funzionante.

## Conclusione

Ora sai come **definire l'area della cella** in Aspose.Cells, **copy excel range c#**, e **copy range same sheet** preservando tutta la funzionalità delle pivot. Questa tecnica elimina gli errori di copia‑incolla manuale e scala a workbook di grandi dimensioni.

Successivamente, esplora argomenti correlati come **how to copy pivot** tra più fogli di lavoro, o utilizza **aspose.cells copy range** per duplicare interi fogli con formattazione. Sperimenta con diverse impostazioni di `CopyOptions` per adattare il comportamento di copia alle esigenze del tuo progetto.

Buona programmazione!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Excel Aspose Cells .NET Copia Dati Intervallo](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Copia Dati Intervallo](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Copia Dati Intervallo](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}