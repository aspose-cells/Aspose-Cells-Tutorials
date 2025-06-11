---
"description": "Scopri come impostare l'ora di creazione di un PDF in .NET utilizzando Aspose.Cells. Segui la nostra guida passo passo per una conversione senza problemi da Excel a PDF."
"linktitle": "Impostazione del tempo di creazione del PDF in .NET"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Impostazione del tempo di creazione del PDF in .NET"
"url": "/it/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Impostazione del tempo di creazione del PDF in .NET

## Introduzione
Nell'era digitale odierna, la possibilità di convertire documenti in diversi formati è fondamentale per molte applicazioni. Un'esigenza comune è la conversione di fogli di calcolo Excel in file PDF. Questo non solo preserva la formattazione, ma semplifica anche notevolmente la condivisione e la stampa. Se sei uno sviluppatore che lavora con .NET, Aspose.Cells è una libreria fantastica che semplifica questo processo. In questo tutorial, approfondiremo come impostare l'ora di creazione del PDF durante la conversione di un file Excel in PDF utilizzando Aspose.Cells per .NET.
## Prerequisiti
Prima di addentrarci nei dettagli del codice, assicuriamoci di avere tutto il necessario per iniziare.
### Ciò di cui hai bisogno
1. Visual Studio: assicurati di aver installato Visual Studio sul tuo computer. Questo sarà il tuo ambiente di sviluppo.
2. Aspose.Cells per .NET: Scarica la libreria Aspose.Cells da [sito web](https://releases.aspose.com/cells/net/)Puoi anche iniziare con una prova gratuita per testarne le funzionalità.
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
4. File Excel: Prepara un file Excel per la conversione. Per questo esempio, useremo un file denominato `Book1.xlsx`.
Ora che hai sistemato i prerequisiti, passiamo alla parte divertente: importare i pacchetti necessari e scrivere il codice!
## Importa pacchetti
Per iniziare, è necessario importare gli spazi dei nomi richiesti nel file C#. Questo è fondamentale perché consente di accedere alle classi e ai metodi forniti dalla libreria Aspose.Cells.
### Apri il tuo progetto C#
Aprire Visual Studio e creare un nuovo progetto oppure aprirne uno esistente in cui si desidera implementare la funzionalità di conversione PDF.
### Aggiungi riferimento Aspose.Cells
Puoi aggiungere la libreria Aspose.Cells al tuo progetto facendo clic con il pulsante destro del mouse sul progetto in Esplora soluzioni, selezionando "Gestisci pacchetti NuGet" e cercando "Aspose.Cells". Installa il pacchetto.
### Importa spazi dei nomi
Nella parte superiore del file C#, includi i seguenti namespace:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Questi namespace ti daranno accesso alla classe Workbook e ad altre funzionalità essenziali.

Ora che abbiamo importato i pacchetti, analizziamo il processo di conversione di un file Excel in PDF, impostando l'ora di creazione.
## Passaggio 1: definire la directory dei documenti
Per prima cosa, devi specificare la directory in cui sono archiviati i tuoi documenti. Questa è la directory in cui si trova il tuo file Excel e dove verrà salvato il PDF di output.
```csharp
string dataDir = "Your Document Directory"; // Specifica la directory dei tuoi documenti
```
Sostituire `"Your Document Directory"` con il percorso effettivo in cui ti trovi `Book1.xlsx` il file si trova. Questo percorso aiuterà l'applicazione a individuare il file per l'elaborazione.
## Passaggio 2: caricare il file Excel
Successivamente, caricherai il file Excel in un `Workbook` oggetto. È qui che Aspose.Cells eccelle, poiché consente di lavorare con i file Excel senza sforzo.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Percorso del file Excel
Workbook workbook = new Workbook(inputPath); // Carica il file Excel
```
IL `Workbook` La classe viene utilizzata per caricare e manipolare file Excel. Passando il percorso di input, si indica all'applicazione con quale file lavorare.
## Passaggio 3: creare PdfSaveOptions
Ora è il momento di creare un'istanza di `PdfSaveOptions`Questa classe consente di specificare varie opzioni per salvare la cartella di lavoro in formato PDF, inclusa l'ora di creazione.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Crea un'istanza di PdfSaveOptions
options.CreatedTime = DateTime.Now; // Imposta l'ora di creazione su adesso
```
Impostando `options.CreatedTime` A `DateTime.Now`, ti assicuri che il PDF rispecchi la data e l'ora correnti in cui è stato creato.
## Passaggio 4: salvare la cartella di lavoro in formato PDF
Infine, salverai la cartella di lavoro come file PDF utilizzando le opzioni appena definite.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Salva come PDF
```
Questa riga di codice prende la cartella di lavoro e la salva in formato PDF nella posizione specificata. `options` Il parametro viene passato per includere l'ora di creazione nei metadati del PDF.

## Conclusione
Ed ecco fatto! Hai convertito con successo un file Excel in PDF utilizzando Aspose.Cells per .NET, completo di timestamp di creazione. Questa funzionalità può essere incredibilmente utile quando devi tenere traccia delle versioni di un documento o quando vuoi fornire ai destinatari informazioni sulla data di creazione del documento.
Se desideri esplorare altre funzionalità di Aspose.Cells, non esitare a dare un'occhiata a [documentazione](https://reference.aspose.com/cells/net/).
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria per .NET che consente agli sviluppatori di creare, manipolare e convertire file Excel.
### Posso usare Aspose.Cells gratuitamente?
Sì, puoi iniziare con una prova gratuita disponibile su [Sito web di Aspose](https://releases.aspose.com/).
### Come posso impostare altre proprietà del PDF?
È possibile impostare varie proprietà PDF utilizzando `PdfSaveOptions` classe, come dimensione della pagina, compressione e altro ancora.
### È possibile convertire più file Excel contemporaneamente?
Sì, è possibile scorrere un elenco di file e applicare lo stesso processo di conversione a ciascuno di essi.
### Dove posso ottenere supporto per Aspose.Cells?
Puoi ottenere supporto dalla comunità Aspose su [forum di supporto](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}