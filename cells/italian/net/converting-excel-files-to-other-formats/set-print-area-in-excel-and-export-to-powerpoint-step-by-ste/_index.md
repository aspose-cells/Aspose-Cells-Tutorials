---
category: general
date: 2026-03-22
description: Imposta l'area di stampa in Excel e converti Excel in PowerPoint con
  forme modificabili. Scopri come ripetere la riga del titolo, creare PowerPoint da
  Excel ed esportare Excel in pptx.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: it
og_description: Imposta l'area di stampa in Excel e convertila in una diapositiva
  PowerPoint con forme modificabili. Segui questa guida completa per ripetere la riga
  del titolo ed esportare Excel in pptx.
og_title: Imposta l'area di stampa in Excel – Tutorial per l'esportazione in PowerPoint
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Imposta l'area di stampa in Excel ed esporta in PowerPoint – Guida passo passo
url: /it/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta l'area di stampa in Excel ed esporta in PowerPoint – Tutorial di programmazione completo

Ti è mai capitato di dover **impostare l'area di stampa** in un foglio Excel e poi trasformare quella porzione in una diapositiva PowerPoint? Non sei l'unico. In molti flussi di reporting gli stessi dati che stampano bene devono apparire anche in una presentazione, spesso con la prima riga ripetuta come titolo. La buona notizia? Con poche righe di C# puoi **convertire excel in powerpoint**, mantenere tutte le caselle di testo modificabili e persino **ripetere la riga del titolo** automaticamente.

In questa guida vedremo passo passo tutto ciò che devi sapere: dalla configurazione dell'area di stampa alla creazione di un file PPTX modificabile direttamente in PowerPoint. Alla fine sarai in grado di **creare powerpoint da excel**, esportare il risultato come **export excel to pptx**, e riutilizzare lo stesso codice in qualsiasi progetto .NET. Nessuna magia, solo passaggi chiari e un esempio completo e funzionante.

## Cosa ti serve

Prima di iniziare, assicurati di avere:

- **.NET 6.0** o versioni successive (l'API funziona anche con .NET Framework)
- **Aspose.Cells for .NET** (la libreria che fornisce `Workbook`, `ImageOrPrintOptions`, ecc.)
- Un IDE C# di base (Visual Studio, Rider o VS Code con l'estensione C#)
- Un file Excel (`input.xlsx`) che contiene i dati da esportare

Tutto qui—nessun pacchetto NuGet aggiuntivo oltre a Aspose.Cells. Se non hai ancora aggiunto la libreria, esegui:

```bash
dotnet add package Aspose.Cells
```

Ora siamo pronti a partire.

## Passo 1: Carica il Workbook – il punto di partenza per l'esportazione

La prima cosa da fare è caricare il workbook che contiene il foglio che vuoi trasformare in una diapositiva. Pensa al workbook come al documento sorgente; senza di esso nulla ha senso.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Perché è importante:** Caricare il workbook ti dà accesso alla collezione di worksheet, alle opzioni di impostazione pagina e al motore di esportazione. Se salti questo passaggio non potrai impostare l'**area di stampa** né ripetere alcuna riga.

> **Consiglio:** Usa un percorso assoluto durante i test, poi passa a un percorso relativo o basato su configurazione per la produzione.

## Passo 2: Configura le opzioni di esportazione – mantieni caselle di testo e forme modificabili

Quando esporti in PowerPoint probabilmente vuoi che la diapositiva risultante sia modificabile. Aspose.Cells ti permette di controllare questo con `ImageOrPrintOptions`. Impostare `ExportTextBoxes` e `ExportShapeObjects` a `true` indica alla libreria di preservare quegli oggetti come elementi nativi di PowerPoint invece di appiattirli in un'immagine.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Perché è importante:** Se devi **convertire excel in powerpoint** e poi modificare manualmente la diapositiva, questa impostazione ti salva dal dover ricreare le caselle di testo da zero. Garantisce inoltre che eventuali forme (come frecce o grafici) rimangano oggetti vettoriali ridimensionabili.

## Passo 3: Imposta l'area di stampa e ripeti la riga del titolo

Ora arriviamo al cuore del tutorial: **impostare l'area di stampa** e fare in modo che la prima riga si ripeta su ogni pagina stampata (o, nel nostro caso, su ogni diapositiva esportata). L'area di stampa indica a Excel quali celle considerare per la stampa—o per l'esportazione nel nostro scenario.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Perché è importante:** Limitando l'esportazione a `A1:G20` eviti di includere ampie aree vuote, velocizzando la conversione e mantenendo la diapositiva ordinata. La riga `PrintTitleRows` fa sì che la prima riga si comporti da intestazione—esattamente ciò che vuoi quando **ripeti la riga del titolo** in una presentazione.

> **Caso limite:** Se i tuoi dati iniziano dalla riga 2, adatta l'intervallo di conseguenza (ad es., `PrintTitleRows = "$2:$2"`).

## Passo 4: Salva il worksheet come file PowerPoint

Infine, scriviamo la diapositiva su disco. Il metodo `Save` accetta il nome del file di destinazione e le opzioni configurate in precedenza. Il risultato è un file PPTX con caselle di testo e forme modificabili, pronto per essere aperto in PowerPoint.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Cosa vedrai:** Apri `SheetWithEditableShapes.pptx` in PowerPoint. La prima riga appare come titolo, tutte le celle da `A1:G20` sono renderizzate, e le forme aggiunte in Excel sono ancora spostabili e modificabili. Nessuna immagine rasterizzata—solo oggetti nativi di PowerPoint.

## Esempio completo funzionante – tutti i passaggi combinati

Di seguito trovi il programma completo, pronto per il copia‑incolla. Eseguilo come app console o integralo in qualsiasi soluzione più ampia.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Output previsto:** Dopo l'esecuzione, la console stampa il messaggio di successo e il file PPTX appare nella posizione specificata. Aprendo il file vedrai una singola diapositiva con l'intervallo selezionato, caselle di testo modificabili e le eventuali forme originali.

## Domande frequenti & Trappole

| Domanda | Risposta |
|----------|----------|
| **Funziona con più fogli di lavoro?** | Sì. Scorri `workbook.Worksheets` e ripeti gli stessi passaggi per ogni foglio, cambiando il nome del file di output ogni volta. |
| **E se devo esportare più di una diapositiva?** | Chiama `workbook.Save` più volte con diversi oggetti `ImageOrPrintOptions`, ciascuno configurato con un diverso `PageSetup` se necessario. |
| **Posso cambiare le dimensioni della diapositiva?** | Usa `exportOptions.ImageFormat` per impostare DPI, o regola `sheet.PageSetup.PaperSize` prima del salvataggio. |
| **Aspose.Cells è gratuito?** | Offre una valutazione gratuita con filigrane. Per la produzione è necessaria una licenza. |
| **E le formule di Excel?** | I valori esportati sono i **risultati calcolati** al momento dell'esportazione. Se ti servono formule live in PowerPoint, serve un approccio diverso. |

## Consigli per un flusso di lavoro fluido

- **Consiglio:** Imposta `Workbook.Settings.CalcMode = CalculationModeType.Automatic` prima dell'esportazione per garantire che tutte le formule siano aggiornate.
- **Attenzione a:** Intervalli molto grandi possono provocare pressione sulla memoria. Riduci l'area di stampa al minimo necessario.
- **Suggerimento di performance:** Riutilizza una singola istanza di `ImageOrPrintOptions` se esporti molti fogli; crearne una nuova ogni volta aggiunge overhead.
- **Nota di versione:** Il codice sopra è basato su Aspose.Cells 23.10 (rilasciato novembre 2023). Le versioni successive mantengono la stessa API, ma verifica sempre le note di rilascio per eventuali breaking changes.

## Conclusione

Abbiamo visto come **impostare l'area di stampa** in un foglio Excel, ripetere la prima riga come titolo e poi **esportare excel in pptx** mantenendo caselle di testo e forme modificabili. In sintesi, ora conosci un metodo affidabile per **convertire excel in powerpoint**, **ripetere la riga del titolo** e **creare powerpoint da excel** con poche righe di C#.

Pronto per il passo successivo? Prova ad automatizzare una conversione batch di decine di report, o aggiungi layout diapositive personalizzati usando il PowerPoint SDK dopo l'esportazione. Il cielo è il limite—sperimenta, rompi le cose e goditi la potenza della generazione programmatica di documenti.

Se questo tutorial ti è stato utile, condividilo, lascia un commento con le tue personalizzazioni, o esplora le nostre altre guide su **export excel to pptx** e argomenti di automazione correlati. Buon coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}