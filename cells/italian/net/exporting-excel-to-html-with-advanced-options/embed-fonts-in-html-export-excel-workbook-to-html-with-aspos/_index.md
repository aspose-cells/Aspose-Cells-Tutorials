---
category: general
date: 2026-06-17
description: Incorpora i caratteri in HTML mentre salvi la cartella di lavoro come
  HTML. Scopri come convertire la cartella di lavoro in HTML ed esportare l'HTML di
  Excel con i caratteri incorporati in pochi passaggi.
draft: false
keywords:
- embed fonts in html
- save workbook as html
- convert workbook to html
- how to export excel html
language: it
og_description: Incorpora i font in HTML quando salvi la cartella di lavoro come HTML.
  Segui questa guida per convertire la cartella di lavoro in HTML e scopri come esportare
  HTML di Excel con supporto completo dei font.
og_title: Incorpora i font in HTML – Esporta cartella di lavoro Excel in HTML
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Embed fonts in HTML while you save workbook as HTML. Learn how to convert
    workbook to HTML and export Excel HTML with embedded fonts in a few steps.
  headline: Embed Fonts in HTML – Export Excel Workbook to HTML with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Excel
- HTML export
title: Incorpora i caratteri in HTML – Esporta cartella di lavoro Excel in HTML con
  Aspose.Cells
url: /it/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-workbook-to-html-with-aspos/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporare i Font in HTML – Esportare una Cartella di Lavoro Excel in HTML con Aspose.Cells

Ti sei mai chiesto come **incorporare i font in HTML** quando esporti un foglio Excel? Non sei il solo. Molti sviluppatori si trovano di fronte a un ostacolo quando l'HTML generato mostra un generico sans‑serif invece dello stile originale di Excel. La buona notizia? Con un paio di righe di codice puoi **salvare la cartella di lavoro come HTML** e mantenere intatti tutti i font.

In questo tutorial percorreremo l'intero processo di **convertire la cartella di lavoro in HTML** usando Aspose.Cells per .NET, spiegheremo perché l'incorporamento dei font è importante e ti mostreremo esattamente **come esportare Excel in HTML** affinché il risultato abbia lo stesso aspetto del foglio di calcolo originale. Nessuno strumento esterno, nessuna post‑elaborazione manuale—solo codice C# pulito e eseguibile.

## Prerequisiti

- .NET 6.0 o versioni successive (l'esempio funziona su .NET Core, .NET Framework e .NET 5+)
- Pacchetto NuGet Aspose.Cells per .NET (`Install-Package Aspose.Cells`)
- Una conoscenza di base di C# e della gestione dei file Excel
- Opzionale: un file di font TrueType personalizzato da incorporare (es., `MyFont.ttf`)

Hai tutto? Ottimo—tuffiamoci.

## Passo 1: Configurare il Progetto e Caricare una Cartella di Lavoro Excel

Per prima cosa abbiamo bisogno di un oggetto workbook. Puoi crearne uno da zero o caricare un `.xlsx` esistente. Ecco una configurazione minima che aggiunge anche un font personalizzato alla collezione di stili del workbook.

```csharp
using Aspose.Cells;
using System.IO;

// Load an existing workbook (replace with your own path)
Workbook wb = new Workbook("SampleData.xlsx");

// OPTIONAL: Register a custom font if your sheet uses one that isn’t standard
string fontPath = Path.Combine(Directory.GetCurrentDirectory(), "MyFont.ttf");
if (File.Exists(fontPath))
{
    // Register the font with the font manager – this ensures Aspose knows about it
    FontConfigs.AddFontFile(fontPath);
}
```

*Perché questo passo?* Caricando prima il workbook diamo ad Aspose.Cells la possibilità di ispezionare tutti gli stili delle celle. Registrare un font personalizzato garantisce che il font sarà trovato quando lo incorporeremo successivamente nel file HTML.

## Passo 2: Configurare le Opzioni di Salvataggio HTML per **Incorporare i Font in HTML**

La magia risiede in `HtmlSaveOptions`. Impostare `EmbedFonts = true` indica alla libreria di incorporare ogni font utilizzato come regola `@font-face` codificata in Base64 all'interno del file HTML generato.

```csharp
// Configure HTML save options – this is where we embed fonts in HTML
HtmlSaveOptions saveOptions = new HtmlSaveOptions
{
    // Embed all referenced fonts directly into the HTML output
    EmbedFonts = true,

    // Optional: keep the original layout (useful for complex sheets)
    ExportActiveWorksheetOnly = true,

    // Optional: produce a single HTML file (no external CSS or images)
    ExportImagesAsBase64 = true
};
```

*Perché abilitare `EmbedFonts`?* Senza di esso, l'HTML di output fa riferimento ai font di sistema, e chi apre il file su una macchina che non dispone di quei font vede un font di riserva. L'incorporamento garantisce fedeltà visiva su tutti i browser e dispositivi.

## Passo 3: **Salvare la Cartella di Lavoro come HTML** con le Opzioni Configurate

Ora scriviamo finalmente il file. Il metodo `Save` accetta tre argomenti: il percorso di destinazione, il formato (`SaveFormat.Html`) e le opzioni appena configurate.

```csharp
// Define the output HTML file path
string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "with-fonts.html");

// Save the workbook as HTML with embedded fonts
wb.Save(outputPath, SaveFormat.Html, saveOptions);
```

Se tutto procede senza intoppi, otterrai un unico file `with-fonts.html` che contiene l'intero layout del foglio di calcolo *e* i dati del font codificati direttamente nel markup.

## Output Atteso

Apri `with-fonts.html` in qualsiasi browser moderno (Chrome, Edge, Firefox). Dovresti vedere:

- Gli stessi valori delle celle, colori e bordi come nel file Excel originale.
- Testo renderizzato con lo stesso font usato in Excel, anche se quel font non è installato sul tuo computer.
- Nessun file `.css` o immagine esterno—tutto è contenuto nel file HTML.

Di seguito è riportato un piccolo estratto di come potrebbe apparire il blocco `<style>` generato (la stringa Base64 è troncata per brevità):

```html
<style type="text/css">
@font-face{
    font-family:'MyCustomFont';
    src:url(data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1Mv... ) format('truetype');
}
...
</style>
```

## Passo 4: Problemi Comuni & Come Risolverli

| Problema | Perché Accade | Soluzione |
|------|----------------|-----|
| **Font mancante nell'HTML** | Il file del font non è stato registrato con `FontConfigs` prima del salvataggio. | Chiamare `FontConfigs.AddFontFile` *prima* di creare `HtmlSaveOptions`. |
| **Dimensione enorme del file HTML** | L'incorporamento di molti font grandi può gonfiare il file. | Incorporare solo i font realmente necessari; usare `saveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset` per incorporare solo le glifi usate (disponibile nelle versioni più recenti di Aspose). |
| **Caratteri errati (es., glifi asiatici)** | Il font non contiene gli intervalli Unicode richiesti. | Assicurarsi che il font di origine supporti i caratteri, o incorporare un font di fallback aggiuntivo. |
| **Rallentamento delle prestazioni su cartelle di lavoro grandi** | L'incorporamento dei font aggiunge un overhead di elaborazione. | Esportare solo il foglio attivo (`ExportActiveWorksheetOnly = true`) o suddividere la cartella di lavoro in parti più piccole. |

## Passo 5: Estendere la Soluzione – Esportare più Fogli di Lavoro

Se hai bisogno di **convertire la cartella di lavoro in HTML** per tutti i fogli, disattiva semplicemente `ExportActiveWorksheetOnly`:

```csharp
saveOptions.ExportActiveWorksheetOnly = false; // Export every sheet
wb.Save("all-sheets.html", SaveFormat.Html, saveOptions);
```

Ogni foglio apparirà come un `<div>` separato nello stesso file HTML, ancora con i font incorporati.

## Consiglio Pro: Combinare con la Personalizzazione CSS

A volte vuoi un controllo più preciso sul markup generato. `HtmlSaveOptions` offre la proprietà `CssClassPrefix` per evitare collisioni di nomi di classi quando si uniscono più esportazioni HTML:

```csharp
saveOptions.CssClassPrefix = "myExcel_";
```

Ora ogni classe CSS generata inizierà con `myExcel_`, facilitando l'applicazione del tuo foglio di stile in seguito.

## Riepilogo

- **Incorpora i font in HTML** impostando `HtmlSaveOptions.EmbedFonts = true`.
- Usa **salva la cartella di lavoro come HTML** (`wb.Save(..., SaveFormat.Html, ...)`) per produrre un unico file autonomo.
- Questo metodo **converte la cartella di lavoro in HTML** preservando ogni dettaglio visivo, rispondendo alla classica domanda **come esportare Excel in HTML** con piena fedeltà.
- Registra i font personalizzati con `FontConfigs.AddFontFile` per assicurarti che siano disponibili per l'incorporamento.
- Regola opzioni come `ExportImagesAsBase64` e `ExportActiveWorksheetOnly` per adattarle alle esigenze del tuo progetto.

## Cosa Viene Dopo?

- Prova a esportare in **MHTML** (`SaveFormat.Mhtml`) per un pacchetto ancora più portabile.
- Esplora la **conversione PDF** (`SaveFormat.Pdf`) se ti serve un formato pronto per la stampa.
- Integra l'esportazione HTML in una web API così gli utenti possono scaricare fogli di calcolo stilizzati al volo.

Sentiti libero di sperimentare—sostituire i font, cambiare le selezioni dei fogli di lavoro o combinare più formati di esportazione. La flessibilità di Aspose.Cells ti permette di personalizzare l'output per qualsiasi scenario, dai dashboard di reportistica automatizzata ai frammenti HTML pronti per l'email.

Buon coding, e che il tuo HTML assomigli sempre esattamente al foglio Excel originale!

## Cosa Dovresti Imparare Dopo?

I tutorial seguenti coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come Creare ed Esportare Excel in HTML Usando Aspose.Cells Java \| Guida alle Operazioni sul Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Imposta il Font Predefinito nella Conversione da Excel a HTML con Aspose.Cells per .NET \| Guida alle Operazioni sul Workbook](/cells/english/net/workbook-operations/excel-html-conversion-default-font-aspose-cells-net/)
- [Come Esportare Excel in HTML con Griglie Usando Aspose.Cells per .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}