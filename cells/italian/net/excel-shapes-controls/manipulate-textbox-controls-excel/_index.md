---
title: Manipolare i controlli TextBox in Excel
linktitle: Manipolare i controlli TextBox in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come manipolare le caselle di testo in Excel utilizzando Aspose.Cells per .NET con questo tutorial passo dopo passo semplice da seguire.
weight: 15
url: /it/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Manipolare i controlli TextBox in Excel

## Introduzione
Se hai mai lavorato con Excel, probabilmente ti sei imbattuto in quelle piccole caselle di testo che ti consentono di aggiungere testo mobile a un foglio di calcolo. Ma cosa succede se hai bisogno di manipolare quelle caselle di testo a livello di programmazione? Ecco dove Aspose.Cells per .NET torna utile. Con esso, puoi accedere e modificare le caselle di testo con facilità, rendendolo perfetto per automatizzare le attività o personalizzare i report. In questo tutorial, ti guideremo attraverso il processo di manipolazione delle caselle di testo in Excel utilizzando Aspose.Cells per .NET.
## Prerequisiti
Prima di immergerci nel codice vero e proprio, assicuriamoci di aver impostato tutto correttamente:
1.  Aspose.Cells per .NET: devi scaricare la libreria Aspose.Cells per .NET. Puoi trovare il link per il download[Qui](https://releases.aspose.com/cells/net/).
2. Ambiente di sviluppo .NET: funzionerà qualsiasi IDE che supporti .NET, come Visual Studio.
3. Conoscenza di base di C#: questo tutorial presuppone che tu abbia familiarità con la sintassi di base di C# e con la struttura delle cartelle di lavoro di Excel.
4.  File Excel: un file Excel esistente con caselle di testo (lo useremo`book1.xls`in questo esempio).
5.  Licenza Aspose: se non stai utilizzando la versione di prova gratuita, dovrai[acquistare](https://purchase.aspose.com/buy) una licenza o ottenere una[temporaneo](https://purchase.aspose.com/temporary-license/).
Ora, entriamo nel vivo dei passaggi!
## Importa pacchetti
Prima di poter manipolare cartelle di lavoro e caselle di testo di Excel usando Aspose.Cells, devi importare i namespace necessari. Ecco il frammento di codice che userai in cima al tuo file C#:
```csharp
using System.IO;
using Aspose.Cells;
```
Questi pacchetti consentono di accedere alla manipolazione delle cartelle di lavoro, ai fogli di lavoro e al disegno di oggetti (come le caselle di testo).
Ora che abbiamo impostato tutto, scomponiamo il processo di manipolazione delle caselle di testo in semplici passaggi.
## Passaggio 1: imposta la directory della cartella di lavoro
 Il primo passo è specificare dove si trovano i file Excel sul tuo sistema. Dovrai sostituire il segnaposto`Your Document Directory` con il percorso effettivo del tuo file. Questo percorso è memorizzato nel`dataDir` variabile per un facile riferimento in tutto il codice.
```csharp
string dataDir = "Your Document Directory";
```
Ciò consente al programma di sapere dove trovare il file Excel di input (`book1.xls`) e dove salvare il file di output.
## Passaggio 2: aprire il file Excel
Successivamente, dovrai caricare il file Excel esistente nell'oggetto Aspose.Cells Workbook. Questa cartella di lavoro funge da contenitore per i tuoi dati Excel, dandoti accesso ai suoi fogli di lavoro e a qualsiasi oggetto di disegno (come le caselle di testo).
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 IL`Workbook` class from Aspose.Cells caricherà il file Excel specificato dalla tua directory. Se il file non esiste nella directory specificata, genererà un'eccezione, quindi assicurati che il percorso sia corretto.
## Passaggio 3: accedi al primo foglio di lavoro
Ora che hai caricato la cartella di lavoro, puoi accedere ai suoi fogli di lavoro. In questo esempio, stiamo accedendo al primo foglio di lavoro nella cartella di lavoro, che è memorizzato all'indice 0.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
 IL`Worksheets` proprietà ti dà accesso a tutti i fogli nella cartella di lavoro. Qui, siamo interessati solo al primo foglio, ma puoi lavorare con qualsiasi foglio specificando l'indice corretto.
## Passaggio 4: ottenere il primo oggetto TextBox
Le caselle di testo in un foglio Excel sono considerate oggetti di disegno. La classe Aspose.Cells.Drawing.TextBox fornisce proprietà e metodi per manipolarle. Per accedere alla prima casella di testo sul foglio di lavoro, basta fare riferimento a`TextBoxes` raccolta per indice.
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
 Questo recupera il primo oggetto casella di testo da`TextBoxes` collection. Se il tuo foglio di lavoro non ha una casella di testo a quell'indice, genererà un'eccezione, quindi assicurati sempre che l'indice sia valido.
## Passaggio 5: Recupera il testo dalla prima casella di testo
 Dopo aver effettuato l'accesso alla casella di testo, è possibile estrarre il testo in essa contenuto utilizzando`.Text` proprietà.
```csharp
string text0 = textbox0.Text;
```
 Questo catturerà il testo dalla prima casella di testo nella`text0` stringa. Ora puoi visualizzarla, manipolarla o elaborarla nella tua applicazione.
## Passaggio 6: accedere al secondo oggetto TextBox
Per manipolare più caselle di testo, possiamo recuperarne altre dal foglio di lavoro. Qui, accederemo alla seconda casella di testo in modo simile alla prima:
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
Ancora una volta, accediamo alla seconda casella di testo utilizzando l'indice 1 da`TextBoxes`collezione.
## Passaggio 7: Recupera il testo dalla seconda casella di testo
Proprio come con la prima casella di testo, puoi recuperare il testo dalla seconda casella di testo e memorizzarlo in una stringa:
```csharp
string text1 = textbox1.Text;
```
Verrà acquisito il testo corrente dalla seconda casella di testo.
## Passaggio 8: modifica il testo nella seconda casella di testo
 Ora, diciamo che vuoi modificare il testo all'interno della seconda casella di testo. Puoi farlo facilmente assegnando una nuova stringa alla`.Text` proprietà dell'oggetto casella di testo.
```csharp
textbox1.Text = "This is an alternative text";
```
Questo modifica il testo all'interno della seconda casella di testo nel nuovo contenuto. Puoi inserire qualsiasi testo qui in base alle tue esigenze.
## Passaggio 9: salvare il file Excel aggiornato
 Infine, dopo aver modificato le caselle di testo, è il momento di salvare le modifiche. Aspose.Cells consente di salvare la cartella di lavoro modificata utilizzando`.Save()` metodo. È possibile specificare un nuovo nome file o sovrascrivere il file esistente.
```csharp
workbook.Save(dataDir + "output.out.xls");
```
Questo salverà il file Excel modificato nel percorso di output designato. Ora, quando apri il file Excel, vedrai le modifiche apportate alle caselle di testo.
## Conclusione
Ed ecco fatto! Hai appena imparato a manipolare le caselle di testo in Excel usando Aspose.Cells per .NET. Che tu stia automatizzando la generazione di report, personalizzando fogli Excel o creando contenuti dinamici, Aspose.Cells semplifica il controllo di ogni aspetto dei tuoi file Excel a livello di programmazione. Dall'estrazione e modifica del testo al salvataggio dei file aggiornati, questa libreria è un potente strumento per gli sviluppatori che lavorano con Excel in ambienti .NET.
## Domande frequenti
### Posso manipolare altri oggetti di disegno con Aspose.Cells oltre alle caselle di testo?
Sì, Aspose.Cells consente di manipolare altri oggetti di disegno come forme, grafici e immagini.
### Cosa succede se provo ad accedere a una casella di testo che non esiste?
 Se l'indice della casella di testo è fuori intervallo, un`IndexOutOfRangeException` verrà lanciato.
### Posso aggiungere nuove caselle di testo a un foglio di lavoro Excel con Aspose.Cells?
 Sì, Aspose.Cells consente di aggiungere nuove caselle di testo utilizzando`AddTextBox` metodo.
### Ho bisogno di una licenza per utilizzare Aspose.Cells?
 Sì, dovrai acquistare una licenza, ma Aspose offre anche un[prova gratuita](https://releases.aspose.com/).
### Posso usare Aspose.Cells con altri linguaggi di programmazione oltre a C#?
Sì, Aspose.Cells può essere utilizzato con qualsiasi linguaggio supportato da .NET, come VB.NET.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
