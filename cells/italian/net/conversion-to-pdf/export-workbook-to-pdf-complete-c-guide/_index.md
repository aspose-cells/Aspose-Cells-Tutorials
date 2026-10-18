---
category: general
date: 2026-02-26
description: Esporta la cartella di lavoro in PDF con caratteri incorporati e esporta
  anche i grafici in PowerPoint in C#. Impara a copiare il foglio della tabella pivot
  e a salvare la cartella di lavoro come PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: it
og_description: Esporta la cartella di lavoro in PDF con caratteri incorporati e anche
  esporta i grafici in PowerPoint in C#. Segui la guida passo‑passo per copiare le
  tabelle pivot e salvare come PPTX.
og_title: Esporta cartella di lavoro in PDF – Guida completa a C#
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Esporta cartella di lavoro in PDF – Guida completa C#
url: /it/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Cartella di Lavoro in PDF – Guida Completa C#

L'esportazione di una cartella di lavoro in PDF è una necessità comune quando devi condividere report con stakeholder che potrebbero non avere Excel installato. In questo tutorial mostreremo anche come **esportare i grafici in PowerPoint**, copiare un **foglio di tabella pivot** e incorporare i font in modo che il PDF abbia esattamente lo stesso aspetto del design sullo schermo.  

Ti sei mai chiesto perché alcuni PDF perdono il layout originale o perché le diapositive PowerPoint finiscono con forme mancanti? La risposta di solito sta nelle opzioni mancanti durante il processo di esportazione. Alla fine di questa guida avrai un unico metodo C# riutilizzabile che gestisce tutti questi punti critici—niente più copia‑incolla manuale o impostazioni di esportazione complicate.

## Cosa Imparerai

- Come creare una cartella di lavoro, aggiungere espressioni Smart Marker e processarle.  
- Come **copiare un foglio di tabella pivot** senza rompere la fonte dati.  
- Come **esportare grafici, forme e caselle di testo** in una presentazione PowerPoint mantenendoli modificabili.  
- Come **incorporare i font standard** durante l'esportazione PDF per una resa coerente su qualsiasi macchina.  
- Come **salvare la cartella di lavoro come PPTX** usando l'approccio `save workbook as pptx`.  

Tutto questo funziona con le ultime librerie Aspose.Cells e Aspose.Slides .NET (versione 23.11 al momento della stesura). Nessun tool esterno, nessuno script di post‑processing—solo puro C#.

> **Suggerimento professionale:** Se stai già usando Aspose nel tuo progetto, puoi inserire gli snippet di codice così come sono; altrimenti, aggiungi prima i pacchetti NuGet `Aspose.Cells` e `Aspose.Slides`.

## Prerequisiti

- .NET 6.0 o successivo (il codice funziona anche su .NET Framework 4.7.2).  
- Visual Studio 2022 (o qualsiasi IDE tu preferisca).  
- Aspose.Cells .NET e Aspose.Slides .NET installati tramite NuGet.  
- Familiarità di base con C# e concetti di Excel come Smart Markers e PivotTables.

---

![Diagramma esportazione cartella di lavoro in PDF](export-workbook-to-pdf.png "Flusso di lavoro per l'esportazione della cartella di lavoro in PDF che mostra le uscite PDF e PPTX")

## Esporta Cartella di Lavoro in PDF – Implementazione Passo‑per‑Passo

Di seguito trovi l'esempio completo, pronto per l'esecuzione. Costruisce una cartella di lavoro, inserisce espressioni Smart Marker, le elabora, copia un intervallo di tabella pivot e infine salva sia un PDF sia un file PowerPoint.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Perché Funziona

1. **L'elaborazione di Smart Marker** ti consente di popolare la cartella di lavoro da qualsiasi fonte dati (JSON, DataTables, ecc.) senza scrivere cicli.  
2. **DetailSheetNewName** crea un foglio separato per ogni dipartimento, fornendoti una scheda pulita per dipartimento.  
3. **Copiare l'intervallo** (`sourceRange.Copy`) duplica la tabella pivot *inclusa* la sua cache, così il foglio copiato si comporta esattamente come l'originale.  
4. **PresentationOptions** con `ExportCharts`, `ExportShapes` e `ExportTextBoxes` indica ad Aspose di renderizzare quegli oggetti come elementi nativi di PowerPoint, preservandone la modificabilità.  
5. **PdfSaveOptions.EmbedStandardFonts** garantisce che il PDF abbia lo stesso aspetto su macchine che non hanno i font originali installati.

Il risultato sono due file—`FinalReport.pdf` e `FinalPresentation.pptx`—che possono essere inviati via email, archiviati o visualizzati in qualsiasi lettore senza perdita di fedeltà.

## Esporta Grafici in PowerPoint (Salva Cartella di Lavoro come PPTX)

Se il tuo report contiene grafici, probabilmente vorrai che siano modificabili in PowerPoint. La classe `PresentationOptions` è la chiave. Ecco uno snippet focalizzato che mostra solo la parte di esportazione dei grafici:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**Cosa succede dietro le quinte?** Aspose traduce ogni grafico Excel in un grafico PowerPoint nativo, preservando serie, titoli degli assi e formattazione. Questo è molto migliore rispetto all'esportazione del grafico come immagine statica, perché il tuo pubblico può modificare i punti dati in seguito.

## Copia Foglio di Tabella Pivot Senza Perdere Dati

Le tabelle pivot sono spesso la parte più delicata di un'esportazione perché si basano su una cache nascosta. Il semplice metodo `Copy` funziona perché Aspose copia sia l'intervallo visibile **che** l'oggetto cache sottostante.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Nota:** Se ti serve la tabella pivot solo su un nuovo foglio all'interno della stessa cartella di lavoro, l'approccio `sourceRange.Copy` precedente è più leggero e evita di creare una cartella di lavoro completamente nuova.

## Incorpora Font per l'Esportazione PDF – Perché è Importante

Quando apri un PDF su una macchina che non dispone dei font originali, il testo può spostarsi, le interruzioni di riga cambiare o i caratteri scomparire. Impostare `EmbedStandardFonts = true` dice ad Aspose di incorporare i font più comuni (Arial, Times New Roman, ecc.) direttamente nel flusso PDF.

Se usi font personalizzati, passa a `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Ecco un esempio:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Ora ogni destinatario vede esattamente lo stesso layout che hai progettato—senza sorprese.

## Riepilogo dell'Esempio Completo

Mettendo tutto insieme, il programma completo (mostrato in precedenza) esegue i seguenti passaggi:

1. **Crea** una cartella di lavoro con segnaposto Smart Marker.  
2. **Elabora** i marker, generando un foglio di dettaglio denominato come il dipartimento.  
3. **Copia** un intervallo che contiene una tabella pivot in un nuovo foglio, preservandone la funzionalità.  
4. **Esporta** la cartella di lavoro in PowerPoint, mantenendo grafici, forme e caselle di testo modificabili.  
5. **Esporta** la stessa cartella di lavoro in PDF incorporando i font standard per una resa affidabile.

Esegui il programma, apri i file generati e vedrai:

- **PDF**: Tabelle nitide, font incorporati e lo stesso stile visivo del file Excel originale.  
- **PowerPoint**: Grafici modificabili che puoi fare clic destro → *Modifica dati* in PowerPoint, e forme completamente manipolabili.

---

## Domande Frequenti (FAQ)

**D: Funziona con .NET Core?**  
Sì—Aspose.Cells e Aspose.Slides sono cross‑platform. Basta puntare a .NET 6 o versioni successive e lo stesso codice funziona su Windows, Linux o macOS.

**D: E se devo esportare solo un sottoinsieme di fogli?**  
Usa `Workbook.Save` con `SaveOptions` che ti permettono di specificare `SheetNames`. Esempio: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**D: Posso criptare il PDF?**  
Assolutamente. Imposta `PdfSaveOptions.EncryptionDetails` con una password prima di chiamare `Save`.

**D: La mia tabella pivot utilizza una fonte dati esterna—la copia romperà il collegamento?**  
L'operazione di copia include la cache, non la connessione esterna. La pivot funzionerà offline, ma non si aggiornerà rispetto alla fonte originale. Se ti serve un aggiornamento live, esporta i dati sorgente insieme alla cartella di lavoro.

## Prossimi Passi & Argomenti Correlati

- **Fonti Dati Dinamiche** – Scopri come alimentare Smart Markers con JSON o DataTable per report in tempo reale.  
- **Stilizzazione Avanzata PDF** – Esplora `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}