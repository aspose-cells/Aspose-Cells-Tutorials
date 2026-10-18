---
category: general
date: 2026-07-14
description: Salva Excel come HTML rapidamente e scopri come convertire Excel in HTML
  con formattazione completa. Esporta Excel con formattazione usando Aspose.Cells
  in pochi minuti.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: it
lastmod: 2026-07-14
og_description: Salva Excel come HTML istantaneamente. Questa guida mostra come convertire
  Excel in HTML mantenendo gli stili e abilitando la formattazione dei numeri con
  Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Salva Excel come HTML – Esportazione passo passo con formattazione completa
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Salva Excel come HTML – Guida completa per esportare Excel con formattazione
url: /it/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salva Excel come HTML – Guida completa per esportare Excel con formattazione

Ti sei mai chiesto come **salvare Excel come HTML** senza perdere colori, bordi o formati numerici? Non sei l'unico. In molti scenari di reporting è necessario avere una visualizzazione pronta per il web di una cartella di lavoro, e il modo più rapido è esportare il file direttamente in HTML.  

In questo tutorial percorreremo passo passo le istruzioni per **convertire Excel in HTML** usando Aspose.Cells, abilitare la formattazione numerica di Grid.js e assicurarci che il risultato abbia lo stesso aspetto del foglio di calcolo originale. Alla fine avrai un file HTML pronto da inserire in qualsiasi server web.

## Cosa imparerai

- Prerequisiti e installazione del pacchetto  
- Caricamento di una cartella di lavoro esistente (o creazione al volo)  
- Configurazione di `HtmlSaveOptions` per una fedeltà visiva perfetta  
- Abilitazione di `GridJsOptions.EnableNumberFormat` per mantenere intatta la formattazione numerica  
- Salvataggio del file e verifica del risultato  

Se hai mai provato a **esportare Excel con formattazione** usando un dump CSV generico, sai quanto può essere frustrante quando i numeri diventano semplice testo. Questa guida evita questa insidia.

---

## Prerequisiti – Configura il tuo ambiente di sviluppo

Prima di immergerci nel codice, assicurati di avere:

| Requisito | Perché è importante |
|-------------|----------------|
| .NET 6.0 o successivo (il tutorial usa .NET 6) | API moderne e migliori prestazioni |
| Visual Studio 2022 (o VS Code con estensione C#) | Editing e debug confortevoli |
| Pacchetto NuGet Aspose.Cells per .NET | La libreria che fornisce `HtmlSaveOptions` e `GridJsOptions` |
| Un file Excel di esempio (`sample.xlsx`) o una cartella di lavoro generata in codice | La sorgente che convertirai |

Installa Aspose.Cells con il seguente comando nella Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

> **Suggerimento professionale:** Se lavori su una pipeline CI, aggiungi la stessa riga `dotnet add package` al tuo script di build così la dipendenza sarà sempre presente.

---

## Passo 1: Carica o crea una cartella di lavoro

Puoi caricare un file esistente oppure crearne uno programmaticamente. Ecco un esempio minimale che crea una cartella di lavoro con alcune celle formattate così da poter vedere la formattazione sopravvivere all'esportazione.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Perché è importante:** Impostando esplicitamente i formati numerici, vedrai più tardi `GridJsOptions.EnableNumberFormat` mantenere quei formati vivi nell'output HTML.

---

## Passo 2: Configura le opzioni di salvataggio HTML

Ora creiamo un'istanza di `HtmlSaveOptions`. Questo oggetto indica ad Aspose.Cells esattamente come vuoi che l'HTML venga renderizzato.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Abilitazione della formattazione numerica di Grid.js

Se prevedi di incorporare l'HTML in una pagina che utilizza **Grid.js** per tabelle interattive, vorrai che i numeri rimangano formattati (ad esempio simboli di valuta, separatori delle migliaia). La riga seguente fa proprio questo:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Cosa succede dietro le quinte?** `EnableNumberFormat` inietta un piccolo snippet JavaScript che dice a Grid.js di interpretare l'attributo `data-format` della cella, preservando la formattazione in stile Excel nel browser.

---

## Passo 3: Salva la cartella di lavoro come file HTML

Con la cartella di lavoro pronta e le opzioni sintonizzate, l'ultima riga scrive il file HTML su disco.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Eseguendo il programma si genera un file `gridjs.html` che appare così (visualizzazione semplificata):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Apri il file in qualsiasi browser e vedrai una tabella ben stilizzata, completa di intestazione con sfondo grigio chiaro e formattazione di valuta. Se inserisci la pagina in un sito che già carica Grid.js, i numeri verranno renderizzati automaticamente con le virgole e i simboli corretti.

---

## Problemi comuni quando **converti Excel in HTML**

| Problema | Perché si verifica | Come evitarlo |
|-------|---------------|-----------------|
| **Formule perse** | L'HTML è statico; le formule diventano valori semplici. | Se ti servono calcoli live, mantieni la cartella di lavoro sul server e usa librerie JavaScript come SheetJS. |
| **Immagini mancanti** | Le immagini sono salvate come risorse separate. | Imposta `HtmlSaveOptions.ExportImagesAsBase64 = true` per incorporarle direttamente. |
| **File ingombranti** | Cartelle di lavoro grandi generano HTML + JS massicci. | Usa `ExportOnlyVisibleSheets` o suddividi in più pagine con `HtmlSaveOptions.OnePagePerSheet`. |
| **Locale numerico errato** | Excel memorizza i numeri in cultura invariante, i browser possono applicare impostazioni locali. | Imposta esplicitamente `htmlOptions.Encoding = Encoding.UTF8` e usa `GridJsOptions.EnableNumberFormat`. |

---

## Avanzato: Esportare più fogli con istanze Grid.js individuali

Se la tua cartella di lavoro contiene diversi fogli e vuoi che ognuno diventi la propria tabella Grid.js, puoi iterare sui fogli di lavoro e salvarli separatamente:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Ogni file conterrà il proprio elemento `<table class="gridjs-table">`, pronto per manipolazioni indipendenti.

---

## Verifica dell'output – Checklist rapida

1. **Stile intatto?** Confronta i colori di sfondo delle celle e i bordi con la visualizzazione originale di Excel.  
2. **Formati numerici preservati?** Cerca l'attributo `data-format` sugli elementi `<td>`.  
3. **Immagini visualizzate?** Se hai esportato le immagini come Base64, dovrebbero apparire in linea.  
4. **Console del browser pulita?** Nessun errore JavaScript relativo a Grid.js.  

Se uno di questi controlli fallisce, ricontrolla la proprietà `HtmlSaveOptions` corrispondente — la maggior parte dei problemi deriva da un flag mancante.

---

## Conclusione

Ora disponi di un metodo solido, pronto per la produzione, per **salvare Excel come HTML** mantenendo ogni stile, bordo e rappresentazione numerica intatti. Configurando `HtmlSaveOptions` e attivando `GridJsOptions.EnableNumberFormat`, hai trasformato un foglio di calcolo statico in una tabella web‑friendly che funziona senza problemi con Grid.js.

In sintesi, questo tutorial ti mostra come **convertire Excel in HTML** e **esportare Excel con formattazione** usando Aspose.Cells. Sentiti libero di sperimentare: prova temi diversi, incorpora grafici, o servi l'HTML tramite un endpoint ASP.NET per conversioni on‑the‑fly.

---

## Cosa c'è dopo?

- **Esplora altri formati di esportazione**: PDF, PNG o CSV tramite `Workbook.Save`.  
- **Integra con ASP.NET Core**: Restituisci la stringa HTML direttamente da un'azione del controller.  
- **Combina con SheetJS**: Carica l'HTML generato nuovamente in un workbook JavaScript per modifiche lato client.  

Se incontri difficoltà, lascia un commento qui sotto o consulta la documentazione di Aspose.Cells per opzioni di configurazione più approfondite. Buon coding!

## Cosa dovresti imparare dopo?


I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Export Excel to HTML Preserving Border Styles Using Aspose.Cells for Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Convert HTML to Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}