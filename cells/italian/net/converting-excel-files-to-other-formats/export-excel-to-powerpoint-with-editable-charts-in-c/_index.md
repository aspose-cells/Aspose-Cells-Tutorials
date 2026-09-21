---
category: general
date: 2026-09-21
description: Esporta Excel in PowerPoint con grafici modificabili usando Aspose.Cells.
  Segui questa guida passo‑passo per convertire un foglio di lavoro in PPTX mantenendo
  i grafici modificabili.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: it
lastmod: 2026-09-21
og_description: Esporta Excel in PowerPoint con grafici modificabili usando Aspose.Cells.
  Scopri come convertire un foglio di lavoro in PPTX mantenendo la piena modificabilità
  dei grafici.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Esporta Excel in PowerPoint con grafici modificabili – tutorial C#
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: Esporta Excel in PowerPoint con grafici modificabili in C#
url: /it/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Excel in PowerPoint con grafici modificabili in C#

Esportare Excel in PowerPoint con grafici modificabili è una necessità comune quando è necessario riutilizzare le visualizzazioni dei fogli di calcolo nelle presentazioni. Questa guida mostra come **esportare Excel in PowerPoint** mantenendo la modificabilità dei grafici, utilizzando Aspose.Cells per .NET.

Imparerai a:

* Caricare una cartella di lavoro esistente che contiene grafici e caselle di testo.  
* Configurare le opzioni di esportazione PPTX in modo che grafici e forme rimangano modificabili.  
* Convertire un foglio di lavoro specifico in un file PowerPoint che può essere aperto e modificato in Microsoft PowerPoint.

Il tutorial presuppone che tu abbia conoscenze di base di C# e una versione recente di .NET (≥ .NET 6). Non è necessaria alcuna esperienza precedente con Aspose.Cells.

---

## Esporta Excel in PowerPoint – panoramica

L'idea principale dietro **esportare Excel in PowerPoint** è trattare ogni foglio di lavoro come una sorgente di immagine che può essere renderizzata in una diapositiva PPTX. Attivando i flag `ExportChartAsEditableText` e `ExportShapeAsEditableText`, Aspose.Cells scrive i dati del grafico sottostante come oggetti di disegno PowerPoint invece di una bitmap piatta. Questo rende la diapositiva risultante completamente modificabile—proprio come un grafico creato direttamente in PowerPoint.

> **Perché usare grafici modificabili?**  
> I grafici modificabili consentono ai presentatori di regolare dati, colori o etichette senza tornare al file Excel originale, accelerando le modifiche dell'ultimo minuto e mantenendo fluido il flusso di lavoro della presentazione.

---

## Converti un foglio di lavoro in PowerPoint (worksheet to PowerPoint)

Di seguito è riportato un esempio completo e eseguibile che dimostra la conversione **worksheet to PowerPoint**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Spiegazione di ogni passaggio

| Passo | Cosa fa il codice | Perché è importante per **export excel chart pptx** |
|------|-------------------|----------------------------------------------|
| 1️⃣   | Carica `input.xlsx` in un oggetto `Aspose.Cells.Workbook`. | La cartella di lavoro fornisce l'accesso ai grafici che desideri esportare. |
| 2️⃣   | Imposta `ExportType` su `Pptx` e abilita `ExportChartAsEditableText` e `ExportShapeAsEditableText`. | Questi flag sono la chiave per **editable charts pptx** – indicano alla libreria di scrivere la geometria del grafico come oggetti di disegno PowerPoint invece di immagini raster. |
| 3️⃣   | Chiama `ConvertToImage` sul primo foglio di lavoro, producendo `Worksheet.pptx`. | Il metodo esegue l'operazione **export excel to powerpoint** e scrive un file PPTX che può essere aperto direttamente in PowerPoint. |

> **Consiglio professionale:** Se devi esportare *più* fogli di lavoro, itera su `workbook.Worksheets` e chiama `ConvertToImage` per ciascuno, opzionalmente nominando i file di output `Sheet1.pptx`, `Sheet2.pptx`, ecc.

---

## Abilita grafici modificabili nel PPTX (export excel chart pptx)

Quando `ExportChartAsEditableText` è impostato su `true`, Aspose.Cells scrive ogni grafico come una raccolta di elementi `<a:graphic>` all'interno del XML del PPTX. PowerPoint tratta quindi quegli elementi come oggetti grafico nativi, che è possibile fare doppio clic per aprire l'editor del grafico.

**Problemi comuni**

* **Licenza Aspose.Cells mancante** – Senza una licenza la libreria aggiunge una filigrana all'output. Registra una licenza all'inizio del tuo programma (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Tipi di grafico non supportati** – Sebbene la maggior parte dei grafici 2‑D (colonna, linea, torta) sia completamente modificabile, alcuni grafici 3‑D complessi o combinati potrebbero ricadere in immagini. Testa i tuoi specifici tipi di grafico se dipendi dalla piena modificabilità.  
* **Fogli di lavoro di grandi dimensioni** – L'esportazione di fogli di lavoro molto grandi può consumare molta memoria. Considera l'uso di `ExportMaxRows` o `ExportMaxColumns` in `ImageOrPrintOptions` per limitare l'area da convertire.

---

## Consigli per mantenere i grafici modificabili (editable charts pptx)

1. **Preserva gli intervalli di dati del grafico** – Assicurati che la sorgente dati del grafico risieda nello stesso foglio di lavoro che stai esportando. I riferimenti incrociati tra fogli vengono convertiti in valori statici nel PPTX.  
2. **Usa l'ultima versione di Aspose.Cells** – Le nuove versioni migliorano il supporto per funzionalità aggiuntive dei grafici e correggono bug di casi limite relativi all'esportazione PPTX.  
3. **Convalida l'output** – Dopo la conversione, apri il PPTX generato in PowerPoint e verifica di poter modificare il titolo del grafico, le serie e le etichette degli assi. Se qualche elemento appare come immagine, ricontrolla che `ExportChartAsEditableText` sia abilitato e che il tipo di grafico sia supportato.  
4. **Elaborazione batch** – Per scenari di automazione (ad esempio, generare una presentazione da molti report Excel), incapsula la logica di conversione in un metodo che accetta `Workbook`, `int worksheetIndex` e `string outputPath`. Questo isola il flusso di lavoro **export excel to powerpoint** e lo rende riutilizzabile.

---

## Riepilogo dell'esempio completo funzionante

Mettendo tutto insieme, ecco il programma minimale che puoi copiare‑incollare in un nuovo progetto console .NET:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Risultato previsto**

* Un file chiamato `Worksheet.pptx` appare in `YOUR_DIRECTORY`.  
* Aprendo il file in Microsoft PowerPoint viene mostrata una diapositiva contenente il grafico originale e le eventuali caselle di testo.  
* Facendo doppio clic sul grafico si apre l'editor dei grafici di PowerPoint, consentendo di modificare i valori delle serie, i colori o i titoli degli assi—verificando che la funzionalità **editable charts pptx** funzioni come previsto.

---

## Conclusione

Ora disponi di una soluzione completa per **esportare Excel in PowerPoint** che mantiene i grafici modificabili. Configurando `ImageOrPrintOptions` con `ExportChartAsEditableText` e `ExportShapeAsEditableText`, il processo di conversione produce un file PPTX nativo in cui i grafici si comportano esattamente come quelli creati direttamente in PowerPoint.  

Da qui puoi:

* Estendere il codice per gestire più fogli di lavoro (**worksheet to PowerPoint** per ciascuno).  
* Combinare l'esportazione con altre funzionalità di Aspose.Cells, come aggiungere titoli alle diapositive o inserire immagini.  
* Esplorare argomenti correlati come **export Excel chart PPTX** con temi personalizzati o automatizzare l'intero flusso di generazione della presentazione.

Sentiti libero di sperimentare con diversi tipi di grafico, aggiungere etichette dati o integrare questo flusso di lavoro in un sistema di reporting più ampio. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come convertire Excel in PowerPoint usando Aspose.Cells per .NET: Guida completa](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}