---
category: general
date: 2026-09-18
description: Crea PowerPoint da Excel con Aspose.Cells – copia le tabelle pivot, esporta
  gli intervalli e salva come PPTX in poche righe di codice C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: it
lastmod: 2026-09-18
og_description: Crea PowerPoint da Excel rapidamente. Scopri come copiare le tabelle
  pivot, esportare gli intervalli e salvare una cartella di lavoro come PPTX usando
  Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Crea PowerPoint da Excel con Aspose.Cells – guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Come creare PowerPoint da Excel usando Aspose.Cells
url: /it/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare PowerPoint da Excel usando Aspose.Cells

Se hai bisogno di creare PowerPoint da Excel, questa guida ti mostra una soluzione concisa, end‑to‑end. Vedrai come copiare una tabella pivot, esportare un intervallo selezionato e salvare il risultato come file PPTX con poche righe di C#.

Generare una presentazione direttamente dai dati del foglio di calcolo elimina il passaggio manuale di copia‑incolla che rallenta i flussi di lavoro di reporting. Il tutorial copre tutto ciò di cui hai bisogno, dalla configurazione del progetto al file PPTX finale, e funziona con l'ultima versione di Aspose.Cells per .NET.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* **Aspose.Cells for .NET** (versione 23.12 o successiva). Installalo tramite NuGet: `Install-Package Aspose.Cells`.
* Un ambiente di sviluppo **.NET 6+** (Visual Studio 2022 o VS Code funzionano).
* Un file Excel (`Source.xlsx`) che contiene i dati e la tabella pivot che desideri riutilizzare.
* Permessi di scrittura sulla cartella di destinazione.

Non sono richieste librerie di terze parti aggiuntive.

## Creare PowerPoint da Excel – passo‑per‑passo

Il processo consiste in quattro passaggi logici che corrispondono direttamente all'esempio di codice che vedrai più avanti.

### Passo 1: Caricare il workbook di origine e definire l'intervallo

Devi caricare il workbook che contiene i dati di origine e la tabella pivot. Selezionare un intervallo preciso garantisce che vengano trasferite solo le celle necessarie, mantenendo la diapositiva risultante leggera.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Perché è importante:**  
`CreateRange` crea un oggetto `Range` che può essere copiato interamente. Limitando l'intervallo a `A1:G20`, eviti di includere celle non correlate, che altrimenti potrebbero ingrandire il file PowerPoint.

### Passo 2: Preparare il workbook di destinazione

Aspose.Cells tratta una diapositiva PowerPoint come un workbook quando lo salvi in formato PPTX. Creare un nuovo workbook ti fornisce una tela pulita per l'intervallo copiato.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Suggerimento:** Se hai bisogno di più diapositive, puoi aggiungere fogli di lavoro aggiuntivi e successivamente salvare ciascuno come file PPTX separato.

### Passo 3: Copiare l'intervallo preservando la tabella pivot

`CopyRange` accetta un oggetto `PasteOptions`. Impostare `CopyPivotTables = true` indica ad Aspose.Cells di mantenere intatta la struttura della tabella pivot, non solo i valori renderizzati.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Come funziona:**  
Quando `CopyPivotTables` è true, il foglio di destinazione riceve sia i dati di origine sia la cache della pivot. Ciò significa che la tabella pivot rimane pienamente funzionale e può essere aggiornata in seguito se i dati di origine cambiano.

### Passo 4: Salvare il workbook come file PowerPoint

Infine, esporta il workbook in formato PPTX. Il flag `SaveFormat.Pptx` indica ad Aspose.Cells di scrivere il foglio di lavoro come diapositiva PowerPoint.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Risultato:**  
`CopyWithPivot.pptx` si apre in Microsoft PowerPoint (o in qualsiasi visualizzatore compatibile) con una singola diapositiva che mostra l'intervallo copiato, inclusa una tabella pivot live con cui è possibile interagire in PowerPoint.

## Esempio completo eseguibile

Di seguito trovi il programma completo che puoi incollare in un nuovo progetto console e eseguire immediatamente.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Output previsto:**  
Eseguendo il programma stampa “PowerPoint file created successfully.” e produce un file chiamato `CopyWithPivot.pptx`. Aprendo il file in PowerPoint si vede una singola diapositiva in cui l'intervallo Excel copiato appare esattamente come nel foglio di origine, con una tabella pivot attiva che può essere aggiornata dall'interno di PowerPoint.

## Varianti comuni e casi limite

| Situazione | Cosa cambiare |
|------------|----------------|
| **Tabelle pivot multiple** | Definisci oggetti `Range` separati per ogni tabella e chiama `CopyRange` per ciascuno, oppure copia l'intero foglio se condividono la stessa origine dati. |
| **Grandi set di dati** | Aumenta l'intervallo (ad es., `"A1:Z5000"`). Considera di abilitare `PasteOptions.CompressData = true` per ridurre le dimensioni del PPTX. |
| **Layout diapositive diversi** | Dopo aver salvato come PPTX, apri il file in PowerPoint e applica un layout o tema personalizzato; i dati rimangono modificabili. |
| **Salvataggio su stream** | Usa `destinationWorkbook.Save(stream, SaveFormat.Pptx)` quando devi restituire il PPTX tramite un'API web. |
| **Preservare la formattazione delle celle** | Imposta `PasteOptions.PasteType = PasteType.All` per mantenere caratteri, colori e bordi. |

**Consiglio professionale:** Verifica sempre che la cartella di destinazione esista prima di chiamare `Save`. Se la cartella manca, `Save` genera una `DirectoryNotFoundException`.

## Conclusione

Ora sai come creare PowerPoint da Excel, copiare una tabella pivot ed esportare il risultato come file PPTX usando Aspose.Cells. I passaggi — caricare il workbook di origine, definire un intervallo, copiare con `CopyPivotTables` e salvare come PPTX — coprono l'intero flusso di lavoro in modo affidabile e pronto per la produzione.

Successivamente, esplora **come esportare Excel in PPTX** per più fogli di lavoro, o impara **come copiare un intervallo tra workbook** quando devi unire dati da diverse fonti prima di generare la presentazione. Entrambi gli argomenti si basano sulla stessa API e possono essere combinati per automatizzare pipeline di reporting complesse.

Buon coding e divertiti a trasformare i tuoi fogli di calcolo in presentazioni curate!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come copiare una tabella pivot in C# – Convertire Excel in PPTX, copiare intervallo e creare casella di testo](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Creare nuovo workbook – Come copiare un foglio di lavoro con una tabella pivot](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Come creare e salvare file Excel con Aspose.Cells per .NET: Guida completa](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}