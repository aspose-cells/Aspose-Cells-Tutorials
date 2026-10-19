---
category: general
date: 2026-09-15
description: Impara come incorporare i font in SVG ed esportare un grafico Excel in
  PowerPoint, coprendo la conversione da XLSX a SVG e da XLSX a PPTX con esempi di
  codice completi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: it
lastmod: 2026-09-15
og_description: Incorpora i font in SVG ed esporta il grafico di Excel in PowerPoint
  con codice C# passo‑passo. Converti XLSX in SVG e XLSX in PPTX rapidamente e in
  modo affidabile.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Incorpora i font in SVG ed esporta il grafico Excel in PowerPoint – guida
  completa
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Come incorporare i caratteri in SVG durante la conversione di file Excel in
  SVG e PowerPoint
url: /it/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come incorporare i font in SVG durante la conversione di file Excel in SVG e PowerPoint  

Se hai bisogno di **incorporare i font in SVG** durante la conversione di una cartella di lavoro Excel, questa guida ti mostra esattamente come farlo. Imparerai anche come **esportare un grafico Excel in PowerPoint**, e come **convertire XLSX in SVG** e **convertire XLSX in PPTX** con grafici modificabili.  

Lavorare con i dati di Excel in modo programmatico spesso significa dover spostare lo stesso contenuto visivo tra formati di file diversi. Ricreare manualmente un grafico in PowerPoint o riapplicare i font in un SVG è soggetto a errori e richiede molto tempo. Alla fine di questo tutorial avrai a disposizione uno snippet C# unico e riutilizzabile che:

* Salva una cartella di lavoro come file SVG con font incorporati e selettori di variazione dei font.  
* Esporta la stessa cartella di lavoro in un file PPTX dove il grafico rimane modificabile.  

L'unico prerequisito è una versione recente di **Aspose.Cells for .NET** (2024‑x o successiva) e un ambiente di sviluppo .NET come Visual Studio 2022.

---

## Cosa ti servirà  

* .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.8).  
* Pacchetto NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`).  
* Un file Excel (`input.xlsx`) che contenga almeno un grafico.  
* Permessi di scrittura sulla directory di output.  

---

## Incorporare i font in SVG durante la conversione da XLSX a SVG  

L'incorporamento dei font garantisce che l'SVG venga visualizzato correttamente su qualsiasi dispositivo, anche se il sistema di destinazione non dispone dei caratteri originali. La classe `SvgSaveOptions` fornisce due flag che rendono possibile ciò: `EmbedFonts` e `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Perché funziona:**  
* `EmbedFonts = true` copia i file dei font nella sezione `<defs>` dell'SVG, eliminando le dipendenze esterne.  
* `FontVariationSelectors = true` aggiunge i selettori necessari per i font che supportano le funzionalità OpenType, preservando le variazioni dei glifi come le legature.  

**Risultato atteso:** Apri `WithFonts.svg` in qualsiasi browser moderno; il testo all'interno del grafico o delle celle appare con lo stesso carattere usato in Excel, anche su macchine che non hanno quel font installato.

---

## Esportare un grafico Excel in PowerPoint con grafici modificabili  

Quando devi incorporare un grafico in una diapositiva PowerPoint ma vuoi comunque consentire al destinatario di modificare i dati del grafico, `PptxSaveOptions` di Aspose.Cells offre il flag `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Perché è importante:**  
Impostare `ExportEditableChart` su `true` salva il grafico come oggetto chart Office Open XML anziché come immagine statica. Quando apri `EditableChart.pptx` in PowerPoint, puoi fare clic con il tasto destro sul grafico → **Edit Data** e modificare le serie proprio come un grafico PowerPoint nativo.

**Passaggi di verifica:**  

1. Apri `EditableChart.pptx` in PowerPoint.  
2. Individua la diapositiva contenente il grafico.  
3. Scegli **Chart Tools → Design → Edit Data**.  
4. Conferma che appare la griglia dati in stile Excel e che puoi cambiare i valori.

---

## Convertire XLSX in SVG – riepilogo del flusso completo  

Di seguito trovi una versione compatta che combina caricamento, manipolazione opzionale dei dati e salvataggio come SVG. Usala quando ti serve solo l'output SVG.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Chiama il metodo così:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Suggerimento per casi limite:** Se la tua cartella di lavoro contiene font personalizzati che non sono installati sul server, incorporali manualmente prima di chiamare `Save`. Usa `FontInfoCollection` per aggiungere i file dei font a `SvgSaveOptions` tramite la proprietà `CustomFonts` (disponibile nelle versioni più recenti di Aspose.Cells).

---

## Convertire XLSX in PPTX – preservare la modificabilità del grafico  

Il metodo di supporto seguente dimostra il percorso **convert XLSX to PPTX** garantendo che il grafico rimanga modificabile.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Utilizzo:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Domanda frequente:** *E se la mia cartella di lavoro ha più fogli con grafici?*  
**Risposta:** Aspose.Cells esporta per impostazione predefinita il primo foglio. Per includere fogli aggiuntivi, itera su `workbook.Worksheets`, copia ogni grafico in una nuova diapositiva e salva ogni diapositiva singolarmente usando gli oggetti `Presentation` di Aspose.Slides. Questo scenario avanzato va oltre il flusso base “salva cartella di lavoro come SVG” e “esporta grafico Excel in PowerPoint”, ma i flag principali rimangono gli stessi.

---

## Consigli pratici e insidie  

* **Performance:** Incorporare i font aumenta la dimensione del file SVG. Se la dimensione è un problema, imposta `EmbedFonts = false` e fai affidamento sui font web‑safe.  
* **Licenza dei font:** Assicurati di avere il diritto di incorporare i font che utilizzi; alcuni font commerciali limitano l’incorporamento.  
* **Compatibilità dei grafici:** I grafici modificabili vengono salvati come parti `chart.xml` all'interno del PPTX. Grafici molto complessi (ad es. 3‑D o grafici combinati) potrebbero perdere parte dello stile quando modificati in PowerPoint. Testa i tipi di grafico più comuni di cui hai bisogno.  
* **Mancata corrispondenza di versione:** Il flag `ExportEditableChart` richiede Aspose.Cells 20.10 o successivo. Usare una versione più vecchia tornerà silenziosamente a un'immagine raster.  
* **Sicurezza dei thread:** Gli oggetti Workbook non sono thread‑safe. Crea una nuova istanza `Workbook` per ogni richiesta in scenari di servizio web.  

---

## Esempio completo end‑to‑end  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Eseguendo questo programma otterrai due file:

* **WithFonts.svg** – un SVG che si rende esattamente come la vista di Excel, con i font inclusi.  
* **EditableChart.pptx** – una presentazione PowerPoint dove il grafico può essere modificato direttamente.

---

## Conclusione  

Ora sai come **incorporare i font in SVG** quando **converti XLSX in SVG**, e come **esportare un grafico Excel in PowerPoint** mantenendo il grafico modificabile. Lo stesso codice dimostra anche un modo pulito per **salvare la cartella di lavoro come SVG** e **convertire XLSX in PPTX** con il minimo sforzo.  

Da qui puoi approfondire ulteriori argomenti, ad esempio:

* Aggiungere font personalizzati programmaticamente (`svgOptions.CustomFonts`).  
* Elaborare in batch più cartelle di lavoro in un servizio in background.  
* Usare Aspose.Slides per creare file PPTX multi‑diapositiva che combinano diversi grafici Excel.  

Sperimenta con le opzioni, adatta gli snippet al tuo progetto e goditi conversioni affidabili da Excel a SVG/PPTX senza post‑processing manuale. Buon coding!


## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}