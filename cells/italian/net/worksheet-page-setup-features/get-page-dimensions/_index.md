---
"description": "Scopri come ottenere le dimensioni di pagina in un foglio di lavoro Excel con Aspose.Cells per .NET. Una guida passo passo per personalizzare i formati carta A2, A3, A4 e Letter."
"linktitle": "Ottieni le dimensioni della pagina del foglio di lavoro"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Ottieni le dimensioni della pagina del foglio di lavoro"
"url": "/it/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ottieni le dimensioni della pagina del foglio di lavoro

## Introduzione
Se si lavora con file Excel a livello di codice utilizzando Aspose.Cells per .NET, potrebbe essere necessario accedere e impostare le dimensioni di pagina di un foglio di lavoro. Conoscere le dimensioni può essere utile per i layout, la stampa e la personalizzazione dei fogli Excel per scopi specifici. In questo articolo, esploreremo come recuperare e visualizzare diverse dimensioni di pagina in Excel utilizzando Aspose.Cells per .NET. Seguiremo un tutorial passo passo per assicurarci che tu abbia tutti i dettagli necessari per iniziare con sicurezza.
## Prerequisiti
Prima di iniziare, assicuriamoci di avere tutto il necessario per seguire questo tutorial.
1. Aspose.Cells per .NET: assicurati di aver installato Aspose.Cells per .NET. Puoi [scarica la libreria qui](https://releases.aspose.com/cells/net/) oppure installalo tramite NuGet nel tuo progetto .NET.
2. Ambiente .NET: un ambiente di sviluppo .NET compatibile (ad esempio, Visual Studio).
3. Impostazione della licenza: per la piena funzionalità di Aspose.Cells, applica una licenza. Puoi [richiedi una licenza temporanea gratuita](https://purchase.aspose.com/temporary-license/) fini di valutazione.
Se è la prima volta che lo valuti, inizia con la versione di prova gratuita di Aspose.Cells.
## Importa pacchetti
Prima di passare al codice, dovrai importare lo spazio dei nomi Aspose.Cells nel tuo progetto per accedere a tutte le classi e i metodi necessari.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Suddividiamo il processo in semplici passaggi. Qui, accederemo a diversi formati di carta, li applicheremo a un foglio di lavoro e stamperemo le dimensioni per ciascuno.
## Passaggio 1: creare un'istanza della cartella di lavoro
Il primo passo è creare un'istanza di `Workbook` classe. Questo oggetto fungerà da cartella di lavoro principale, contenente fogli di lavoro che potremo manipolare.
```csharp
Workbook book = new Workbook();
```
Pensa a `Workbook` Come contenitore principale per il tuo file Excel. Ci serve per accedere e controllare i singoli fogli di lavoro.
## Passaggio 2: accedi al primo foglio di lavoro
Ora accediamo al primo foglio di lavoro della cartella di lavoro. Per impostazione predefinita, una nuova cartella di lavoro include un foglio, quindi possiamo farvi riferimento direttamente utilizzando un indice di `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
IL `Worksheets` raccolta in `Workbook` ci permette di accedere a ciascun foglio di lavoro tramite indice. Qui, selezioniamo il primo foglio per iniziare a impostare le dimensioni della pagina.
## Passaggio 3: imposta il formato carta su A2 e visualizza le dimensioni
Ora che abbiamo accesso al nostro foglio di lavoro, impostiamo il formato carta su A2. Impostare il formato carta è utile per formattare la pagina prima di stamparla o esportarla. Una volta impostato il formato carta, stamperemo le dimensioni della pagina in pollici.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Qui, cambiamo il `PaperSize` proprietà a `PaperA2`Dopo aver impostato la dimensione, `PageSetup.PaperWidth` E `PageSetup.PaperHeight` Recupera la larghezza e l'altezza del foglio in pollici. Questo ci dà una rapida panoramica delle dimensioni della pagina.
## Passaggio 4: impostare il formato carta su A3 e le dimensioni di visualizzazione
Seguendo gli stessi passaggi di cui sopra, regoliamo le dimensioni della pagina al formato A3. Questa modifica è utile per stampe leggermente più grandi o per inserire più contenuti in una sola pagina.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Il formato A3 è il doppio dell'A4, il che lo rende un'ottima scelta per tabelle di grandi dimensioni o grafici dettagliati. Modificare il formato della carta aiuta ad adattare di conseguenza il layout del foglio di lavoro.
## Passaggio 5: impostare il formato carta su A4 e le dimensioni di visualizzazione
Ora impostiamo il formato carta su A4. Questo è il formato pagina più comunemente utilizzato per la stampa di documenti. Visualizzeremo le dimensioni aggiornate in seguito.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Se il tuo target è un formato di documento standard, l'A4 è in genere il formato più adatto. Conoscere le dimensioni può aiutarti a modificare l'impaginazione dei contenuti ed evitare problemi di stampa.
## Passaggio 6: impostare il formato della carta su Lettera e visualizzare le dimensioni
Infine, imposteremo il formato carta sul formato Letter, comunemente usato in Nord America. Stampiamo le dimensioni un'ultima volta.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Il formato Letter è ampiamente utilizzato per i documenti in Nord America, pertanto impostare questa dimensione è utile quando si collabora con team o clienti che hanno sede lì.
## Conclusione
In questo tutorial, abbiamo illustrato come impostare e recuperare le dimensioni di pagina per diversi formati di carta utilizzando Aspose.Cells per .NET. Configurando formati di pagina come A2, A3, A4 e Lettera, è possibile formattare i fogli di lavoro Excel in base a specifiche esigenze di stampa e layout. Questo controllo sulle dimensioni di pagina è particolarmente utile per la creazione di report e presentazioni professionali, poiché garantisce che i contenuti si adattino perfettamente a ogni formato di pagina.
## Domande frequenti
### Come posso cambiare l'orientamento della pagina in Aspose.Cells?  
È possibile modificare l'orientamento utilizzando `PageSetup.Orientation` proprietà, impostandola su `PageOrientationType.POtrait` or `PageOrientationType.Landscape`.
### Posso impostare dimensioni di pagina personalizzate in Aspose.Cells?  
Sì, puoi impostare dimensioni di pagina personalizzate regolando i margini e le opzioni di ridimensionamento in `PageSetup` per un maggiore controllo.
### Qual è il formato carta predefinito in Aspose.Cells?  
Il formato carta predefinito è in genere A4. Tuttavia, questo può dipendere dalle impostazioni locali e può essere modificato in base alle esigenze.
### È possibile visualizzare in anteprima i layout di pagina in Aspose.Cells?  
Sebbene Aspose.Cells non offra un'anteprima grafica, è possibile impostare layout a livello di programmazione e utilizzare anteprime di stampa in Excel.
### Come faccio a installare Aspose.Cells per .NET?  
È possibile installare Aspose.Cells utilizzando NuGet Package Manager in Visual Studio o scaricare la DLL da [Pagina di download di Aspose.Cells](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}