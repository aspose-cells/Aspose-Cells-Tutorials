---
category: general
date: 2026-10-26
description: Scopri come esportare i grafici di Excel in PowerPoint con C#. Mantieni
  la modificabilità delle forme e salva come PPTX in poche righe di codice.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: it
lastmod: 2026-10-26
og_description: Esporta i grafici di Excel in PowerPoint con C#. Questa guida ti mostra
  come mantenere le forme modificabili e salvare come PPTX usando Aspose.Cells.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: Esporta i grafici di Excel in PowerPoint con C# – guida passo‑passo
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: Come esportare i grafici di Excel in PowerPoint usando C#
url: /it/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare i grafici di Excel in PowerPoint usando C#

Se hai bisogno di **esportare i grafici di Excel in PowerPoint**, questa guida ti accompagna passo passo attraverso una soluzione completa, pronta‑da‑eseguire. Che tu stia creando un cruscotto di reporting o automatizzando presentazioni, vedrai come poche righe di codice C# mantengono le forme dei grafici completamente modificabili dopo la conversione.

In questo tutorial imparerai a:

* Caricare una cartella di lavoro Excel esistente che contiene grafici.  
* (Facoltativamente) modificare le impostazioni della cartella di lavoro prima della conversione.  
* Salvare la cartella di lavoro come file PowerPoint mantenendo la modificabilità delle forme.  

Tutto questo viene eseguito con **Aspose.Cells for .NET**, una libreria che gestisce la conversione da Excel a PowerPoint senza richiedere Microsoft Office sul server.

## Di cosa avrai bisogno

| Requisito | Motivo |
|-------------|--------|
| .NET 6.0 o versioni successive | Runtime moderno con tutte le funzionalità del linguaggio |
| Visual Studio 2022 (o qualsiasi IDE) | Editor e debugger comodi |
| **Aspose.Cells for .NET** Pacchetto NuGet | Fornisce la classe `Workbook` e il supporto `SaveFormat.Pptx` |
| Un file Excel (`ChartAndShapes.xlsx`) che contiene almeno un grafico | Fonte dei grafici che desideri esportare |

> **Suggerimento:** Usa la versione gratuita **Aspose.Cells Evaluation** per testare il codice; una chiave di licenza rimuove il watermark di valutazione.

```bash
dotnet add package Aspose.Cells
```

## Esporta i grafici di Excel in PowerPoint – flusso di lavoro completo

Di seguito il codice end‑to‑end che esegue l'esportazione mantenendo **la modificabilità delle forme**. Ogni passaggio è spiegato in dettaglio.

### Passo 1: Carica la cartella di lavoro Excel

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*La classe `Workbook` rappresenta l'intero file Excel. Il caricamento del file legge tutti i fogli di lavoro, i grafici e le forme in memoria, operazione necessaria per qualsiasi ulteriore manipolazione.*

### Passo 2: (Facoltativo) Regola le impostazioni della cartella di lavoro

Nella maggior parte dei casi le impostazioni predefinite sono sufficienti per un'esportazione pulita. Tuttavia, se devi modificare la modalità di calcolo, l'impostazione della pagina o nascondere alcuni fogli, puoi farlo qui.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Perché è importante:** Regolare le impostazioni prima della conversione garantisce che le diapositive generate riflettano lo stato esatto desiderato, soprattutto quando formule o fogli nascosti potrebbero influenzare i dati del grafico.

### Passo 3: Salva la cartella di lavoro come file PowerPoint

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*La costante `SaveFormat.Pptx` indica ad Aspose.Cells di scrivere una presentazione PowerPoint. Internamente, la libreria converte ogni grafico Excel in una forma PowerPoint che rimane completamente modificabile in Microsoft PowerPoint.*

### Passo 4: Verifica il risultato

Apri `Shapes.pptx` in PowerPoint e:

1. Seleziona un grafico su qualsiasi diapositiva.  
2. Fai clic destro → **Edit Data**.  
3. Conferma che la tabella dei dati del grafico appare e che puoi modificare i valori.

Se il grafico apre il pannello **Edit Data**, la conversione è riuscita e la **modificabilità delle forme** è preservata.

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Esempio di esportazione di grafici Excel in PowerPoint"}

## Problemi comuni e come evitarli

| Problema | Causa | Soluzione |
|-------|-------|-----|
| I grafici appaiono come immagini statiche | Uso di una versione più vecchia di Aspose.Cells che non supporta l'esportazione PPTX | Aggiorna all'ultima Aspose.Cells 23.x o successiva |
| Dati mancanti nel grafico PowerPoint | Cartella di lavoro non completamente calcolata prima dell'esportazione | Chiama `workbook.CalculateFormula()` prima di `Save` |
| Le forme non sono modificabili | Salvataggio con `SaveFormat.Xlsx` invece di `SaveFormat.Pptx` | Assicurati di passare `SaveFormat.Pptx` a `Workbook.Save` |
| Eccezione di licenza a runtime | Versione di valutazione senza licenza registrata | Registra la tua licenza con `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Caso limite: Esportare più fogli di lavoro con grafici separati

Se il tuo file Excel contiene diversi fogli di lavoro, ognuno con il proprio grafico, Aspose.Cells crea automaticamente una diapositiva separata per ogni grafico. Puoi controllare l'ordine delle diapositive riorganizzando i fogli di lavoro prima dell'operazione di salvataggio.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Suggerimento sulle prestazioni: Trasmetti l'output invece di scriverlo su disco

Quando generi file PowerPoint in una web API, evita i file temporanei scrivendo su un `MemoryStream`.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Esempio completo, eseguibile

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Output previsto:** la console stampa il messaggio di conferma, e `Shapes.pptx` si apre in PowerPoint con ogni grafico Excel che appare su una propria diapositiva. Selezionare un grafico ti permette di modificare i suoi dati, confermando che la **modificabilità delle forme** è mantenuta.

## Riepilogo e prossimi passi

Ora sai come **esportare i grafici di Excel in PowerPoint** con C# mantenendo i grafici completamente modificabili. Il fulcro della soluzione è il metodo `Workbook.Save` con `SaveFormat.Pptx`, una funzionalità di **Aspose.Cells export** che astrae la complessa gestione di Open XML.

Da qui potresti esplorare:

* Aggiungere titoli o note personalizzate alle diapositive usando l'API **Aspose.Slides**.  
* Convertire altri oggetti Excel (tabelle, immagini) insieme ai grafici.  
* Automatizzare l'elaborazione batch di più cartelle di lavoro in un servizio in background.

Sentiti libero di sperimentare con le impostazioni opzionali mostrate sopra e integrare questo modello nei tuoi flussi di reporting per una generazione di PowerPoint rapida e affidabile.

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Esporta grafico Excel in PowerPoint con C# – guida completa Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [Come esportare Excel in PowerPoint con C# – Guida completa](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Come esportare forme da Excel a PowerPoint – Guida completa](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}