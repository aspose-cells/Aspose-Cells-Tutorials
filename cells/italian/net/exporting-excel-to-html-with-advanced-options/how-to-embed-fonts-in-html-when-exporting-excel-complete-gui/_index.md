---
category: general
date: 2026-02-09
description: Scopri come incorporare i caratteri in HTML mentre esporti Excel in HTML
  usando Aspose.Cells. Questo tutorial passo‑passo copre anche la conversione di Excel
  in HTML e come esportare Excel con i caratteri incorporati.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- export excel to html
- convert excel to html
- how to export excel
language: it
og_description: Come incorporare i font in HTML durante l'esportazione di Excel. Segui
  questa guida completa per convertire Excel in HTML con font incorporati usando Aspose.Cells.
og_title: Come incorporare i font in HTML – Guida all'esportazione di Excel in HTML
tags:
- Aspose.Cells
- C#
- Excel
- HTML
title: Come incorporare i font in HTML durante l'esportazione di Excel – Guida completa
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-when-exporting-excel-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font in HTML durante l'esportazione di Excel – Guida completa

Ti sei mai chiesto **come incorporare i font in HTML** mentre trasformi una cartella di lavoro Excel in una pagina pronta per il web? Non sei l'unico. Molti sviluppatori si trovano di fronte a un ostacolo quando l'HTML generato appare corretto sulla loro macchina ma viene visualizzato con font di fallback generici nel browser. La buona notizia? Con poche righe di C# e le opzioni di salvataggio corrette, puoi distribuire esattamente la tipografia che hai progettato in Excel.

In questo tutorial vedremo come esportare un file Excel in HTML **con font incorporati**, usando Aspose.Cells per .NET. Lungo il percorso parleremo anche delle basi di *export excel to html*, ti mostreremo come *convert excel to html* in diversi scenari e risponderemo alle inevitabili domande “**how to export excel**” che compaiono nei forum.

## Cosa otterrai

- Un'app console C# completamente eseguibile che salva una cartella di lavoro `.xlsx` come `embedded.html`.
- Una spiegazione del perché incorporare i font è importante per la fedeltà tra diversi browser.
- Suggerimenti per gestire le licenze dei font, cartelle di lavoro di grandi dimensioni e le prestazioni.
- Indicazioni rapide su metodi alternativi per *export excel to html* se non utilizzi Aspose.Cells.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7+).
- Aspose.Cells per .NET installato tramite NuGet (`Install-Package Aspose.Cells`).
- Una conoscenza di base di C# e del modello oggetto di Excel.
- Un font TrueType (`.ttf`) o OpenType (`.otf`) di cui possiedi i diritti di incorporamento.

Nessuna configurazione complessa, nessun interop COM, solo qualche pacchetto NuGet e un editor di testo.

---

## Come incorporare i font in HTML – Passo 1: Preparare la cartella di lavoro

Prima di poter indicare ad Aspose.Cells di incorporare i font, ci serve una cartella di lavoro che utilizzi effettivamente un font personalizzato. Creiamo una piccola cartella di lavoro in memoria, applichiamo un font non di sistema a una cella e la salviamo.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Saving;   // Needed for HtmlSaveOptions

// Step 1: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];

// Step 2: Insert some text and apply a custom font (e.g., "Comic Sans MS")
Style style = workbook.CreateStyle();
style.Font.Name = "Comic Sans MS";   // This font is usually not available on all browsers
style.Font.Size = 14;
style.Font.IsBold = true;

// Apply the style to cell A1
Cell cell = sheet.Cells["A1"];
cell.PutValue("Hello, embedded fonts!");
cell.SetStyle(style);

// Save the workbook as an intermediate .xlsx (optional, just for inspection)
workbook.Save("sample.xlsx");
```

**Perché è importante:** Se la cartella di lavoro non fa mai riferimento a un font personalizzato, non c'è nulla che Aspose.Cells possa incorporare. Impostando esplicitamente `style.Font.Name`, costringiamo l'esportatore a cercare il file del font sul sistema e a includerlo nell'output HTML.

> **Consiglio professionale:** Testa sempre con un font che non è garantito presente sulle macchine di destinazione. I font di sistema come Arial non mostreranno la funzionalità di incorporamento.

## Come incorporare i font in HTML – Passo 2: Configurare le opzioni di salvataggio HTML

Ora arriva la riga magica che risponde alla domanda principale: *how to embed fonts in HTML*.

```csharp
// Step 3: Create HtmlSaveOptions and enable font embedding
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Setting this flag tells Aspose.Cells to embed all referenced fonts as base‑64 data URIs
    EmbedFonts = true,

    // Optional: Reduce file size by embedding only the characters actually used
    EmbedFontSubset = true,

    // Optional: Choose a folder for external resources (images, CSS)
    ExportImagesAsBase64 = true
};
```

- `EmbedFonts = true` fa il lavoro pesante; scansiona la cartella di lavoro alla ricerca di riferimenti a font, individua i file `.ttf`/`.otf` corrispondenti e li inserisce direttamente nel blocco `<style>` HTML generato.
- `EmbedFontSubset = true` è un acceleratore di prestazioni — solo i glifi effettivamente utilizzati vengono inclusi, mantenendo l'HTML finale snello.
- `ExportImagesAsBase64` è utile quando hai anche grafici o immagini; tutto finisce in un unico file, perfetto per email o demo rapide.

## Come incorporare i font in HTML – Passo 3: Salvare la cartella di lavoro

Infine, chiamiamo `Save` con le opzioni appena configurate.

```csharp
// Step 4: Export the workbook to HTML with embedded fonts
string outputPath = "embedded.html";
workbook.Save(outputPath, htmlOptions);

Console.WriteLine($"Workbook exported with embedded fonts to: {outputPath}");
```

Dopo che l'esecuzione è terminata, apri `embedded.html` in qualsiasi browser moderno. Dovresti vedere il testo visualizzato in *Comic Sans MS* anche se il font non è installato localmente. Il browser legge il blocco `<style>` che contiene una regola `@font-face` con un payload `data:font/ttf;base64,...` — esattamente ciò che volevamo.

![Output HTML con font incorporati](embed-fonts-html.png "Screenshot che mostra come incorporare i font in HTML")

*Testo alternativo dell'immagine:* **come incorporare i font in HTML** – screenshot della pagina generata con il font personalizzato applicato.

---

## Esportare Excel in HTML – Approcci alternativi

Se non sei vincolato ad Aspose.Cells, ci sono altri modi per *export excel to html*:

| Libreria / Strumento | Supporto all'incorporamento dei font | Nota rapida |
|----------------------|--------------------------------------|-------------|
| **ClosedXML**        | Nessun incorporamento dei font integrato | Genera HTML semplice; devi aggiungere manualmente `@font-face`. |
| **EPPlus**           | Nessun incorporamento dei font | Buono per tabelle di dati, ma perde lo stile. |
| **Office Interop**   | Può incorporare i font tramite `SaveAs` con `xlHtmlStatic` | Richiede Excel installato sul server — generalmente sconsigliato. |
| **LibreOffice CLI**  | Può incorporare i font con il flag `--embed-fonts` | Funziona cross‑platform ma aggiunge una dipendenza pesante. |

Quando hai bisogno di una soluzione affidabile lato server senza Office installato, Aspose.Cells rimane il percorso più semplice per *convert excel to html* con font incorporati.

## Come esportare Excel – Problemi comuni e come risolverli

1. **File di font mancanti** – Se il font di destinazione non è presente sulla macchina che esegue il codice, Aspose.Cells salta silenziosamente l'incorporamento e l'HTML ricade su un font generico.  
   *Soluzione:* Installa il font sul server o copia i file `.ttf`/`.otf` accanto all'eseguibile e imposta manualmente `FontSources`:

   ```csharp
   FontSources.AddFolder(@"C:\MyFonts");
   ```

2. **Restrizioni di licenza** – Alcuni font commerciali vietano l'incorporamento.  
   *Soluzione:* Controlla la EULA del font. Se l'incorporamento è proibito, scegli un font diverso o ospita il file del font tu stesso con la licenza appropriata.

3. **Cartelle di lavoro grandi** – Incorporare molti font può gonfiare le dimensioni dell'HTML.  
   *Soluzione:* Usa `EmbedFontSubset = true` (come mostrato prima) o limita la cartella di lavoro solo ai fogli necessari prima dell'esportazione.

4. **Compatibilità del browser** – I browser più vecchi (IE 8 e precedenti) non comprendono `@font-face` in base‑64.  
   *Soluzione:* Fornisci una regola CSS di fallback che faccia riferimento a una versione `.woff` del font accessibile via web.

---

## Convertire Excel in HTML – Verificare il risultato

Dopo aver eseguito l'esempio, apri `embedded.html` e cerca un blocco `<style>` che inizi così:

```html
<style type="text/css">
@font-face {
    font-family: 'Comic Sans MS';
    src: url('data:font/ttf;base64,AAEAAAALAIAAAwAwT1MvMg8S...') format('truetype');
}
...
</style>
```

Se vedi l'URL `data:`, l'incorporamento è riuscito. Il corpo della pagina conterrà qualcosa di simile a:

```html
<div class="c0">Hello, embedded fonts!</div>
```

Il testo dovrebbe essere visualizzato esattamente come in Excel, indipendentemente dai font installati sul client.

---

## Domande frequenti (FAQ)

**D: Funziona con le formule di Excel?**  
**R:** Assolutamente. Le formule vengono valutate prima che l'HTML sia generato, quindi i valori visualizzati sono stringhe statiche — proprio come in un'esportazione normale.

**D: Posso incorporare i font esportando in un pacchetto ZIP invece di un singolo file HTML?**  
**R:** Sì. Imposta `htmlOptions.ExportToSingleFile = false` e Aspose.Cells creerà una cartella con CSS e file di font separati, che alcuni team preferiscono per il controllo di versione.

**D: E se ho bisogno di incorporare**  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}