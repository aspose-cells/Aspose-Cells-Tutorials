---
category: general
date: 2026-10-01
description: Aggiungi un grafico a Word con Aspose in pochi minuti. Impara a incorporare
  un grafico Excel in Word, esportare il grafico da Excel a Word, creare un documento
  Word con Aspose e salvare il grafico nel documento Word.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: it
lastmod: 2026-10-01
og_description: Aggiungi un grafico a Word con Aspose in pochi minuti. Questa guida
  mostra come incorporare un grafico Excel in Word, esportare il grafico da Excel
  a Word, creare un documento Word con Aspose e salvare il grafico nel documento Word.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Aggiungi grafico a Word con Aspose – incorpora grafico Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Come aggiungere un grafico a Word con Aspose – incorporare un grafico Excel
url: /it/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere un grafico a Word con Aspose – incorporare un grafico Excel

Se hai bisogno di **add chart to Word** rapidamente, questo tutorial ti offre una soluzione completa, pronta all'uso. Vedrai come incorporare un grafico Excel in un file Word, esportare il grafico da Excel a Word e, infine, **save chart Word document** con poche righe di C#.

Incorporare grafici è una necessità comune quando generi report, fatture o dashboard in modo programmatico. Alla fine di questa guida sarai in grado di **create Word document Aspose** che contiene qualsiasi grafico da una cartella di lavoro Excel, senza copia‑incolla manuale.

## Prerequisiti

- .NET 6.0 o versioni successive (il codice funziona anche con .NET Framework 4.7+)
- Pacchetti NuGet Aspose.Cells e Aspose.Words (installa tramite `dotnet add package Aspose.Cells` e `dotnet add package Aspose.Words`)
- Un file Excel esistente (`Chart.xlsx`) che contiene almeno un grafico
- Un ambiente di sviluppo come Visual Studio 2022 o VS Code

## Aggiungere un grafico a Word con Aspose

Di seguito trovi il programma completo e autonomo. Copialo in un nuovo progetto console, ripristina i pacchetti ed eseguilo. Il programma carica la cartella di lavoro Excel, crea un documento Word, inserisce il primo grafico e salva il risultato.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Perché ogni riga è importante

1. **Loading the workbook** – `Workbook` analizza il file Excel e ti fornisce accesso programmatico ai suoi fogli di lavoro e grafici.  
2. **Creating the Word document** – `Document` è il punto di ingresso di Aspose.Words per qualsiasi operazione di elaborazione Word.  
3. **DocumentBuilder** – Questa classe di supporto ti consente di inserire contenuti (testo, immagini, grafici) nella posizione corrente del cursore.  
4. **InsertChart** – La sovraccarico che accetta un oggetto `Aspose.Cells.Chart` copia i dati, la formattazione e le serie del grafico direttamente nel file Word. Non è necessaria alcuna conversione intermedia in immagine, preservando la qualità vettoriale.  
5. **Save** – `Save` scrive il pacchetto .docx su disco, completando il passaggio **save chart word document**.

#### Output previsto

Dopo aver eseguito il programma, apri `Chart.docx`. Vedrai lo stesso grafico memorizzato in `Chart.xlsx`, posizionato dove è stato inserito il builder (l'inizio del documento). Il grafico rimane completamente modificabile all'interno di Word (puoi ridimensionarlo, cambiare i colori o modificare l'origine dei dati).

## Incorporare un grafico Excel in Word

Se hai bisogno di incorporare più di un grafico, ripeti la chiamata `InsertChart` per ogni oggetto grafico. Ad esempio, per incorporare tutti i grafici dal primo foglio di lavoro:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**Suggerimento:** Usa `builder.Writeln()` per inserire un'interruzione di paragrafo, garantendo che ogni grafico inizi su una nuova riga.

## Esportare grafico Excel Word – gestire più fogli di lavoro

Quando i grafici sono distribuiti su più fogli di lavoro, itera attraverso la collezione `Worksheets` della cartella di lavoro:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Questo approccio **export chart Excel Word** per qualsiasi layout di cartella di lavoro, rendendo la soluzione robusta per report complessi.

## Creare documento Word Aspose – personalizzare l'aspetto

Puoi controllare la dimensione e la posizione di ogni grafico inserito modificando lo `Shape` restituito da `InsertChart`:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

Impostare `WrapType` su `Inline` garantisce che il grafico si comporti come un normale paragrafo, spesso desiderabile per la generazione automatica di documenti.

## Salvataggio del documento Word con grafico – best practices

- **Usa un nome file descrittivo** (`Report_Q1_2026.docx`) per semplificare il versionamento.
- **Rilascia gli oggetti** quando hai finito, soprattutto in processi batch di grandi dimensioni:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Valida il risultato** programmaticamente se generi molti file:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Domande comuni e casi particolari

| Question | Answer |
|----------|--------|
| *Posso inserire un grafico che non è il primo nel foglio?* | Sì. Accedilo per indice: `sheet.Charts[2]` per il terzo grafico. |
| *Cosa succede se il grafico Excel utilizza una fonte dati che non è nella cartella di lavoro?* | Aspose.Cells incorpora i dati direttamente nell'oggetto grafico, quindi il grafico rimane funzionale anche se l'intervallo di origine viene rimosso. |
| *Ho bisogno di una licenza per Aspose?* | Una valutazione gratuita funziona, ma una versione con licenza rimuove il watermark di valutazione e sblocca tutte le funzionalità. |
| *Il grafico sarà modificabile in Word dopo l'inserimento?* | Il grafico è inserito come grafico Word nativo, quindi gli utenti possono modificare serie, titoli e stili usando l'interfaccia di Word. |
| *Come inserire un grafico come immagine invece di un grafico nativo?* | Usa `builder.InsertImage(chart.ToImage())` per incorporare un'immagine raster. Questo è utile quando vuoi preservare il rendering visivo esatto senza modificabilità a livello Word. |

## Esempio completo funzionante (copia‑incolla)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Eseguendo il codice si genera un file Word (`ReportWithCharts.docx`) che contiene i risultati di **add chart to word** per ogni grafico nella cartella di lavoro di origine.

## Conclusione

Ora sai come **add chart to Word** usando Aspose.Cells e Aspose.Words, come **embed Excel chart word**, **export chart Excel Word**, **create Word document Aspose**, e infine **save chart word document**. L'approccio funziona per scenari con un solo grafico così come per cartelle di lavoro complesse con molti grafici su più fogli.

Prossimi passi che potresti esplorare:

- [Come salvare DOCX da Excel – Guida completa per esportare grafici in Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Creare cartella di lavoro Excel con grafico a torta usando Aspose.Cells .NET - Guida completa](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Creare un grafico a bolle in Excel usando Aspose.Cells .NET&#58; Guida passo‑passo](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}