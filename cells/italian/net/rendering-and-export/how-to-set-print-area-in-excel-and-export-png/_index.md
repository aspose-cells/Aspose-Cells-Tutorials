---
category: general
date: 2026-09-27
description: Imposta l'area di stampa in Excel e scopri come esportare immagini PNG
  delle celle selezionate. Questa guida copre anche il salvataggio dell'intervallo
  come immagine e l'aggiunta di un'immagine al foglio di lavoro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: it
lastmod: 2026-09-27
og_description: Imposta l'area di stampa in Excel ed esporta PNG con Aspose.Cells.
  Segui questa guida passo‑passo per salvare l'intervallo come immagine e aggiungere
  l'immagine al foglio di lavoro.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Imposta l'area di stampa in Excel – esporta PNG in C#
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Come impostare l'area di stampa in Excel ed esportare PNG
url: /it/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come impostare l'area di stampa in Excel ed esportare PNG

Se hai bisogno di **set print area excel** prima di creare un'immagine, questa guida ti mostra esattamente come farlo. Imparerai anche **how to export png** file da un intervallo specifico, **save range as image**, e **add picture to worksheet** in un unico flusso di lavoro ripetibile.

Lavorare con Excel in modo programmatico spesso significa che desideri solo un sottoinsieme di celle — ad esempio una tabella pivot o un grafico — da trasformare in un'immagine. Definendo prima un'area di stampa, garantisci che il PNG esportato contenga esattamente le celle che ti aspetti, né più né meno. Questo tutorial ti guida passo passo, dal caricamento della cartella di lavoro al salvataggio del file PNG finale, e spiega perché ogni impostazione è importante.

## Prerequisiti

* .NET 6.0 o versioni successive installato  
* Visual Studio 2022 (o qualsiasi IDE C#)  
* Il pacchetto NuGet **Aspose.Cells for .NET** (`Install-Package Aspose.Cells`)  
* Un file Excel (`input.xlsx`) situato in una directory nota  

Questi requisiti garantiscono che il codice venga eseguito senza configurazioni aggiuntive.

## Passo 1: Carica la cartella di lavoro con cui vuoi lavorare

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

La classe `Workbook` rappresenta l'intero file Excel. Caricarla per prima ti dà accesso ai fogli di lavoro, alle celle e alle opzioni di impostazione pagina.

## Passo 2: **Set print area excel** per l'intervallo target

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

Impostare la **print area** indica a Excel (e a Aspose.Cells) quali celle appartengono alla pagina stampabile. Quando successivamente esporti il foglio come immagine, verrà renderizzata solo quest'area, il che è essenziale per un'operazione pulita di **export selected cells image**.

## Passo 3: Configura le opzioni di esportazione immagine – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` controlla il formato di output. Scegliendo `ImageFormat.Png`, garantisci un'immagine ad alta risoluzione, con sfondo trasparente, che funziona bene in contesti web e desktop.

## Passo 4: Crea un'immagine dall'intervallo definito e **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

Il metodo `Pictures.Add` inserisce una nuova immagine nel foglio di lavoro. Passando l'intervallo creato nel Passo 2, **save range as image** direttamente sul foglio, il che è utile se in seguito devi fare riferimento all'immagine in altre parti della cartella di lavoro.

## Passo 5: **Save the picture as an image file** – completando il flusso di lavoro **export selected cells image**

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

Chiamando `Save` l'immagine viene scritta nel file system usando le opzioni definite nel Passo 3. Il file risultante `selected_range.png` contiene esattamente le celle definite dal comando **set print area excel**.

## Esempio completo, eseguibile

Unendo tutti i pezzi ottieni un programma compatto che puoi inserire in qualsiasi applicazione console:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Output previsto

L'esecuzione del programma stampa:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

E troverai un file `selected_range.png` che mostra solo le celle da A1 a G20 di `input.xlsx`.

## Problemi comuni e come evitarli

| Problema | Perché accade | Soluzione |
|----------|----------------|-----------|
| L'immagine esportata contiene l'intero foglio | Nessuna area di stampa è stata definita | Assicurati di **set print area excel** prima di creare l'immagine |
| PNG è sfocato | Il DPI predefinito è basso | Imposta `imageOptions.DpiX` e `imageOptions.DpiY` a un valore più alto (ad esempio, 300) |
| Errore file non trovato | Percorso della directory errato | Usa `Path.Combine` o verifica che la cartella esista |
| L'immagine appare spostata | Indici di riga/colonna errati | I primi due parametri di `Pictures.Add` sono la cella in alto a sinistra dove l'immagine è posizionata; mantienili a `0,0` per un'esportazione pulita |

## Consiglio professionale: Esporta più intervalli in un'unica esecuzione

Se hai bisogno di **export selected cells image** per diverse aree, ripeti i Passi 2‑5 all'interno di un ciclo, modificando `printArea` ad ogni iterazione. Ricorda di assegnare a ogni immagine un nome file unico, altrimenti il salvataggio successivo sovrascriverà il file precedente.

## Conclusione

Ora sai come **set print area excel**, configurare **how to export png**, **save range as image** e **add picture to worksheet** usando Aspose.Cells. Questa soluzione end‑to‑end ti consente di trasformare qualsiasi blocco di celle in un PNG di alta qualità con poche righe di codice C#.

Successivamente, potresti approfondire:

* Aggiungere bordi o filigrane al PNG esportato (cerca *add picture to worksheet* con stile)
* Esportare direttamente in PDF per report stampabili (*export selected cells image* → flusso di lavoro PDF)
* Automatizzare il processo per più cartelle di lavoro in un lavoro batch

Sentiti libero di sperimentare con diversi intervalli, impostazioni DPI o formati immagine per adattarli alle esigenze del tuo progetto. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Imposta l'area di stampa in Excel ed esporta in PowerPoint – Guida passo‑passo](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Esporta l'area di stampa di Excel in HTML con Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Come impostare un'area di stampa in Excel usando Aspose.Cells per .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}