---
category: general
date: 2026-11-19
description: Come esportare un grafico Excel come immagine PNG usando Aspose.Cells.
  Scopri come salvare l'immagine del grafico Excel e impostare il formato immagine
  PNG in pochi passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: it
lastmod: 2026-11-19
og_description: Come esportare un grafico Excel come immagine PNG con Aspose.Cells.
  Segui questa guida passo‑passo per salvare l'immagine del grafico Excel e impostare
  il formato immagine PNG in modo efficiente.
og_image_alt: How to export Excel chart as a PNG image
og_title: Come esportare un grafico Excel come immagine PNG – guida rapida in C#
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: Come esportare un grafico Excel come immagine PNG con C#
url: /it/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare un grafico Excel come immagine PNG con C#

Se hai bisogno di **how to export Excel chart** in un'immagine portatile, questa guida mostra una soluzione completa, pronta all'uso. Utilizzando Aspose.Cells puoi **save Excel chart image** in formato PNG con sole tre righe di codice, e il tutorial spiega anche come **set image format png** e **save Excel picture file** in modo sicuro.

Concluderai questo articolo con un programma eseguibile che carica una cartella di lavoro, rende il primo grafico e scrive un file `pivot.png` su disco. Nessun strumento aggiuntivo, nessun copia‑incolla manuale—solo codice C# pulito che puoi inserire in qualsiasi progetto .NET.

## Prerequisiti

* .NET 6.0 SDK o successivo (il codice funziona anche con .NET Framework 4.6+)
* Visual Studio 2022 o qualsiasi editor C#
* Una licenza Aspose.Cells per .NET (o una chiave di valutazione temporanea)
* Un file Excel (`pivot.xlsx`) che contiene almeno un grafico nel primo foglio di lavoro

Questi elementi sono le uniche dipendenze esterne; il tutorial non richiede Office installato sulla macchina.

## Passo 1: Installare Aspose.Cells

Apri un terminale nella cartella del tuo progetto ed esegui:

```bash
dotnet add package Aspose.Cells
```

Il pacchetto aggiunge lo spazio dei nomi `Aspose.Cells`, che fornisce le classi `Workbook`, `ImageOrPrintOptions` e altre necessarie per **save Excel chart image**.

## Passo 2: Creare un programma console minimale

Crea una nuova app console (`dotnet new console -n ExportChartDemo`) e sostituisci il file `Program.cs` generato automaticamente con il codice seguente. Il programma dimostra **how to export Excel chart** e include commenti che spiegano ogni decisione.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Perché ogni parte è importante

* **Loading the workbook** – `Workbook` analizza il file `.xlsx` senza necessità di Microsoft Excel installato.
* **ImageOrPrintOptions** – Questo oggetto controlla il formato di output. Impostare `ImageFormat = ImageFormat.Png` **sets image format png**, che è senza perdita e ampiamente supportato.
* **RenderToImage** – Il metodo `RenderToImage` converte il grafico (un oggetto `Picture`) in un file immagine. Il metodo gestisce anche automaticamente il ridimensionamento, DPI e trasparenza.
* **Error handling** – Il controllo `sheet.Pictures.Count == 0` previene un'eccezione a runtime se il foglio di lavoro non contiene grafici, un caso limite comune quando gli utenti puntano al foglio sbagliato.

## Passo 3: Eseguire il programma e verificare il risultato

1. Compila il progetto: `dotnet build`.
2. Eseguilo: `dotnet run --project ExportChartDemo`.

Se tutto è configurato correttamente, vedrai:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

Apri `pivot.png` con qualsiasi visualizzatore di immagini. Dovresti vedere la rappresentazione visiva esatta del grafico Excel, confermando che hai **saved Excel picture file** con successo.

### Output previsto

Di seguito è un esempio di come potrebbe apparire il PNG esportato

![Grafico Excel esportato salvato come immagine PNG](images/exported-chart.png){: .center alt="Come esportare un grafico Excel come immagine PNG"}

## Passo 4: Opzioni avanzate – esportare più grafici

Se la tua cartella di lavoro contiene più di un grafico, puoi iterare la collezione `Pictures`:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Questo schema ti consente di **save Excel chart image** per ogni grafico nel foglio, utile per pipeline di reporting.

## Problemi comuni e come evitarli

| Sintomo | Probabile causa | Soluzione |
|---------|-----------------|-----------|
| `ArgumentOutOfRangeException` on `Pictures[0]` | Il foglio di lavoro non ha grafico o il grafico è su un foglio diverso. | Verifica l'indice del foglio (`Worksheets[0]`) e assicurati che il grafico esista. Usa `Worksheets["SheetName"]` se necessario. |
| Exported image is blurry | DPI impostato troppo basso (default 96). | Aumenta `HorizontalResolution` e `VerticalResolution` in `ImageOrPrintOptions`. |
| PNG file is empty or corrupted | Licenza mancante che causa restrizioni di valutazione. | Applica una licenza valida di Aspose.Cells prima di caricare la cartella di lavoro (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| File path errors (`FileNotFoundException`) | Segnaposto `YOUR_DIRECTORY` errato. | Usa percorsi assoluti o `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`. |

Affrontare questi problemi garantisce un'esperienza fluida di **save excel picture file**.

## Consiglio professionale: Esportare direttamente in uno stream di memoria

A volte hai bisogno dell'immagine in memoria (ad esempio, per caricarla su un'API web) invece di scriverla su disco:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

La stessa logica di **set image format png** si applica; basta sostituire il percorso del file con uno stream.

## Conclusione

Ora sai **how to export Excel chart** come file PNG usando Aspose.Cells per .NET. Il tutorial ha coperto:

* Installare la libreria
* Caricare una cartella di lavoro
* **Setting image format png**
* **Saving Excel chart image** su disco
* Gestire più grafici e errori comuni

Con questa base puoi integrare l'esportazione dei grafici in report automatizzati, servizi web o utility desktop. Successivamente, esplora argomenti correlati come **save excel picture file** come JPEG (`ImageFormat.Jpeg`) o la conversione dei grafici in PDF per report stampabili.

Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Converti grafico a torta Excel in immagine usando Aspose.Cells .NET&#58; Guida passo‑passo](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Esporta grafico come PNG – Guida completa per convertire Excel in HTML con Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Esporta celle Excel in immagine usando Aspose.Cells .NET&#58; Guida passo‑passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}