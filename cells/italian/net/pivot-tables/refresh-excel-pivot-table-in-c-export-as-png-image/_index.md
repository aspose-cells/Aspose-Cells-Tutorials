---
category: general
date: 2026-02-23
description: Aggiorna la tabella pivot di Excel in C# ed esportala come immagine PNG.
  Impara a caricare una cartella di lavoro Excel in C#, aggiornare la pivot e salvare
  il risultato.
draft: false
keywords:
- refresh excel pivot table
- load excel workbook c#
- export pivot as image
- export excel pivot image
language: it
og_description: Aggiorna la tabella pivot di Excel in C# ed esportala come immagine
  PNG. Guida passo‑passo con codice completo e consigli pratici.
og_title: Aggiorna la tabella pivot di Excel in C# – Esporta come immagine PNG
tags:
- C#
- Excel
- Aspose.Cells
- Data Automation
title: Aggiorna tabella pivot di Excel in C# – Esporta come immagine PNG
url: /it/net/pivot-tables/refresh-excel-pivot-table-in-c-export-as-png-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiorna la tabella pivot di Excel in C# – Esporta come immagine PNG

Hai mai dovuto **aggiornare una tabella pivot di Excel** da un'applicazione C# e poi trasformarla in un'immagine? Non sei l'unico a grattarsi la testa per questo. In questo tutorial vedremo passo passo come **aggiornare una tabella pivot di Excel**, **caricare una cartella di lavoro Excel in C#**, e infine **esportare la pivot come immagine** — il tutto in un frammento di codice pulito e eseguibile.

Alla fine otterrai un file PNG che appare esattamente come la pivot che vedresti in Excel, pronto per essere inserito in report, email o dashboard. Nessun copia‑incolla manuale, nessun COM interop complicato, solo codice .NET semplice.

## Prerequisiti

- .NET 6+ (o .NET Framework 4.7+)
- Aspose.Cells per .NET (versione di prova gratuita o con licenza) – puoi ottenerlo da NuGet con `Install-Package Aspose.Cells`.
- Un file `input.xlsx` esistente che contiene almeno una tabella pivot.
- Una cartella in cui hai i permessi di scrittura per l'immagine di output.

> **Suggerimento:** Se usi Visual Studio, abilita **nullable reference types** (`<Nullable>enable</Nullable>`) per rilevare i bug legati a null in anticipo.

---

## Passo 1: Carica la cartella di lavoro Excel in C#

La prima cosa di cui abbiamo bisogno è un oggetto `Workbook` che punti al nostro file di origine. Consideralo come l'apertura del file Excel in modo programmatico.

```csharp
using System;
using Aspose.Cells;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // The rest of the steps follow…
```

**Perché è importante:** Caricare la cartella di lavoro ci dà accesso ai fogli di lavoro, alle celle e — soprattutto — alle tabelle pivot che hai creato. Se il file non viene trovato, Aspose genera una chiara `FileNotFoundException`, che puoi gestire per un fallback elegante.

---

## Passo 2: Configura le opzioni di esportazione immagine (Esporta la pivot come immagine)

Aspose.Cells ti permette di definire come deve essere renderizzata la pivot. Qui richiediamo un PNG perché è senza perdita e ampiamente supportato.

```csharp
        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            // Optional: set resolution for sharper output
            HorizontalResolution = 300,
            VerticalResolution = 300
        };
```

**Perché PNG?** A differenza del JPEG, il PNG conserva le linee di griglia nitide e le sfumature di testo su cui le tabelle pivot fanno affidamento. Se ti serve un file più piccolo, puoi passare a `ImageFormat.Jpeg` e regolare la qualità, ma perderai un po' di nitidezza.

---

## Passo 3: Aggiorna la tabella pivot

Prima di catturare l'immagine, dobbiamo assicurarci che la pivot rifletta i dati più recenti. Questo è il fulcro di **aggiornare la tabella pivot di Excel**.

```csharp
        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();
```

**Cosa succede dietro le quinte?** `Refresh()` ricalcola la pivot in base all'intervallo di origine. Se hai aggiunto righe ai dati di origine dopo aver salvato la cartella di lavoro, questa chiamata le incorpora. Saltare questo passo produce un'immagine obsoleta che non corrisponde ai dati attuali.

---

## Passo 4: Renderizza la tabella pivot in PNG (Esporta l'immagine della pivot di Excel)

Ora che tutto è aggiornato, possiamo renderizzare la pivot direttamente in un file immagine.

```csharp
        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = @"YOUR_DIRECTORY\pivot.png";
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");
    }
}
```

**Risultato:** Apri `pivot.png` e vedrai un'istantanea pixel‑perfect della pivot aggiornata. Questo file può essere allegato a un'email, inserito in una pagina web o inviato a un motore di reporting.

### Output previsto

```
Pivot table exported successfully to: YOUR_DIRECTORY\pivot.png
```

Se navighi nella cartella, il PNG dovrebbe mostrare le stesse righe, colonne e filtri che vedresti in Excel.

---

## Gestione dei casi limite comuni

| Situazione | Cosa fare |
|-----------|-----------|
| **Più tabelle pivot** | Itera su `worksheet.PivotTables` e chiama `Refresh()` / `RenderToImage()` per ciascuna. |
| **Nomi di foglio dinamici** | Usa `wb.Worksheets[wb.Worksheets.IndexOf("SheetName")]` o cerca tramite `worksheet.Name`. |
| **Set di dati di grandi dimensioni** | Imposta `imgOptions.OnePagePerSheet = false` e definisci `imgOptions.PageWidth`/`PageHeight` per controllare l'impaginazione. |
| **Licenza Aspose.Cells mancante** | La versione di prova aggiunge una filigrana. Acquista una licenza e chiama `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` prima di caricare la cartella di lavoro. |
| **Problemi di percorso file** | Usa `Path.Combine(Environment.CurrentDirectory, "input.xlsx")` per evitare separatori hard‑coded. |

---

## Suggerimenti professionali e migliori pratiche

- **Gestisci correttamente le risorse** – Avvolgi il `Workbook` in un blocco `using` o chiama `wb.Dispose()` al termine per liberare le risorse native.
- **Cache delle immagini renderizzate** – Se hai bisogno ripetutamente della stessa immagine pivot, memorizza il PNG su disco e riutilizzalo invece di renderizzarlo ogni volta.
- **Sicurezza dei thread** – Ogni thread dovrebbe lavorare con la propria istanza di `Workbook`; gli oggetti Aspose.Cells non sono thread‑safe.
- **Prestazioni** – Renderizzare pivot di grandi dimensioni può richiedere molta memoria. Imposta `imgOptions.ImageFormat` a `Bmp` per velocità maggiore ma file più grandi, o riduci il DPI per renderizzazioni più rapide.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class PivotExportDemo
{
    static void Main()
    {
        // 👉 Step 1: Load the workbook and obtain the first worksheet
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.xlsx");
        if (!File.Exists(inputPath))
        {
            Console.Error.WriteLine($"File not found: {inputPath}");
            return;
        }

        Workbook wb = new Workbook(inputPath);
        Worksheet worksheet = wb.Worksheets[0];

        // 👉 Step 2: Configure image export options to use PNG format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 👉 Step 3: Refresh the first pivot table so it reflects the latest data
        if (worksheet.PivotTables.Count == 0)
        {
            Console.Error.WriteLine("No pivot tables found on the first worksheet.");
            return;
        }

        PivotTable pivot = worksheet.PivotTables[0];
        pivot.Refresh();

        // 👉 Step 4: Export the refreshed pivot table as a PNG image
        string outputPath = Path.Combine(Environment.CurrentDirectory, "pivot.png");
        pivot.RenderToImage(imgOptions, outputPath);

        Console.WriteLine($"Pivot table exported successfully to: {outputPath}");

        // Clean up
        wb.Dispose();
    }
}
```

Esegui il programma, apri `pivot.png` e vedrai la tabella pivot aggiornata esattamente come appare in Excel.

---

## Domande frequenti

**D: Questo funziona con file .xlsx creati da LibreOffice?**  
R: Sì. Aspose.Cells legge il formato Open XML indipendentemente dall'applicazione di origine, quindi puoi **caricare una cartella di lavoro Excel in C#** da LibreOffice, esportazione di Google Sheets o qualsiasi altra fonte.

**D: Posso esportare più fogli di lavoro contemporaneamente?**  
R: Assolutamente. Itera su `wb.Worksheets` e applica la stessa logica `RenderToImage` per ogni foglio. Ricorda solo di assegnare a ciascun output un nome file unico.

**D: E se la pivot utilizza una fonte dati esterna?**  
R: Aspose.Cells può aggiornare le connessioni esterne se sono incorporate nel file, ma dovrai fornire la stringa di connessione e le credenziali programmaticamente. Consulta la documentazione di Aspose per `DataSourceOptions`.

---

## Conclusione

Ora disponi di una soluzione solida, end‑to‑end, per **aggiornare la tabella pivot di Excel** da C# e **esportare l'immagine della pivot di Excel** come PNG. Il codice mostra come **caricare una cartella di lavoro Excel in C#**, configurare le impostazioni dell'immagine, garantire che la pivot rifletta i dati più recenti e infine renderizzarla in un file.

Successivamente, potresti esplorare **esportare la pivot come immagine** in altri formati (PDF, SVG) o automatizzare il processo per più cartelle di lavoro in un lavoro batch. Vuoi inserire il PNG in un report Word? La stessa classe `ImageOrPrintOptions` funziona con Aspose.Words.

Sentiti libero di sperimentare, rompere le cose e fare domande nei commenti — buona programmazione!

![Screenshot della tabella pivot di Excel](image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}