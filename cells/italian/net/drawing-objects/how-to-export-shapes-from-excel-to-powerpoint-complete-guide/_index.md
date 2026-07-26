---
category: general
date: 2026-07-26
description: Come esportare forme da un foglio di lavoro Excel a PowerPoint in pochi
  passaggi – un rapido tutorial su come esportare da Excel a PPTX per sviluppatori.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: it
lastmod: 2026-07-26
og_description: Come esportare forme da Excel a PowerPoint passo dopo passo. Segui
  questo tutorial su come esportare Excel in PPTX e guarda i tuoi fogli di lavoro
  trasformarsi in diapositive modificabili.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Come esportare forme da Excel a PowerPoint – veloce e facile
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Come esportare forme da Excel a PowerPoint – Guida completa
url: /it/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare forme da Excel a PowerPoint – Guida completa

Ti sei mai chiesto **come esportare forme** da un file Excel e mantenerle modificabili in una presentazione PowerPoint? Non sei l'unico. Che tu stia costruendo una pipeline di reporting o abbia semplicemente bisogno di un modo rapido per trasformare un foglio di calcolo in una presentazione, la capacità di **convertire un foglio di lavoro in PowerPoint** senza perdere la modificabilità delle forme può farti risparmiare ore di lavoro manuale.

In questo **excel to powerpoint tutorial** ti guideremo attraverso un esempio C# completo che carica una cartella di lavoro, configura le opzioni di esportazione corrette e scrive un file PPTX in cui caselle di testo e altri oggetti di disegno rimangono modificabili. Nessun riferimento vago—solo il codice che puoi copiare, incollare ed eseguire subito.

## Cosa imparerai

- I passaggi esatti per **export excel to pptx** mantenendo la modificabilità delle forme.  
- Come la libreria `Aspose.Cells` e il suo `PptxSaveOptions` controllano il comportamento di esportazione.  
- Suggerimenti per gestire più fogli di lavoro, file mancanti e impostazioni personalizzate delle forme.  
- Un programma completo e eseguibile che puoi inserire in qualsiasi progetto .NET.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+).  
- Una licenza valida per **Aspose.Cells for .NET** (la versione di prova gratuita funziona per i test).  
- Un workbook Excel (ad es., `ShapesDemo.xlsx`) che contiene almeno una casella di testo o una forma.  
- Un ambiente di sviluppo—Visual Studio, Rider o VS Code vanno bene.

Se li hai, immergiamoci.

## Passo 1: Caricare il Workbook – Il punto di partenza per Come esportare forme  

Per prima cosa dobbiamo aprire il file Excel che contiene le forme che vogliamo mantenere modificabili.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Perché è importante:**  
L'oggetto `Workbook` è il gateway a ogni cella, grafico e oggetto di disegno all'interno del file. Prelevando il primo foglio di lavoro (`Worksheets[0]`) ci assicuriamo di lavorare su un foglio noto, ma puoi sostituire l'indice con un nome (`workbook.Worksheets["Sheet2"]`) se ti serve una scheda specifica.

> **Consiglio:** Avvolgi la chiamata di caricamento in un blocco `try / catch` per fornire un errore amichevole se il percorso del file è errato.

## Passo 2: Configurare le Opzioni di Esportazione PPTX – Il nucleo di Come esportare forme  

Ora diciamo ad Aspose.Cells di mantenere le forme modificabili nel PPTX risultante.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Perché questi flag?**  
- `ExportEditableTextBoxes` converte le caselle di testo di Excel in segnaposto di testo PowerPoint che puoi fare doppio clic e modificare.  
- `ExportEditableShapes` fa lo stesso per forme come frecce, rettangoli e SmartArt. Senza questi, gli oggetti diventano immagini statiche, vanificando lo scopo di un flusso di lavoro **convert worksheet to powerpoint**.  

Puoi anche modificare `PptxSaveOptions` per controllare la dimensione della diapositiva, il tema o se incorporare i font—utile quando la tua presentazione deve corrispondere al branding aziendale.

## Passo 3: Salvare il Foglio di lavoro come PPTX – L'ultimo pezzo di Export Excel Workbook PowerPoint  

Con le opzioni impostate, il salvataggio è semplice.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Cosa succede dietro le quinte?**  
Aspose.Cells itera su ogni oggetto di disegno nel foglio, lo mappa alla classe di forma PowerPoint corrispondente e scrive l'XML che PowerPoint legge. Poiché abbiamo abilitato i flag modificabili, l'XML contrassegna ogni forma come `Shape` anziché `Picture`, così PowerPoint la tratta come un oggetto attivo.

## Passo 4: Confermare l'Esportazione – Feedback rapido per l'utente  

Un piccolo messaggio nella console ti informa che il processo è riuscito.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Se esegui il programma e vedi il messaggio, apri `ShapesEditable.pptx` in PowerPoint. Clicca su qualsiasi casella di testo—dovresti poter modificare il testo direttamente, e trascinare una forma dovrebbe spostarla come un oggetto PowerPoint nativo.

## Passo 5: Gestire scenari reali  

Di seguito sono riportate variazioni comuni che potresti incontrare lavorando su un **excel to powerpoint tutorial**.

### Più fogli di lavoro

Se devi esportare diversi fogli in un unico PPTX, itera su `workbook.Worksheets` e chiama `worksheet.Save` con le stesse `pptxOptions`. Aspose.Cells aggiungerà automaticamente una nuova diapositiva per ogni foglio.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Layout di diapositiva personalizzati

Puoi specificare `pptxOptions.SlideSize` (ad es., `SlideSizeType.Widescreen`) per corrispondere alle dimensioni del tuo deck aziendale.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### File mancanti o permessi

Avvolgi l'intero metodo `Main` in un blocco `try`:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Questo rende il processo **export excel workbook powerpoint** robusto per pipeline di produzione.

## Esempio completo funzionante

Ecco il programma completo che puoi compilare subito. Salvalo come `ExportEditableShapes.cs`, regola i percorsi dei file e esegui `dotnet run`.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Output previsto** quando esegui il programma:

```
Exported worksheet with editable shapes.
```

Apri il `ShapesEditable.pptx` generato e vedrai ogni forma di Excel come un oggetto PowerPoint completamente modificabile—esattamente ciò che cercavi quando hai digitato **how to export shapes**.

## Domande frequenti

- **Funziona con formati Excel più vecchi (.xls)?**  
  Sì. `Workbook` può aprire file `.xls`, `.xlsx` e anche CSV. L'esportazione delle forme funziona allo stesso modo.

- **E se devo mantenere i grafici modificabili?**  
  I grafici vengono già esportati come grafici PowerPoint nativi; non servono flag aggiuntivi.

- **Posso esportare in PDF invece di PPTX?**  
  Assolutamente—basta sostituire `SaveFormat.Pptx` con `SaveFormat.Pdf` e omettere le `PptxSaveOptions`.

## Conclusione

Ora hai una risposta solida, end‑to‑end, a **how to export shapes** da Excel a un deck PowerPoint modificabile. Sfruttando le `PptxSaveOptions` di `Aspose.Cells`, conservi ogni casella di testo e oggetto di disegno, trasformando un foglio di calcolo statico in una presentazione dinamica con il minimo sforzo.

Pronto per la prossima sfida? Prova ad aggiungere master di diapositiva personalizzati, inserire immagini programmaticamente, o concatenare questa esportazione in una pipeline CI/CD che genera automaticamente deck di vendita settimanali. Il mondo **export excel workbook powerpoint** è tutto aperto—esplora!

--- 

*Se hai trovato utile questo **excel to powerpoint tutorial**, metti una stella su GitHub o condividilo con un collega che ancora copia‑incolla fogli di calcolo nelle diapositive. Buon coding!*

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [How to Export Excel Cells as Images Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}