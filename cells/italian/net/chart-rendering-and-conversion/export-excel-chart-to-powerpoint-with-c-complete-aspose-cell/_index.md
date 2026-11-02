---
category: general
date: 2026-08-04
description: Esporta il grafico di Excel in PowerPoint usando Aspose.Cells in C#.
  Segui questa guida passo‑passo per la conversione da Excel a PowerPoint e mantieni
  le forme modificabili.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: it
lastmod: 2026-08-04
og_description: Esporta il grafico di Excel in PowerPoint con Aspose.Cells in C#.
  Scopri come creare un PPTX modificabile, preservare i dati del grafico e automatizzare
  la conversione da Excel a PowerPoint.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Esporta il grafico Excel in PowerPoint con C# – tutorial completo di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Esporta grafico Excel in PowerPoint con C# – guida completa ad Aspose.Cells
url: /it/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta grafico Excel in PowerPoint con C# – guida completa Aspose.Cells

Se hai bisogno di **esportare un grafico Excel in PowerPoint**, questo tutorial ti mostra come farlo con Aspose.Cells e Aspose.Slides in C#. Otterrai un file PPTX completamente modificabile che conserva i dati e le forme del grafico, rendendo la conversione pronta per ulteriori lavori di design.

Esportare grafici da Excel a PowerPoint è una necessità comune quando si costruiscono pipeline di reporting automatizzate, presentazioni di vendita o materiale formativo. In questa guida imparerai i passaggi esatti per eseguire una **conversione da Excel a PowerPoint** che mantiene tutti gli elementi del grafico modificabili. Non è necessario alcun copia‑incolla manuale e il codice funziona con .NET 6+ così come con il classico .NET Framework.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- Una licenza valida di Aspose.Cells (o una chiave di valutazione gratuita)  
- Aspose.Slides per .NET aggiunto al progetto (la libreria gestisce l'output PPTX)  
- .NET 6 SDK o versioni successive installate  
- Un workbook Excel che contenga almeno un grafico (per questo esempio usiamo `Shapes.xlsx`)  

Puoi installare i pacchetti NuGet con i seguenti comandi:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Step 1: Load the Excel workbook

La prima operazione è aprire il workbook che contiene il grafico da esportare. La classe `Workbook` rappresenta l'intero file Excel.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Perché è importante:** Caricare il workbook ti dà accesso ai fogli di lavoro, ai grafici e alla formattazione. Aspose.Cells legge il file senza richiedere l'installazione di Microsoft Office, mantenendo la soluzione leggera e adatta ai server.

## Step 2: Select the worksheet and define the print area

Un foglio di lavoro può contenere molti grafici, ma di solito si esporta una regione specifica. Impostare il `PrintArea` indica ad Aspose.Cells quali celle (inclusi i grafici) devono essere renderizzate.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Perché è importante:** Limitando l'esportazione a un'area di stampa definita eviti diapositive vuote inutili e mantieni ridotto il peso del file PPTX. L'area può essere regolata per corrispondere esattamente all'intervallo del tuo grafico.

## Step 3: Configure export options for an editable PPTX

Aspose.Cells utilizza la classe `ImageOrPrintOptions` per controllare il formato di output e la modificabilità. Impostare `ImageFormat` su `ImageFormat.Pptx` crea un file PowerPoint, mentre `ExportEditableShapes = true` preserva gli oggetti del grafico come forme modificabili.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Perché è importante:** Il flag `ExportEditableShapes` è la chiave per ottenere **forme modificabili in PowerPoint**. Senza di esso, il grafico verrebbe rasterizzato come immagine, perdendo la possibilità di modificare i punti dati o lo stile in seguito.

## Step 4: Save the worksheet as a PowerPoint presentation

Infine, invoca il metodo `Save` sull'oggetto `Workbook`. L'enumerazione `SaveFormat.Pptx` indica ad Aspose.Cells di produrre un file PowerPoint.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Quando il codice termina, apri `ShapesExport.pptx` in PowerPoint. Vedrai una diapositiva che contiene il grafico Excel originale come oggetto grafico nativo di PowerPoint. Fai doppio clic sul grafico per modificare i dati, cambiare i colori o aggiungere animazioni—proprio come se avessi creato il grafico direttamente in PowerPoint.

### Expected output

| Nome file                | Contenuto nella diapositiva                         |
|--------------------------|-----------------------------------------------------|
| `ShapesExport.pptx`      | Il grafico da `Shapes.xlsx` renderizzato come un grafico PowerPoint modificabile, con etichette degli assi, legende e serie di dati intatte. |

## Full, runnable example

Di seguito trovi il programma completo che puoi copiare, incollare ed eseguire. Include tutte le istruzioni `using` necessarie, la gestione degli errori e i commenti.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Spiegazione di ciascun blocco**

| Blocco | Scopo |
|--------|-------|
| `using` directives | Importa gli spazi dei nomi Aspose.Cells e Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Carica il file Excel senza necessità di Office installato. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Limita l'esportazione alla regione che contiene il grafico. |
| `ImageOrPrintOptions` | Configura l'output PPTX e abilita **l'esportazione PPTX di Aspose.Cells** con forme modificabili. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Scrive il file PowerPoint su disco. |
| `try / catch` | Fornisce una gestione di base degli errori per file mancanti o problemi di licenza. |

Eseguendo questo programma otterrai una diapositiva PowerPoint che potrai aprire in Microsoft PowerPoint, Google Slides (dopo conversione) o qualsiasi visualizzatore compatibile.

## Common variations and edge cases

### Exporting multiple worksheets

Se ti serve una diapositiva per ogni foglio di lavoro, itera su `workbook.Worksheets` e chiama `Save` con un nome file unico per ogni iterazione.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Controlling slide layout

Aspose.Slides ti consente di aggiungere un layout di diapositiva personalizzato dopo l'esportazione. Crea una nuova presentazione, importa la diapositiva generata e poi applica un tema master.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Handling charts with external data sources

Se un grafico fa riferimento a un intervallo di dati al di fuori dell'area di stampa definita, estendi il `PrintArea` per includere quelle celle. Altrimenti il grafico potrebbe perdere le serie di dati durante l'esportazione.

### Licensing considerations

Le librerie Aspose funzionano in modalità valutazione con una filigrana. Per rimuovere la filigrana, imposta la licenza prima di qualsiasi chiamata API:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Fai lo stesso per Aspose.Slides se utilizzi le sue funzionalità avanzate.

## Pro tips

- **Riutilizza le opzioni di esportazione:** Crea un'unica istanza di `ImageOrPrintOptions` e assegnala a ciascun foglio di lavoro per mantenere il codice DRY.  
- **Elaborazione batch:** Per reporting su larga scala, combina questa logica di esportazione con un worker in background o una Azure Function per generare file PPTX su richiesta.  
- **Prestazioni:** Se ti serve solo l'immagine del grafico (non modificabile), imposta `ExportEditableShapes = false`. Questo riduce l'uso di memoria e velocizza la conversione.  
- **Test:** Verifica il PPTX generato sia su installazioni PowerPoint Windows che macOS, poiché alcune peculiarità di rendering differiscono tra le piattaforme.

## Conclusion

Ora disponi di una soluzione completa, end‑to‑end, per **esportare un grafico Excel in PowerPoint** usando C#. Il tutorial ha coperto il caricamento del workbook, la selezione dell'area di stampa, la configurazione dell'**esportazione PPTX di Aspose.Cells** con **forme modificabili in PowerPoint**, e il salvataggio del risultato come file PPTX completamente editabile.  

Da qui puoi esplorare scenari aggiuntivi di **conversione da Excel a PowerPoint** come l'esportazione batch, layout di diapositive personalizzati o l'integrazione del processo in una Web API. Sperimenta con diversi tipi di grafico, aggiungi immagini o combina più fogli di lavoro in una singola presentazione per adattare l'output alle esigenze della tua azienda.

Pronto a automatizzare il tuo flusso di reporting? Prova a sostituire il file di origine, a regolare l'area di stampa e a integrare il codice nei tuoi servizi .NET esistenti. Buona programmazione!

## What Should You Learn Next?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}