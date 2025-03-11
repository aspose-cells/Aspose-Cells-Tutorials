---
title: Ruotare il testo con la forma in Excel
linktitle: Ruotare il testo con la forma in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come ruotare il testo con le forme in Excel usando Aspose.Cells per .NET. Segui questa guida passo passo per una presentazione Excel perfetta.
weight: 12
url: /it/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ruotare il testo con la forma in Excel

## Introduzione
Nel mondo di Excel, la rappresentazione visiva è importante tanto quanto i dati stessi. Che tu stia creando un report o progettando una dashboard dinamica, il modo in cui le informazioni sono disposte può avere un impatto notevole sulla loro leggibilità e sul loro aspetto generale. Quindi, hai mai desiderato ruotare il testo per allinearlo con stile alle forme? Sei fortunato! In questo tutorial, approfondiremo come ruotare il testo con le forme usando Aspose.Cells per .NET, assicurandoti che i tuoi fogli di calcolo non solo informino, ma anche impressionino.
## Prerequisiti
Prima di iniziare, assicuriamoci di avere tutto ciò di cui hai bisogno:
1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer, poiché è lì che scriveremo il nostro codice.
2.  Aspose.Cells per .NET: avrai bisogno della libreria Aspose.Cells. Puoi[scarica l'ultima versione qui](https://releases.aspose.com/cells/net/) oppure provalo gratuitamente con un[prova gratuita](https://releases.aspose.com/).
3. Conoscenza di base di C#: la familiarità con C# e l'ambiente .NET sarà utile, anche se ti guideremo in ogni fase del percorso.
4.  File Excel: un file Excel di esempio, chiamiamolo`sampleRotateTextWithShapeInsideWorksheet.xlsx`, è necessario per testare il nostro codice. Dovresti mettere questo file in una directory a cui puoi accedere facilmente.
Tutto pronto? Fantastico! Passiamo alla parte divertente.
## Importa pacchetti
Per essere avviati, dobbiamo importare i pacchetti necessari nel nostro progetto. Ecco come fare:
### Crea un nuovo progetto
1. Aprire Visual Studio.
2. Seleziona "Crea un nuovo progetto".
3. Seleziona "App Console" e C# come linguaggio di programmazione preferito.
### Installa Aspose.Cells
Ora aggiungiamo Aspose.Cells al tuo progetto. Puoi farlo usando NuGet Package Manager:
1. Aprire "Strumenti" nel menu in alto.
2. Selezionare "Gestore pacchetti NuGet" e quindi "Gestisci pacchetti NuGet per la soluzione".
3. Cerca "Aspose.Cells."
4. Fai clic su "Installa" per aggiungerlo al tuo progetto.
### Aggiungi direttiva di utilizzo
Nella parte superiore del file C# principale, è necessario aggiungere la seguente direttiva:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Ora siamo pronti per iniziare a programmare!
Analizziamo il processo in passaggi facilmente digeribili. Ecco come ruotare il testo con le forme in un file Excel:
## Passaggio 1: imposta i percorsi delle directory
Per prima cosa, devi impostare le directory di origine e di output in cui verranno archiviati i tuoi file Excel. Ecco come fare:
```csharp
//Elenco di origine
string sourceDir = "Your Document Directory"; // Imposta la directory dei tuoi documenti
//Directory di output
string outputDir = "Your Document Directory"; // Imposta la directory di output
```
 Sostituire`"Your Document Directory"` con il percorso effettivo in cui ti trovi`sampleRotateTextWithShapeInsideWorksheet.xlsx` il file si trova.
## Passaggio 2: caricare il file Excel di esempio
Ora, carichiamo il file Excel di esempio. Questo è fondamentale, perché vogliamo manipolare i dati esistenti.
```csharp
//Carica il file Excel di esempio.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Passaggio 3: accedi al foglio di lavoro
Una volta caricato il file, dobbiamo accedere al foglio di lavoro specifico che vogliamo modificare. Nel nostro caso, è il primo foglio di lavoro.
```csharp
//Accedi al primo foglio di lavoro.
Worksheet ws = wb.Worksheets[0];
```
## Passaggio 4: modifica una cella
Successivamente, modificheremo una cella specifica per visualizzare un messaggio. Nel nostro esempio, useremo la cella B4.
```csharp
//Accedi alla cella B4 e aggiungi un messaggio al suo interno.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Questo passaggio riguarda principalmente la comunicazione: assicurarsi che chiunque apra questo foglio capisca cosa stiamo modificando.
## Passaggio 5: accedi alla prima forma
Per ruotare il testo, abbiamo bisogno di una forma con cui lavorare. Qui, accederemo alla prima forma nel foglio di lavoro.
```csharp
//Accedi prima alla forma.
Shape sh = ws.Shapes[0];
```
## Passaggio 6: regola l'allineamento del testo della forma
Ecco dove avviene la magia. Regoleremo le proprietà di allineamento del testo della forma.
```csharp
//Accedi all'allineamento del testo della forma.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Non ruotare il testo con forma impostando RotateTextWithShape su false.
shapeTextAlignment.RotateTextWithShape = false;
```
 Impostando`RotateTextWithShape` su falso, ci assicuriamo che il testo rimanga in posizione verticale e non ruoti con la forma, mantenendo così tutto ordinato e organizzato.
## Passaggio 7: salvare il file Excel di output
Infine, salviamo le nostre modifiche in un nuovo file Excel. Questo ci assicura di non perdere le nostre modifiche e di avere un output ordinato.
```csharp
//Salvare il file Excel di output.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Ed ecco fatto! Il tuo file di output è ora salvato, incluso il testo nella cella B4 e le modifiche apportate alla forma.
## Passaggio 8: eseguire il codice
 Nel tuo`Main` metodo, esegui il wrap di tutti i frammenti di codice sopra, ed esegui il tuo progetto. Guarda le modifiche riflettersi nel tuo file di output!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Conclusione
Ruotare il testo con le forme in Excel usando Aspose.Cells per .NET potrebbe sembrare un processo elaborato all'inizio, ma è piuttosto semplice una volta che lo si analizza. Seguendo questi semplici passaggi, è possibile personalizzare i fogli di calcolo per renderli più professionali e visivamente accattivanti. Ora, che lo si faccia per un cliente o per i propri progetti personali, tutti saranno entusiasti della qualità del proprio lavoro!
## Domande frequenti
### Posso usare Aspose.Cells gratuitamente?
 Sì! Puoi usare il[prova gratuita](https://releases.aspose.com/) per provare la biblioteca.
### Quali versioni di Excel sono supportate da Aspose.Cells?
Aspose.Cells supporta diversi formati Excel, tra cui XLS, XLSX, CSV e altri.
### È possibile ruotare il testo con forme nelle vecchie versioni di Excel?
Sì, la funzionalità può essere applicata ai formati più vecchi supportati da Aspose.Cells.
### Dove posso trovare ulteriore documentazione su Aspose.Cells?
 Puoi esplorare l'intero[documentazione](https://reference.aspose.com/cells/net/) per ulteriori approfondimenti.
### Come posso ottenere supporto per Aspose.Cells?
 Puoi chiedere supporto visitando il[Forum di Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
