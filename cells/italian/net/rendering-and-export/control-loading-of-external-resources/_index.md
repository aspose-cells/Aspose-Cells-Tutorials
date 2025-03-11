---
title: Controllo delle risorse esterne in Excel in PDF in Aspose.Cells
linktitle: Controllo delle risorse esterne in Excel in PDF in Aspose.Cells
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come controllare le risorse esterne nella conversione da Excel a PDF utilizzando Aspose.Cells per .NET con la nostra guida facile da seguire.
weight: 12
url: /it/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Controllo delle risorse esterne in Excel in PDF in Aspose.Cells

## Introduzione
Nell'era digitale odierna, convertire i fogli di calcolo Excel in documenti PDF è un'attività comune. Che si tratti di preparare report, dati finanziari o materiali di presentazione, vuoi assicurarti che i tuoi PDF abbiano esattamente l'aspetto che desideri. Aspose.Cells per .NET è una libreria robusta che ti consente di controllare questo processo di conversione fino all'ultimo dettaglio, specialmente quando gestisci risorse esterne come le immagini che accompagnano i tuoi file Excel. In questa guida, ci immergiamo in come controllare le risorse esterne durante il processo di conversione da Excel a PDF utilizzando Aspose.Cells. Quindi, prendi la tua bevanda preferita e iniziamo!
## Prerequisiti
Prima di entrare nel vivo dell'argomento, assicuriamoci di avere tutto ciò che serve per iniziare. Ecco una rapida checklist:
1. Visual Studio o qualsiasi IDE compatibile con .NET: ti servirà un ambiente in cui scrivere e testare il codice.
2.  Aspose.Cells per .NET: se non lo hai ancora installato, vai su[Scarica Aspose](https://releases.aspose.com/cells/net/) pagina e scarica l'ultima versione.
3. Conoscenza di base di C#: la familiarità con il linguaggio di programmazione C# sarà utile. Se non sei sicuro di qualche concetto, non esitare a cercarlo.
4. Un file Excel di esempio: prepara un file Excel con tutte le risorse esterne che desideri convertire. Puoi usare il file di esempio fornito "samplePdfSaveOptions_StreamProvider.xlsx".
5. Un file immagine per il test: verrà utilizzato come risorsa esterna durante la conversione. Il file immagine "newPdfSaveOptions_StreamProvider.png" è un buon segnaposto.
## Importa pacchetti
Per dare il via alle cose, dovrai importare i namespace necessari dalla libreria Aspose.Cells. Questo è fondamentale per accedere alle sue funzionalità. Assicurati di aggiungere le seguenti direttive using in cima al tuo file:
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
## Passaggio 1: crea la tua classe di provider di streaming
 Il primo ordine del giorno è creare una classe di provider di streaming che implementi l'`IStreamProvider` interfaccia. Questa classe ti consentirà di controllare come vengono caricate le risorse esterne.
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
- CloseStream: questo metodo verrà chiamato quando il flusso verrà chiuso. Per ora, stiamo solo scrivendo un messaggio di debug per il tracciamento.
-  InitStream: è qui che inizia la magia. Qui, leggerai la tua immagine esterna come un array di byte, la convertirai in un flusso di memoria e la assegnerai al`options.Stream` proprietà.
## Passaggio 2: impostare le directory di origine e di output
Ora che il tuo provider di streaming è pronto, è il momento di stabilire dove si trova il tuo file Excel e dove desideri salvare il tuo PDF.
```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";
// Directory di uscita
string outputDir = "Your Document Directory";
```
 Sostituisci semplicemente`"Your Document Directory"` con il percorso effettivo sul tuo computer dove risiedono i tuoi file. Mantenere i tuoi file organizzati è fondamentale!
## Passaggio 3: carica il file Excel
Successivamente, caricherai il file Excel da cui vuoi creare il PDF.
```csharp
// Carica il file Excel di origine contenente immagini esterne
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 Stiamo usando il`Workbook` classe da Aspose.Cells, che rappresenta il tuo file Excel. Il file può includere varie risorse esterne come immagini che vuoi controllare durante la conversione.
## Passaggio 4: imposta le opzioni di salvataggio PDF
Prima di salvare la cartella di lavoro come PDF, specifichiamo come desideri salvarla. Puoi regolare queste opzioni in base alle tue esigenze.
```csharp
// Specificare le opzioni di salvataggio PDF - Fornitore di streaming
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Salva ogni foglio su una nuova pagina
```
 Qui stiamo creando una nuova istanza di`PdfSaveOptions` , che consente di personalizzare il modo in cui verrà formattato il PDF. Il`OnePagePerSheet`Questa opzione è utile per garantire che ogni foglio Excel abbia la propria pagina nel PDF finale.
## Passaggio 5: Assegna il tuo fornitore di streaming
Una volta impostate le opzioni PDF, è necessario indicare ad Aspose di utilizzare il provider di flussi personalizzato per le risorse esterne.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 Questa linea collega il tuo`Workbook` istanza con il`MyStreamProvider` classe creata in precedenza. Ciò significa che ogni volta che vengono incontrate risorse esterne durante la conversione, il tuo provider le gestirà come specificato.
## Passaggio 6: salvare la cartella di lavoro in formato PDF
Dopo aver impostato tutto, è finalmente giunto il momento di salvare la cartella di lavoro di Excel in formato PDF.
```csharp
// Salva la cartella di lavoro in PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 Chiamando il`Save` sull'oggetto cartella di lavoro e passando la directory di output insieme alle opzioni PDF, si converte il file Excel in un PDF splendidamente formattato.
## Passaggio 7: confermare l'esecuzione corretta
Per concludere, è sempre bello avere la conferma che il processo ha avuto successo!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Stampare un messaggio di successo sulla console aiuta a tenerti informato sullo stato della tua operazione. È una buona abitudine includere queste piccole conferme nel tuo codice.
## Conclusione
Ecco fatto! Seguendo questi semplici passaggi, puoi controllare in modo esperto come vengono gestite le risorse esterne durante le conversioni da Excel a PDF usando Aspose.Cells. Ciò significa che i tuoi documenti possono ora includere immagini e altri elementi esterni in modo accurato, assicurando ogni volta un prodotto finale rifinito.
## Domande frequenti
### Che cos'è Aspose.Cells?  
Aspose.Cells è una potente libreria per sviluppatori .NET che consente di creare, manipolare, convertire e visualizzare file Excel in vari formati.
### Come posso scaricare Aspose.Cells?  
 Puoi scaricare l'ultima versione di Aspose.Cells da[Link per scaricare](https://releases.aspose.com/cells/net/).
### Posso provare Aspose.Cells gratuitamente?  
 Sì! Puoi ottenere una prova gratuita visitando il[Pagina di prova gratuita](https://releases.aspose.com/).
### Dove posso trovare supporto per Aspose.Cells?  
 Per qualsiasi domanda relativa al supporto, puoi visitare il[Forum di supporto Aspose](https://forum.aspose.com/c/cells/9).
### Come posso ottenere una licenza temporanea per Aspose.Cells?  
 Puoi richiedere una licenza temporanea[Qui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
