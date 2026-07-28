---
category: general
date: 2026-01-14
description: Come copiare una tabella pivot usando Aspose.Cells e imparare anche a
  convertire Excel in PPTX, copiare un intervallo in un altro workbook e rendere modificabile
  una casella di testo in PPTX in un unico tutorial.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: it
og_description: Come copiare una tabella pivot e poi convertire Excel in PPTX, copiare
  un intervallo in un altro workbook e rendere modificabile la casella di testo in
  PPTX—tutto con Aspose.Cells.
og_title: Come copiare una tabella pivot in C# – Guida completa da Excel a PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Come copiare una tabella pivot in C# – Convertire Excel in PPTX, copiare l’intervallo
  e rendere la casella di testo modificabile
url: /it/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come Copiare una Tabella Pivot in C# – Guida Completa da Excel a PPTX

Come copiare una tabella pivot da una cartella di lavoro all'altra è una domanda frequente quando si automatizzano report basati su Excel. In questo tutorial vedremo tre scenari reali usando **Aspose.Cells for .NET**: copiare un intervallo di tabella pivot, esportare un foglio di lavoro in un file PPTX con una casella di testo modificabile e popolare una singola cella con un array JSON tramite Smart Markers.  

Vedrai anche come **convertire Excel in PPTX**, **copiare un intervallo in un'altra cartella di lavoro** e **rendere modificabile la casella di testo in PPTX** senza rompere alcuna formattazione. Alla fine avrai una base di codice pronta all'uso che potrai inserire in qualsiasi progetto .NET.

> **Consiglio esperto:** tutti gli esempi sono basati su Aspose.Cells 23.12, ma gli stessi concetti si applicano alle versioni precedenti con piccole modifiche all'API.

![Diagramma che mostra come una tabella pivot viene copiata, un foglio di lavoro esportato in PPTX e un array JSON inserito – flusso di lavoro per copiare una tabella pivot](how-to-copy-pivot-table-diagram.png)

---

## Cosa Ti Serve

- Visual Studio 2022 (o qualsiasi IDE C#)
- Runtime .NET 6.0 o successivo
- Pacchetto NuGet Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Due file Excel di esempio (`source.xlsx`, `chartWithTextbox.xlsx`) posizionati in una cartella di tua scelta (sostituisci `YOUR_DIRECTORY` con il percorso reale).

Non sono necessarie librerie aggiuntive; lo stesso assembly `Aspose.Cells` gestisce Excel, PPTX e Smart Markers.

---

## Come Copiare una Tabella Pivot e Conservare i Suoi Dati

Quando copi un intervallo che contiene una tabella pivot, il comportamento predefinito è incollare solo i **valori**. Per mantenere intatta la definizione della pivot devi abilitare il flag `CopyPivotTable`.

### Passo‑per‑Passo

1. **Carica la cartella di lavoro di origine** che contiene la tabella pivot.  
2. **Crea una cartella di lavoro di destinazione vuota** – riceverà l'intervallo copiato.  
3. **Usa `CopyRange` con `CopyPivotTable = true`** così la definizione della pivot viaggia con i dati.  
4. **Salva il file di destinazione** dove ti serve.

#### Esempio di Codice Completo

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Perché funziona:**  
`CopyOptions.CopyPivotTable` indica ad Aspose.Cells di clonare l'oggetto `PivotTable` sottostante anziché solo i valori renderizzati. La cartella di lavoro di destinazione ora contiene una pivot pienamente funzionante che puoi aggiornare o modificare programmaticamente.

**Caso limite:** Se la cartella di lavoro di origine utilizza fonti dati esterne, potresti dover incorporare i dati o regolare le stringhe di connessione dopo la copia, altrimenti la pivot mostrerà “#REF!”.

---

## Convertire Excel in PPTX e Rendere Modificabile la Casella di Testo

Esportare un foglio di lavoro in PowerPoint è utile per creare presentazioni direttamente dai dati. Per impostazione predefinita la casella di testo esportata diventa una forma statica, ma impostando `IsTextBoxEditable` si inverte questo comportamento.

### Passo‑per‑Passo

1. **Apri la cartella di lavoro** che contiene il grafico e la casella di testo da esportare.  
2. **Configura `ImageOrPrintOptions`** con `SaveFormat = SaveFormat.Pptx`.  
3. **Definisci un'area di stampa** che includa la casella di testo.  
4. **Abilita `IsTextBoxEditable`** così il testo potrà essere modificato dopo l'apertura del PPTX.  
5. **Salva il file PPTX**.

#### Esempio di Codice Completo

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Risultato:** Apri `result.pptx` in PowerPoint – la casella di testo che hai inserito in Excel sarà ora una normale casella di testo in cui potrai digitare. Non è necessario ricrearla manualmente.

**Errore comune:** Se il foglio di lavoro contiene celle unite che intersecano l'area di stampa, la diapositiva risultante potrebbe spostarsi. Regola l'area di stampa o separa le celle prima dell'esportazione.

---

## Copiare un Intervallo in un'Altra Cartella di Lavoro con Smart Markers (JSON → Singola Cellola)

A volte è necessario inserire un array JSON in una singola cella Excel, ad esempio quando si passa un dato a sistemi a valle che si aspettano una stringa JSON. Gli Smart Markers di Aspose.Cells possono serializzare un array come una singola cella impostando `ArrayAsSingle = true`.

### Passo‑per‑Passo

1. **Carica un modello di cartella di lavoro** che contiene un segnaposto Smart Marker (es. `&=Items.Name`).  
2. **Prepara l'oggetto dati** – un tipo anonimo con un array `Items`.  
3. **Crea un `SmartMarkerProcessor`** e applica i dati con `ArrayAsSingle`.  
4. **Salva la cartella di lavoro popolata**.

#### Esempio di Codice Completo

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Spiegazione:**  
Quando `ArrayAsSingle` è true, Aspose.Cells concatena ogni elemento di `Items.Name` in una stringa in stile JSON (`["A","B"]`) e la scrive nella cella che conteneva lo smart marker. Questo evita di creare una riga separata per ogni elemento dell'array.

**Quando usarlo:** Ideale per esportare tabelle di configurazione, payload API o qualsiasi scenario in cui il consumatore si aspetta una stringa JSON compatta anziché un layout tabellare.

---

## Suggerimenti Aggiuntivi & Gestione dei Casi Limite

| Scenario | Cosa Controllare | Correzione Suggerita |
|----------|-------------------|----------------------|
| **Tabelle Pivot di grandi dimensioni** | Picchi di utilizzo della memoria durante la copia di cache pivot molto grandi. | Usa `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` prima del caricamento. |
| **Esportazione in PPTX con Immagini** | Le immagini potrebbero essere rasterizzate a bassa DPI. | Imposta `pptxOptions.ImageResolution = 300` per diapositive più nitide. |
| **Formattazione JSON con Smart Marker** | Caratteri speciali (`"` , `\`) interrompono il JSON. | Escapalili manualmente o usa `JsonSerializer` per pre‑serializzare prima di passare agli Smart Markers. |
| **Copia di Intervalli tra Versioni Excel Diverse** | I file `.xls` più vecchi possono perdere la formattazione. | Salva la destinazione come `.xlsx` per preservare le funzionalità moderne. |

---

## Riepilogo – Come Copiare una Tabella Pivot e Fare Molto di Più

Abbiamo iniziato rispondendo a **come copiare una tabella pivot** mantenendone la funzionalità, poi ti abbiamo mostrato come **convertire Excel in PPTX**, **rendere modificabile la casella di testo in PPTX**, e infine come **copiare un intervallo in un'altra cartella di lavoro** usando Smart Markers per inserire un array JSON in una singola cella.  

Tutti e tre gli snippet sono autonomi; puoi incollarli in una nuova console app, regolare i percorsi dei file e farli girare subito.

---

## Cosa Viene Dopo?

- **Esplora altri formati di esportazione** – Aspose.Cells supporta anche PDF, XPS e HTML.  
- **Aggiorna le tabelle pivot programmaticamente** usando `PivotTable.RefreshData()` dopo la copia.  
- **Combina Smart Markers con grafici** per generare dashboard dinamiche che si aggiornano automaticamente.  

Se sei interessato a **salvare la cartella di lavoro come PPTX** con layout diapositive personalizzati, consulta la documentazione di Aspose.Cells su `SlideOptions`.  

Sentiti libero di sperimentare—cambia l'area di stampa, prova diverse `CopyOptions` o fornisci un payload JSON più complesso. L'API è sufficientemente flessibile per la maggior parte delle pipeline di reporting.

---

### Domande Frequenti

**D: `CopyPivotTable` copia anche gli slicer?**  
R: Non direttamente. Gli slicer sono oggetti separati; dopo la copia dovrai ricrearli o copiarli tramite la collezione `Worksheet.Shapes`.

**D: Posso esportare più fogli di lavoro in un unico deck PPTX?**  
R: Sì. Itera su ogni foglio di lavoro, chiama `Save` con le stesse `ImageOrPrintOptions` e imposta `pptxOptions.StartSlideNumber` per continuare la numerazione.

**D: E se il mio array JSON contiene oggetti nidificati?**  
R: Imposta `ArrayAsSingle = false` e usa un modello personalizzato che itera su

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}