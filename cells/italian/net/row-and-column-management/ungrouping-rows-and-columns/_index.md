---
title: Separare righe e colonne in Excel con Aspose.Cells
linktitle: Separare righe e colonne in Excel con Aspose.Cells
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come separare righe e colonne in Excel usando Aspose.Cells per .NET con questa guida completa. Semplifica la manipolazione dei dati Excel.
weight: 15
url: /it/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Separare righe e colonne in Excel con Aspose.Cells

## Introduzione
Quando si tratta di gestire file Excel, potresti trovarti in situazioni in cui hai bisogno di separare righe e colonne. Che tu stia pulendo un foglio di calcolo o riformattando i dati per una migliore presentazione, Aspose.Cells per .NET è uno strumento fantastico che semplifica il processo. In questo tutorial, ti guiderò attraverso i passaggi per separare righe e colonne in Excel utilizzando Aspose.Cells. Alla fine, avrai una solida comprensione di come lavorare con i file Excel a livello di programmazione.
## Prerequisiti
Prima di immergerci nel codice, assicuriamoci di aver impostato tutto. Ecco cosa ti servirà:
1.  Visual Studio: dovresti avere una versione funzionante di Visual Studio installata sul tuo computer. Se non ce l'hai ancora, puoi scaricarla da[Sito di Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells per .NET: dovrai scaricare la libreria Aspose.Cells. Puoi prenderla da[Pagina delle release di Aspose](https://releases.aspose.com/cells/net/) . Assicurati di avere le licenze necessarie, che possono essere acquistate o ottenute tramite un[licenza temporanea](https://purchase.aspose.com/temporary-license/).
3. Conoscenza di base di C#: una conoscenza di base della programmazione in C# ti aiuterà a seguire più facilmente il corso.
Una volta che tutto è pronto, possiamo passare alla parte divertente: il codice!
## Importa pacchetti
Per iniziare, devi importare i pacchetti necessari nel tuo progetto C#. Ecco come fare:
1. Apri il tuo progetto in Visual Studio.
2. Aggiungi un riferimento alla libreria Aspose.Cells. Puoi farlo cliccando con il tasto destro del mouse su References nel tuo progetto e selezionando Add Reference. Naviga fino alla posizione in cui hai salvato la DLL Aspose.Cells.
3. Nella parte superiore del file C#, aggiungi le seguenti direttive using:
```csharp
using System.IO;
using Aspose.Cells;
```
Ora che tutto è impostato, vediamo i passaggi per separare righe e colonne nel foglio Excel. 
## Passaggio 1: definire la directory dei documenti
Per prima cosa, devi specificare la directory in cui si trova il tuo file Excel. Puoi impostarla come segue:
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```
 Sostituire`"Your Document Directory"` con il percorso effettivo sul computer in cui è salvato il file Excel. 
## Passaggio 2: creare un flusso di file
Successivamente, devi creare un flusso di file per aprire il file Excel. Ecco come puoi farlo:
```csharp
// Creazione di un flusso di file contenente il file Excel da aprire
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Qui, stai aprendo il file denominato`book1.xls`Assicurati che questo file esista nella directory specificata, altrimenti riceverai un errore di file non trovato.
## Passaggio 3: creare un'istanza di un oggetto cartella di lavoro
Ora, carichiamo il file Excel in un oggetto Workbook. Questo ti consente di manipolare la cartella di lavoro a livello di programmazione:
```csharp
// Creazione di un'istanza di un oggetto Workbook
// Apertura del file Excel tramite il flusso di file
Workbook workbook = new Workbook(fstream);
```
Con questa riga di codice hai caricato correttamente il file Excel nella memoria e sei pronto per lavorarci.
## Passaggio 4: accedi al foglio di lavoro
Dopo aver ottenuto la cartella di lavoro, il passo successivo è accedere al foglio di lavoro specifico in cui si desidera separare righe e colonne. Ecco come fare:
```csharp
// Accesso al primo foglio di lavoro nel file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
In questo caso, stiamo accedendo al primo foglio di lavoro. Se i tuoi dati sono su un foglio diverso, puoi modificare l'indice di conseguenza.
## Passaggio 5: separare le righe
Ora arriva la parte emozionante! Separiamo le prime sei righe (dalla riga 0 alla riga 5). Usate il seguente codice:
```csharp
// Separazione delle prime sei righe (da 0 a 5)
worksheet.Cells.UngroupRows(0, 5);
```
Questo metodo rimuove qualsiasi raggruppamento applicato alle righe specificate. È così semplice!
## Passaggio 6: separare le colonne
Proprio come le righe, puoi anche separare le colonne. Ecco come separare le prime tre colonne (dalla colonna 0 alla colonna 2):
```csharp
// Separazione delle prime tre colonne (da 0 a 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Passaggio 7: salvare il file Excel modificato
 Una volta che hai separato le righe e le colonne, il passo successivo è salvare le modifiche in un file Excel. Puoi farlo usando`Save` metodo:
```csharp
// Salvataggio del file Excel modificato
workbook.Save(dataDir + "output.xls");
```
 In questo esempio, salviamo il file modificato come`output.xls`Puoi cambiare il nome del file come preferisci.
## Passaggio 8: chiudere il flusso di file
Infine, per liberare risorse, dovresti chiudere il flusso di file:
```csharp
// Chiusura del flusso di file per liberare tutte le risorse
fstream.Close();
```
Questa è una buona norma per garantire che l'applicazione non conservi gli handle dei file più a lungo del necessario.
## Conclusione
Ed ecco fatto! Hai imparato con successo come separare righe e colonne in un file Excel usando Aspose.Cells per .NET. Con solo poche righe di codice, puoi apportare modifiche significative ai tuoi file Excel a livello di programmazione. Che tu stia automatizzando report o preparando dati per l'analisi, padroneggiare queste tecniche può farti risparmiare un sacco di tempo.
## Domande frequenti
### Che cos'è Aspose.Cells?
Aspose.Cells è una potente libreria per lavorare con file Excel nelle applicazioni .NET, consentendo una facile manipolazione, conversione e creazione di fogli di calcolo.
### Posso separare righe e colonne in Excel utilizzando altre librerie?
Sì, sono disponibili altre librerie per la manipolazione di Excel in .NET, ma Aspose.Cells offre funzionalità estese e facilità d'uso.
### C'è un modo per annullare le modifiche dopo aver salvato?
Una volta salvato un file Excel, non è possibile ripristinare lo stato precedente a meno che non si disponga di un backup del file originale.
### Come posso ottenere supporto per Aspose.Cells?
 Puoi trovare supporto visitando il[Forum di supporto Aspose](https://forum.aspose.com/c/cells/9), dove puoi porre domande e trovare soluzioni.
### Posso usare Aspose.Cells senza licenza?
Sì, puoi utilizzare Aspose.Cells gratuitamente con alcune limitazioni e puoi iniziare con un[licenza temporanea](https://purchase.aspose.com/temporary-license/) per la piena funzionalità.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
