---
category: general
date: 2026-07-29
description: Copia le righe da un foglio di lavoro a un altro e impara come caricare
  programmaticamente una cartella di lavoro Excel usando Aspose.Cells in un tutorial
  passo‑passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: it
lastmod: 2026-07-29
og_description: Copia le righe da un foglio di lavoro a un altro usando Aspose.Cells.
  Impara a caricare programmaticamente una cartella di lavoro Excel e a preservare
  le tabelle pivot con poche righe di C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Copia righe da un foglio di lavoro all'altro – Guida all'automazione Excel
  in C#
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Copia le righe da un foglio di lavoro all'altro – Guida completa a C#
url: /it/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia righe da un foglio di lavoro a un altro – Guida completa C#

Ti è mai capitato di **copiare righe da un foglio di lavoro a un altro** senza sapere come mantenere intatti formule e tabelle pivot? Non sei il solo. In molti flussi di reporting dobbiamo estrarre una porzione di dati da un foglio master e inserirla in una nuova cartella di lavoro per l'elaborazione successiva. La buona notizia? Con Aspose.Cells puoi farlo programmaticamente, e l’intera operazione richiede solo poche righe di codice.

In questo tutorial vedremo come caricare un workbook Excel programmaticamente, selezionare un intervallo e poi copiare quelle righe in un nuovo workbook preservando eventuali tabelle pivot incorporate. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto C#—senza necessità di copia‑incolla manuale.

## Cosa otterrai

- **Carica un workbook Excel programmaticamente** usando la classe `Workbook` di Aspose.Cells.  
- Definisci un **area di celle** che contiene le righe che vuoi spostare.  
- **Copia righe da un foglio di lavoro a un altro** con una singola chiamata di metodo che mantiene le tabelle pivot attive.  
- Salva il risultato in un nuovo file pronto per la distribuzione o per ulteriori elaborazioni.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona sia su .NET Core che su .NET Framework).  
- Una licenza valida di Aspose.Cells (o una chiave di valutazione temporanea).  
- Due cartelle sul disco: una per il workbook di origine (`Source.xlsx`) e una per la destinazione (`Destination.xlsx`).  

Se hai tutto questo, immergiamoci.

## Passo 1: Carica un workbook Excel programmaticamente

Prima di tutto—prima di poter copiare qualcosa devi caricare il file di origine in memoria. Aspose.Cells rende tutto questo un gioco da ragazzi:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Perché è importante:** Caricare il workbook programmaticamente ti dà il pieno controllo sul contenuto del file senza mai aprire Excel sul server. Evita inoltre problemi di interop COM e funziona in ambienti headless come le pipeline CI.

## Passo 2: Definisci l’intervallo di origine che contiene le righe

Successivamente, individua esattamente quali righe vuoi trasferire. L’oggetto `CellArea` ti consente di specificare un blocco rettangolare usando gli indirizzi delle celle in alto‑sinistra e in basso‑destra:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Consiglio pro:** Se la dimensione dei dati cambia dinamicamente, puoi calcolare `EndRow` con `sourceWorksheet.Cells.MaxDataRow` per catturare sempre l’intera tabella.

## Passo 3: Crea un nuovo workbook per la destinazione

Ora crea un workbook vuoto che riceverà le righe copiate. Questo workbook parte con un unico foglio di lavoro per impostazione predefinita:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Perché un nuovo workbook?** Partire da zero garantisce che non sovrascriverai accidentalmente dati esistenti e ti offre un ambiente prevedibile per i test.

## Passo 4: Copia righe da un foglio di lavoro a un altro (preservando le tabelle pivot)

Ecco il cuore del tutorial. Il metodo `CopyRows` copia le righe selezionate e, quando passi `true` come ultimo argomento, copia anche le eventuali tabelle pivot presenti nell’intervallo:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### Cosa succede dietro le quinte?

- **Foglio di lavoro di origine**: `sourceWorkbook.Worksheets[0]` punta al primo foglio nel file di origine.  
- **Indici di riga**: Aspose.Cells utilizza indicizzazione a base zero, quindi `StartRow` e `EndRow` corrispondono alle righe definite in `sourceRange`.  
- **Riga di inizio destinazione**: Iniziamo dalla riga 0 nel nuovo foglio, posizionando effettivamente il blocco copiato in cima.  
- **Flag `true`**: Questo è l’interruttore magico che indica ad Aspose.Cells di clonare le tabelle pivot trovate all’interno delle righe copiate, preservandone cache e connessioni.

> **Avviso caso limite:** Se l’intervallo di origine contiene celle unite che si estendono oltre l’area definita, tali unioni verranno troncate. Per mantenerle intatte, espandi l’intervallo in modo da coprire completamente la regione unita.

## Passo 5: Salva il workbook di destinazione

Infine, scrivi il nuovo file su disco. Puoi scegliere qualsiasi cartella ti piaccia; assicurati solo che il processo abbia i permessi di scrittura:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

Quando apri `Destination.xlsx` vedrai le righe A1‑H20 duplicate, complete di tutte le tabelle pivot originariamente incorporate. Il resto del workbook rimane vuoto, pronto per aggiungere altri fogli o dati in seguito.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo e eseguibile:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Output previsto** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Apri il file di destinazione e verifica che dati, formattazione e tabelle pivot siano esattamente come nel file di origine. Se noti dati mancanti, ricontrolla che `sourceRange` racchiuda completamente le righe rilevanti.

## Domande comuni e consigli

- **Posso copiare in un foglio di lavoro specifico invece del primo?**  
  Assolutamente. Sostituisci `destinationWorkbook.Worksheets[0]` con `destinationWorkbook.Worksheets["TargetSheet"]` (crea il foglio prima se non esiste).

- **E se devo copiare solo i valori, non le formule?**  
  Usa `CopyRows` con la sovraccarico che accetta un oggetto `CopyRowsOptions` e imposta `PasteType` su `PasteType.Values`.

- **Come gestire file di grandi dimensioni senza esaurire la memoria?**  
  Aspose.Cells supporta lo **streaming** tramite `LoadOptions` con `MemorySetting.MemoryPreference`. Carica il workbook di origine con un'impronta di memoria ridotta e l’operazione di copia rimarrà efficiente.

- **Le tabelle pivot rimangono collegate alla fonte dati originale?**  
  Quando imposti il flag `true`, la cache della pivot viene duplicata, quindi le pivot del nuovo workbook fanno riferimento ai dati copiati, non al file originale.

## Conclusione

Ora sai come **copiare righe da un foglio di lavoro a un altro** mantenendo intatte le tabelle pivot, e hai visto come **caricare un workbook Excel programmaticamente** usando Aspose.Cells. Questo modello è una solida base per costruire pipeline di reporting automatizzate, script di migrazione dati o qualsiasi scenario in cui sia necessario manipolare dati Excel al volo.

Qual è il prossimo passo? Prova ad ampliare lo snippet per:

- Iterare su più intervalli di origine e aggregarli in un unico file di destinazione.  
- Applicare formattazione condizionale dopo la copia per evidenziare metriche chiave.  
- Esportare il workbook finale in PDF o CSV per il consumo a valle.

Sentiti libero di sperimentare e, se incontri difficoltà, lascia un commento qui sotto. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come copiare righe in Excel usando Aspose.Cells per .NET: Guida C#](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Copia foglio di lavoro da un workbook a un altro usando Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [Come esportare le righe visibili di Excel usando Aspose.Cells per .NET: Guida passo‑passo](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}