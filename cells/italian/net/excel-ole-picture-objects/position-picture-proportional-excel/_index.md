---
"description": "Scopri come posizionare le immagini in modo proporzionale in Excel utilizzando Aspose.Cells per .NET. Rendi i tuoi fogli di calcolo visivamente più accattivanti."
"linktitle": "Immagine di posizione (proporzionale) in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Immagine di posizione (proporzionale) in Excel"
"url": "/it/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Immagine di posizione (proporzionale) in Excel

## Introduzione
Stanco di quelle immagini pixelate che non sembrano mai adattarsi perfettamente ai tuoi fogli di calcolo Excel? Immagina questo: hai un bellissimo logo che deve essere ben visibile nel tuo foglio Excel, ma finisce per essere schiacciato, allungato o posizionato male. Nessuno lo vuole! Bene, tieniti forte perché oggi imparerai a posizionare le immagini in modo proporzionale in Excel utilizzando la libreria Aspose.Cells per .NET. Questa potente libreria semplifica la manipolazione dei file Excel, che si tratti di report, analisi dei dati o semplicemente di abbellire le tue presentazioni. Immergiamoci nei dettagli dell'allineamento perfetto delle immagini!
## Prerequisiti
Prima di addentrarci nella codifica vera e propria, ci sono alcune cose che devi impostare sul tuo computer:
1. Visual Studio: assicurati di aver installato Visual Studio, poiché fornirà un ambiente pratico per il tuo progetto .NET.
2. Libreria Aspose.Cells: avrai bisogno della libreria Aspose.Cells. Puoi ottenere una prova gratuita o acquistarla da [Sito web di Aspose](https://purchase.aspose.com/buy).
3. Conoscenza di base di C#: una minima conoscenza della programmazione in C# sarà molto utile per comprendere gli esempi che discuteremo.
4. Un file immagine: tieni pronta un'immagine (come il tuo logo) che vuoi inserire nel foglio Excel.
Ora che hai tutto a posto, passiamo alla codifica!
## Importa pacchetti
Per iniziare a utilizzare Aspose.Cells nel tuo progetto, devi importare gli spazi dei nomi specifici. Ecco come fare:
### Crea un nuovo progetto
In Visual Studio, crea un nuovo progetto:
- Aprire Visual Studio.
- Fare clic su "Crea un nuovo progetto".
- Scegli "Libreria di classi (.NET Framework)" o "Applicazione console", a seconda delle tue preferenze.
### Installa Aspose.Cells
Puoi aggiungere il pacchetto Aspose.Cells al tuo progetto tramite NuGet. Ecco come:
- Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
- Seleziona "Gestisci pacchetti NuGet".
- Cerca "Aspose.Cells" e clicca su "Installa".
### Aggiungi direttive di utilizzo
Nella parte superiore del file di codice, includi le seguenti direttive:
```csharp
using System.IO;
using Aspose.Cells;
```
Queste direttive ti daranno accesso alle classi di cui avrai bisogno per manipolare i tuoi file Excel.
Ora analizziamo nel dettaglio i passaggi necessari per posizionare correttamente un'immagine in modo proporzionale in Excel.
## Passaggio 1: imposta la tua directory
Per prima cosa, assicurati di avere una cartella designata per i tuoi documenti. Ecco come creare una directory se non esiste:
```csharp
string dataDir = "Your Document Directory";
// Creare la directory se non è già presente.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Questo frammento crea una nuova directory (se non esiste) per archiviare i file Excel. Basta sostituirla `"Your Document Directory"` con il percorso effettivo in cui desideri salvare i file.
## Passaggio 2: creare un'istanza di una cartella di lavoro
Ora creiamo una nuova cartella di lavoro:
```csharp
Workbook workbook = new Workbook();
```
Questa riga inizializza un nuovo oggetto cartella di lavoro, offrendoti una tela bianca su cui lavorare.
## Passaggio 3: aggiungere un nuovo foglio di lavoro
Ora che abbiamo impostato la nostra cartella di lavoro, aggiungiamo un nuovo foglio di lavoro:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Questo aggiungerà un nuovo foglio di lavoro e restituirà l'indice di quel foglio, che potremo utilizzare per manipolarlo in seguito.
## Passaggio 4: accedi al nuovo foglio di lavoro
Per manipolare il foglio di lavoro appena aggiunto, è necessario accedervi:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Ora, `worksheet` ci consentirà di aggiungere contenuti e immagini a quel foglio specifico.
## Passaggio 5: Inserisci l'immagine
Ora arriva la parte emozionante! Aggiungiamo la tua bellissima immagine. Sostituisci `"logo.jpg"` con il nome del tuo file immagine:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Questa riga aggiunge l'immagine alla cella F6 (poiché le righe e le colonne sono indicizzate a zero, `5` si riferisce alla sesta cellula).
## Passaggio 6: accedi all'immagine aggiunta
Una volta inserita l'immagine, è possibile accedervi in questo modo:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Ciò consente di manipolare le proprietà dell'immagine.
## Passaggio 7: posizionare l'immagine in modo proporzionale
Ora posizioniamo l'immagine proporzionalmente:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Qui, `UpperDeltaX` E `UpperDeltaY` Regola la posizione dell'immagine rispetto alle dimensioni della cella. Puoi modificare questi valori per ottenere l'immagine perfetta.
## Passaggio 8: salva le modifiche
Infine, salva la cartella di lavoro per conservare tutte le modifiche:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Questa riga salva la cartella di lavoro come `book1.out.xls` nella directory designata.
## Conclusione
Ed ecco fatto! Hai appena imparato a posizionare le immagini in modo proporzionale in Excel usando Aspose.Cells per .NET. Non si tratta solo di inserire immagini; si tratta di renderle perfette nei tuoi fogli di calcolo. Ricorda: un'immagine ben posizionata può migliorare significativamente la presentazione dei tuoi dati.
Divertitevi a sperimentare con immagini e posizionamenti diversi e non esitate ad approfondire le ricche funzionalità offerte da Aspose.Cells. I vostri fogli Excel stanno per ricevere un vero restyling!
## Domande frequenti
### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria per .NET che consente agli utenti di creare, manipolare e convertire file Excel senza dover installare Microsoft Excel.
### Posso usare Aspose.Cells gratuitamente?
Sì, Aspose.Cells offre una prova gratuita, che puoi scaricare [Qui](https://releases.aspose.com/).
### Dove posso trovare la documentazione?
Puoi accedere alla completa [documentazione](https://reference.aspose.com/cells/net/) per Aspose.Cells.
### Aspose.Cells supporta tutti i formati immagine?
Aspose.Cells supporta vari formati, tra cui JPEG, PNG, BMP, GIF e TIFF.
### Come posso ottenere supporto per Aspose.Cells?
Per qualsiasi domanda, non esitate a visitare il [forum di supporto](https://forum.aspose.com/c/cells/9) dove puoi porre le tue domande.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}