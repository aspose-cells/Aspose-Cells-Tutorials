---
"description": "Scopri come ottenere punti di connessione delle forme in Excel con Aspose.Cells per .NET. Segui la nostra guida passo passo per estrarre e visualizzare facilmente i punti di connessione delle forme a livello di codice."
"linktitle": "Ottieni i punti di connessione della forma in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Ottieni i punti di connessione della forma in Excel"
"url": "/it/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni i punti di connessione della forma in Excel

## Introduzione
Quando si lavora con file Excel a livello di programmazione, spesso è necessario interagire con le forme incorporate nei fogli. Una delle attività più avanzate che è possibile eseguire è l'estrazione di punti di connessione da una forma. I punti di connessione vengono utilizzati per collegare le forme con connettori e gestirne il layout in modo più preciso. Se si desidera ottenere i punti di connessione di una forma in Excel, Aspose.Cells per .NET è lo strumento che fa al caso proprio. In questo tutorial, vi guideremo passo dopo passo attraverso una procedura per ottenere questo risultato.
## Prerequisiti
Prima di immergerti nel codice, assicurati di avere i seguenti prerequisiti:
- Aspose.Cells per .NET: è necessario che Aspose.Cells sia installato nel tuo ambiente di sviluppo. Se non lo hai ancora, puoi [scarica l'ultima versione qui](https://releases.aspose.com/cells/net/).
- Ambiente di sviluppo: assicurati di avere un'installazione funzionante di Visual Studio o di qualsiasi altro IDE compatibile con .NET.
- Conoscenza di base di C#: questo tutorial presuppone una conoscenza di base della programmazione C# e dei principi orientati agli oggetti.
Puoi anche iscriverti a un [prova gratuita di Aspose.Cells](https://releases.aspose.com/) Se non l'hai già fatto, avrai accesso a tutte le funzionalità necessarie per questa guida.

## Importa pacchetti
Per utilizzare Aspose.Cells nel tuo progetto, devi includere gli spazi dei nomi necessari. Le seguenti istruzioni di importazione devono essere inserite all'inizio del codice:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Questi namespace consentono di accedere alle funzionalità principali di Aspose.Cells e di manipolare fogli di lavoro e forme.

## Guida passo passo per ottenere i punti di connessione di una forma
In questa sezione, ti guideremo nell'estrazione dei punti di connessione di una forma all'interno di un foglio di lavoro Excel. Segui attentamente ogni passaggio per una comprensione chiara.
## Passaggio 1: creare una nuova cartella di lavoro
Prima di tutto, dobbiamo creare un'istanza di `Workbook` classe. Questo rappresenta un file Excel in Aspose.Cells. Se non hai un file esistente, nessun problema: puoi iniziare con una cartella di lavoro vuota.
```csharp
// Crea una nuova cartella di lavoro
Workbook workbook = new Workbook();
```
In questo passaggio, abbiamo creato una cartella di lavoro Excel vuota, ma puoi anche caricarne una esistente passando il percorso del file al `Workbook` costruttore.
## Passaggio 2: accedi al primo foglio di lavoro
Successivamente, dobbiamo accedere al foglio di lavoro in cui vogliamo lavorare con le forme. In questo caso, useremo il primo foglio di lavoro della cartella di lavoro.
```csharp
// Ottieni il primo foglio di lavoro nella cartella di lavoro
Worksheet worksheet = workbook.Worksheets[0];
```
Questa riga accede al primo foglio di lavoro dalla raccolta di fogli di lavoro nella cartella di lavoro. Se si sta lavorando con un foglio specifico, è possibile sostituire l'indice. `0` con l'indice desiderato.
## Passaggio 3: aggiungere una nuova casella di testo (forma)
Ora aggiungiamo una nuova forma al foglio di lavoro. Creeremo una casella di testo, che è un tipo di forma. Puoi aggiungere anche altri tipi di forme, ma per semplicità, in questo tutorial ci limiteremo a una casella di testo.
```csharp
// Aggiungi una nuova casella di testo alla raccolta
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Ecco cosa abbiamo fatto:
- Aggiunta una casella di testo alla riga `2`, colonna `1`.
- Imposta le dimensioni della casella di testo su `160` unità in larghezza e `200` unità di altezza.
## Passaggio 4: accedere alla forma dalla raccolta Forme
Una volta aggiunta la casella di testo, questa diventa parte della raccolta di forme del foglio di lavoro. Ora accederemo a quella forma utilizzando `Shapes` collezione.
```csharp
// Accedi alla forma (casella di testo) dalla raccolta di forme
Shape shape = workbook.Worksheets[0].Shapes[0];
```
In questo passaggio, recuperiamo la prima forma (la nostra casella di testo) dalla raccolta. Se hai più forme, puoi specificare l'indice o persino cercarle per nome.
## Passaggio 5: recuperare i punti di connessione
Ora che abbiamo la nostra forma, estraiamo i suoi punti di connessione. Questi punti servono per collegare i connettori alla forma. `ConnectionPoints` la proprietà della forma restituisce tutti i punti di connessione disponibili.
```csharp
// Ottieni tutti i punti di connessione in questa forma
var connectionPoints = shape.ConnectionPoints;
```
Questo ci fornisce una raccolta di tutti i punti di connessione disponibili per quella forma.
## Passaggio 6: visualizzare i punti di connessione
Infine, vogliamo visualizzare le coordinate di ogni punto di connessione. A questo punto, eseguiamo un ciclo sui punti di connessione e li stampiamo sulla console.
```csharp
// Visualizza tutti i punti della forma
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
Questo ciclo itera su ogni punto di connessione e stampa il `X` E `Y` coordinate. Questo può essere utile per il debug o per confermare visivamente i punti di connessione di una forma.
## Passaggio 7: eseguire e completare
Una volta impostati tutti i passaggi precedenti, puoi eseguire il codice. Ecco la riga finale che garantisce il completamento corretto del processo:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Questa riga registra semplicemente un messaggio sulla console indicando che il processo è stato completato.

## Conclusione
In questo tutorial abbiamo spiegato come recuperare i punti di connessione di una forma in Excel utilizzando Aspose.Cells per .NET. Suddividendo l'attività in piccoli passaggi di facile comprensione, abbiamo esplorato il processo di creazione di una cartella di lavoro, aggiunta di una forma ed estrazione dei punti di connessione.
Imparando a manipolare le forme a livello di programmazione, si apre un mondo di possibilità per la creazione di fogli Excel dinamici e interattivi. Che si tratti di creare report, dashboard o diagrammi, queste conoscenze saranno utili.
## Domande frequenti
### Cos'è un punto di connessione in una forma?
Un punto di connessione è un punto specifico su una forma in cui è possibile collegare dei connettori o collegarla ad altre forme.
### Posso recuperare i punti di connessione per tutte le forme in un foglio di lavoro?
Sì, Aspose.Cells consente di recuperare i punti di connessione per qualsiasi forma che li supporti. È sufficiente scorrere la raccolta di forme nel foglio di lavoro.
### Ho bisogno di una licenza per utilizzare Aspose.Cells?
Sì, anche se puoi provarlo gratuitamente, è richiesta una licenza per le funzionalità complete. Puoi [acquista una licenza qui](https://purchase.aspose.com/buy) o ottenere un [licenza temporanea](https://purchase.aspose.com/temporary-license/).
### Come posso aggiungere diversi tipi di forme in Aspose.Cells?
Puoi usare il `Add` Metodo per forme come rettangoli, ellissi e altro ancora. Ogni forma ha parametri specifici che è possibile personalizzare.
### Come faccio a caricare un file Excel esistente invece di crearne uno nuovo?
Per caricare un file esistente, passare il percorso del file al `Workbook` costruttore, in questo modo:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}