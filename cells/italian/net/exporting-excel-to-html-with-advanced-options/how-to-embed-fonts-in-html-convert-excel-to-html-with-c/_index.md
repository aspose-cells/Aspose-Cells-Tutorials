---
category: general
date: 2026-03-01
description: Scopri come incorporare i caratteri in HTML durante la conversione di
  Excel in HTML utilizzando Aspose.Cells. Questa guida passo‑passo mostra anche come
  salvare Excel come HTML.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- create html from excel
- save excel as html
language: it
og_description: Come incorporare i font in HTML durante l'esportazione di Excel in
  HTML. Segui questo tutorial completo per preservare la tipografia su tutti i browser.
og_title: Come incorporare i font in HTML – Guida rapida a C#
tags:
- Aspose.Cells
- C#
- HTML export
title: Come incorporare i font in HTML – Converti Excel in HTML con C#
url: /it/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font in HTML – Convertire Excel in HTML con C#

Ti sei mai chiesto **come incorporare i font in HTML** in modo che la tua conversione da Excel a HTML sia pixel‑perfect? Non sei l'unico. Quando esporti una cartella di lavoro in HTML, il comportamento predefinito è fare riferimento ai font di sistema, il che può rompere il layout su macchine che non hanno quei font installati.  

Attivando l'incorporamento dei font garantisci che l'output preservi la tipografia originale, indipendentemente da dove venga visualizzato. In questo tutorial percorreremo i passaggi esatti per **incorporare i font in HTML** usando Aspose.Cells per .NET, e toccheremo anche attività correlate come **convertire Excel in HTML**, **creare HTML da Excel** e **salvare Excel come HTML**.

## Cosa imparerai

- Perché l'incorporamento dei font è importante per la coerenza tra browser.  
- Il codice C# esatto necessario per abilitare **embed fonts in html** quando si salva una cartella di lavoro.  
- Come gestire casi particolari comuni, come file di font di grandi dimensioni o restrizioni di licenza.  
- Passaggi rapidi di verifica per assicurarsi che i font siano davvero incorporati.

### Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche con .NET Framework 4.6+).  
- Pacchetto NuGet Aspose.Cells per .NET installato (`Install-Package Aspose.Cells`).  
- Una conoscenza di base di C# e della gestione dei file Excel.  
- Almeno un font TrueType/OpenType personalizzato usato nella tua cartella di lavoro.

> **Suggerimento:** Se usi Visual Studio, abilita “Nullable reference types” per intercettare potenziali problemi di null in anticipo.

---

## Passo 1: Configura il progetto e carica la cartella di lavoro

Per prima cosa, crea una nuova app console (o integrala nella tua soluzione esistente). Quindi aggiungi lo spazio dei nomi Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load an existing Excel file that uses custom fonts
        string sourcePath = @"C:\Temp\Report.xlsx";
        Workbook wb = new Workbook(sourcePath);
```

*Perché è importante:* Caricare la cartella di lavoro dà alla libreria accesso agli stili delle celle, che includono le informazioni sui font che vogliamo incorporare in seguito.

---

## Passo 2: Crea **HtmlSaveOptions** e attiva l'incorporamento dei font

La classe `HtmlSaveOptions` controlla ogni aspetto dell'esportazione HTML. Impostare `EmbedFonts = true` indica ad Aspose.Cells di incorporare i file di font necessari direttamente nell'HTML (come URL dati codificati Base64).

```csharp
        // Step 2: Create HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();

        // Enable embedding of fonts in the saved HTML
        htmlOptions.EmbedFonts = true;

        // Optional: Reduce the size of embedded fonts by subsetting
        htmlOptions.SubsetEmbeddedFonts = true;
```

*Perché abilitiamo `SubsetEmbeddedFonts`*: Rimuove i glifi non utilizzati, riducendo il file HTML finale—particolarmente utile quando si gestiscono famiglie di font di grandi dimensioni.

---

## Passo 3: Scegli una cartella di output e salva l'HTML

Ora decidi dove deve essere salvato il file HTML. Aspose.Cells genererà anche una cartella per le risorse di supporto (immagini, CSS, ecc.).  

```csharp
        // Define output location
        string outputFolder = @"C:\Temp\ExportedHtml";
        string outputFile = System.IO.Path.Combine(outputFolder, "Report.html");

        // Ensure the folder exists
        System.IO.Directory.CreateDirectory(outputFolder);

        // Step 3: Save the workbook as HTML with the configured options
        wb.Save(outputFile, htmlOptions);

        Console.WriteLine($"HTML file with embedded fonts saved to: {outputFile}");
    }
}
```

*Ciò che vedrai:* Apri il `Report.html` risultante in qualsiasi browser. I font personalizzati dovrebbero essere visualizzati correttamente anche se il font non è installato sulla macchina.

---

## Passo 4: Verifica che i font siano davvero incorporati

Un modo rapido per confermare l'incorporamento è ispezionare il file HTML generato. Cerca blocchi `<style>` che contengono regole `@font-face` con `src: url(data:font/ttf;base64,…)`.  

```html
/* Example snippet from the output */
@font-face {
    font-family: 'MyCustomFont';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
    font-weight: normal;
    font-style: normal;
}
```

Se vedi l'URI `data:`, il font è incorporato. Non dovrebbero essere referenziati file `.ttf` o `.woff` esterni.

---

## Domande comuni e casi particolari

| Question | Answer |
|----------|--------|
| **E se la mia cartella di lavoro utilizza molti font diversi?** | Incorporare tutti i font può gonfiare l'HTML. Usa `htmlOptions.SubsetEmbeddedFonts = true` per mantenere solo i glifi necessari, oppure limita manualmente i font da incorporare tramite `htmlOptions.FontsToEmbed`. |
| **Devo preoccuparmi della licenza dei font?** | Assolutamente. Incorporare un font in un file HTML crea una copia che viene distribuita con il tuo contenuto. Assicurati di avere il diritto di ridistribuire il font (ad esempio, i font open‑source come Google Fonts sono sicuri). |
| **Funzionerà in browser più vecchi come IE9?** | L'approccio Base64 data‑URI è supportato fino a IE8, ma ha un limite di dimensione (~32 KB). Per font molto grandi, considera di ricorrere a file font esterni e servirli via HTTP. |
| **Posso incorporare i font quando converto Excel in PDF invece di HTML?** | Sì—Aspose.Cells supporta anche `PdfSaveOptions.EmbedStandardFonts` e `PdfSaveOptions.FontEmbeddingMode`. Il concetto è lo stesso, solo un'API diversa. |
| **E se devo **creare HTML da Excel** su un server senza interfaccia grafica?** | Lo stesso codice funziona in ASP.NET Core, Azure Functions o qualsiasi ambiente headless—basta assicurarsi che il processo abbia accesso in lettura ai file dei font. |

---

## Suggerimenti sulle prestazioni

1. **Cache l'HTML** se esporti la stessa cartella di lavoro più volte; il passaggio di incorporamento può essere intensivo per la CPU.  
2. **Comprimi la cartella di output** (zip) prima di inviarla sulla rete; i font incorporati sono già codificati Base64, quindi lo zip ridurrà comunque qualche kilobyte.  
3. **Evita di incorporare i font di sistema** (Arial, Times New Roman) a meno che non ti serva una versione personalizzata; i browser li hanno già.

---

## Esempio completo funzionante (pronto per copia‑incolla)

```csharp
using System;
using Aspose.Cells;

class EmbedFontsDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook (your Excel file must contain custom fonts)
        string excelPath = @"C:\Temp\Sample.xlsx";
        Workbook workbook = new Workbook(excelPath);

        // 2️⃣ Prepare HTML options with font embedding enabled
        HtmlSaveOptions options = new HtmlSaveOptions
        {
            EmbedFonts = true,               // ✅ This is the key line for embedding fonts
            SubsetEmbeddedFonts = true,      // ✅ Reduces file size by keeping only used glyphs
            ExportActiveWorksheetOnly = true // Optional: export just the active sheet
        };

        // 3️⃣ Define where the HTML will be saved
        string outputDir = @"C:\Temp\HtmlExport";
        System.IO.Directory.CreateDirectory(outputDir);
        string htmlPath = System.IO.Path.Combine(outputDir, "Sample.html");

        // 4️⃣ Save the workbook as HTML
        workbook.Save(htmlPath, options);

        Console.WriteLine($"✅ HTML with embedded fonts saved at: {htmlPath}");
    }
}
```

Eseguendo questo programma si produce un file `Sample.html` che **embed fonts in html** e può essere aperto su qualsiasi dispositivo senza perdere l'aspetto originale.

---

## Conclusione

Abbiamo coperto **come incorporare i font in HTML** quando **converti Excel in HTML**, garantendo che la fedeltà visiva della tua cartella di lavoro sopravviva al viaggio verso il web. Attivando `HtmlSaveOptions.EmbedFonts` (e opzionalmente `SubsetEmbeddedFonts`) ottieni un file HTML autonomo che funziona su tutti i browser, anche su macchine che non hanno i font originali.  

Successivamente, potresti esplorare **creare HTML da Excel** per più fogli di lavoro, o approfondire **salvare Excel come HTML** con temi CSS personalizzati. Entrambi gli scenari riutilizzano lo stesso oggetto `HtmlSaveOptions`—basta regolare proprietà come `ExportActiveWorksheetOnly` o `CssStyleSheetType`.  

Provalo, modifica le opzioni e lascia che i font incorporati facciano il lavoro pesante. Se incontri problemi, lascia un commento—buona programmazione!  

![How to embed fonts in HTML example](https://example.com/images/embed-fonts.png "How to embed fonts in HTML")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}