---
"description": "Scopri come controllare le risorse esterne nella conversione da Excel a PDF utilizzando Aspose.Cells per .NET con la nostra guida facile da seguire."
"linktitle": "Controllo delle risorse esterne in Excel in PDF in Aspose.Cells"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Controllo delle risorse esterne in Excel in PDF in Aspose.Cells"
"url": "/it/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Controllo delle risorse esterne in Excel in PDF in Aspose.Cells

## Introduzione
Nell'era digitale odierna, convertire fogli di calcolo Excel in documenti PDF è un'attività comune. Che si tratti di preparare report, dati finanziari o materiale per presentazioni, è importante assicurarsi che i PDF abbiano esattamente l'aspetto desiderato. Aspose.Cells per .NET è una libreria affidabile che consente di controllare questo processo di conversione fino al minimo dettaglio, soprattutto quando si gestiscono risorse esterne come le immagini che accompagnano i file Excel. In questa guida, approfondiamo come controllare le risorse esterne durante il processo di conversione da Excel a PDF utilizzando Aspose.Cells. Quindi, prendi la tua bevanda preferita e iniziamo!
## Prerequisiti
Prima di entrare nel vivo dell'argomento, assicuriamoci di avere tutto il necessario per iniziare. Ecco una breve lista di controllo:
1. Visual Studio o qualsiasi IDE compatibile con .NET: ti servirà un ambiente in cui scrivere e testare il codice.
2. Aspose.Cells per .NET: se non lo hai ancora installato, vai su [Download di Aspose](https://releases.aspose.com/cells/net/) pagina e scarica l'ultima versione.
3. Conoscenza di base di C#: la familiarità con il linguaggio di programmazione C# sarà utile. Se hai dubbi su qualche concetto, non esitare a consultarlo.
4. Un file Excel di esempio: prepara un file Excel con tutte le risorse esterne che desideri convertire. Puoi utilizzare il file di esempio fornito "samplePdfSaveOptions_StreamProvider.xlsx".
5. Un file immagine per i test: verrà utilizzato come risorsa esterna durante la conversione. Il file immagine "newPdfSaveOptions_StreamProvider.png" è un buon segnaposto.
## Importa pacchetti
Per iniziare, dovrai importare i namespace necessari dalla libreria Aspose.Cells. Questo è fondamentale per accedere alle sue funzionalità. Assicurati di aggiungere le seguenti direttive using all'inizio del file:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Questi pacchetti forniranno tutte le classi e i metodi essenziali di cui avrai bisogno per svolgere le tue attività.
## Passaggio 1: crea la classe del provider di streaming
Il primo ordine del giorno è creare una classe di provider di flusso che implementi il `IStreamProvider` interfaccia. Questa classe ti permetterà di controllare come vengono caricate le risorse esterne.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Leggere la nuova immagine in un flusso di memoria e assegnarla alla proprietà Stream
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
In questa classe:
- CloseStream: questo metodo verrà chiamato alla chiusura del flusso. Per ora, stiamo solo scrivendo un messaggio di debug per il tracciamento.
- InitStream: È qui che inizia la magia. Qui, leggerete l'immagine esterna come un array di byte, la convertirete in un flusso di memoria e la assegnerete a `options.Stream` proprietà.
## Passaggio 2: impostare le directory di origine e di output
Ora che il tuo provider di streaming è pronto, è il momento di stabilire dove si trova il tuo file Excel e dove desideri salvare il tuo PDF.
```csharp
// Directory di origine
string sourceDir = "Your Document Directory";
// Directory di output
string outputDir = "Your Document Directory";
```
Sostituisci semplicemente `"Your Document Directory"` Con il percorso effettivo sul computer in cui risiedono i tuoi file. Mantenere i file organizzati è fondamentale!
## Passaggio 3: carica il file Excel
Successivamente, caricherai il file Excel da cui vuoi creare il PDF.
```csharp
// Carica il file Excel di origine contenente immagini esterne
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Stiamo usando il `Workbook` classe di Aspose.Cells, che rappresenta il file Excel. Il file può includere diverse risorse esterne, come immagini, che si desidera controllare durante la conversione.
## Passaggio 4: imposta le opzioni di salvataggio PDF
Prima di salvare la cartella di lavoro in formato PDF, specifichiamo come desideri salvarla. Puoi personalizzare queste opzioni in base alle tue esigenze.
```csharp
// Specificare le opzioni di salvataggio PDF - Fornitore di streaming
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Salva ogni foglio su una nuova pagina
```
Qui stiamo creando una nuova istanza di `PdfSaveOptions`che consente di personalizzare il modo in cui verrà formattato il PDF. `OnePagePerSheet` Questa opzione è utile per garantire che ogni foglio Excel abbia la propria pagina nel PDF finale.
## Passaggio 5: Assegna il tuo fornitore di streaming
Una volta impostate le opzioni PDF, è necessario indicare ad Aspose di utilizzare il provider di flussi personalizzato per le risorse esterne.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Questa linea collega il tuo `Workbook` esempio con il `MyStreamProvider` classe creata in precedenza. Ciò significa che ogni volta che vengono rilevate risorse esterne durante la conversione, il provider le gestirà come specificato.
## Passaggio 6: salvare la cartella di lavoro in formato PDF
Dopo aver impostato tutto, è finalmente giunto il momento di salvare la cartella di lavoro di Excel in formato PDF.
```csharp
// Salva la cartella di lavoro in PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Chiamando il `Save` sull'oggetto cartella di lavoro e passando la directory di output insieme alle opzioni PDF, si converte il file Excel in un PDF formattato magnificamente.
## Passaggio 7: Confermare l'esecuzione corretta
Per concludere, è sempre bello avere la conferma che il processo ha avuto successo!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Visualizzare un messaggio di successo sulla console aiuta a rimanere informati sullo stato dell'operazione. È una buona abitudine includere queste piccole conferme nel codice.
## Conclusione
Ecco fatto! Seguendo questi semplici passaggi, puoi controllare in modo professionale la gestione delle risorse esterne durante le conversioni da Excel a PDF utilizzando Aspose.Cells. Ciò significa che i tuoi documenti possono ora includere immagini e altri elementi esterni in modo accurato, garantendo ogni volta un prodotto finale impeccabile.
## Domande frequenti
### Che cosa è Aspose.Cells?  
Aspose.Cells è una potente libreria per sviluppatori .NET che consente di creare, manipolare, convertire e visualizzare file Excel in vari formati.
### Come faccio a scaricare Aspose.Cells?  
Puoi scaricare l'ultima versione di Aspose.Cells da [Link per il download](https://releases.aspose.com/cells/net/).
### Posso provare Aspose.Cells gratuitamente?  
Sì! Puoi ottenere una prova gratuita visitando il [Pagina di prova gratuita](https://releases.aspose.com/).
### Dove posso trovare supporto per Aspose.Cells?  
Per qualsiasi domanda relativa al supporto, puoi visitare [Forum di supporto di Aspose](https://forum.aspose.com/c/cells/9).
### Come posso ottenere una licenza temporanea per Aspose.Cells?  
Puoi richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}