---
category: general
date: 2026-10-10
description: Converti Excel in PowerPoint e imposta l'area di stampa in C# con Aspose.Cells
  – scopri come esportare Excel, impostare l'area di stampa e generare un file PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: it
lastmod: 2026-10-10
og_description: Converti Excel in PowerPoint con Aspose.Cells. Questo tutorial mostra
  come impostare l'area di stampa, esportare Excel e creare un file PPTX in C#.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Converti Excel in PowerPoint – guida completa per gli sviluppatori C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Converti Excel in PowerPoint e imposta l'area di stampa
url: /it/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Converti Excel in PowerPoint e imposta l'area di stampa

Se hai bisogno di **convert Excel to PowerPoint**, questa guida ti mostra esattamente come farlo in C#. Definendo prima un'area di stampa, controlli quali celle appaiono su ogni diapositiva e il file PPTX finale corrisponde alle tue aspettative di layout. La soluzione risponde anche a “how to export Excel” e “how to set print area” utilizzando la stessa base di codice.

In questo tutorial imparerai a:

* Caricare una cartella di lavoro esistente.
* Impostare l'area di stampa per un foglio di lavoro (il passaggio **set print area excel**).
* Configurare le opzioni di conversione per l'output PowerPoint.
* Generare un file **convert excel to pptx** con una singola chiamata di metodo.

Tutto il codice necessario è incluso, così puoi copiarlo, incollarlo ed eseguirlo immediatamente.

## Prerequisiti

Prima di iniziare, assicurati di avere:

| Requisito | Perché è importante |
|-------------|----------------|
| **.NET 6.0 o successivo** | Il campione è destinato a .NET 6+, ma qualsiasi versione di .NET che supporta C# 10 funziona. |
| **Aspose.Cells for .NET** | Questa libreria fornisce `Workbook`, `ImageOrPrintOptions` e il metodo `ConvertToPdf` (usato per PPTX). Installala via NuGet: `dotnet add package Aspose.Cells` |
| **Un file Excel di input** | Il tutorial utilizza `input.xlsx`. Posizionalo in una cartella a cui puoi fare riferimento dal codice. |
| **Permesso di scrittura nella cartella di output** | Il programma scrive `output.pptx`. Assicurati che la directory esista e sia scrivibile. |

> **Suggerimento:** Se lavori con più fogli di lavoro, ripeti il passaggio dell'area di stampa per ogni foglio prima della conversione.

## Passo 1: Crea un nuovo progetto console C#

Apri un terminale o una finestra PowerShell ed esegui:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Questo crea un progetto nuovo chiamato **ExcelToPowerPointDemo** e aggiunge il pacchetto Aspose.Cells, che è la dipendenza principale per **how to export Excel** in altri formati.

## Passo 2: Scrivi il codice di conversione

Sostituisci il contenuto di `Program.cs` con l'esempio completo qui sotto. Il codice dimostra **convert excel to powerpoint**, mostra **how to set print area** e produce un file **convert excel to pptx**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Perché ogni parte è importante

* **Loading the workbook** – Questo è il primo passo in qualsiasi scenario **how to export Excel**. `Workbook` legge il file in memoria, fornendoti pieno accesso a fogli, celle e formattazione.
* **Setting the print area** – Assegnando `PageSetup.PrintArea`, indichi ad Aspose.Cells quali celle renderizzare. Questo è il fulcro di **set print area excel**; senza di esso, l'intero foglio verrebbe esportato, creando potenzialmente diapositive enormi e illeggibili.
* **Choosing `SaveFormat.Pptx`** – L'oggetto `ImageOrPrintOptions` ti permette di cambiare il formato di output. Impostare `SaveFormat` a `Pptx` avvia la pipeline **convert excel to pptx**.
* **Calling `ConvertToPdf`** – Nonostante il nome del metodo, quando `SaveFormat` è `Pptx` la libreria genera un file PowerPoint. Questo è il modo consigliato per **convert excel to powerpoint** in una singola chiamata.

## Passo 3: Esegui il programma

Dalla cartella del progetto, esegui:

```bash
dotnet run
```

Se tutto è configurato correttamente, dovresti vedere un output della console simile a:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Apri `output.pptx` in Microsoft PowerPoint o in qualsiasi visualizzatore compatibile. Ogni diapositiva corrisponde alla pagina stampata del foglio di lavoro, limitata all'intervallo che hai definito.

## Gestione di più fogli di lavoro

Se il tuo workbook contiene più di un foglio e desideri che ogni foglio abbia il proprio set di diapositive, itera sulla collezione:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Questo schema mostra **how to export Excel** foglio‑per‑foglio mantenendo **setting print area** individualmente.

## Casi limite e consigli di best‑practice

| Situazione | Approccio consigliato |
|-----------|----------------------|
| **Very large worksheets** | Riduci l'area di stampa o aumenta `HorizontalResolution`/`VerticalResolution` per mantenere la dimensione del PPTX gestibile. |
| **Different page orientations** | Imposta `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` prima della conversione. |
| **Custom slide size** | Usa `conversionOptions.OnePagePerSheet = false;` e regola `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Avvolgi il codice di caricamento in un blocco `try { … } catch (FileNotFoundException)` per fornire un messaggio di errore chiaro. |
| **Non‑ASCII characters** | Assicurati che il workbook sia salvato con codifica UTF‑8; Aspose.Cells gestisce Unicode automaticamente. |

## Codice sorgente completo per riferimento

Di seguito trovi l'intero programma, incluse le direttive `using` e i commenti. Salvalo come `Program.cs` all'interno del progetto creato nel **Passo 1**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Output previsto

L'esecuzione del programma produce un file PowerPoint (`output.pptx`) che contiene:

* Una diapositiva per ogni pagina stampata del foglio di lavoro.
* Solo le celle all'interno di **A1:G30** visibili su ogni diapositiva.
* Formattazione preservata (font, colori, bordi) come appaiono in Excel.

Apri il file in PowerPoint per verificare che il layout corrisponda all'area di stampa definita.

## Conclusione

Ora sai come **convert Excel to PowerPoint** impostando con precisione **set print area excel** usando Aspose.Cells in C#. Il tutorial ha coperto **how to export Excel**, ha dimostrato **how to set print area** e ha mostrato il completo **convert excel to pptx**.

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come impostare un'area di stampa in Excel usando Aspose.Cells per .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Imposta l'area di stampa in Excel ed esportala in PowerPoint – Guida passo‑per‑passo](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}