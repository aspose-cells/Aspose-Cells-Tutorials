---
category: general
date: 2026-10-01
description: Scopri come incorporare i font in HTML durante la conversione di Excel
  in HTML usando Aspose.Cells. Esporta Excel in HTML con i font incorporati in pochi
  passaggi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: it
lastmod: 2026-10-01
og_description: Come incorporare i font in HTML durante l'esportazione di file Excel.
  Segui questa guida passo passo per convertire Excel in HTML con i font incorporati.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Come incorporare i font in HTML da Excel – Guida Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Come incorporare i font durante la conversione di Excel in HTML con Aspose.Cells
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font durante la conversione di Excel in HTML con Aspose.Cells

Incorporare i font in HTML quando si converte una cartella di lavoro Excel è fondamentale per preservare l’aspetto originale su tutti i browser. Se devi convertire Excel in HTML mantenendo intatti i font personalizzati, questa guida mostra l’intero processo. Vedrai anche come esportare Excel come HTML e perché l’incorporamento dei font in HTML è importante per una resa coerente.

Questo tutorial copre tutto ciò che devi sapere: librerie necessarie, configurazione del codice e verifica del file HTML generato. Alla fine, sarai in grado di esportare Excel come HTML con i font incorporati in poche righe di C#.

## Di cosa avrai bisogno

Prima di iniziare, assicurati di avere:

* **.NET 6.0 o successivo** – il codice è destinato a .NET 6, ma qualsiasi versione di .NET che supporti Aspose.Cells funziona.
* **Aspose.Cells per .NET** – ottieni una licenza o usa la versione di valutazione gratuita dal sito web di Aspose.
* Un ambiente di sviluppo **C#** (Visual Studio, Rider o VS Code) – qualsiasi IDE in grado di compilare progetti .NET.
* Una cartella di lavoro Excel (`Styled.xlsx`) che utilizza i font personalizzati che desideri preservare.

## Passo 1: Configura Aspose.Cells nel tuo progetto .NET

Per prima cosa, aggiungi il pacchetto NuGet Aspose.Cells al tuo progetto:

```bash
dotnet add package Aspose.Cells
```

Quindi includi lo spazio dei nomi all’inizio del tuo file C#:

```csharp
using Aspose.Cells;
```

L’aggiunta del pacchetto rende disponibili le classi `Workbook`, `HtmlSaveOptions` e le altre correlate.

## Passo 2: Carica la cartella di lavoro Excel

Caricare la cartella di lavoro è il primo passo concreto in **come esportare i dati di Excel**. Il costruttore `Workbook` legge il file dal disco:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Perché è importante:* Aspose.Cells analizza la cartella di lavoro, includendo stili delle celle, formule e informazioni sui font. Se il file non viene trovato, viene generata un’eccezione, quindi assicurati che il percorso sia corretto.

## Passo 3: Configura le opzioni di salvataggio HTML per incorporare i font

Il fulcro di **incorporare i font in html** è la classe `HtmlSaveOptions`. Imposta `EmbedFonts` su `true` affinché ogni font usato nella cartella di lavoro venga scritto nell’output HTML come regola `@font-face` codificata in Base64.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Perché è importante:* Per impostazione predefinita Aspose.Cells fa riferimento a file di font esterni, che potrebbero non essere disponibili sulla macchina client. Abilitare `EmbedFonts` garantisce che l’HTML renderizzato abbia lo stesso aspetto del foglio Excel originale, indipendentemente dai font installati sul visualizzatore.

### Caso limite: font non supportati

Se la cartella di lavoro utilizza un font non installato sul server, Aspose.Cells ricade su un font di sistema predefinito. Per evitare ciò, installa i font richiesti sul server o incorporali manualmente dopo l’esportazione.

## Passo 4: Salva la cartella di lavoro come HTML usando le opzioni configurate

Ora puoi scrivere il file HTML. Il metodo `Save` accetta il percorso di output e l’istanza `HtmlSaveOptions`:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Al termine dell’esecuzione, `Styled.html` contiene i dati del foglio di calcolo e un blocco `<style>` con le definizioni `@font-face` codificate in Base64 per ciascun font personalizzato.

## Passo 5: Verifica i font incorporati

Apri `Styled.html` in un browser. Ispeziona la sezione `<head>`; dovresti vedere qualcosa di simile a:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Se i font compaiono correttamente nella tabella renderizzata, l’incorporamento è riuscito. Se noti caratteri mancanti, ricontrolla che i file di font di origine siano installati sulla macchina che esegue la conversione.

## Variazioni comuni e opzioni aggiuntive

### Conversione di più fogli di lavoro

Se devi **convertire Excel in HTML** per tutti i fogli, imposta `ExportActiveWorksheetOnly = false` (valore predefinito). Aspose.Cells creerà un file HTML separato per ogni foglio.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### Controllo dell’output CSS

Puoi ridurre le dimensioni dell’HTML disabilitando il CSS inline:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Utilizzare uno stream anziché un file

Quando integri la funzionalità in una Web API, scrivi l’HTML in un `MemoryStream` e restituiscilo direttamente:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Suggerimento professionale: licenzia il prodotto per rimuovere le filigrane di valutazione

Se stai usando la versione di valutazione, l’HTML generato potrebbe contenere un commento di filigrana. Applica la licenza Aspose.Cells prima di caricare la cartella di lavoro per produrre un output pulito:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Esempio completo funzionante

Di seguito trovi un programma completo, eseguibile, che dimostra **come incorporare i font**, **convertire excel in html** e **esportare excel come html** in un unico passaggio:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Output previsto:** Dopo aver eseguito il programma, `Styled.html` appare in `YOUR_DIRECTORY`. Aprendo il file in qualsiasi browser moderno, vedrai il foglio di calcolo con gli stessi font del file Excel originale, anche su macchine che non possiedono quei font.

## Conclusione

Ora sai **come incorporare i font** quando **converti Excel in HTML** usando Aspose.Cells, e hai visto l’intero flusso dal caricamento della cartella di lavoro alla verifica dei font incorporati. Questo approccio garantisce che la fedeltà visiva dei tuoi file Excel sia mantenuta nell’HTML generato, rendendolo ideale per report web, newsletter email o qualsiasi scenario in cui devi **esportare Excel come HTML** con tipografia personalizzata.

Successivamente, esplora argomenti correlati come **esportare Excel come PDF**, **stilizzare l’output HTML con CSS personalizzato**, o **elaborare in batch più cartelle di lavoro**. Ognuno di questi si basa sullo stesso modello `HtmlSaveOptions`, così potrai adattare il codice con modifiche minime.

Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci alternativi di implementazione nei tuoi progetti.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}