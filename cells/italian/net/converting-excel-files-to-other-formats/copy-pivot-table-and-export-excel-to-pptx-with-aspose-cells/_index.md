---
category: general
date: 2026-09-11
description: Copia la tabella pivot ed esporta Excel in PPTX usando Aspose.Cells.
  Impara a generare PPTX modificabili e a salvare la cartella di lavoro come PPTX
  in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: it
lastmod: 2026-09-11
og_description: Copia la tabella pivot ed esporta Excel in PPTX in C# usando Aspose.Cells.
  Genera un PPTX modificabile e salva la cartella di lavoro come PPTX con poche righe
  di codice.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Copia tabella pivot ed esporta Excel in PPTX – guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Copia tabella pivot ed esporta Excel in PPTX con Aspose.Cells
url: /it/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia tabella pivot ed esporta Excel in PPTX con Aspose.Cells

Se hai bisogno di copiare una tabella pivot da un foglio di lavoro a un altro e poi esportare il file Excel in una presentazione PowerPoint, questa guida ti mostra come fare. Utilizzando Aspose.Cells puoi generare un PPTX modificabile e salvare la cartella di lavoro come PPTX in poche righe di codice C#.

Il tutorial copre ogni passaggio necessario per spostare una tabella pivot, preservarne la funzionalità e produrre un file PPTX in cui il grafico e le forme rimangono modificabili. Non sono necessari strumenti esterni—solo la libreria Aspose.Cells e un ambiente di sviluppo .NET.

## Cosa otterrai

* **Copy pivot table** da un foglio di origine a un foglio di destinazione mantenendo intatti tutti i collegamenti dati.  
* **Export Excel to PPTX** così la diapositiva risultante può essere modificata in PowerPoint.  
* **Generate editable PPTX** dove grafici, tabelle e forme non sono rasterizzate in immagini.  
* **Save workbook as PPTX** usando la stessa chiamata API di Aspose.Cells.  

### Prerequisiti

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+).  
* Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`).  
* Una conoscenza di base delle applicazioni console C#.  

> **Consiglio professionale:** Installa il pacchetto NuGet tramite la CLI per garantire di avere l'ultima versione:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Come copiare una tabella pivot tra fogli di lavoro

La prima operazione è spostare la tabella pivot preservandone la definizione. Aspose.Cells fornisce un metodo `CopyRange` con un oggetto `CopyOptions` che include il flag `CopyPivotTable`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Perché funziona:**  
`CopyRange` copia i dati delle celle, la formattazione e, quando `CopyPivotTable` è true, la cache e i metadati della tabella pivot. L'intervallo di destinazione inizia dalla cella `A1` (riga 0, colonna 0) ma è possibile modificare gli offset per posizionare la tabella pivot altrove.

**Caso limite comune:** Se il foglio di destinazione contiene già una tabella pivot con lo stesso nome, Aspose.Cells rinominerà automaticamente quella in ingresso, evitando conflitti di nome.

## Esporta Excel in PPTX e genera PPTX modificabile

Una volta che la tabella pivot è al suo posto, puoi esportare l'intera cartella di lavoro in un file PPTX. La classe `ImageOrPrintOptions` consente di specificare `ExportImageFormat = ImageFormat.Pptx`, che indica ad Aspose.Cells di trattare l'output come una presentazione PowerPoint anziché come un'immagine raster.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Perché funziona:**  
Quando `ExportImageFormat` è impostato su `Pptx`, Aspose.Cells traduce ogni foglio di lavoro in una diapositiva. Forme, grafici e tabelle pivot vengono scritti come oggetti nativi di PowerPoint, così puoi fare doppio clic su di essi in PowerPoint e modificare i dati sottostanti.

**Suggerimento per cartelle di lavoro grandi:** Se ti serve solo un sottoinsieme di fogli, imposta `workbook.Worksheets.RemoveAt(index)` per i fogli che non vuoi esportare prima di chiamare `Save`. Questo riduce le dimensioni del file PPTX.

## Esempio completo, eseguibile

Di seguito trovi il programma completo che collega i passaggi precedenti. Sostituisci `YOUR_DIRECTORY` con il percorso reale sul tuo computer.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Output previsto

L'esecuzione del programma stampa:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Quando apri `output.pptx` in Microsoft PowerPoint, vedrai una diapositiva che contiene la tabella pivot copiata come grafico modificabile. Facendo doppio clic sul grafico si apre l'editor di grafici di PowerPoint, consentendoti di modificare serie, assi e etichette dei dati senza tornare a Excel.

## Gestione delle difficoltà tipiche

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| La tabella pivot appare come immagine statica | Flag `CopyPivotTable` omesso o `ExportImageFormat` impostato su `Png` | Assicurati che `CopyPivotTable = true` e `ExportImageFormat = ImageFormat.Pptx`. |
| Il foglio di destinazione mostra celle vuote | L'intervallo di origine non copre l'intera area della tabella pivot | Espandi l'intervallo (es. `"A1:H30"`) per includere tutti i campi pivot. |
| Il PPTX esportato è enorme | Sono inclusi fogli di lavoro non necessari | Rimuovi i fogli indesiderati prima di chiamare `Save`. |
| PowerPoint non può modificare il grafico | Uso di una versione più vecchia di Aspose.Cells priva del supporto PPTX | Aggiorna all'ultima versione di Aspose.Cells (controlla le note di rilascio). |

## Prossimi passi e argomenti correlati

* **Export Excel sheet to PPTX with custom slide layouts** – esplora `WorksheetToPdfConverter` per un controllo più fine sull'aspetto delle diapositive.  
* **Export Excel to PDF** – sostituisci `ImageFormat.Pptx` con `ImageFormat.Pdf` per generare un PDF invece.  
* **Programmatically modify PPTX after export** – usa la libreria `Aspose.Slides` per aggiungere animazioni o note del relatore.  

Padroneggiando **copy pivot table**, **export excel to pptx** e **generate editable pptx**, potrai costruire pipeline di reporting end‑to‑end che spostano i dati da fogli di calcolo direttamente in presentazioni senza perdere la possibilità di modificarli.

---


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come copiare una tabella pivot in C# – Convertire Excel in PPTX, Copiare intervallo e creare casella di testo](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Creare nuovo workbook Excel – Copiare e duplicare tabella pivot](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Creare una tabella pivot in Excel usando Aspose.Cells per .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}