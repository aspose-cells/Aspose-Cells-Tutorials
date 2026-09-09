---
category: general
date: 2026-02-09
description: Crea un intervallo di riferimento pivot in C# ed esporta l'immagine della
  tabella pivot. Scopri come salvare un intervallo Excel come PNG usando Aspose.Cells
  – guida rapida e completa.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: it
og_description: Crea un intervallo di riferimento pivot in C# ed esporta l'immagine
  della tabella pivot in PNG. Guida completa passo‑passo per salvare un intervallo
  Excel come PNG.
og_title: Crea intervallo di riferimento pivot – Esporta immagine della tabella pivot
  come PNG
tags:
- Aspose.Cells
- C#
- Excel
title: Crea intervallo di riferimento pivot – Esporta immagine della tabella pivot
  in PNG
url: /it/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea Intervallo di Riferimento Pivot – Esporta Immagine della Tabella Pivot come PNG

Hai bisogno di **creare un intervallo di riferimento pivot** in una cartella di lavoro Excel usando C#? Puoi anche **esportare l'immagine della tabella pivot** e **salvare l'intervallo Excel come png** con poche righe di codice. Nella mia esperienza, trasformare un pivot attivo in un'immagine statica è un modo pratico per incorporare analisi in report, email o dashboard senza dover includere l'intera cartella di lavoro.

In questo tutorial vedremo tutto quello che devi sapere: le librerie richieste, il codice esatto, perché ogni chiamata è importante e alcuni inconvenienti a cui potresti andare incontro. Alla fine sarai in grado di generare un file PNG di qualsiasi tabella pivot con sicurezza e comprenderai come adattare il modello a più fogli di lavoro o formati immagine personalizzati.

## Prerequisiti

Prima di iniziare, assicurati di avere:

- **Aspose.Cells for .NET** (la versione di prova gratuita funziona bene per i test).  
- **.NET 6.0** o successivo – l'API che utilizziamo è pienamente compatibile con .NET Standard 2.0+, quindi anche i framework più vecchi compileranno.  
- Un progetto C# di base (Console App, WinForms o ASP.NET – qualsiasi cosa possa fare riferimento a un pacchetto NuGet).  

Se non hai ancora installato Aspose.Cells, esegui:

```bash
dotnet add package Aspose.Cells
```

Questo è tutto – nessun COM interop, nessun Excel installato sul server.

## Passo 1: Apri la Cartella di Lavoro e Accedi al Primo Foglio

La prima cosa da fare è caricare il file della cartella di lavoro e prendere il foglio che contiene la tabella pivot. Scegliamo deliberatamente il **primo foglio** (`Worksheets[0]`) perché la maggior parte dei file demo posiziona il pivot lì, ma puoi sostituire l'indice con un nome se preferisci.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Perché è importante:* `Worksheet` è il punto di ingresso per qualsiasi operazione basata su intervalli. Se punti al foglio sbagliato, la successiva chiamata `PivotTables[0]` genererà un `IndexOutOfRangeException`.

## Passo 2: Crea Intervallo di Riferimento Pivot

Ora chiediamo alla stessa tabella pivot di fornirci un **intervallo di riferimento**. Questo intervallo rappresenta le celle esatte che compongono il pivot – intestazioni, righe di dati e totali. Il metodo `CreateReferenceRange()` gestisce internamente il lavoro pesante, occupandosi di celle unite e righe nascoste per te.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Suggerimento:** Se la tua cartella di lavoro contiene più pivot, itera `worksheet.PivotTables` e scegli quello necessario tramite la proprietà `Name`.

## Passo 3: Renderizza l'Intervallo di Riferimento come Immagine

Aspose.Cells può renderizzare qualsiasi `Range` in un'immagine. L'oggetto restituito implementa sia formati raster (PNG, JPEG) sia vettoriali (SVG). Qui richiediamo l'immagine raster predefinita, che è un oggetto compatibile con `System.Drawing.Image`.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Cosa succede dietro le quinte?* L'API cattura lo stato visivo dell'intervallo, rispettando stili delle celle, caratteri e formattazione condizionale. È essenzialmente lo stesso di fare uno screenshot, ma in modo programmatico e senza interfaccia utente.

## Passo 4: Salva l'Immagine Generata su File

Infine, persistiamo l'immagine. Il metodo `Save` sceglie automaticamente PNG quando gli fornisci un’estensione “.png”. Puoi anche passare un oggetto `SaveOptions` se hai bisogno di controllare DPI o un formato diverso.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Dopo l'esecuzione di questa riga, apri `pivot.png` e vedrai un'istantanea pixel‑perfect della tabella pivot, pronta per essere incorporata ovunque.

## Esempio Completo Funzionante

Mettendo tutto insieme, ecco un programma console autonomo che puoi copiare‑incollare ed eseguire:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Output previsto:** un file chiamato `pivot.png` situato in `YOUR_DIRECTORY`. Aprilo con qualsiasi visualizzatore di immagini – dovresti vedere la disposizione esatta del pivot originale, incluse le intestazioni di colonna, le righe di dati e i totali generali.

## Esporta Immagine della Tabella Pivot – Personalizzare Dimensione e DPI

A volte l'immagine predefinita è troppo piccola per una diapositiva di presentazione. Puoi controllare la risoluzione passando un oggetto `ImageOrVectorSaveOptions`:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Perché regolare il DPI?* Un DPI più alto produce bordi più nitidi, specialmente quando il PNG viene ingrandito in PowerPoint o in un PDF.

## Salva Intervallo Excel come PNG – Gestire più Fogli di Lavoro

Se devi esportare pivot da diversi fogli, cicla attraverso `Workbook.Worksheets` e ripeti i passaggi. Ecco uno snippet conciso:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Questo modello **export pivot table image** per ogni pivot nell'intera cartella di lavoro, e ogni file è nominato in base al suo foglio e pivot – perfetto per l'elaborazione batch.

## Problemi Comuni & Come Evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| `IndexOutOfRangeException` su `PivotTables[0]` | Il foglio non contiene tabelle pivot. | Controlla `worksheet.PivotTables.Count` prima di accedere. |
| Immagine vuota | La pivot è filtrata per nascondere tutte le righe. | Assicurati che la pivot abbia dati visibili, o chiama `pivot.RefreshData();` prima di creare l'intervallo. |
| PNG a bassa risoluzione | Il DPI predefinito è 96. | Usa `ImageOrVectorSaveOptions.Resolution` come mostrato sopra. |
| Errori di percorso file | Caratteri non validi in `YOUR_DIRECTORY`. | Usa `Path.Combine` e `Path.GetInvalidPathChars()` per sanificare. |

## Verifica – Test Rapido

Dopo aver eseguito l'esempio completo:

1. Apri `pivot.png` in Windows Photo Viewer.  
2. Verifica che le intestazioni di colonna, le righe di dati e le righe totali corrispondano alla visualizzazione di Excel.  
3. Se noti righe mancanti, ricontrolla che il metodo **RefreshData** della pivot sia stato chiamato prima di `CreateReferenceRange()`.

## Bonus: Incorporare il PNG in un Documento Word

Poiché l'immagine è già un PNG, puoi inserirla direttamente in Aspose.Words:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Ora hai un report Word che contiene l'istantanea esatta del tuo pivot – nessun copia‑incolla manuale necessario.

## Conclusione

Hai appena imparato come **creare un intervallo di riferimento pivot**, **esportare l'immagine della tabella pivot** e **salvare l'intervallo Excel come png** usando Aspose.Cells in C#. I punti chiave sono:

- Usa `PivotTable.CreateReferenceRange()` per isolare l'area visiva di una pivot.  
- Converte quell'intervallo in un'immagine con `Range.ToImage()`.  
- Salva l'immagine come PNG, eventualmente regolando il DPI per la qualità di stampa.  

Da qui puoi esplorare l'esportazione batch, formati immagine diversi (SVG, JPEG) o persino incorporare il PNG in PDF o documenti Word. Il cielo è il limite una volta che hai catturato il pivot come grafica statica.

Hai domande o uno scenario complesso? Lascia un commento qui sotto, e buona programmazione!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}