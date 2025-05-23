---
"description": "Scopri come convertire senza sforzo le cartelle di lavoro di Excel in formato CSV con Aspose.Cells in questo tutorial completo e dettagliato, pensato per gli sviluppatori .NET."
"linktitle": "Salva cartella di lavoro in formato CSV di testo"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Salva cartella di lavoro in formato CSV di testo"
"url": "/it/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Salva cartella di lavoro in formato CSV di testo

## Introduzione
Quando si gestiscono i dati, il formato scelto può davvero determinare la facilità di utilizzo. Tra i formati più comuni per la gestione dei dati tabellari c'è il CSV (Comma-Separated Values). Se sei uno sviluppatore che lavora con file Excel e devi convertire le cartelle di lavoro in formato CSV, Aspose.Cells per .NET è una libreria fantastica che semplifica questo compito. In questo tutorial, analizzeremo i passaggi per convertire una cartella di lavoro Excel in un formato CSV di testo senza problemi.
## Prerequisiti
Prima di iniziare, assicuriamoci che tutto sia pronto per iniziare:
1. Conoscenza di base di C# e .NET: poiché scriveremo codice in C#, è essenziale avere familiarità con il linguaggio e con il framework .NET.
2. Libreria Aspose.Cells: assicurati di aver installato la libreria Aspose.Cells per .NET nel tuo ambiente di sviluppo. Puoi scaricarla. [Qui](https://releases.aspose.com/cells/net/).
3. Visual Studio o qualsiasi IDE C#: avrai bisogno di un ambiente di sviluppo integrato (IDE) per scrivere ed eseguire il codice. Visual Studio è una scelta diffusa.
4. Cartella di lavoro Excel: preparare una cartella di lavoro Excel di esempio (ad esempio, "book1.xls") contenente alcuni dati per testare la conversione.
## Importa pacchetti
Ora che abbiamo chiarito i prerequisiti, il primo passo del processo è importare i pacchetti necessari. Nel tuo progetto C#, devi includere il seguente namespace all'inizio del file di codice:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Questi namespace ti daranno accesso alle classi e ai metodi necessari per lavorare con i file Excel e gestire i flussi di memoria.
## Passaggio 1: definire il percorso per la directory dei documenti
Il primo passo del nostro processo è definire dove sono archiviati i nostri documenti (cartelle di lavoro Excel). Questo è essenziale perché permette al nostro programma di sapere dove trovare i file da elaborare. 
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```
Assicurati di sostituire `"Your Document Directory"` Con il percorso effettivo in cui si trova il file "book1.xls". Potrebbe essere una directory sul computer o un percorso verso un server.
## Passaggio 2: carica la cartella di lavoro di origine
Ora dobbiamo caricare la cartella di lavoro di Excel che verrà convertita in formato CSV.
```csharp
// Carica la cartella di lavoro di origine
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
IL `Workbook` La classe della libreria Aspose.Cells consente la manipolazione e l'accesso alle cartelle di lavoro di Excel. Passando il percorso del file, carichiamo la cartella di lavoro specificata per l'elaborazione.
## Passaggio 3: inizializzare un array di byte per i dati della cartella di lavoro
Prima di iniziare a convertire la cartella di lavoro in CSV, dobbiamo inizializzare un array di byte vuoto che conterrà tutti i dati del foglio di lavoro.
```csharp
// matrice di 0 byte
byte[] workbookData = new byte[0];
```
Questo array di byte combinerà i dati di ciascun foglio di lavoro in un'unica struttura che potremo scrivere in un file in un secondo momento.
## Passaggio 4: imposta le opzioni di salvataggio del testo
Ora impostiamo le opzioni per salvare il formato del testo. Puoi scegliere delimitatori personalizzati o usare le tabulazioni.
```csharp
// Opzioni di salvataggio del testo. Puoi usare qualsiasi tipo di separatore.
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Impostazione della tabulazione come separatore
```
In questo esempio, usiamo un carattere di tabulazione come separatore. Puoi sostituirlo `'\t'` con qualsiasi carattere desideri, come una virgola (`,`), a seconda di come desideri formattare il tuo CSV.
## Passaggio 5: scorrere ogni foglio di lavoro
Successivamente, scorreremo tutti i fogli di lavoro all'interno della cartella di lavoro, salvandone ciascuno nel nostro `workbookData` array, ma prima devi selezionare su quale foglio di lavoro lavorare.
```csharp
// Copiare ogni dato del foglio di lavoro in formato testo all'interno dell'array di dati della cartella di lavoro
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Salva il foglio di lavoro attivo in formato testo
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
Il ciclo si estende su ogni foglio di lavoro della cartella di lavoro. `ActiveSheetIndex` è impostato in modo che ogni volta che si esegue il ciclo, si salvi il foglio di lavoro corrente. I risultati verranno salvati in memoria utilizzando un `MemoryStream`.
## Passaggio 6: recuperare i dati del foglio di lavoro
Dopo aver salvato un foglio di lavoro nel flusso di memoria, il passo successivo è recuperare questi dati e aggiungerli al nostro `workbookData` vettore.
```csharp
    // Salva i dati del foglio di lavoro nella matrice dei dati del foglio
    ms.Position = 0; // Reimposta la posizione del flusso di memoria
    byte[] sheetData = ms.ToArray(); // Ottieni l'array di byte
```
`ms.Position = 0;` reimposta la posizione per la lettura dopo la scrittura. Quindi, usiamo `ToArray()` per convertire il flusso di memoria in un array di byte contenente i dati del foglio di lavoro.
## Passaggio 7: combinare i dati del foglio di lavoro
Ora combineremo i dati di ogni foglio di lavoro in un unico `workbookData` array inizializzato in precedenza.
```csharp
    // Combina i dati di questo foglio di lavoro nella matrice dei dati della cartella di lavoro
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Creiamo un nuovo array sufficientemente grande da contenere sia i dati esistenti della cartella di lavoro che quelli del nuovo foglio di lavoro. Quindi copiamo i dati esistenti e quelli nuovi in questo array combinato per un utilizzo successivo.
## Passaggio 8: salvare tutti i dati della cartella di lavoro nel file
Infine, con tutti i dati combinati nel nostro `workbookData` array, possiamo salvare questo array in un percorso di file specificato.
```csharp
// Salva tutti i dati della cartella di lavoro in un file
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` prende l'array di byte combinato e lo scrive in un file di testo denominato "out.txt" nella directory specificata.
## Conclusione
Ed ecco fatto! Hai convertito con successo una cartella di lavoro Excel in formato CSV utilizzando Aspose.Cells per .NET. Questo processo non solo è efficiente, ma consente anche di manipolare facilmente i dati Excel per ulteriori analisi o report. Ora puoi automatizzare le tue attività di elaborazione dati o persino integrare questa funzionalità in applicazioni più grandi.
## Domande frequenti
### Posso usare delimitatori diversi per il file CSV?
Sì, puoi cambiare il `opts.Separator` a qualsiasi carattere desiderato, ad esempio virgole o barre verticali.
### Aspose.Cells è gratuito?
Aspose.Cells non è gratuito, ma puoi ottenere una prova gratuita [Qui](https://releases.aspose.com/).
### In quali altri formati posso salvare oltre al CSV?
Aspose.Cells consente di salvare in diversi formati, tra cui XLSX, PDF e altri.
### Posso elaborare file Excel di grandi dimensioni utilizzando Aspose.Cells?
Sì, Aspose.Cells è progettato per gestire in modo efficiente file di grandi dimensioni, ma le prestazioni potrebbero dipendere dalle risorse di sistema.
### Dove posso trovare una documentazione più dettagliata?
Puoi trovare documentazione completa ed esempi sul loro [sito di riferimento](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}