---
"description": "Scopri come impostare i font predefiniti per le opzioni di salvataggio PDF utilizzando Aspose.Cells per .NET, assicurandoti che i tuoi documenti abbiano sempre un aspetto perfetto."
"linktitle": "Imposta il carattere predefinito per le opzioni di salvataggio PDF"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Imposta il carattere predefinito per le opzioni di salvataggio PDF"
"url": "/it/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Imposta il carattere predefinito per le opzioni di salvataggio PDF

## Introduzione
Quando si tratta di generare report, fatture o qualsiasi altro documento in formato PDF, assicurarsi che il contenuto abbia un aspetto impeccabile è fondamentale. I font svolgono un ruolo fondamentale nel mantenere l'aspetto visivo e la leggibilità dei documenti. Tuttavia, cosa succede quando il font utilizzato nel file Excel non è disponibile sul sistema in cui si genera il PDF? È qui che Aspose.Cells per .NET torna utile. Questa potente libreria consente di impostare font predefiniti per le opzioni di salvataggio dei PDF, garantendo che i documenti abbiano un aspetto professionale e coerente, indipendentemente da dove vengano aperti.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
1. Visual Studio: per scrivere ed eseguire il codice avrai bisogno di un ambiente di sviluppo come Visual Studio.
2. Aspose.Cells per .NET: puoi scaricare l'ultima versione da [questo collegamento](https://releases.aspose.com/cells/net/)In alternativa, è possibile installarlo tramite NuGet Package Manager in Visual Studio.
3. Conoscenza di base di C#: comprendere le basi di C# ti aiuterà a seguire gli esempi di codice.
4. File Excel di esempio: tieni pronto un file Excel di esempio per i test. Puoi crearne uno con diversi font e stili per vedere come Aspose.Cells gestisce i font mancanti.
## Importa pacchetti
Prima di poter utilizzare Aspose.Cells nel tuo progetto, devi importare i pacchetti necessari. Ecco come fare:
1. Apri il tuo progetto: avvia Visual Studio e apri il progetto esistente oppure creane uno nuovo.
2. Aggiungere riferimenti: fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni e selezionare "Gestisci pacchetti NuGet".
3. Installa Aspose.Cells: cerca "Aspose.Cells" e clicca sul pulsante "Installa".
4. Aggiungi direttive Using: all'inizio del file C#, includi i seguenti namespace:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Passaggio 1: imposta le tue directory
Prima di lavorare con i file, è importante definire le directory di origine e di output. Questo renderà più facile individuare il file Excel di input e salvare i file di output generati.
```csharp
// Directory di origine
string sourceDir = "Your Document Directory";
// Directory di output
string outputDir = "Your Document Directory";
```
Sostituire `"Your Document Directory"` con il percorso effettivo delle tue directory.
## Passaggio 2: aprire il file Excel
Ora che abbiamo impostato le nostre directory, apriamo il file Excel con cui desideri lavorare. `Workbook` La classe in Aspose.Cells viene utilizzata per caricare il documento Excel.
```csharp
// Aprire un file Excel
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Assicurati di sostituire il nome del file con il nome effettivo del file.
## Passaggio 3: impostare le opzioni di rendering dell'immagine
Successivamente, dobbiamo configurare le opzioni di rendering per convertire il nostro foglio Excel in un formato immagine. Creeremo un'istanza di `ImageOrPrintOptions`, specificando il tipo di immagine e il font predefinito.
```csharp
// Rendering in formato file PNG
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
In questo frammento di codice, impostiamo il `CheckWorkbookDefaultFont` proprietà a `false`il che significa che se manca un font, verrà utilizzato il font predefinito specificato ("Times New Roman").
## Passaggio 4: rendering del foglio come immagine
Ora, trasformiamo il primo foglio della cartella di lavoro in un'immagine PNG. Useremo il `SheetRender` classe per raggiungere questo obiettivo.
```csharp
// Trasforma il primo foglio di lavoro in un'immagine
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Passaggio 5: modifica il tipo di immagine e il rendering in TIFF
Se vuoi rendere lo stesso foglio in un formato immagine diverso, come TIFF, puoi semplicemente cambiare il `ImageType` proprietà e ripetere il processo di rendering.
```csharp
// Imposta sul formato TIFF
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Passaggio 6: configurare le opzioni di salvataggio PDF
Ora impostiamo le opzioni di salvataggio del PDF. Creeremo un'istanza di `PdfSaveOptions`, imposta il font predefinito e specifica che vogliamo controllare i font mancanti.
```csharp
// Configurare le opzioni di salvataggio PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Passaggio 7: salvare la cartella di lavoro come PDF
Una volta configurate le opzioni di salvataggio, è il momento di salvare la nostra cartella di lavoro Excel come file PDF. 
```csharp
// Salva la cartella di lavoro in PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Passaggio 8: conferma dell'esecuzione
Infine, è buona norma informare l'utente che il processo è stato completato correttamente. È possibile farlo utilizzando un semplice messaggio nella console.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Conclusione
Aspose.Cells offre un modo flessibile e affidabile per gestire le manipolazioni dei file Excel, semplificando la creazione di documenti visivamente accattivanti che mantengano la formattazione originale. Che si lavori su report, documenti finanziari o qualsiasi altra forma di presentazione dei dati, avere il controllo sul rendering dei font può migliorare significativamente la qualità dell'output.
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria .NET che consente agli sviluppatori di manipolare file Excel senza dover installare Microsoft Excel. Supporta vari formati di file e offre funzionalità avanzate per l'utilizzo con i fogli di calcolo.
### Come posso impostare un font predefinito per i miei file Excel?
È possibile impostare un font predefinito utilizzando `PdfSaveOptions` classe e specifica il nome del font desiderato. Questo garantisce che, anche se manca un font, il documento utilizzerà il font predefinito specificato.
### Posso convertire i file Excel in formati diversi dal PDF?
Assolutamente sì! Aspose.Cells consente di convertire file Excel in vari formati, tra cui immagini (PNG, TIFF), HTML, CSV e altri ancora.
### Aspose.Cells è gratuito?
Aspose.Cells è un prodotto commerciale, ma puoi provarlo gratuitamente con una versione di prova limitata. Per sfruttare tutte le funzionalità, è necessario acquistare una licenza.
### Dove posso trovare supporto per Aspose.Cells?
Puoi trovare supporto per Aspose.Cells visitando il [Forum di Aspose](https://forum.aspose.com/c/cells/9), dove puoi porre domande e condividere opinioni con altri utenti e sviluppatori.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}