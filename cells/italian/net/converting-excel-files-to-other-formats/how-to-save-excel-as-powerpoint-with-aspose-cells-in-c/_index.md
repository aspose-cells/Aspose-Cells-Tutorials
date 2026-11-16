---
category: general
date: 2026-11-16
description: Scopri come salvare Excel come PowerPoint e convertire Excel in PowerPoint
  programmaticamente. Questa guida passo‑passo copre anche l’esportazione di Excel
  in PPTX e il salvataggio di una cartella di lavoro come PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: it
lastmod: 2026-11-16
og_description: Salva Excel come PowerPoint usando Aspose.Cells. Segui questa guida
  per convertire Excel in PowerPoint, esportare Excel in PPTX e salvare la cartella
  di lavoro come PPTX in pochi minuti.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Salva Excel come PowerPoint – Guida completa a C#
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Come salvare Excel come PowerPoint con Aspose.Cells in C#
url: /it/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come salvare Excel come PowerPoint con Aspose.Cells in C#

Se hai bisogno di **salvare Excel come PowerPoint** programmaticamente, questo tutorial ti fornisce una soluzione completa, pronta all'uso. Che tu stia costruendo un motore di reporting o un generatore di slide automatizzato, i passaggi seguenti ti consentono di convertire un foglio di lavoro Excel in una slide PPTX modificabile in poche righe di codice.

Imparerai come **convertire Excel in PowerPoint**, esportare il foglio in un file PPTX e mantenere caselle di testo e forme modificabili – il tutto senza uscire dall'ambiente .NET.

## Prerequisiti

* .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7.2+)
* Una licenza valida di Aspose.Cells (la versione di prova gratuita è valida per la valutazione)
* Visual Studio 2022 (o qualsiasi IDE C#)
* Una cartella di lavoro Excel che contiene i dati e le forme che desideri esportare

## Passo 1: Installare Aspose.Cells

Add the Aspose.Cells NuGet package to your project:

```bash
dotnet add package Aspose.Cells
```

> **Suggerimento professionale:** usa il flag `-v` per puntare a una versione specifica, ad esempio `Aspose.Cells.24.5`.

## Passo 2: Caricare la cartella di lavoro da esportare

The first operation in the **save Excel as PowerPoint** workflow is loading the source workbook.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Perché è importante:* Caricare la cartella di lavoro ti dà accesso ai suoi fogli di lavoro, alle impostazioni di pagina e agli oggetti di disegno che diventeranno forme modificabili in PowerPoint.

## Passo 3: Configurare le opzioni di esportazione per una slide PPTX modificabile

To **convert Excel to PowerPoint** while preserving editability, you must set a few properties on `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Spiegazione:*  
* `SaveFormat = SaveFormat.Pptx` indica ad Aspose.Cells di generare un file PowerPoint.  
* `ExportEditableText` e `ExportEditableShapes` garantiscono che la slide risultante si comporti come una slide PowerPoint nativa — puoi fare clic su una casella di testo o su una forma e modificarla direttamente in PowerPoint.

## Passo 4: Definire l'area di esportazione e adattarla a una singola slide

When you **export Excel to PPTX**, you usually want a specific range to appear on the slide. Setting the print area and fitting options guarantees a clean, single‑slide output.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Perché è importante:* `PrintArea` limita l'esportazione alle celle da A1 a G30, mentre `FitToPagesTall` e `FitToPagesWide` comprimono tutto in una singola slide, evitando pagine extra indesiderate.

## Passo 5: Salvare il foglio di lavoro come file PPTX modificabile

Now you can finally **save workbook as PPTX** and complete the **save Excel as PowerPoint** process.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

After running the program, open `EditableShapes.pptx` in Microsoft PowerPoint. You’ll see a slide that mirrors the selected Excel range, and all text boxes and shapes are fully editable.

### Output previsto

* Un file chiamato `EditableShapes.pptx` situato in `C:\Output\`.
* Una slide PowerPoint contenente l'intervallo A1:G30.
* Caselle di testo, grafici e forme che puoi fare doppio clic e modificare direttamente in PowerPoint.

## Codice sorgente completo (pronto da copiare)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Domande comuni e gestione dei casi limite

| Question | Answer |
|----------|--------|
| **E se ho più fogli di lavoro?** | Itera su `workbook.Worksheets` e ripeti i passi 3‑5 per ogni foglio, cambiando il nome del file di output (ad es., `Sheet1.pptx`, `Sheet2.pptx`). |
| **Posso esportare l'intera cartella di lavoro in un unico deck PowerPoint?** | Sì. Imposta `ExportAllSheets = true` su `ImageOrPrintOptions`. Ogni foglio di lavoro diventa una slide separata. |
| **Le mie forme appaiono come immagini, non come oggetti modificabili.** | Assicurati che `ExportEditableShapes = true` e che tu stia usando Aspose.Cells 24.5+ (le versioni precedenti non hanno questa funzionalità). |
| **Il PPTX generato è troppo grande.** | Riduci l'area di stampa o abbassa la risoluzione dell'immagine tramite `exportOptions.ImageResolution`. |
| **È necessaria una licenza per l'uso in produzione?** | Una licenza a pagamento rimuove il watermark di valutazione e sblocca le prestazioni complete. La versione di prova gratuita è valida per i test. |

## Suggerimenti per un codice di produzione robusto

* **Convalida i percorsi dei file** prima di chiamare `Workbook` o `Save` per evitare `FileNotFoundException`.  
* **Avvolgi l'esportazione in un blocco try/catch** per gestire errori di licenza (`Aspose.Cells.LicenseException`).  
* **Rilascia la cartella di lavoro** (`workbook.Dispose()`) al termine per liberare le risorse non gestite.  
* **Usa I/O asincrono** (`FileStream` con `await`) se stai esportando molti fogli di grandi dimensioni in un servizio web.

## Prossimi passi

Ora che sai come **salvare Excel come PowerPoint**, puoi esplorare argomenti correlati:

* **Esporta Excel in PPTX con layout di slide personalizzati** – regola `SlideSize` e aggiungi una slide master.  
* **Converti una slide Excel in PDF** – usa `SaveFormat.Pdf` per una versione stampabile.  
* **Converti in batch una cartella di cartelle di lavoro** – combina il ciclo mostrato sopra con `Directory.GetFiles`.  

Sperimenta con diverse aree di stampa, opzioni di scala e temi PowerPoint per adattare l'output al branding della tua organizzazione.

---

*Buon coding! Se questa guida ti ha aiutato a **convertire Excel in PowerPoint**, sentiti libero di condividerla con i colleghi o aprire un issue sul repository GitHub di Aspose.Cells per ulteriore assistenza.*

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come salvare Excel come PowerPoint usando C# e Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Come salvare PPTX da Excel – Guida completa per esportare foglio Excel in PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Convertire Excel in PowerPoint – Guida completa passo‑passo](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}