---
"description": "Scopri come posizionare le immagini in modo assoluto in Excel utilizzando Aspose.Cells per .NET con questo tutorial completo passo dopo passo."
"linktitle": "Posizione Immagine (Assoluta) in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Posizione Immagine (Assoluta) in Excel"
"url": "/it/net/excel-ole-picture-objects/position-picture-absolute-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Posizione Immagine (Assoluta) in Excel

## Introduzione
Hai mai avuto difficoltà a posizionare correttamente le immagini in un foglio di calcolo Excel? Non sei il solo! Molti utenti affrontano questa sfida, soprattutto quando le loro esigenze di visualizzazione dei dati richiedono un posizionamento assoluto per una migliore estetica o chiarezza. Bene, non cercare oltre; questa guida ti guiderà attraverso il semplice processo di posizionamento assoluto delle immagini in un foglio di lavoro Excel utilizzando Aspose.Cells per .NET. Che tu sia uno sviluppatore che lavora sulla manipolazione di Excel o un analista di dati che desidera migliorare i propri report, il nostro tutorial passo passo è qui per semplificare la tua esperienza con Excel e le immagini!
## Prerequisiti
Prima di addentrarci nel codice e nei dettagli, ecco alcune cose che devi tenere pronte:
1. Libreria Aspose.Cells: assicurati di avere la versione più recente della libreria Aspose.Cells per .NET. Puoi scaricarla da [pagina delle release](https://releases.aspose.com/cells/net/).
2. Ambiente di sviluppo: assicurati di avere un ambiente di sviluppo .NET funzionante. Puoi usare Visual Studio o qualsiasi altro IDE di tua scelta.
3. Conoscenza di base di C#: la familiarità con il linguaggio di programmazione C# sarà utile per comprendere i frammenti di codice.
4. File immagine: salva un file immagine (ad esempio "logo.jpg") nella directory dei documenti designata che intendi inserire nel foglio Excel.

## Importa pacchetti
Per iniziare, assicuriamoci di importare i pacchetti necessari per il nostro progetto. Il file di progetto dovrebbe includere i seguenti namespace:
```csharp
using System.IO;
using Aspose.Cells;
```
Importando questi namespace, garantiamo che il nostro programma possa sfruttare le funzionalità fornite da Aspose.Cells.
Per maggiore chiarezza, scomponiamo il tutto in passaggi gestibili.
## Passaggio 1: imposta la directory dei documenti
In questa fase iniziale, è necessario definire la directory in cui si trovano i documenti. Questo è essenziale affinché il programma sappia dove salvare o recuperare i file. Ecco come impostarla:
```csharp
string dataDir = "Your Document Directory";
```
Sostituisci semplicemente `"Your Document Directory"` con il percorso effettivo in cui si trova il file immagine. Potrebbe essere qualcosa del tipo `"C:\\Users\\YourUsername\\Documents\\"`.
## Passaggio 2: creazione di un oggetto cartella di lavoro
Successivamente, è necessario creare una nuova istanza di `Workbook` classe. Questo oggetto rappresenta il tuo file Excel:
```csharp
Workbook workbook = new Workbook();
```
A questo punto avrai una cartella di lavoro pronta per essere popolata con dati e immagini.
## Passaggio 3: aggiunta di un nuovo foglio di lavoro
Ora che hai la cartella di lavoro, devi aggiungervi un foglio di lavoro. È qui che avviene la magia dell'aggiunta e del posizionamento delle immagini:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Questa riga crea un nuovo foglio di lavoro all'interno della cartella di lavoro e restituisce il suo indice, che memorizziamo nella variabile `sheetIndex`.
## Fase 4: Ottenere il nuovo foglio di lavoro
Facciamo riferimento al foglio di lavoro appena creato. Utilizzando l'indice appena ottenuto, possiamo accedere al foglio di lavoro e manipolarlo:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Ora puoi lavorare con il `worksheet` oggetto per aggiungere contenuti, comprese le immagini.
## Passaggio 5: aggiunta di un'immagine
Ora la parte interessante! Ecco dove aggiungiamo l'immagine al nostro foglio di lavoro. Specifichiamo gli indici di riga e di colonna a cui vogliamo che l'immagine venga ancorata (in questo caso, alla cella "F6", che corrisponde alla riga 5 e alla colonna 5):
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Questa riga blocca di fatto l'immagine nella posizione specificata rispetto all'intero foglio di lavoro. Tuttavia, al momento, è ancora soggetta a ridimensionamento insieme alle celle.
## Passaggio 6: accesso all'immagine appena aggiunta
Per manipolare ulteriormente l'immagine, è necessario accedere alle sue proprietà:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Grazie a questo, avrai accesso alle proprietà dell'immagine che abbiamo appena aggiunto!
## Passaggio 7: impostazione del posizionamento assoluto per l'immagine
Per posizionare l'immagine in modo assoluto (in pixel), sarà necessario definire la sua posizione utilizzando `Left` E `Top` Proprietà. Qui potrai controllare dove apparirà l'immagine:
```csharp
picture.Left = 60;
picture.Top = 10;
```
È possibile regolare entrambi i valori in base alle proprie esigenze; essi rappresentano rispettivamente il posizionamento orizzontale e verticale dell'immagine.
## Passaggio 8: salvataggio del file Excel
Infine, dopo aver apportato tutte le modifiche, è il momento di salvare la cartella di lavoro:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Questo creerà un file Excel denominato `book1.out.xls` nella directory dei documenti definita in precedenza, contenente il foglio di lavoro con l'immagine posizionata in modo assoluto.

## Conclusione
Ed ecco fatto! Hai posizionato correttamente un'immagine in un foglio Excel con posizionamento assoluto utilizzando Aspose.Cells per .NET. Questo semplice processo non solo migliora la presentazione visiva dei tuoi documenti Excel, ma garantisce anche che le immagini rimangano esattamente dove desideri, indipendentemente da eventuali modifiche apportate alle dimensioni delle celle e all'altezza delle righe. Ora, che tu stia preparando un report o creando una dashboard, puoi garantire che le tue immagini siano posizionate perfettamente ogni volta.
## Domande frequenti
### Che cos'è Aspose.Cells per .NET?
Aspose.Cells per .NET è una libreria .NET che consente agli sviluppatori di creare, manipolare e convertire fogli di calcolo Excel a livello di programmazione, senza dover ricorrere a Microsoft Excel.
### Posso eseguire altre manipolazioni delle immagini utilizzando Aspose.Cells?
Sì, oltre al posizionamento, puoi anche ridimensionare, ruotare e modificare le immagini nei fogli di calcolo Excel utilizzando la libreria Aspose.Cells.
### Aspose.Cells è gratuito?
Aspose.Cells è un prodotto commerciale, ma puoi iniziare con una prova gratuita disponibile sul loro sito [pagina di prova gratuita](https://releases.aspose.com/).
### Come posso ottenere una licenza temporanea per Aspose.Cells?
È possibile richiedere una licenza temporanea tramite [pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/) fornito da Aspose.
### Dove posso trovare altri esempi e documentazione?
IL [Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) contiene risorse estese, tra cui esempi di codice e funzionalità più dettagliate.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}