---
title: Invia forma anteriore o posteriore in Excel
linktitle: Invia forma anteriore o posteriore in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come inviare forme in primo piano o in secondo piano in Excel usando Aspose.Cells per .NET. Questa guida fornisce un tutorial passo dopo passo con suggerimenti.
weight: 16
url: /it/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Invia forma anteriore o posteriore in Excel

## Introduzione
Quando lavori con file Excel, potresti scoprire di aver bisogno di un maggiore controllo sugli elementi visivi nel tuo foglio di calcolo. Le forme, come immagini e grafici, possono migliorare la presentazione dei tuoi dati. Ma cosa succede quando queste forme si sovrappongono o devono essere riordinate? È qui che brilla Aspose.Cells per .NET. In questo tutorial, ti guideremo attraverso i passaggi per manipolare le forme in un foglio di lavoro Excel, in particolare inviando le forme in primo piano o in secondo piano rispetto ad altre forme. Se sei pronto a potenziare il tuo gioco Excel, tuffiamoci subito!
## Prerequisiti
Prima di iniziare, devi predisporre alcune cose:
1.  Installazione della libreria Aspose.Cells: assicurati di aver installato la libreria Aspose.Cells per .NET. Puoi trovarla[Qui](https://releases.aspose.com/cells/net/).
2. Ambiente di sviluppo: assicurati di disporre di un ambiente di sviluppo configurato con supporto .NET, come Visual Studio.
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
Bene, hai spuntato tutte le caselle nell'elenco dei prerequisiti? Ottimo! Passiamo alla parte divertente: scrivere un po' di codice!
## Importa pacchetti
Prima di immergerci nella codifica vera e propria, importiamo i pacchetti necessari. Basta aggiungere la seguente direttiva using in cima al tuo file C#:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Questi spazi dei nomi sono fondamentali perché contengono le classi e i metodi che utilizzeremo per manipolare i file e le forme di Excel.
## Passaggio 1: definire i percorsi dei file
In questo primo passaggio, dobbiamo stabilire le directory di origine e di output. È qui che si trova il tuo file Excel e dove vuoi salvare il file modificato.
```csharp
//Elenco di origine
string sourceDir = "Your Document Directory";
//Directory di output
string outputDir = "Your Document Directory";
```
 Sostituire`"Your Document Directory"` con il percorso effettivo in cui sono archiviati i file Excel.
## Passaggio 2: caricare la cartella di lavoro
Ora che abbiamo impostato le directory, carichiamo la cartella di lavoro (il file Excel) che contiene le forme che vogliamo manipolare.
```csharp
//Carica il file Excel di origine
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Questa riga di codice inizializza un nuovo`Workbook` oggetto, caricando il file Excel specificato nella memoria in modo da poterci lavorare.
## Passaggio 3: accedi al foglio di lavoro 
Poi, dobbiamo accedere al foglio di lavoro specifico in cui risiedono le nostre forme. Per questo esempio, useremo il primo foglio di lavoro.
```csharp
//Accedi al primo foglio di lavoro
Worksheet ws = wb.Worksheets[0];
```
 Facendo riferimento`Worksheets[0]`, stiamo prendendo di mira il primo foglio della nostra cartella di lavoro. Se le tue forme sono su un foglio diverso, regola l'indice di conseguenza.
## Passaggio 4: accedi alle forme
Con l'accesso al foglio di lavoro pronto, prendiamo le forme che ci interessano. Per questo esempio, accederemo alla prima e alla quarta forma.
```csharp
//Accesso prima e quarta forma
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Queste linee assumono le forme specifiche dal foglio di lavoro in base al loro indice.
## Passaggio 5: stampare la posizione dell'ordine Z delle forme
Prima di spostare qualsiasi forma, stampiamo la loro posizione Z-Order corrente. Questo ci aiuta a tracciare il loro posizionamento prima di apportare modifiche.
```csharp
//Stampa la posizione Z-Order della forma
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Chiamando`ZOrderPosition`, possiamo vedere dove si trova ogni forma nell'ordine del disegno.
## Passaggio 6: Invia la prima forma in primo piano
Ora è il momento di agire! Mandiamo la prima forma in prima linea nello Z-Order.
```csharp
//Invia questa forma in primo piano
sh1.ToFrontOrBack(2);
```
 Passando`2` A`ToFrontOrBack`, stiamo chiedendo ad Aspose.Cells di portare questa forma in primo piano. 
## Passaggio 7: stampare la posizione dell'ordine Z della seconda forma
Prima di mandare indietro la seconda forma, controlliamo dove si trova.
```csharp
//Stampa la posizione Z-Order della forma
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Questo ci dà un'idea della posizione della quarta forma prima di apportare modifiche.
## Passaggio 8: Invia la quarta forma indietro
Infine, invieremo la quarta forma in fondo alla pila Z-Order.
```csharp
//Invia questa forma indietro
sh4.ToFrontOrBack(-2);
```
 Utilizzando`-2` poiché il parametro sposta la forma verso la parte posteriore della pila, assicurando che non ostruisca altre forme o testo.
## Passaggio 9: Salvare la cartella di lavoro 
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
questo conclude il codice del nostro tutorial!
## Conclusione
Manipolare le forme in Excel usando Aspose.Cells per .NET non è solo semplice ma anche potente. Seguendo questa guida, dovresti ora essere in grado di inviare le forme in primo piano o in secondo piano con facilità, consentendo un controllo migliore sulle tue presentazioni Excel. Con questi strumenti a tua disposizione, sei pronto a migliorare l'aspetto visivo dei tuoi fogli di calcolo.
## Domande frequenti
### Di quale linguaggio di programmazione ho bisogno per Aspose.Cells?  
Per lavorare con Aspose.Cells è necessario utilizzare C# o qualsiasi linguaggio supportato da .NET.
### Posso provare Aspose.Cells gratuitamente?  
 Sì, puoi iniziare con una prova gratuita di Aspose.Cells[Qui](https://releases.aspose.com/).
### Che tipo di forme posso manipolare in Excel?  
È possibile manipolare varie forme, come rettangoli, cerchi, linee e immagini.
### Come posso ottenere supporto per Aspose.Cells?  
 Puoi visitare il forum della loro comunità per qualsiasi supporto o domanda[Qui](https://forum.aspose.com/c/cells/9).
### È disponibile una licenza temporanea per Aspose.Cells?  
 Sì, puoi richiedere una licenza temporanea[Qui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
