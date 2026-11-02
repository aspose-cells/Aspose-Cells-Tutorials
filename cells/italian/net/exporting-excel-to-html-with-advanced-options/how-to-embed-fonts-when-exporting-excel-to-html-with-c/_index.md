---
category: general
date: 2026-10-10
description: Impara come incorporare i font durante l'esportazione di Excel in HTML
  con C#. Questa guida copre l'esportazione di Excel in HTML, la conversione di Excel
  in HTML e come salvare Excel con i font incorporati.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- export excel html
- convert excel html
- how to save excel
- embed fonts html
language: it
lastmod: 2026-10-10
og_description: Come incorporare i font durante l'esportazione di Excel in HTML con
  C#. Segui questo tutorial completo per esportare Excel in HTML, convertire Excel
  in HTML e imparare come salvare Excel con i font incorporati.
og_image_alt: Screenshot showing exported HTML file that demonstrates how to embed
  fonts from Excel
og_title: Come incorporare i font durante l'esportazione di Excel in HTML – guida
  passo‑passo C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to embed fonts while exporting Excel to HTML in C#. This
    guide covers export excel html, convert excel html, and how to save Excel with
    embedded fonts.
  headline: How to embed fonts when exporting Excel to HTML with C#
  type: TechArticle
tags:
- Excel
- HTML export
- Font embedding
- C#
title: Come incorporare i font durante l'esportazione di Excel in HTML con C#
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-exporting-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font quando si esporta Excel in HTML con C#

Se hai bisogno di **come incorporare i font** in un file HTML generato da una cartella di lavoro Excel, questo tutorial mostra i passaggi esatti. L'esportazione di Excel in HTML spesso rimuove i font personalizzati, compromettendo la fedeltà visiva del foglio originale. Configurando le opzioni corrette è possibile preservare ogni tipo di carattere direttamente nell'output HTML.

In questa guida imparerai a **export excel html**, **convert excel html** e **how to save Excel** con i font incorporati, usando la libreria Aspose.Cells per .NET. La soluzione funziona con .NET 6+ e richiede solo poche righe di codice C#.

## Cosa otterrai

- Un programma C# completo e funzionante che carica un file `.xlsx` esistente.
- Output HTML in cui tutti i font utilizzati sono incorporati come regole `@font-face` codificate in Base64.
- La certezza che l'HTML esportato abbia lo stesso aspetto del workbook di origine in qualsiasi browser.

## Prerequisiti

| Requisito | Motivo |
|-------------|--------|
| .NET 6 SDK o successivo | Fornisce il runtime per il progetto C#. |
| Visual Studio 2022 (o qualsiasi IDE) | Rende facile creare ed eseguire l'app console. |
| Aspose.Cells per .NET (pacchetto NuGet `Aspose.Cells`) | Fornisce la classe `HtmlSaveOptions` e la funzionalità `EmbedFonts`. |
| Un file Excel (`sample.xlsx`) che utilizza un font personalizzato (ad es., *Calibri* o un TrueType scaricato) | Dimostra l'effetto dell'incorporamento dei font. |

> **Suggerimento:** Se lavori dietro un proxy aziendale, configura NuGet per usare il proxy prima di installare il pacchetto.

## Passo 1: Installa Aspose.Cells

Apri un terminale nella cartella del progetto ed esegui:

```bash
dotnet add package Aspose.Cells
```

Il comando aggiunge l'ultima versione stabile di Aspose.Cells al tuo progetto, rendendo disponibili le classi `Workbook` e `HtmlSaveOptions`.

## Passo 2: Carica il workbook Excel

Crea una nuova applicazione console (`dotnet new console`) e aggiungi il seguente codice in `Program.cs`:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing workbook. Replace the path with your actual file location.
        Workbook wb = new Workbook("sample.xlsx");
        // Continue with HTML export...
    }
}
```

**Perché questo passo è importante:**  
Caricare il workbook ti dà accesso ai fogli, agli stili e ai font personalizzati referenziati all'interno del file. Senza un'istanza `Workbook` caricata non puoi configurare le opzioni di esportazione.

## Passo 3: Configura le opzioni di salvataggio HTML per incorporare i font

La classe `HtmlSaveOptions` controlla ogni aspetto dell'esportazione HTML. Impostare `EmbedFonts = true` indica ad Aspose.Cells di incorporare ogni font usato nel workbook direttamente nel file HTML generato.

```csharp
// Configure HTML save options to embed fonts
HtmlSaveOptions opts = new HtmlSaveOptions
{
    // When true, the exporter creates @font-face rules with Base64 data.
    EmbedFonts = true,

    // Optional: keep the original folder structure for images.
    ExportImagesAsBase64 = true,

    // Optional: generate a single HTML file (no external CSS folder).
    ExportActiveWorksheetOnly = false
};
```

**Spiegazione:**  
- `EmbedFonts` è il flag chiave che soddisfa il requisito **how to embed fonts**.  
- `ExportImagesAsBase64` garantisce che anche le immagini diventino parte del singolo file HTML, semplificando il deployment.  
- `ExportActiveWorksheetOnly` impostato a `false` assicura che tutti i fogli vengano inclusi, utile quando il workbook si estende su più schede.

## Passo 4: Salva il workbook come HTML con i font incorporati

Ora invoca il metodo `Save`, passando il percorso di output desiderato e le opzioni appena configurate:

```csharp
// Save the workbook as an HTML file with embedded fonts
wb.Save("Embedded.html", opts);
```

Il file `Embedded.html` risultante contiene:

- Markup HTML standard per i dati del foglio.
- Uno o più blocchi `<style>` con regole `@font-face` che incorporano i font personalizzati come stringhe Base64.
- Tutte le immagini codificate direttamente nell'HTML (se presenti).

## Passo 5: Verifica che i font siano davvero incorporati

Apri `Embedded.html` in un browser (Chrome, Edge, Firefox). La pagina dovrebbe renderizzare esattamente come il workbook Excel originale, anche se la macchina di destinazione non ha i font personalizzati installati.

Per ricontrollare l'incorporamento:

1. Apri il sorgente della pagina (`Ctrl+U` nella maggior parte dei browser).  
2. Cerca `@font-face`. Vedrai un blocco simile a:

```css
@font-face {
    font-family: 'Calibri';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1Mv...') format('truetype');
    font-weight: normal;
    font-style: normal;
}
```

Se l'attributo `src` contiene un URL `data:`, il font è stato incorporato correttamente.

## Varianti comuni e casi limite

| Situazione | Regolazione suggerita |
|-----------|----------------------|
| **Workbook grande con molti font personalizzati** | Aumenta `MaxFontEmbeddingSize` (se disponibile) o suddividi l'esportazione in più file HTML per evitare i limiti di dimensione dei browser. |
| **Hai bisogno di un solo foglio** | Imposta `opts.ExportActiveWorksheetOnly = true` e attiva il foglio desiderato prima di salvare (`wb.Worksheets[0].Activate();`). |
| **L'incorporamento dei font non è consentito dalla policy aziendale** | Imposta `opts.EmbedFonts = false` e fai affidamento su font web‑safe o fornisci i file dei font accanto all'HTML. |
| **Target di browser più vecchi che non supportano i font Base64** | Usa `opts.FontEmbeddingMode = FontEmbeddingMode.FontFile;` (se la versione della libreria lo supporta) per generare file `.ttf` separati e riferirli con URL normali. |

## Esempio completo e eseguibile

Di seguito trovi il programma completo che puoi copiare‑incollare in `Program.cs`. Include tutti i `using` necessari e la gestione degli errori per uno script pronto per la produzione.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load the workbook (replace with your file path)
            Workbook wb = new Workbook("sample.xlsx");

            // 2️⃣ Configure HTML export options to embed fonts
            HtmlSaveOptions opts = new HtmlSaveOptions
            {
                EmbedFonts = true,               // ✅ Core requirement: how to embed fonts
                ExportImagesAsBase64 = true,     // Keep everything in one file
                ExportActiveWorksheetOnly = false
            };

            // 3️⃣ Save as HTML with embedded fonts
            string outputPath = "Embedded.html";
            wb.Save(outputPath, opts);

            Console.WriteLine($"HTML file with embedded fonts saved to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Output previsto:**  
L'esecuzione del programma stampa la riga di conferma e crea `Embedded.html`. Aprendo il file in qualsiasi browser moderno vedrai il foglio con tutti i font originali intatti, soddisfacendo l'obiettivo **how to embed fonts**.

## Conclusione

Ora sai **come incorporare i font** durante un'operazione di **export excel html**, come **convert excel html** senza perdere i caratteri, e i passaggi esatti per **how to save excel** come file HTML con i font incorporati. Utilizzando `HtmlSaveOptions.EmbedFonts = true`, l'HTML generato diventa autonomo, portabile e visivamente identico al workbook di origine.

### Cosa fare dopo?

- Esplora le proprietà di `HtmlSaveOptions` per controllare CSS, gestione delle immagini e selezione dei fogli.  
- Combina questa tecnica con l'automazione lato server per generare report HTML al volo.  
- Approfondisci **embed fonts html** per altri formati di documento (ad es., PDF) usando API Aspose analoghe.

Sentiti libero di sperimentare con diversi font, dimensioni di workbook e ambienti browser. Se incontri problemi, ricontrolla la tabella dei casi limite sopra o consulta la documentazione di Aspose.Cells per scenari avanzati di incorporamento dei font. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export Excel to HTML – Complete Programming Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-complete-programming-guide/)
- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts When Converting Excel to PDF – Complete Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-complete-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}