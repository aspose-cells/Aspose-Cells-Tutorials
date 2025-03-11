---
title: Modificare i dati di origine della tabella pivot a livello di programmazione in .NET
linktitle: Modificare i dati di origine della tabella pivot a livello di programmazione in .NET
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come modificare a livello di programmazione i dati sorgente della tabella pivot utilizzando Aspose.Cells per .NET con il nostro tutorial completo passo dopo passo.
weight: 10
url: /it/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modificare i dati di origine della tabella pivot a livello di programmazione in .NET

## Introduzione
Nel mondo dell'analisi dei dati, pochi strumenti brillano quanto Microsoft Excel. Ogni giorno, innumerevoli utenti dipendono da Excel per gestire e analizzare i dati, ma dietro le quinte, è molto più complesso del semplice clic e trascinamento. Se hai mai desiderato manipolare programmaticamente i file Excel, in particolare per modificare i dati di origine di una tabella pivot, sei nel posto giusto! In questa guida, esploreremo come puoi ottenere questo risultato utilizzando Aspose.Cells per .NET. Che tu sia uno sviluppatore esperto o che tu stia semplicemente immergendo i piedi nel mare della programmazione, troverai questo tutorial pieno di informazioni preziose e facili da seguire.
## Prerequisiti
Prima di iniziare il nostro percorso di modifica dei dati sorgente di una tabella pivot, assicuriamoci di aver impostato tutto e di essere pronti all'uso:
1. Visual Studio: assicurati di avere installata una copia di Microsoft Visual Studio, poiché scriveremo il nostro codice qui.
2. Libreria Aspose.Cells: dovrai scaricare e referenziare la libreria Aspose.Cells nel tuo progetto. Puoi scaricarla[Qui](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: sebbene questo tutorial sia semplificato, avere una conoscenza di C# ti aiuterà a comprendere meglio il codice.
4. File Excel: dovresti avere un file Excel di esempio (ad esempio "Book1.xlsx") contenente una tabella pivot che possiamo manipolare.
Bene, una volta soddisfatti questi prerequisiti, possiamo procedere all'importazione dei pacchetti necessari e iniziare a scrivere il codice!
## Importa pacchetti
Prima di tutto, importiamo i pacchetti di cui avremo bisogno. Apri il tuo progetto C# in Visual Studio e aggiungi le seguenti direttive using all'inizio del tuo file di codice:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Questi namespace ti daranno accesso alle classi essenziali necessarie per lavorare con i file Excel e manipolarne il contenuto utilizzando Aspose.Cells.

Ora, scomponiamo il processo in passaggi gestibili. Passeremo in rassegna l'apertura di un file Excel, la modifica del foglio di lavoro, la modifica della fonte dati della tabella pivot e il salvataggio dei risultati.
## Passaggio 1: definire la directory dei documenti
 Per prima cosa, devi specificare dove si trova il tuo file Excel. Modifica il`dataDir` variabile per puntare alla cartella contenente il file "Book1.xlsx".
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```
Questa riga imposta la directory in cui verrà archiviato il file Excel, rendendolo più semplice da utilizzare in seguito.
## Passaggio 2: specificare il percorso di input
Ora creiamo una stringa per specificare il percorso completo del file Excel di input:
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
Ciò semplifica l'accesso ai file: non sarà più necessario digitare lo stesso percorso più volte nel codice.
## Passaggio 3: creare un flusso di file
 Ora è il momento di aprire il file Excel. Creeremo un`FileStream` che consente di leggere il contenuto del file Excel:
```csharp
// Creazione di un flusso di file contenente il file Excel da aprire
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
Questa riga apre il file in modalità lettura, consentendoci di accedere ai suoi dati.
## Passaggio 4: caricare la cartella di lavoro
Una volta impostato il flusso di file, il passaggio successivo consiste nel caricare la cartella di lavoro:
```csharp
// Apertura del file Excel tramite il flusso di file
Workbook workbook = new Workbook(fstream);
```
 Questo comando prende il tuo file Excel e lo carica in un`Workbook` oggetto. Una volta caricato, puoi manipolare il file come preferisci.
## Passaggio 5: accedi al foglio di lavoro
È il momento di entrare nei dettagli. Accederemo al primo foglio di lavoro nella cartella di lavoro:
```csharp
// Accesso al primo foglio di lavoro nel file Excel
Worksheet worksheet = workbook.Worksheets[0];
```
In questo modo è possibile accedere direttamente ai dati presenti nel primo foglio di lavoro, semplificandone la modifica.
## Passaggio 6: popolare nuovi dati
Ora vogliamo inserire nuovi dati nelle celle. In questo esempio aggiungeremo alcuni dati campione:
```csharp
// Inserimento di nuovi dati nelle celle del foglio di lavoro
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
 Qui inseriamo i valori "Golf", "Qtr4" e`7000` in celle specifiche. Puoi modificare questi valori in base alle tue esigenze.
## Passaggio 7: modificare l'intervallo denominato
Ora, cambieremo l'intervallo denominato a cui fa riferimento la tabella pivot. Ciò comporta la creazione o l'aggiornamento di un intervallo:
```csharp
// Modifica dell'intervallo denominato "DataSource"
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
Definendo un nuovo intervallo, ci assicuriamo che la tabella pivot utilizzi questi nuovi dati quando viene aggiornata.
## Passaggio 8: salvare il file Excel modificato
Dopo tutte le modifiche, è fondamentale salvare il lavoro! Salviamo la cartella di lavoro modificata:
```csharp
// Salvataggio del file Excel modificato
workbook.Save(dataDir + "output.xls");
```
Questo comando salva la cartella di lavoro in un nuovo file, così non sovrascriverai il file originale, a meno che tu non lo voglia!
## Passaggio 9: chiudere il flusso di file
Infine, è essenziale chiudere il flusso di file per liberare tutte le risorse che stai utilizzando:
```csharp
// Chiusura del flusso di file per liberare tutte le risorse
fstream.Close();
```
Questo passaggio garantisce che l'applicazione non perda memoria e rimanga efficiente.
## Conclusione
Congratulazioni! Hai appena modificato con successo i dati sorgente di una tabella pivot a livello di programmazione in .NET utilizzando Aspose.Cells. Questa funzionalità apre molte possibilità per automatizzare le attività di Excel e migliorare il flusso di lavoro. Che tu stia aggiornando report finanziari, monitorando i dati di vendita o anche solo giocando con i set di dati, avere la possibilità di farlo a livello di programmazione può farti risparmiare un sacco di tempo e ridurre il rischio di errori.

## Domande frequenti
### Che cos'è Aspose.Cells?
Aspose.Cells è una potente libreria .NET per lavorare con i file Excel, che consente agli utenti di creare, modificare e manipolare documenti Excel a livello di programmazione.
### Posso modificare i dati sorgente delle tabelle pivot esistenti utilizzando questo metodo?
Assolutamente! Questo metodo consente di aggiornare l'origine dati per le tabelle pivot esistenti nella cartella di lavoro di Excel.
### Per utilizzare Aspose.Cells è necessario che Office sia installato?
No! Aspose.Cells è una libreria autonoma, il che significa che non è necessario che Microsoft Office sia installato per lavorare con i file Excel.
### Aspose.Cells è gratuito?
Aspose.Cells offre una versione di prova gratuita, ma per la piena funzionalità, dovrai acquistare una licenza. Puoi trovare i dettagli[Qui](https://purchase.aspose.com/buy).
### Dove posso trovare altri esempi e supporto?
 Per ulteriori esempi e supporto, consulta il[Documentazione di Aspose.Cells](https://reference.aspose.com/cells/net/) e il loro forum comunitario[Qui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
