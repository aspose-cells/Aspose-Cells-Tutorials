---
category: general
date: 2026-06-08
description: Crea opzioni di salvataggio HTML in C# per incorporare tutti i caratteri
  e salvare la cartella di lavoro come HTML. Scopri come esportare una cartella di
  lavoro Excel in HTML con un esempio semplice e completo.
draft: false
keywords:
- create html save options
- save workbook as html
- export excel workbook to html
- embed all fonts in html
language: it
og_description: Crea opzioni di salvataggio HTML in C# per incorporare tutti i font
  ed esportare la cartella di lavoro Excel in HTML. Questa guida ti accompagna passo
  passo in una soluzione completa, pronta all'uso.
og_title: Crea opzioni di salvataggio HTML in C# – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  headline: Create HTML Save Options in C# – Full Guide
  type: TechArticle
- description: Create HTML save options in C# to embed all fonts and save workbook
    as HTML. Learn how to export Excel workbook to HTML with a simple, complete example.
  name: Create HTML Save Options in C# – Full Guide
  steps:
  - name: Expected Output
    text: Running the program produces `EmbeddedWorkbook.html` in the execution folder.
      Open it in any modern browser and you’ll see the text **“Hello, Aspose.Cells!”**
      rendered in **Comic Sans MS**, even if your system doesn’t have that font installed.
      Inspect the HTML source and you’ll notice a `<style>` bl
  - name: What if the workbook contains many different fonts?
    text: Embedding *all* fonts can inflate the HTML size dramatically (each font
      is Base64‑encoded). If file size becomes a concern, consider setting `EmbedAllFonts
      = false` and manually embedding only the critical fonts via `htmlOptions.FontEmbeddingMode
      = FontEmbeddingMode.Custom;`.
  - name: Does this work with older Excel files (`.xls`)?
    text: Absolutely. Aspose.Cells abstracts the source format, so whether you load
      an `.xlsx`, `.xls`, or even a CSV, the **export excel workbook to html** step
      behaves the same.
  - name: Can I control the output folder dynamically?
    text: 'Sure thing—just replace the hard‑coded `outputPath` with something like:'
  - name: What about images or charts inside the workbook?
    text: '`HtmlSaveOptions` also handles images, charts, and even formulas. By default
      they’re rendered as PNGs embedded in the HTML. If you prefer external files,
      toggle `htmlOptions.ExportImagesAsBase64 = false`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Export
- HTML Export
title: Crea opzioni di salvataggio HTML in C# – Guida completa
url: /it/net/exporting-excel-to-html-with-advanced-options/create-html-save-options-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea opzioni di salvataggio HTML in C# – Tutorial completo

Ti sei mai chiesto come **creare opzioni di salvataggio HTML** che mantengano ogni carattere esattamente come appare in Excel? Non sei solo. Molti sviluppatori incontrano un ostacolo quando l'HTML esportato elimina i caratteri personalizzati, lasciando la pagina dall'aspetto piatto. La buona notizia? Con un paio di righe di C# puoi **incorporare tutti i caratteri in HTML** e **salvare la cartella di lavoro come HTML** senza problemi.

In questa guida percorreremo l'intero processo di **esportazione della cartella di lavoro Excel in HTML** usando Aspose.Cells. Alla fine avrai un programma autonomo e eseguibile che non solo crea le opzioni corrette ma spiega anche *perché* ogni impostazione è importante. Nessun pezzo mancante, nessun “vedi la documentazione” — solo una soluzione chiara, dall'inizio alla fine.

## Prerequisiti

* .NET 6.0 SDK (o qualsiasi versione recente di .NET) – il codice funziona sia su .NET Core che su .NET Framework.  
* Il pacchetto NuGet **Aspose.Cells** – `dotnet add package Aspose.Cells`.  
* Una conoscenza di base della sintassi C# – se sai scrivere un `Console.WriteLine`, sei pronto.  

Questo è tutto. Nessun tool aggiuntivo, nessun file di configurazione oscuro.

## Passo 1: Configura il progetto e carica una cartella di lavoro

Prima di tutto: ci serve un progetto console e una cartella di lavoro con cui lavorare. Se hai già un file Excel, ottimo—altrimenti il campione lo crea al volo.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook or load an existing one
        Workbook wb = new Workbook(); // starts with a default sheet

        // Populate the sheet with some styled text so we can see font embedding in action
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS";   // a non‑system font to test embedding
        style.Font.Size = 14;
        cell.SetStyle(style);

        // Continue with HTML export...
```

**Perché lo facciamo:** Caricare una cartella di lavoro ci dà qualcosa da esportare. Aggiungere un carattere personalizzato (`Comic Sans MS`) rende visibile in seguito l'impostazione *embed all fonts* nel HTML generato.

## Passo 2: **Crea opzioni di salvataggio HTML** – Il cuore del compito

Ora arriviamo al cuore della questione: configurare `HtmlSaveOptions`. Questo oggetto indica ad Aspose.Cells esattamente come deve essere scritto l'HTML.

```csharp
        // Step 2: Create HTML save options and embed all fonts in the output
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Setting this to true forces every used font to be base‑64 encoded
            // and placed directly inside the HTML file. No external .ttf files.
            EmbedAllFonts = true,

            // Optional but handy: keep the original Excel formatting
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };
```

**Perché `EmbedAllFonts = true` è importante:** Quando apri l'HTML risultante in un browser, i caratteri personalizzati sono già incorporati nel file. Ciò significa che la pagina appare identica alla fonte Excel, anche su macchine che non hanno il carattere installato.

## Passo 3: **Salva la cartella di lavoro come HTML** usando le opzioni configurate

Con le nostre opzioni pronte, possiamo finalmente **salvare la cartella di lavoro come HTML**. La firma del metodo accetta il percorso del file, il formato desiderato e l'oggetto opzioni che abbiamo appena creato.

```csharp
        // Step 3: Save the workbook as an HTML file using the configured options
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

**Cosa succede dietro le quinte?** Aspose.Cells rende ogni cella, converte le definizioni dei caratteri in Base64 e le inserisce in un blocco `<style>`. L'`EmbeddedWorkbook.html` risultante è un unico file autonomo—senza file `.css` o di caratteri sparsi.

## Esempio completo funzionante

Mettendo tutto insieme, ecco il programma completo che puoi copiare‑incollare in `Program.cs` e eseguire:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create or load a workbook
        Workbook wb = new Workbook();
        var sheet = wb.Worksheets[0];
        var cell = sheet.Cells["A1"];
        cell.PutValue("Hello, Aspose.Cells!");
        var style = cell.GetStyle();
        style.Font.Name = "Comic Sans MS"; // non‑standard font for testing
        style.Font.Size = 14;
        cell.SetStyle(style);

        // 2️⃣ Create HTML save options – embed all fonts
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            EmbedAllFonts = true,
            ExportColumnHeaders = true,
            ExportRowHeaders = true
        };

        // 3️⃣ Save workbook as HTML
        string outputPath = "EmbeddedWorkbook.html";
        wb.Save(outputPath, SaveFormat.Html, htmlOptions);

        Console.WriteLine($"Workbook successfully exported to {outputPath}");
    }
}
```

### Output previsto

Eseguendo il programma viene generato `EmbeddedWorkbook.html` nella cartella di esecuzione. Aprilo in qualsiasi browser moderno e vedrai il testo **“Hello, Aspose.Cells!”** renderizzato in **Comic Sans MS**, anche se il tuo sistema non ha quel carattere installato. Ispeziona il sorgente HTML e noterai un blocco `<style>` con una regola `@font-face` contenente una enorme stringa Base64—quel carattere è incorporato.

![Diagramma delle opzioni di salvataggio HTML](image.png "Diagramma del flusso di esportazione HTML"){: alt="Diagramma delle opzioni di salvataggio HTML"}

*Il testo alternativo include la parola chiave principale per SEO.*

## Domande comuni e casi particolari

### E se la cartella di lavoro contiene molti caratteri diversi?

Incorporare *tutti* i caratteri può gonfiare notevolmente le dimensioni dell'HTML (ogni carattere è codificato in Base64). Se le dimensioni del file diventano un problema, considera di impostare `EmbedAllFonts = false` e incorporare manualmente solo i caratteri critici tramite `htmlOptions.FontEmbeddingMode = FontEmbeddingMode.Custom;`.

### Funziona con file Excel più vecchi (`.xls`)?

Assolutamente. Aspose.Cells astrae il formato di origine, quindi che tu carichi un `.xlsx`, `.xls` o anche un CSV, il passo di **esportazione della cartella di lavoro Excel in HTML** si comporta allo stesso modo.

### Posso controllare dinamicamente la cartella di destinazione?

Certo—basta sostituire l'`outputPath` hard‑coded con qualcosa del tipo:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "Reports", "MyExport.html");
Directory.CreateDirectory(Path.GetDirectoryName(outputPath));
```

In questo modo puoi **salvare la cartella di lavoro come HTML** dove ti serve.

### E per quanto riguarda immagini o grafici all'interno della cartella di lavoro?

`HtmlSaveOptions` gestisce anche immagini, grafici e persino formule. Per impostazione predefinita vengono renderizzate come PNG incorporati nell'HTML. Se preferisci file esterni, imposta `htmlOptions.ExportImagesAsBase64 = false`.

## Consigli professionali

* **Suggerimento di performance:** Riutilizza una singola istanza di `HtmlSaveOptions` se stai esportando molte cartelle di lavoro in un ciclo—crea meno spazzatura.  
* **Suggerimento di test:** Usa un browser headless (ad es., Puppeteer) per verificare automaticamente che i caratteri incorporati vengano renderizzati correttamente.  
* **Controllo versione:** Il flag `EmbedAllFonts` è stato introdotto in Aspose.Cells 20.9. Assicurati che il tuo pacchetto NuGet sia aggiornato.

## Conclusione

Ora sai esattamente come **creare opzioni di salvataggio HTML** in C# che **incorporano tutti i caratteri in HTML**, e hai visto un modo pratico per **salvare la cartella di lavoro come HTML** per qualsiasi file Excel. Questo esempio completo, pronto all'uso, copre il *cosa*, il *perché* e il *come* della **esportazione della cartella di lavoro Excel in HTML**, fornendoti una solida base per scenari più avanzati come l'elaborazione batch o lo styling personalizzato.

Pronto per il passo successivo? Prova a esportare una cartella di lavoro che contiene grafici, o sperimenta con diverse proprietà di `HtmlSaveOptions` come `ExportImagesAsBase64` o `CssClassPrefix`. Lo stesso schema si applica—crea le opzioni, modifica i flag e chiama `wb.Save`. Buona programmazione, e che le tue esportazioni HTML siano sempre esattamente come i fogli Excel originali!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Prefissare gli stili degli elementi della tabella con le opzioni di salvataggio HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/prefixing-table-elements-styles/)
- [Imposta il carattere predefinito nella conversione da Excel a HTML con Aspose.Cells per .NET \| Guida alle operazioni sulla cartella di lavoro](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Esporta le proprietà della cartella di lavoro e del foglio di lavoro Excel in HTML usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}