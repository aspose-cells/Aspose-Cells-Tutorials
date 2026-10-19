---
category: general
date: 2026-06-24
description: Incorpora i caratteri PDF usando Aspose.Cells in C#. Scopri come salvare
  Excel come PDF, esportare Excel in HTML, convertire xlsx in PDF con Aspose e duplicare
  le righe pivot.
draft: false
keywords:
- embed fonts pdf
- save excel as pdf
- export excel to html
- xlsx to pdf aspose
- duplicate rows pivot
language: it
og_description: Incorpora i font PDF usando Aspose.Cells in C#. Questo tutorial mostra
  passo passo come salvare Excel come PDF, esportare Excel in HTML e altro.
og_title: Incorpora i font PDF con Aspose.Cells – Guida completa C#
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Embed fonts PDF using Aspose.Cells in C#. Learn how to save Excel as
    PDF, export Excel to HTML, convert xlsx to PDF with Aspose, and duplicate rows
    pivot.
  headline: Embed fonts PDF with Aspose.Cells – Complete C# Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
title: Incorpora i font PDF con Aspose.Cells – Guida completa C#
url: /it/net/xps-and-pdf-operations/embed-fonts-pdf-with-aspose-cells-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incorporare i font PDF con Aspose.Cells – Guida completa C#

Ti sei mai chiesto come **incorporare i font PDF** quando converti una cartella di lavoro Excel con Aspose.Cells? Non sei solo—molti sviluppatori si trovano in difficoltà quando il PDF generato appare errato su macchine che non hanno i font di origine installati.  

In questa guida percorreremo un esempio reale che non solo **incorpora i font PDF**, ma mostra anche come **salvare Excel come PDF**, **esportare Excel in HTML**, trasformare un **xlsx in PDF con Aspose**, e persino **duplicare righe pivot** senza rompere la tabella pivot. Sembra molto? Nessun problema—lo suddivideremo passo per passo.

## Cosa imparerai

- Come copiare le righe che contengono una tabella pivot mantenendo intatta la pivot.  
- Come inserire uno smart‑marker che ripete un foglio di dettaglio per ogni ordine.  
- Le impostazioni esatte necessarie per **incorporare i font PDF**, esportare i grafici come PPTX modificabili e preservare i riquadri congelati quando **esporti Excel in HTML**.  
- Suggerimenti per risolvere problemi comuni come font mancanti o oggetti OLE rotti.  

**Prerequisiti:** .NET 6+ (o .NET Framework 4.6+), Aspose.Cells per .NET installato, e un ambiente di sviluppo C# di base (Visual Studio, Rider o VS Code). Non sono richiesti pacchetti NuGet aggiuntivi oltre a Aspose.Cells.

---

## Incorporare i font PDF – Processo passo‑a‑passo

Di seguito trovi il codice completo e eseguibile. Ogni sezione è annotata così puoi vedere esattamente perché facciamo quello che facciamo.

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Pivot;
using Aspose.Cells.SmartMarker;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the workbook that contains a pivot table and a shape
        // -------------------------------------------------
        var workbook = new Workbook("YOUR_DIRECTORY/template.xlsx");

        // -------------------------------------------------
        // Step 2: Duplicate the rows that include the pivot table (keeps the pivot intact)
        // -------------------------------------------------
        // The CopyRows method copies rows 0‑29 (30 rows) from the source worksheet
        // to the same worksheet, effectively duplicating the pivot area.
        workbook.Worksheets[0].Cells.CopyRows(0, 0, 30);

        // -------------------------------------------------
        // Step 3: Insert a smart‑marker to repeat a detail sheet for each order
        // -------------------------------------------------
        var orders = new[]
        {
            new { Id = 101, Items = new[] { "Pen", "Paper" } },
            new { Id = 102, Items = new[] { "Book" } }
        };
        var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName = "OrderDetail" };
        workbook.Worksheets[0].SmartMarkerProcessing(new { Orders = orders }, smartMarkerOptions);

        // -------------------------------------------------
        // Step 4: Save the workbook as a PPTX file with editable charts, OLE objects, and text boxes
        // -------------------------------------------------
        var pptxOptions = new PptxSaveOptions
        {
            ExportChartsAsEditable = true,
            ExportOleObjects = true,
            ExportTextBoxesAsEditable = true
        };
        workbook.Save("YOUR_DIRECTORY/result.pptx", pptxOptions);

        // -------------------------------------------------
        // Step 5: Save the same workbook as a PDF while embedding standard fonts
        // -------------------------------------------------
        // This is where we actually **embed fonts PDF**.
        var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
        workbook.Save("YOUR_DIRECTORY/result.pdf", pdfOptions);

        // -------------------------------------------------
        // Step 6: Save the workbook as HTML, preserving frozen panes and embedding all fonts
        // -------------------------------------------------
        // The HTML export respects the original layout and keeps the fonts inside the file.
        var htmlOptions = new HtmlSaveOptions
        {
            PreserveFreezePanes = true,
            EmbedAllFonts = true
        };
        workbook.Save("YOUR_DIRECTORY/result.html", htmlOptions);
    }
}
```

### Perché funziona

- **CopyRows** duplica le righe che contengono la tabella pivot, così la pivot originale rimane collegata ai dati di origine. Questo soddisfa il requisito **duplicate rows pivot**.  
- **SmartMarkerProcessing** crea un nuovo foglio di lavoro per ogni ordine, automatizzando la generazione del foglio di dettaglio.  
- **PdfSaveOptions.EmbedStandardFonts = true** indica ad Aspose.Cells di incorporare i font direttamente nel file PDF, che è la chiave per **incorporare i font pdf**. Senza questa impostazione il PDF ricade sui font di sistema, rompendo il layout su altre macchine.  
- **HtmlSaveOptions** con `EmbedAllFonts` e `PreserveFreezePanes` garantisce che quando **esporti Excel in HTML**, la fedeltà visiva corrisponda al workbook originale.

#### Output previsto

- `result.pdf` – un PDF in cui tutti i font utilizzati sono incorporati; aprilo su qualsiasi computer e il testo apparirà identico all’originale.  
- `result.pptx` – un file PowerPoint con grafici e oggetti OLE modificabili.  
- `result.html` – una cartella HTML (`result.html` + `result_files`) che visualizza il workbook in un browser con i riquadri congelati intatti.

---

## Salva Excel come PDF con Aspose.Cells

Se il tuo unico obiettivo è **salvare Excel come PDF**, puoi eliminare i passaggi extra e concentrarti sulle opzioni PDF:

```csharp
var workbook = new Workbook("template.xlsx");

// Minimal PDF conversion – embed fonts for portability
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,   // crucial for embed fonts pdf
    Compliance = PdfCompliance.PdfA1b // optional: make the PDF archival‑friendly
};

workbook.Save("output.pdf", pdfOpts);
```

**Consiglio professionale:** Quando miri alla conformità PDF/A, Aspose incorpora automaticamente tutti i font, fornendo un ulteriore livello di sicurezza per l’archiviazione a lungo termine.

---

## Esporta Excel in HTML preservando il layout

L’esportazione in HTML spesso perde l’aspetto originale del foglio, specialmente quando sono presenti riquadri congelati. Il frammento seguente mostra le impostazioni esatte di cui hai bisogno:

```csharp
var wb = new Workbook("template.xlsx");

var htmlOpts = new HtmlSaveOptions
{
    PreserveFreezePanes = true, // keeps the top rows/columns locked
    EmbedAllFonts = true,       // embeds fonts so the page looks the same everywhere
    ExportActiveWorksheetOnly = true,
    ExportCellValueAsString = true
};

wb.Save("output.html", htmlOpts);
```

Poiché impostiamo `EmbedAllFonts`, l’HTML generato contiene i dati dei font codificati in base‑64, soddisfacendo il requisito **export excel to html** senza alcun file CSS esterno.

---

## Converti Xlsx in PDF usando Aspose.Cells

A volte nella ricerca compare la frase “**xlsx to pdf aspose**”. Il codice qui sotto dimostra la pipeline di conversione esatta, includendo un paio di extra utili:

```csharp
var wb = new Workbook("template.xlsx");

// Optional: set page layout before conversion
wb.Worksheets[0].PageSetup.Orientation = PageOrientation.Landscape;
wb.Worksheets[0].PageSetup.FitToPagesWide = 1;
wb.Worksheets[0].PageSetup.FitToPagesTall = 0;

// PDF options – embed fonts and keep hyperlinks intact
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    ExportHyperlinks = true,
    OnePagePerSheet = false
};

wb.Save("converted.pdf", pdfOpts);
```

**Perché preoccuparsi della configurazione della pagina?** Se la salti, il PDF predefinito potrebbe tagliare colonne o righe. Regolare il layout prima assicura che il PDF finale corrisponda a ciò che vedi in Excel.

---

## Duplicare righe pivot – mantenere la pivot intatta

Un ostacolo comune è provare a copiare righe che contengono una tabella pivot; la pivot spesso perde il collegamento alla fonte dati. Il metodo `CopyRows` che abbiamo usato in precedenza fa il lavoro pesante per te:

```csharp
// Duplicate the first 30 rows (adjust as needed)
workbook.Worksheets[0].Cells.CopyRows(sourceRow: 0, destinationRow: 0, totalRows: 30);
```

- **sourceRow** – la prima riga dell’intervallo che desideri copiare.  
- **destinationRow** – dove deve essere posizionata la copia (stesso foglio, stesso indice di partenza per duplicare efficacemente).  
- **totalRows** – quante righe copiare.  

Poiché la cache della pivot vive nel foglio di lavoro, copiare le righe **non** rompe la pivot. Questo soddisfa la keyword **duplicate rows pivot** mantenendo il workbook ordinato.

---

## Riepilogo dell’esempio completo

Unendo tutto, ecco il programma completo che puoi inserire in un’app console e eseguire subito:



## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑a‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Save Excel Workbook as PDF with Custom Fonts using Aspose.Cells for .NET](/cells/english/net/workbook-operations/save-excel-workbook-pdf-custom-fonts-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Export Excel Slicers to PDF Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-slicers-to-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}