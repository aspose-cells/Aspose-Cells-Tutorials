---
category: general
date: 2026-09-15
description: Scopri come copiare una tabella pivot, copiare un foglio di lavoro con
  pivot e salvare la cartella di lavoro come pptx usando Aspose.Cells in C#. Guida
  completa passo passo.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: it
lastmod: 2026-09-15
og_description: Come copiare una tabella pivot, copiare un foglio di lavoro con pivot
  e salvare la cartella di lavoro come pptx usando Aspose.Cells. Segui gli esempi
  completi e eseguibili in C#.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Come copiare la tabella pivot e esportare i fogli di lavoro – guida completa
  C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come copiare una tabella pivot preservando i fogli di lavoro
url: /it/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come copiare una tabella pivot preservando i fogli di lavoro

Se hai bisogno di **come copiare una tabella pivot** da una cartella di lavoro all'altra senza perdere la cache pivot sottostante, questa guida fornisce una soluzione pronta all'uso. Vedrai anche come **copiare un foglio di lavoro con pivot** e come **salvare una cartella di lavoro come pptx** mantenendo intatti i riquadri di testo modificabili. Tutti gli esempi utilizzano l'ultima versione di Aspose.Cells per .NET, così potrai inserire il codice in qualsiasi progetto C# e vedere risultati immediati.

Lavorare programmaticamente con file Excel spesso comporta lo spostamento di dati tra cartelle di lavoro, l'esportazione in presentazioni o l'inserimento di Smart Marker complessi. I tre frammenti di codice qui sotto coprono questi scenari comuni e spiegano perché ogni passaggio è importante.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* .NET 6.0 o versioni successive installate  
* Aspose.Cells per .NET (versione 25.11 o più recente) referenziato nel tuo progetto  
* Una cartella denominata `YOUR_DIRECTORY` dove i file di esempio saranno letti e scritti  

Non sono richiesti pacchetti NuGet aggiuntivi.

---

## Come copiare una tabella pivot con Aspose.Cells

Copiare un intervallo che contiene una tabella pivot preservando la cache pivot è una necessità frequente. I passaggi seguenti mostrano la sequenza esatta di cui hai bisogno.

### Passo 1 – Carica la cartella di lavoro sorgente che contiene la tabella pivot

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Perché*: Aspose.Cells legge la cartella di lavoro in memoria, fornendoti l'accesso a fogli, celle e tabelle pivot.

### Passo 2 – Crea una cartella di lavoro di destinazione vuota

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Perché*: Iniziare con una cartella di lavoro vuota garantisce che nessuno stile nascosto o intervallo denominato interferisca con l'operazione di copia.

### Passo 3 – Copia le righe che includono la tabella pivot

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Perché*: `CopyRows` copia i valori grezzi delle celle, i formati e i riferimenti alla cache pivot sottostante. L'intervallo deve includere l'intera area della tabella pivot.

### Passo 4 – Copia le colonne che contengono la tabella pivot

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Perché*: Le tabelle pivot si estendono sia su righe che su colonne; copiare le colonne assicura che l'intero layout della tabella venga mantenuto.

### Passo 5 – Trasferisci il foglio preparato nella cartella di lavoro di destinazione

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Perché*: Il metodo `Copy` clona il foglio di lavoro, inclusa la cache pivot, così la cartella di lavoro di destinazione mostra una tabella pivot identica.

### Passo 6 – Salva il risultato – la tabella pivot rimane intatta

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Perché*: Persistendo la cartella di lavoro si scrivono tutte le strutture interne, garantendo che la pivot possa essere aggiornata in seguito.

**Suggerimento professionale**: Dopo la copia, puoi chiamare `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` per aggiornare i dati se la sorgente è cambiata.

---

## Copia un foglio di lavoro con pivot – un’alternativa concisa

Se ti serve semplicemente duplicare un intero foglio di lavoro che già contiene una tabella pivot, puoi saltare i passaggi di copia riga/colonna e usare direttamente il metodo `Copy` a livello di foglio.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Questo approccio è utile quando il foglio di lavoro non contiene dati extra al di fuori dell'area pivot. L'operazione **copia foglio di lavoro con pivot** preserva automaticamente tutta la formattazione, gli intervalli denominati e le cache pivot.

---

## Salva una cartella di lavoro come PPTX con riquadri di testo modificabili

Esportare un foglio Excel che contiene un riquadro di testo modificabile in PowerPoint può essere necessario per dashboard di reporting. Il codice qui sotto mostra **salvare una cartella di lavoro come pptx** mantenendo il riquadro di testo modificabile.

### Passo 1 – Carica la cartella di lavoro che include il riquadro di testo

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Passo 2 – Configura le opzioni di salvataggio PPTX

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Perché*: Impostare `ExportEditableTextBox` indica ad Aspose.Cells di tradurre il riquadro di testo di Excel in una forma PowerPoint che rimane modificabile dopo l'esportazione.

### Passo 3 – Salva la cartella di lavoro come PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Risultato atteso**: Apri `Result.pptx` in PowerPoint, seleziona il riquadro di testo e modifica il suo contenuto come faresti con qualsiasi forma nativa.

**Domanda comune**: *E se avessi bisogno di mantenere il riquadro di testo bloccato?*  
Imposta `pptxOptions.ExportEditableTextBox = false`; la forma verrà convertita in un'immagine statica.

---

## Esporta uno Smart Marker che contiene un array JSON come valore di una singola cella

Gli Smart Marker ti permettono di popolare modelli Excel con strutture dati complesse. Di seguito trovi un esempio completo che dimostra **come copiare una tabella pivot**‑style gestendo l'inserimento di un array JSON in una singola cella.

### Passo 1 – Prepara lo SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Passo 2 – Inserisci uno Smart Marker nella cella A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Passo 3 – Definisci la fonte dati con un array in stile JSON

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Passo 4 – Processa la cartella di lavoro

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Passo 5 – Salva la cartella di lavoro risultante

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Verifica del risultato**: Apri `JsonSingleCell.xlsx` e conferma che la cella A1 contiene `A,B,C`. Questo dimostra come trattare una collezione come valore di una singola cella, un modello spesso necessario quando si esportano dati per sistemi downstream.

---

## Esempio completo funzionante

Di seguito trovi un unico programma che combina i tre scenari. Puoi copiare il codice in un'app console, regolare i percorsi dei file e eseguirlo per vedere tutti e tre i risultati.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Eseguendo questo programma otterrai:

* `CopyWithPivot.xlsx` – una copia perfetta della tabella pivot originale.  
* `Result.pptx` – una diapositiva PowerPoint con un riquadro di testo modificabile.  
* `JsonSingleCell.xlsx` – un foglio dove l'array JSON appare in una singola cella.

---

## Conclusione

Ora sai **come copiare una tabella pivot** in modo sicuro, come **copiare un foglio di lavoro con pivot** con una singola chiamata, e come **salvare una cartella di lavoro come pptx** preservando i riquadri di testo modificabili. Questi modelli coprono i flussi di lavoro più comuni da Excel a PowerPoint e da Excel a JSON che incontrerai nei progetti di automazione aziendale.

Successivamente, considera di approfondire:

* Aggiornare programmaticamente le tabelle pivot copiate (`PivotTable.Refresh()`)  
* Esportare in altri formati come PDF o HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Utilizzare opzioni avanzate di Smart Marker come funzioni personalizzate o formattazione condizionale  

Sentiti libero di sperimentare con intervalli diversi, più fogli di lavoro o strutture JSON più grandi. L'API Aspose.Cells ti offre un controllo granulare, così potrai adattare questi esempi a qualsiasi scenario reale. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci alternativi nei tuoi progetti.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}