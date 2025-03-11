---
title: Conversione da foglio di lavoro a immagine in .NET
linktitle: Conversione da foglio di lavoro a immagine in .NET
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come convertire i fogli di lavoro Excel in immagini in .NET usando Aspose.Cells con la nostra guida passo-passo. Semplifica la visualizzazione dei tuoi dati.
weight: 11
url: /it/net/image-and-chart-operations/worksheet-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversione da foglio di lavoro a immagine in .NET

## Introduzione
Quando si tratta di manipolare file Excel in .NET, Aspose.Cells si distingue come una libreria affidabile e robusta. Una delle attività frequenti che potresti incontrare è la conversione di un foglio di lavoro Excel in un'immagine. Che tu voglia visualizzare il foglio su una pagina Web, includerlo in un report o semplicemente condividere i dati visivamente, questa guida passo passo ti guiderà attraverso l'intero processo. Alla fine, sarai equipaggiato con tutto ciò di cui hai bisogno per convertire i fogli di lavoro in immagini senza problemi. Quindi tuffiamoci dentro!
## Prerequisiti
Prima di iniziare la conversione, è essenziale assicurarsi di aver impostato tutto correttamente. Ecco i prerequisiti di cui avrai bisogno:
1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. È l'IDE che ti aiuterà a eseguire senza problemi i tuoi progetti .NET.
2.  Aspose.Cells per la libreria .NET: è necessario acquisire questa libreria. È possibile[scaricalo qui](https://releases.aspose.com/cells/net/) o iniziare con un[prova gratuita](https://releases.aspose.com/).
3. Conoscenza di base di C#: la familiarità con la programmazione C# sarà utile, poiché i nostri esempi e le nostre spiegazioni saranno scritti in questo linguaggio.
4.  Un file Excel di esempio: per una dimostrazione, crea o scarica un file Excel. Salvalo come`MyTestBook1.xls` nella directory del tuo progetto.
5. Nozioni di base sui progetti .NET: sapere come creare un semplice progetto .NET renderà il tutto più semplice, ma non preoccuparti: ti guideremo attraverso i passaggi.
## Importa pacchetti
Il primo passo del nostro viaggio è importare i pacchetti Aspose.Cells necessari nel nostro progetto. Questo è essenziale perché ci consente di utilizzare tutte le funzionalità che Aspose.Cells offre.
## Passaggio 1: creare un nuovo progetto 
Per iniziare, crea un nuovo progetto .NET in Visual Studio:
- Aprire Visual Studio.
- Fare clic su "Crea un nuovo progetto".
- Seleziona "App console (.NET Framework)" o "App console (.NET Core)" a seconda delle tue preferenze.
- Assegna un nome al tuo progetto (ad esempio WorksheetToImage) e fai clic su "Crea".
## Passaggio 2: aggiungere il riferimento Aspose.Cells
Ora che abbiamo il nostro progetto, dobbiamo aggiungere Aspose.Cells:
- Fare clic con il pulsante destro del mouse sul progetto in Esplora soluzioni.
- Seleziona "Gestisci pacchetti NuGet".
- Cerca “Aspose.Cells” e installa la versione più recente.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```
Ora sei pronto per la parte di codifica!

Ora, analizziamo passo dopo passo il processo di conversione effettivo. Utilizzeremo un semplice programma C# che apre un file Excel, converte un foglio di lavoro in un'immagine e salva quell'immagine in una directory specificata.
## Fase 3: Impostazione dell'ambiente
Per prima cosa, configura il tuo ambiente definendo il percorso verso la directory dei tuoi documenti:
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```
 Qui definiamo una variabile chiamata`dataDir` che contiene il percorso alla directory in cui verranno archiviati i nostri file. Sostituisci`"Your Document Directory"` con il percorso effettivo sul tuo sistema (ad esempio, "C:\\I miei file\\").
## Passaggio 4: aprire la cartella di lavoro di Excel
 Successivamente, apriremo il file Excel utilizzando`Workbook` classe da Aspose.Cells:
```csharp
// Aprire un file modello Excel.
Workbook book = new Workbook(dataDir + "MyTestBook1.xls");
```
 In questo passaggio, creiamo un'istanza di`Workbook` class e passare il percorso al nostro file Excel. Questo ci consente di interagire con il contenuto del file a livello di programmazione.
## Passaggio 5: accesso al foglio di lavoro
Ora che abbiamo aperto la cartella di lavoro, accediamo al primo foglio di lavoro:
```csharp
// Ottieni il primo foglio di lavoro.
Worksheet sheet = book.Worksheets[0];
```
 Qui recuperiamo il primo foglio di lavoro (indice`0` dalla cartella di lavoro. Gli array Aspose.Cells sono indicizzati a zero, il che significa che il primo foglio è`0`.
## Passaggio 6: definire le opzioni di immagine o di stampa
 Prima di rendere l'immagine, dobbiamo specificare come vogliamo che appaia utilizzando`ImageOrPrintOptions`:
```csharp
// Definisci ImageOrPrintOptions
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
// Specificare il formato dell'immagine
imgOptions.ImageType = Drawing.ImageType.Jpeg;
// Verrebbe renderizzata solo una pagina per l'intero foglio
imgOptions.OnePagePerSheet = true;
```
 In questo passaggio, creiamo un'istanza di`ImageOrPrintOptions` . Specifichiamo che vogliamo salvare l'output come immagine JPEG e impostiamo`OnePagePerSheet` A`true` per garantire che l'intero foglio venga catturato in un'unica immagine.
## Fase 7: rendering del foglio di lavoro
Con le opzioni a disposizione, possiamo ora visualizzare il foglio di lavoro:
```csharp
// Esegue il rendering del foglio in base alle opzioni di immagine/stampa specificate
SheetRender sr = new SheetRender(sheet, imgOptions);
// Rendi l'immagine per il foglio
Bitmap bitmap = sr.ToImage(0);
```
 IL`SheetRender` la classe aiuta a rendere il foglio di lavoro in un'immagine bitmap. Chiamiamo`ToImage(0)` per trasformare la pagina zero (il nostro primo foglio) in un bitmap.
## Passaggio 8: salvataggio dell'immagine
Dopo il rendering, dobbiamo salvare l'immagine nella directory specificata:
```csharp
//Salvare il file immagine specificandone il formato.
bitmap.Save(dataDir + "SheetImage.out.jpg");
```
 Qui salviamo l'immagine bitmap che abbiamo generato. Questa riga scrive l'immagine nel`dataDir` posizione con il nome del file`SheetImage.out.jpg`.
## Fase 9: Notifica di completamento
Per assicurarci che il processo sia completo, aggiungiamo un semplice messaggio alla console:
```csharp
// Visualizza il risultato in modo che l'utente sappia che l'elaborazione è terminata.
System.Console.WriteLine("Conversion to Image(s) completed.");
```
Questa riga invia un messaggio di conferma alla console, informando l'utente che la conversione è riuscita.
## Conclusione
Ed ecco fatto! In pochi semplici passaggi, hai imparato a convertire un foglio di lavoro Excel in un'immagine usando Aspose.Cells per .NET. Questo processo non è solo rapido ma anche potente, consentendoti di creare rappresentazioni visive dei dati del tuo foglio di calcolo senza sforzo.
## Domande frequenti
### Che cos'è Aspose.Cells?
Aspose.Cells è una libreria .NET che consente agli sviluppatori di creare, manipolare, convertire ed elaborare file Excel a livello di programmazione.
### Posso usare Aspose.Cells gratuitamente?
 Sì, puoi iniziare a utilizzare Aspose.Cells scaricando una versione di prova gratuita dal loro[sito web](https://releases.aspose.com/).
### Quali formati di immagine supporta Aspose.Cells per l'esportazione?
Aspose.Cells supporta vari formati di immagine, tra cui JPEG, PNG, BMP e GIF.
### Dove posso trovare ulteriore supporto per Aspose.Cells?
 Puoi accedere al forum di supporto per Aspose.Cells[Qui](https://forum.aspose.com/c/cells/9).
### Come posso ottenere una licenza temporanea per Aspose.Cells?
 È possibile ottenere una licenza temporanea recandosi presso il loro[pagina della licenza temporanea](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
