---
category: general
date: 2026-10-20
description: Copia la tabella pivot in una nuova cartella di lavoro usando Aspose.Cells
  e impara come esportare una forma modificabile in PowerPoint in una guida unica.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: it
lastmod: 2026-10-20
og_description: Copia la tabella pivot in una nuova cartella di lavoro usando Aspose.Cells
  ed esporta una forma modificabile in PowerPoint—codice passo‑passo che puoi eseguire
  oggi.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Copia tabella pivot in una nuova cartella di lavoro, esporta forma in PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Copia tabella pivot in una nuova cartella di lavoro, esporta forma in PowerPoint
url: /it/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copia tabella pivot in una nuova cartella di lavoro, esporta forma in PowerPoint

Se hai bisogno di **copy pivot table to new workbook** mantenendo la sua funzionalità, questa guida ti mostra esattamente come farlo con Aspose.Cells. Vedrai anche il modo più rapido per **export an editable shape to PowerPoint**, così la casella di testo rimane modificabile dopo la conversione.

Molti sviluppatori presumono che copiare un intervallo che contiene una tabella pivot perda la logica della pivot, o che le forme diventino immagini statiche quando salvate come PPTX. Questo tutorial smentisce questi miti e ti offre una soluzione affidabile, pronta per la produzione.

Nelle sezioni seguenti potrai:

* Caricare una cartella di lavoro di origine e copiare un intervallo che include una tabella pivot.
* Creare una cartella di lavoro di destinazione che contiene la stessa tabella pivot.
* Aggiungere una forma di casella di testo, modificarne il contenuto e salvare la cartella di lavoro come presentazione PowerPoint dove la casella di testo rimane modificabile.
* Comprendere perché ogni chiamata API è necessaria e come evitare gli errori più comuni.

**Prerequisiti**

* .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.7+).
* Aspose.Cells per .NET installato (`Install-Package Aspose.Cells`).
* Conoscenze di base di C# e Visual Studio (o qualsiasi IDE tu preferisca).

---

## Copia tabella pivot in una nuova cartella di lavoro

Questa sezione passo‑per‑passo dimostra come copiare un intervallo che contiene una tabella pivot e mantenere la definizione della pivot nel nuovo file.

### Step 1 – Carica la cartella di lavoro di origine e seleziona il primo foglio

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Perché?*  
`Workbook` è il punto di ingresso per qualsiasi manipolazione di Excel in Aspose.Cells. Selezionare il foglio corretto garantisce di lavorare esattamente sulla posizione della tabella pivot.

### Step 2 – Definisci l’area di celle che include la tabella pivot

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Perché?*  
La tabella pivot vive all’interno di un blocco specifico di celle. Specificando un `CellArea` che racchiude completamente la pivot, Aspose.Cells sa copiare anche la cache della pivot sottostante.

### Step 3 – Crea la cartella di lavoro di destinazione e ottieni il suo primo foglio

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Perché?*  
Una nuova cartella di lavoro garantisce l’assenza di intervalli denominati in conflitto o pivot esistenti, rendendo l’operazione di copia pulita.

### Step 4 – Copia le righe dall’area di origine al foglio di destinazione

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Perché?*  
`CopyRows` fa parte dell’API **Aspose.Cells copy rows**. Copia sia i valori delle celle sia la cache della pivot nascosta, così la tabella pivot rimane funzionale dopo lo spostamento.

### Step 5 – Salva la nuova cartella di lavoro

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Risultato*  
Apri `CopyWithPivot.xlsx` in Excel. La tabella pivot appare esattamente come nel file di origine e puoi aggiornarla o modificarla normalmente.

---

## Esporta forma modificabile in PowerPoint

Ora aggiungeremo una forma di casella di testo, ne cambieremo il contenuto e salveremo la cartella di lavoro come file PPTX. La forma rimane completamente modificabile quando aperta in PowerPoint.

### Step 1 – Crea una nuova cartella di lavoro e accedi al suo primo foglio

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Aggiungi una forma di casella di testo al foglio

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Perché?*  
`AddTextBox` crea una forma **editable textbox in PowerPoint**‑compatible. Le coordinate sono in punti; regolale per adattarle al tuo layout.

### Step 3 – Recupera la forma e modifica il suo testo

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Perché?*  
Accedere direttamente all’oggetto `Shape` ti consente di modificare proprietà come `Text`, `Font` o `Fill`. Questo passaggio dimostra come impostare programmaticamente il contenuto iniziale.

### Step 4 – Salva la cartella di lavoro come presentazione PowerPoint

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Risultato*  
Apri `Presentation.pptx` in Microsoft PowerPoint. La casella di testo appare nella prima diapositiva e puoi fare doppio clic per modificare il testo proprio come qualsiasi forma nativa di PowerPoint.

---

## Output previsto

| File | Cosa vedrai |
|------|--------------|
| `CopyWithPivot.xlsx` | Un foglio contenente la tabella pivot originale, pienamente funzionale (l’aggiornamento funziona). |
| `Presentation.pptx` | Una singola diapositiva con una casella di testo modificabile che recita “Change me in PowerPoint”. |

---

## Problemi comuni e consigli di best‑practice

* **Perdita della cache della pivot** – Se copi solo i valori delle celle (ad es., usando `CopyRows` con l’opzione `PasteOptions` impostata su `PasteValues`), la cache della pivot viene omessa e la tabella diventa statica. Usa sempre il sovraccarico predefinito di `CopyRows` mostrato.
* **Posizionamento della forma** – `AddTextBox` utilizza unità di punto, non indici di cella di Excel. Prova le coordinate su un file di esempio per evitare posizionamenti fuori dalla diapositiva.
* **Mancata corrispondenza del formato file** – Salvare una cartella di lavoro come PPTX con `SaveFormat.Pptx` converte automaticamente tutte le forme supportate. Tentare di salvare come `Pdf` rasterizzerà la forma, rendendola non modificabile.

---

## Conclusione

Ora sai come **copy pivot table to new workbook** e come **export an editable shape to PowerPoint** usando Aspose.Cells per .NET. Gli esempi di codice completi e eseguibili coprono ogni chiamata API necessaria, spiegano perché ogni passaggio è importante e mostrano i risultati attesi.

Successivamente, potresti approfondire:

* **Lavorare con i grafici** – copia grafici insieme alle tabelle pivot (`Aspose.Cells copy rows between worksheets`).
* 

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare ulteriori funzionalità dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}