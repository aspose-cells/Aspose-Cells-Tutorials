---
title: Leggi l'ora di creazione dei commenti con thread nel foglio di lavoro
linktitle: Leggi l'ora di creazione dei commenti con thread nel foglio di lavoro
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Impara a leggere l'ora di creazione dei commenti concatenati in Excel utilizzando Aspose.Cells per .NET. Guida dettagliata con esempi di codice inclusi.
weight: 21
url: /it/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Leggi l'ora di creazione dei commenti con thread nel foglio di lavoro

## Introduzione
Quando si lavora con file Excel, la gestione dei commenti può essere un aspetto cruciale della collaborazione sui dati e del feedback. Se si utilizza Aspose.Cells per .NET, lo si troverà incredibilmente potente per gestire varie funzionalità di Excel, inclusi i commenti con thread. In questo tutorial, ci concentreremo su come leggere l'ora di creazione dei commenti con thread in un foglio di lavoro. Che tu sia uno sviluppatore esperto o alle prime armi, questa guida ti guiderà passo dopo passo nel processo.
## Prerequisiti
Prima di immergerci nel codice, assicuriamoci di avere tutto il necessario per iniziare:
1. Aspose.Cells per .NET: assicurati di avere installata la libreria Aspose.Cells. Puoi scaricarla da[Sito web di Aspose](https://releases.aspose.com/cells/net/).
2. Visual Studio: un'installazione funzionante di Visual Studio o di qualsiasi altro IDE .NET in cui è possibile scrivere ed eseguire il codice C#.
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
4.  File Excel: tieni pronto un file Excel con alcuni commenti in thread. Per questo esempio, useremo un file denominato`ThreadedCommentsSample.xlsx`.
Ora che abbiamo soddisfatto i prerequisiti, importiamo i pacchetti necessari.
## Importa pacchetti
Per iniziare con Aspose.Cells, devi importare i namespace richiesti. Ecco come fare:
### Importa lo spazio dei nomi Aspose.Cells
Apri il tuo progetto C# in Visual Studio e aggiungi la seguente direttiva using all'inizio del tuo file di codice:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Questo spazio dei nomi consente di accedere a tutte le classi e ai metodi forniti dalla libreria Aspose.Cells.
Ora che abbiamo impostato la scena, scomponiamo il processo di lettura dell'ora di creazione dei commenti inseriti in thread in passaggi gestibili.
## Passaggio 1: definire la directory di origine
Per prima cosa, devi specificare la directory in cui si trova il tuo file Excel. Questo è fondamentale perché il programma deve sapere dove cercare il file.
```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";
```
 Sostituire`"Your Document Directory"`con il percorso effettivo del tuo file Excel. Potrebbe essere qualcosa del tipo`"C:\\Documents\\"`.
## Passaggio 2: caricare la cartella di lavoro
Successivamente, caricherai la cartella di lavoro Excel che contiene i commenti thread. Ecco come fare:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
 Questa riga di codice crea un nuovo`Workbook` oggetto caricando il file Excel specificato. Se il file non viene trovato, verrà generata un'eccezione, quindi assicurati che il percorso sia corretto.
## Passaggio 3: accedi al foglio di lavoro
Una volta caricata la cartella di lavoro, il passo successivo è accedere al foglio di lavoro specifico che contiene i commenti. Nel nostro caso, accederemo al primo foglio di lavoro:
```csharp
// Accedi al primo foglio di lavoro
Worksheet worksheet = workbook.Worksheets[0];
```
Questa riga recupera il primo foglio di lavoro (indice 0) dalla cartella di lavoro. Se i tuoi commenti si trovano su un foglio di lavoro diverso, modifica l'indice di conseguenza.
## Passaggio 4: Ottieni commenti con thread
Ora è il momento di recuperare i commenti thread da una cella specifica. In questo esempio, otterremo i commenti dalla cella A1:
```csharp
// Ottieni commenti con thread
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
Questa riga recupera tutti i commenti threaded associati alla cella A1. Se non ci sono commenti, la raccolta sarà vuota.
## Passaggio 5: scorrere i commenti
Dopo aver recuperato i commenti suddivisi in thread, possiamo scorrerli e visualizzarne i dettagli, inclusa l'ora di creazione:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
 Questo ciclo attraversa ogni commento nel`threadedComments` raccolta e stampa il testo del commento, il nome dell'autore e l'ora in cui è stato creato il commento.
## Passaggio 6: messaggio di conferma
Infine, dopo aver eseguito la logica di lettura dei commenti, è sempre una buona idea fornire un messaggio di conferma. Questo aiuta nel debug e assicura che il codice sia stato eseguito correttamente:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## Conclusione
Congratulazioni! Hai imparato con successo come leggere l'ora di creazione dei commenti con thread in un foglio di lavoro Excel usando Aspose.Cells per .NET. Questa funzionalità può essere incredibilmente utile per tenere traccia del feedback e della collaborazione nei tuoi documenti Excel. Con solo poche righe di codice, puoi estrarre informazioni preziose che possono migliorare i tuoi processi di analisi dei dati e reporting.
## Domande frequenti
### Che cos'è Aspose.Cells per .NET?
Aspose.Cells per .NET è una potente libreria che consente agli sviluppatori di creare, manipolare e convertire file Excel nelle applicazioni .NET.
### Come posso scaricare Aspose.Cells per .NET?
 Puoi scaricarlo da[Sito web di Aspose](https://releases.aspose.com/cells/net/).
### È disponibile una prova gratuita?
 Sì, puoi provare Aspose.Cells gratuitamente visitando il[pagina di prova gratuita](https://releases.aspose.com/).
### Posso accedere ai commenti di altre celle?
Assolutamente! Puoi modificare il riferimento di cella in`GetThreadedComments` metodo per accedere ai commenti da qualsiasi cella.
### Dove posso ottenere supporto per Aspose.Cells?
 Per supporto, puoi visitare il[Forum di Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
