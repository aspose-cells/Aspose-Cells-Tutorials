---
category: general
date: 2026-09-24
description: Esporta intervallo Excel come immagine in C# usando Aspose.Cells – guida
  passo‑passo per salvare un'area del foglio di lavoro come PNG o JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: it
lastmod: 2026-09-24
og_description: Esporta un intervallo Excel come immagine in C# con Aspose.Cells.
  Scopri come convertire qualsiasi area del foglio di lavoro, incluse le tabelle pivot,
  in PNG o JPEG in pochi minuti.
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: Esporta un intervallo di Excel come immagine con C# – guida completa ad
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: Come esportare un intervallo Excel come immagine con C# e Aspose.Cells
url: /it/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare un intervallo di Excel come immagine con C# e Aspose.Cells

Se hai bisogno di **esportare un intervallo di Excel come immagine** in un'applicazione .NET, questa guida ti mostra una soluzione completa, pronta all'uso. Che tu stia pubblicando un dashboard, incorporando una tabella pivot in una pagina web o generando una miniatura di un report, puoi trasformare qualsiasi area di un foglio di lavoro in un PNG (o JPEG) con poche righe di codice C#.

In questo tutorial imparerai a:

* Caricare un workbook esistente (`Workbook` class)  
* Definire l'esatto intervallo di celle da catturare (`PrintArea`)  
* Configurare le opzioni di esportazione immagine (`ImageOrPrintOptions`)  
* Salvare l'immagine risultante su disco  

Tutti i prerequisiti, i casi limite e le insidie comuni sono trattati così potrai adattare il codice ai tuoi progetti senza sorprese.

## Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | Fornisce le API `Workbook`, `Worksheet` e `ImageOrPrintOptions` utilizzate nell'esempio. |
| **.NET 6.0 or later** | L'esempio è destinato a .NET 6, ma qualsiasi versione di .NET Core/Framework che supporta Aspose.Cells funziona. |
| **A valid Excel file** (e.g., `input.xlsx`) | Il workbook che desideri convertire. |
| **Write permission to the output folder** | Necessario affinché `Save` abbia successo. |

Puoi installare Aspose.Cells via NuGet:

```bash
dotnet add package Aspose.Cells
```

## Esportare un intervallo di Excel come immagine – panoramica del processo

L'operazione è composta da tre fasi logiche:

1. **Carica** il workbook dal disco.  
2. **Definisci** l'area di celle che diventerà l'immagine (l'*area di stampa*).  
3. **Esporta** l'area usando `ImageOrPrintOptions` e scrivi il file.

Di seguito ogni fase è suddivisa in uno step dedicato con codice sorgente completo e spiegazione.

## Passo 1: Caricare il workbook

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**Perché è importante:**  
`Workbook` è il punto di ingresso per tutte le operazioni su Excel. Caricare il file una sola volta mantiene basso l'uso di memoria e ti permette di accedere a qualsiasi foglio successivamente.

## Passo 2: Accedere al foglio di lavoro target

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Suggerimento:** Se ti serve un foglio specifico per nome, sostituisci l'indice con `workbook.Worksheets["SheetName"]`. Questo evita errori quando la struttura del workbook cambia.

## Passo 3: Definire l'intervallo da esportare

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**Perché impostare `PrintArea`?**  
Aspose.Cells rende l'*area di stampa* quando crea un'immagine. Limitandola all'intervallo esatto, eviti spazi bianchi extra e migliori le prestazioni.

### Alternativa: Esportare l'intero foglio

Se vuoi l'intero foglio di lavoro, semplicemente ometti l'assegnazione di `PrintArea`. Aspose.Cells utilizzerà per impostazione predefinita l'intervallo usato del foglio.

## Passo 4: Configurare le opzioni di esportazione immagine

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Spiegazione delle proprietà chiave:**

* `ImageFormat` – Determina il tipo di file (`Png`, `Jpeg`, `Bmp`, ecc.). PNG è ideale per grafici e testo perché conserva bordi nitidi.  
* `HorizontalResolution` / `VerticalResolution` – Controllano la densità dei pixel. Per miniature web 96 DPI è sufficiente; per grafiche pronte per la stampa si consiglia 300 DPI.  
* `PageOrientation` – Aiuta quando l'intervallo selezionato è più largo che alto.  

## Passo 5: Esportare l'intervallo in un file immagine

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**Cosa succede dietro le quinte:**  
Quando `PrintArea` è impostato, Aspose.Cells genera un'immagine temporanea che rappresenta quell'area. L'oggetto `Pictures[0]` viene poi salvato usando le opzioni fornite.

### Gestione dei fogli di lavoro senza immagini

Se il foglio di lavoro non contiene già un'immagine (ad esempio, un file nuovo di zecca), puoi crearne una al volo:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## Esempio completo, eseguibile

Unendo tutto, ecco un'applicazione console autonoma che puoi copiare, incollare ed eseguire:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**Output previsto:**  
Un file chiamato `range.png` appare in `YOUR_DIRECTORY`. Aprendolo vedrai le celle esatte da **A1 a G20** renderizzate come immagine PNG nitida.

## Varianti comuni e gestione dei casi limite

| Scenario | Adeguamento |
|----------|------------|
| **Export to JPEG** | Modifica `ImageFormat = ImageFormat.Jpeg` e opzionalmente imposta `Quality = 90` (intervallo 0‑100). |
| **Multiple ranges** | Chiama `sheet.Pictures.Add` per ogni intervallo e salva ogni immagine con un nome file distinto. |
| **Large worksheets** | Aumenta `HorizontalResolution`/`VerticalResolution` solo per l'intervallo necessario per evitare picchi di memoria. |
| **No picture generated** | Verifica che `PrintArea` sia formattato correttamente (`"A1:G20"`). Un indirizzo non valido genera una collezione `Pictures` vuota. |
| **Saving to a stream** | Usa `pic.Save(Stream, imgOptions)` quando hai bisogno dell'immagine in memoria (ad es., per una risposta ASP.NET). |

## Consigli professionali per un'esportazione immagine affidabile

* **Convalida l'area di stampa** – Usa il parsing di `CellArea` (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) per costruire programmaticamente gli intervalli ed evitare errori di battitura.  
* **Rilascia le risorse** – Avvolgi `Workbook` in un blocco `using` se stai elaborando molti file per liberare rapidamente le risorse native.  
* **Elaborazione batch** – Quando esporti decine di intervalli, riutilizza una singola istanza di `ImageOrPrintOptions` per ridurre l'overhead di allocazione degli oggetti.  
* **Sicurezza dei thread** – Gli oggetti Aspose.Cells **non** sono thread‑safe. Crea un `Workbook` separato per ogni thread o sincronizza l'accesso.  

## Conclusione

Ora disponi di un metodo completo e pronto per la produzione per **esportare un intervallo di Excel come immagine** usando C# e Aspose.Cells. I passaggi—caricare il workbook, impostare l'area di stampa, configurare `ImageOrPrintOptions` e salvare l'immagine—coprono sia il “come” sia il “perché”, garantendo che tu possa adattare il codice a tabelle pivot, grafici o qualsiasi blocco di celle personalizzato.

Successivamente, potresti approfondire:

* **Export excel range as image** in other formats (SVG, BMP) – another secondary keyword to try.  
* **Embedding the PNG in a PDF** using Aspose.PDF for end‑to‑end report generation.  
* **Automating batch exports** across multiple workbooks with a simple console loop.

Sentiti libero di sperimentare con diverse risoluzioni, orientamenti e directory di output. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Esporta celle Excel in immagine usando Aspose.Cells .NET: Guida passo‑passo](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Esporta workbook Excel come immagine usando Aspose.Cells per Java](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Come esportare un foglio di lavoro Excel in PNG usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}