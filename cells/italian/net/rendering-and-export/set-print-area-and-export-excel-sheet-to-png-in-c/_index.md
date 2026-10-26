---
category: general
date: 2026-10-26
description: Imposta l'area di stampa ed esporta un foglio Excel in PNG con C#. Scopri
  le opzioni di esportazione dell'immagine, come esportare in PNG e ottenere un'immagine
  stampabile da una cartella di lavoro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: it
lastmod: 2026-10-26
og_description: Imposta l'area di stampa ed esporta un foglio Excel in PNG in C#.
  Questo tutorial passo‑passo copre le opzioni di esportazione delle immagini e come
  esportare PNG da una cartella di lavoro.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Imposta l'area di stampa ed esporta il foglio Excel in PNG – Guida C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Imposta l'area di stampa ed esporta il foglio Excel in PNG in C#
url: /it/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Imposta l'area di stampa ed esporta il foglio Excel in PNG con C#

Se hai bisogno di **impostare l'area di stampa** prima di esportare un foglio Excel in PNG, questa guida ti mostra come fare. Vedrai un esempio completo in C# che configura le opzioni di esportazione dell'immagine, regola l'area di stampa del foglio di lavoro e salva il risultato come immagine.

Esportare un foglio Excel in PNG è una necessità comune quando vuoi inserire un'istantanea del foglio di lavoro in un report, email o pagina web. Il codice qui sotto funziona con qualsiasi cartella di lavoro che contiene una tabella pivot, ma la tecnica è valida anche per intervalli di dati regolari. Non sono necessari strumenti esterni—solo la libreria Aspose.Cells per .NET.

## Prerequisiti

- .NET 6.0 o successivo (l'esempio è destinato a .NET 6, ma funziona con qualsiasi versione recente di .NET)
- Aspose.Cells per .NET (installazione tramite NuGet: `Install-Package Aspose.Cells`)
- Familiarità di base con C# e i concetti di Excel come fogli di lavoro e aree di stampa

## Passo 1: Configura le opzioni di esportazione dell'immagine

La prima cosa da fare è creare un'istanza di `ImageOrPrintOptions`. Questo oggetto indica ad Aspose.Cells come rendere il foglio come immagine.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Perché è importante:** `ImageOrPrintOptions` controlla il formato di output, la risoluzione e altri dettagli di rendering. L'uso del PNG garantisce una qualità senza perdita, ideale per report che richiedono testo e grafica nitidi.

## Passo 2: Carica la cartella di lavoro e accedi al foglio di lavoro target

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Perché è importante:** Devi lavorare con un oggetto `Worksheet` specifico perché l'area di stampa è una impostazione a livello di foglio di lavoro.

## Passo 3: Identifica l'intervallo che vuoi stampare

In molti scenari i dati di interesse si trovano all'interno di una tabella pivot. Il codice seguente estrae l'intervallo di dati della prima tabella pivot nel foglio.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Se il tuo foglio di lavoro non contiene una tabella pivot, puoi sostituire `pivotDataRange` con qualsiasi `CellArea` crei manualmente, ad esempio:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Passo 4: **Imposta l'area di stampa** per corrispondere all'intervallo selezionato

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Perché è importante:** L'area di stampa indica a Excel (e ad Aspose.Cells) quali celle includere quando il foglio viene renderizzato come immagine. Allineando l'area di stampa con l'intervallo di dati della pivot, eviti margini vuoti e garantisci che il PNG esportato contenga solo i dati rilevanti.

## Passo 5: Esporta il foglio di lavoro in un'immagine PNG

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Perché è importante:** `worksheet.ToImage` rispetta l'area di stampa impostata in precedenza, quindi il file PNG contiene esattamente le celle che hai definito. Assegnare l'immagine a una forma immagine ti permette di reinserirla nella cartella di lavoro se necessario, mentre salvarla su disco ti fornisce un file autonomo.

## Esempio completo funzionante

Unendo tutti i passaggi ottieni un programma autonomo che puoi eseguire immediatamente.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Output previsto

L'esecuzione del programma crea `C:\Temp\WorksheetExport.png`. Aprendo il file si visualizza un'immagine PNG nitida che contiene solo le celle definite dall'**area di stampa impostata** (i dati della tabella pivot in questo esempio). L'immagine può essere inserita in documenti Word, diapositive PowerPoint o pagine web senza passaggi di conversione aggiuntivi.

## Gestione di più fogli di lavoro o tabelle pivot

- **Più fogli di lavoro:** Scorri `wb.Worksheets` e ripeti i passaggi 3‑5 per ogni foglio che devi esportare.
- **Più tabelle pivot:** Scegli la `PivotTables[index]` appropriata o itera su `worksheet.PivotTables` per esportare ogni tabella singolarmente.
- **Nessuna tabella pivot:** Crea manualmente un `CellArea` (vedi il commento nel Passo 3) e assegnalo a `PrintArea`.

## Consigli pratici (E‑E‑A‑T)

- **Consiglio professionale:** Imposta `HorizontalResolution` e `VerticalResolution` a 300 DPI per PNG pronti per la stampa; valori più bassi riducono le dimensioni del file per l'uso web.
- **Attenzione alle forme immagine vuote:** Se il foglio di lavoro non ha forme immagine, aggiungine una prima di assegnare l'immagine:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Prestazioni:** Riutilizzare una singola istanza di `ImageOrPrintOptions` per più fogli di lavoro evita allocazioni non necessarie.
- **Compatibilità:** Aspose.Cells 23.9+ supporta pienamente .NET 6 e versioni successive; versioni precedenti potrebbero richiedere aggiustamenti ai nomi delle API.

## Conclusione

Ora sai come **impostare l'area di stampa** ed esportare un Excel


## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche illustrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}