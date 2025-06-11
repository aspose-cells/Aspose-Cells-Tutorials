---
"date": "2025-04-05"
"description": "Scopri come convertire file Excel in formato PNG, TIFF e PDF utilizzando font personalizzati con Aspose.Cells per .NET. Garantisci una tipografia coerente in tutte le conversioni dei documenti."
"title": "Trasforma Excel in PNG, TIFF, PDF con font personalizzati in .NET utilizzando Aspose.Cells"
"url": "/it/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Trasforma i file Excel in PNG, TIFF e PDF con font personalizzati utilizzando Aspose.Cells per .NET

## Introduzione

Mantenere l'integrità dei font durante la conversione di file Excel in immagini o PDF è fondamentale per la coerenza del brand. Aspose.Cells per .NET offre una soluzione affidabile, consentendo di specificare font predefiniti personalizzati nelle conversioni dei documenti.

In questo tutorial, ti guideremo nel rendering di file Excel in formato PNG, TIFF e PDF utilizzando Aspose.Cells per .NET con font predefiniti personalizzati. Questo è ideale se:
- Cercare di ottenere una tipografia coerente nei documenti renderizzati.
- È necessario personalizzare le impostazioni dei caratteri durante le conversioni.
- Vuoi esplorare le opzioni di configurazione in Aspose.Cells per .NET.

Configuriamo il tuo ambiente e implementiamo queste funzionalità senza problemi.

### Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:
- **Ambiente .NET**: Installalo sul tuo computer (preferibilmente .NET Core o .NET Framework).
- **Aspose.Cells per la libreria .NET**: Installato nel tuo progetto.
- **File Excel**: Una cartella di lavoro Excel con dati da convertire.

### Impostazione di Aspose.Cells per .NET

Per iniziare, aggiungi la libreria Aspose.Cells al tuo progetto:

**Utilizzo della CLI .NET:**
```bash
dotnet add package Aspose.Cells
```

**Utilizzo del Gestore Pacchetti:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Ottieni una licenza per l'accesso completo alle funzionalità:
- **Prova gratuita**: Visita [Prova gratuita di Aspose](https://releases.aspose.com/cells/net/) per l'accesso iniziale.
- **Licenza temporanea**: Ottienilo da [Licenza temporanea Aspose](https://purchase.aspose.com/temporary-license/).
- **Acquistare**: Per una licenza permanente, vai a [Acquisto Aspose](https://purchase.aspose.com/buy).

Dopo aver acquisito la licenza, inizializza Aspose.Cells nella tua applicazione:
```csharp
// Imposta la licenza per Aspose.Cells.
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## Guida all'implementazione

### Rendering in PNG con font predefinito personalizzato

Il rendering di un foglio di lavoro Excel in formato PNG impostando un font predefinito personalizzato garantisce la coerenza visiva. Ecco come:

#### Passaggio 1: configurare le opzioni dell'immagine

Configura le opzioni di rendering per l'output dell'immagine.
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Specificare le directory.
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Aprire un file Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Imposta le opzioni di rendering dell'immagine.
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // Utilizzare un font personalizzato per i font mancanti nella cartella di lavoro.
imgOpt.DefaultFont = "Times New Roman";
```

#### Passaggio 2: rendering e salvataggio

Utilizzando queste impostazioni, converti il tuo foglio di lavoro in un file immagine.
```csharp
// Converti il primo foglio di lavoro in un'immagine PNG.
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### Rendering in TIFF con font predefinito personalizzato

Il formato TIFF è ideale per immagini di alta qualità. Ecco come convertire un'intera cartella di lavoro in un file TIFF:

#### Passaggio 3: impostare le opzioni immagine per TIFF

Configurare le opzioni di rendering specificamente per l'output TIFF.
```csharp
// Riutilizzare le directory definite in precedenza e aprire il file Excel.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Configura le opzioni di rendering delle immagini per TIFF.
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### Passaggio 4: rendering dell'intera cartella di lavoro in TIFF

Converti l'intera cartella di lavoro in un singolo file TIFF.
```csharp
// Rendi la cartella di lavoro come immagine TIFF.
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### Rendering in PDF con font predefinito personalizzato

Per una documentazione professionale è fondamentale salvare una cartella di lavoro di Excel in formato PDF, garantendo al contempo la coerenza dei caratteri.

#### Passaggio 5: configurare le opzioni di salvataggio PDF

Imposta le opzioni necessarie per salvare il file come PDF.
```csharp
using Aspose.Cells;

// Riaprire la cartella di lavoro.
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// Imposta le opzioni di salvataggio PDF.
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // Utilizzare un font personalizzato per i font mancanti nella cartella di lavoro.
```

#### Passaggio 6: Salva come PDF

Esporta la tua cartella di lavoro in un documento PDF.
```csharp
// Salvare la cartella di lavoro come file PDF.
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## Applicazioni pratiche

- **Rapporti aziendali**: Garantisci un marchio coerente in tutti i report esportati utilizzando caratteri personalizzati.
- **Archiviazione dei documenti**: Converti i file Excel legacy in PDF per una facile condivisione e archiviazione con una tipografia uniforme.
- **Graphic design**: Crea immagini TIFF ad alta risoluzione di dati Excel per presentazioni o progetti di design.

L'integrazione con altri sistemi, come piattaforme CRM o soluzioni di gestione dei documenti, può migliorare ulteriormente questi casi d'uso automatizzando le esportazioni in base a trigger o eventi specifici.

## Considerazioni sulle prestazioni

Ottimizzare il processo di rendering è fondamentale:
- **Gestione della memoria**: Smaltire `Workbook`, `SheetRender`, E `WorkbookRender` oggetti tempestivamente per liberare risorse.
- **Elaborazione batch**:Se si gestiscono più file, implementare l'elaborazione in batch per una gestione efficiente.
- **Operazioni asincrone**: Utilizzare metodi asincroni ove possibile per migliorare la reattività delle applicazioni.

## Conclusione

Ora hai imparato a visualizzare le cartelle di lavoro di Excel nei formati PNG, TIFF e PDF, impostando font predefiniti personalizzati tramite Aspose.Cells per .NET. Questa funzionalità garantisce che i tuoi documenti mantengano l'integrità visiva su diverse piattaforme e utilizzi.

Esplora le funzionalità aggiuntive offerte da Aspose.Cells per migliorare ulteriormente le capacità di gestione dei documenti. Per ulteriori informazioni o assistenza, visita il sito [Forum Aspose](https://forum.aspose.com/c/cells/9).

## Sezione FAQ

**1. Che cos'è Aspose.Cells per .NET?**
   — Aspose.Cells per .NET è una libreria che fornisce funzionalità avanzate per gestire e convertire i file Excel a livello di programmazione.

**2. Posso utilizzare Aspose.Cells nelle applicazioni web?**
   — Sì, Aspose.Cells può essere integrato in ASP.NET o in qualsiasi altra applicazione web basata su .NET.

**3. Come posso gestire i font mancanti durante il rendering?**
   — Impostando il `CheckWorkbookDefaultFont` su falso e specificando un `DefaultFont`, ti assicuri che tutto il testo utilizzi il font scelto, anche se l'originale non è disponibile.

**4. Sono supportati formati diversi da PNG, TIFF e PDF?**
   — Sì, Aspose.Cells supporta vari formati di immagine come JPEG, BMP, ecc. e offre ampie capacità di conversione dei documenti.

**5. Quali sono le best practice per l'utilizzo di Aspose.Cells in applicazioni su larga scala?**
   — Utilizzare tecniche efficienti di gestione della memoria, elaborazione batch per la gestione di più file e prendere in considerazione operazioni asincrone per migliorare le prestazioni dell'applicazione.

## Risorse
- **Documentazione**: [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/)
- **Scaricamento**: [Rilasci di Aspose.Cells](https://releases.aspose.com/cells/net/)
- **Acquistare**: [Acquista Aspose.Cells](https://purchase.aspose.com/buy)
- **Prova gratuita**: [Prova Aspose.Cells gratuitamente](https://releases.aspose.com/cells/net/)
- **Licenza temporanea**: [Ottieni una licenza temporanea](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}