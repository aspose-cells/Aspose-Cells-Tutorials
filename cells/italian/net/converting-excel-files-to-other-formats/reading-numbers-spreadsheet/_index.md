---
"description": "In questo tutorial dettagliato scoprirai come leggere i fogli di calcolo Numbers e convertirli in PDF utilizzando Aspose.Cells per .NET."
"linktitle": "Lettura di fogli di calcolo numerici in modo programmatico in .NET"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Lettura di fogli di calcolo numerici in modo programmatico in .NET"
"url": "/it/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lettura di fogli di calcolo numerici in modo programmatico in .NET

## Introduzione
Nel mondo digitale odierno, la gestione dei dati è una competenza fondamentale e i fogli di calcolo sono all'avanguardia nell'organizzazione dei dati. Ma cosa succede se devi lavorare con un foglio di calcolo Numbers, ovvero i file creati dall'app Numbers di Apple, utilizzando .NET? Non preoccuparti; non sei il solo! In questo tutorial, ti guideremo attraverso il processo di lettura di un foglio di calcolo Numbers a livello di codice con Aspose.Cells per .NET. Imparerai come caricare un file Numbers e convertirlo in PDF.
## Prerequisiti
Prima di iniziare, ecco alcune cose che devi sapere:
1. Aspose.Cells per .NET: assicurati di aver installato la libreria Aspose.Cells. Puoi scaricarla. [Qui](https://releases.aspose.com/cells/net/).
2. Visual Studio: si consiglia di installare Visual Studio (o qualsiasi altro IDE compatibile con .NET) sul computer.
3. Conoscenza di base di C#: una minima familiarità con la programmazione C# ti aiuterà a seguire il tutorial senza problemi.
4. Directory dei documenti: avrai bisogno di una directory in cui archiviare il file Numbers, insieme a una posizione in cui salvare il PDF convertito.
Una volta soddisfatti questi prerequisiti, sei pronto per iniziare!
## Importa pacchetti
Per iniziare, dobbiamo importare i pacchetti necessari nel nostro progetto C#. Questo è un passaggio cruciale perché ci permette di sfruttare le funzionalità fornite dalla libreria Aspose.Cells.
1. Apri il tuo progetto C# in Visual Studio.
2. Aggiungere un riferimento alla libreria Aspose.Cells:
   - Se utilizzi NuGet, esegui semplicemente il seguente comando nella console di Package Manager:
```
 Install-Package Aspose.Cells
 ```
3. Importa gli spazi dei nomi necessari nel tuo codice:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Ora che abbiamo importato i pacchetti necessari, passiamo alla guida dettagliata per la lettura di un foglio di calcolo Numbers.
## Passaggio 1: specificare le directory di origine e di output
In questo passaggio imposteremo le directory in cui si trova il file Numbers sorgente e in cui desideri salvare il PDF di output.
```csharp
// Directory di origine
string sourceDir = "Your Document Directory"; // Aggiornalo alla tua directory effettiva
// Directory di output
string outputDir = "Your Document Directory"; // Aggiornalo alla tua directory effettiva
```
Qui stiamo definendo due variabili stringa, `sourceDir` E `outputDir`, per specificare le posizioni dei file di input e output. Assicurati di sostituire `"Your Document Directory"` con i percorsi effettivi del tuo sistema.
## Passaggio 2: impostare le opzioni di caricamento per il formato Numbers
Successivamente, specificheremo le opzioni di caricamento per la lettura di un foglio di calcolo Numbers. Questo passaggio è essenziale perché indica ad Aspose come interpretare il file Numbers.
```csharp
// Specificare le opzioni di caricamento; vogliamo caricare il foglio di calcolo Numbers
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
Creiamo un `LoadOptions` oggetto e specificare il formato come `LoadFormat.Numbers`Questo indica alla libreria Aspose.Cells che stiamo lavorando con un file Numbers. 
## Passaggio 3: caricare il foglio di calcolo Numbers in una cartella di lavoro
Ora è il momento di caricare il foglio di calcolo Numbers effettivo in un `Workbook` oggetto.
```csharp
// Carica il foglio di calcolo Numbers nella cartella di lavoro con le opzioni di caricamento sopra indicate
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
Istanziamo un `Workbook` object e passa il percorso del file Numbers insieme alle nostre opzioni di caricamento. Assicurati che il nome del file (`sampleNumbersByAppleInc.numbers`) corrisponde al nome effettivo del file Numbers.
## Passaggio 4: salvare la cartella di lavoro in formato PDF
Una volta caricato correttamente il file Numbers, il passo successivo è salvarlo in un formato diverso, nello specifico PDF.
```csharp
// Salva la cartella di lavoro in formato PDF
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
Qui chiamiamo il `Save` metodo sul `Workbook` oggetto, specificando il percorso del file di output e il formato in cui vogliamo salvarlo. In questo caso, lo salviamo come PDF. Assicurati che il nome del file di output (`outputNumbersByAppleInc.pdf`) è univoco e non sovrascrive alcun file esistente.
## Passaggio 5: conferma il successo
Infine, aggiungiamo un messaggio per confermare che l'operazione è andata a buon fine.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Questa riga di codice mostrerà un messaggio di successo sulla console una volta completato tutto. È sempre bello ricevere feedback, vero?
## Conclusione
Ed ecco fatto! Hai letto con successo un foglio di calcolo Numbers e lo hai convertito in PDF utilizzando Aspose.Cells per .NET. Questa potente libreria ti permette di manipolare i fogli di calcolo senza sforzo, semplificando le tue attività di gestione dei dati. Che tu stia sviluppando applicazioni o semplicemente abbia bisogno di gestire i fogli di calcolo in modo più efficiente, Aspose.Cells è uno strumento fantastico da avere nel tuo kit di strumenti.
## Domande frequenti
### Quali tipi di file può leggere Aspose.Cells?  
Aspose.Cells può leggere vari formati di file, tra cui XLS, XLSX, CSV e Numbers. 
### Posso modificare i file Numbers utilizzando Aspose.Cells?  
Sì, puoi leggere, manipolare e salvare i file Numbers con Aspose.Cells.
### Aspose.Cells è gratuito?  
Aspose.Cells offre una prova gratuita, ma per un utilizzo prolungato è necessaria una licenza. Verifica i prezzi. [Qui](https://purchase.aspose.com/buy).
### Cosa devo fare se riscontro un errore durante il caricamento di un file Numbers?  
Assicurati di utilizzare le opzioni di caricamento corrette e che il percorso del file sia corretto. Per ulteriore supporto, visita [Forum di supporto Aspose](https://forum.aspose.com/c/cells/9).
### Come posso ottenere una licenza temporanea per Aspose.Cells?  
Puoi richiedere una licenza temporanea [Qui](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}