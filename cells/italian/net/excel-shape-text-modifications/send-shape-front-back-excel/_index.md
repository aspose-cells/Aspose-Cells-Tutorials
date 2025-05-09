---
"description": "Scopri come portare le forme in primo piano o sullo sfondo in Excel utilizzando Aspose.Cells per .NET. Questa guida fornisce un tutorial passo passo con suggerimenti."
"linktitle": "Invia forma anteriore o posteriore in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Invia forma anteriore o posteriore in Excel"
"url": "/it/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Invia forma anteriore o posteriore in Excel

## Introduzione
Quando si lavora con file Excel, potrebbe essere necessario un maggiore controllo sugli elementi visivi del foglio di calcolo. Le forme, come immagini e grafici, possono migliorare la presentazione dei dati. Ma cosa succede quando queste forme si sovrappongono o devono essere riordinate? È qui che Aspose.Cells per .NET eccelle. In questo tutorial, vi guideremo attraverso i passaggi per manipolare le forme in un foglio di lavoro Excel, in particolare per posizionarle in primo piano o in secondo piano rispetto ad altre forme. Se siete pronti a potenziare le vostre capacità in Excel, iniziamo subito!
## Prerequisiti
Prima di iniziare, devi predisporre alcune cose:
1. Installazione della libreria Aspose.Cells: assicurati di aver installato la libreria Aspose.Cells per .NET. Puoi trovarla [Qui](https://releases.aspose.com/cells/net/).
2. Ambiente di sviluppo: assicurati di disporre di un ambiente di sviluppo configurato con supporto .NET, come Visual Studio.
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
Bene, hai soddisfatto tutti i requisiti? Ottimo! Passiamo alla parte divertente: scrivere un po' di codice!
## Importa pacchetti
Prima di immergerci nella codifica vera e propria, importiamo i pacchetti necessari. Basta aggiungere la seguente direttiva using all'inizio del file C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Questi namespace sono fondamentali perché contengono le classi e i metodi che utilizzeremo per manipolare i file e le forme di Excel.
## Passaggio 1: definire i percorsi dei file
In questo primo passaggio, dobbiamo stabilire le directory di origine e di output. Qui si trova il file Excel e dove si desidera salvare il file modificato.
```csharp
//Directory di origine
string sourceDir = "Your Document Directory";
//Directory di output
string outputDir = "Your Document Directory";
```
Sostituire `"Your Document Directory"` con il percorso effettivo in cui sono archiviati i file Excel.
## Passaggio 2: caricare la cartella di lavoro
Ora che abbiamo impostato le directory, carichiamo la cartella di lavoro (il file Excel) che contiene le forme che vogliamo manipolare.
```csharp
//Carica il file Excel di origine
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Questa riga di codice inizializza un nuovo `Workbook` oggetto, caricando nella memoria il file Excel specificato in modo da poterci lavorare.
## Passaggio 3: accedi al foglio di lavoro 
Successivamente, dobbiamo accedere al foglio di lavoro specifico in cui risiedono le nostre forme. Per questo esempio, useremo il primo foglio di lavoro.
```csharp
//Accedi al primo foglio di lavoro
Worksheet ws = wb.Worksheets[0];
```
Facendo riferimento `Worksheets[0]`, stiamo prendendo di mira il primo foglio della nostra cartella di lavoro. Se le forme si trovano su un foglio diverso, modifica l'indice di conseguenza.
## Passaggio 4: accedi alle forme
Con l'accesso al foglio di lavoro pronto, selezioniamo le forme che ci interessano. In questo esempio, selezioneremo la prima e la quarta forma.
```csharp
//Accesso prima e quarta forma
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Queste linee ottengono le forme specifiche dal foglio di lavoro in base al loro indice.
## Passaggio 5: stampare la posizione Z-Order delle forme
Prima di spostare qualsiasi forma, stampiamo la sua posizione attuale in ordine Z. Questo ci aiuta a tracciarne il posizionamento prima di apportare modifiche.
```csharp
//Stampa la posizione Z-Order della forma
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Chiamando `ZOrderPosition`, possiamo vedere dove si trova ogni forma nell'ordine del disegno.
## Passaggio 6: Invia la prima forma in primo piano
Ora è il momento di agire! Mandiamo la prima forma in primo piano nell'ordine Z.
```csharp
//Invia questa forma in primo piano
sh1.ToFrontOrBack(2);
```
Passando `2` A `ToFrontOrBack`, stiamo chiedendo ad Aspose.Cells di portare questa forma in primo piano. 
## Passaggio 7: stampare la posizione dell'ordine Z della seconda forma
Prima di mandare indietro la seconda forma, controlliamo dove si trova.
```csharp
//Stampa la posizione Z-Order della forma
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Questo ci dà un'idea della posizione della quarta forma prima di apportare modifiche.
## Passaggio 8: mandare la quarta forma indietro
Infine, sposteremo la quarta forma in fondo alla pila Z-Order.
```csharp
//Invia questa forma indietro
sh4.ToFrontOrBack(-2);
```
Utilizzo `-2` poiché il parametro sposta la forma verso la parte posteriore della pila, assicurando che non ostruisca altre forme o testo.
## Passaggio 9: salvare la cartella di lavoro 
L'ultimo passaggio consiste nel salvare la cartella di lavoro con le forme appena posizionate.
```csharp
//Salvare il file Excel di output
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Questo comando salva la cartella di lavoro modificata nella directory di output specificata.
## Passaggio 10: messaggio di conferma
Infine, forniamo una semplice conferma per farci sapere che il nostro compito è stato completato con successo.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
E questo conclude il codice del nostro tutorial!
## Conclusione
Manipolare le forme in Excel utilizzando Aspose.Cells per .NET non è solo semplice, ma anche potente. Seguendo questa guida, ora dovresti essere in grado di spostare le forme in primo piano o sullo sfondo con facilità, ottenendo un maggiore controllo sulle tue presentazioni Excel. Con questi strumenti a tua disposizione, sei pronto a migliorare l'aspetto visivo dei tuoi fogli di calcolo.
## Domande frequenti
### Di quale linguaggio di programmazione ho bisogno per Aspose.Cells?  
Per lavorare con Aspose.Cells è necessario utilizzare C# o qualsiasi linguaggio supportato da .NET.
### Posso provare Aspose.Cells gratuitamente?  
Sì, puoi iniziare con una prova gratuita di Aspose.Cells [Qui](https://releases.aspose.com/).
### Quali tipi di forme posso manipolare in Excel?  
È possibile manipolare varie forme, come rettangoli, cerchi, linee e immagini.
### Come posso ottenere supporto per Aspose.Cells?  
Puoi visitare il forum della loro comunità per qualsiasi supporto o domanda [Qui](https://forum.aspose.com/c/cells/9).
### È disponibile una licenza temporanea per Aspose.Cells?  
Sì, puoi richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}