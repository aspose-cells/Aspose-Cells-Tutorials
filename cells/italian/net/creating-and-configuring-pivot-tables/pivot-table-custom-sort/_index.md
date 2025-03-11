---
title: Ordinamento personalizzato della tabella pivot a livello di programmazione in .NET
linktitle: Ordinamento personalizzato della tabella pivot a livello di programmazione in .NET
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come ordinare a livello di programmazione le tabelle pivot in .NET usando Aspose.Cells. Una guida passo passo che copre l'impostazione, la configurazione, l'ordinamento e il salvataggio dei risultati come file Excel e PDF.
weight: 29
url: /it/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ordinamento personalizzato della tabella pivot a livello di programmazione in .NET

## Introduzione
Quando si tratta di lavorare con Excel in un ambiente .NET, una libreria si distingue dalle altre: Aspose.Cells. Ora, non ami quando uno strumento ti consente di manipolare i fogli di calcolo a livello di programmazione? È esattamente ciò che fa Aspose.Cells! Nel tutorial di oggi, ci immergiamo nel mondo delle tabelle pivot e ti mostriamo come implementare l'ordinamento personalizzato a livello di programmazione utilizzando questa versatile libreria.
## Prerequisiti
Prima di rimboccarci le maniche e buttarci a capofitto nel codice, assicurati di aver messo a punto alcune cose:
1. Visual Studio: ti servirà una versione funzionante di Visual Studio. È il parco giochi dove avviene tutta la magia.
2. .NET Framework: la familiarità con la programmazione .NET è essenziale. Che tu sia un appassionato di .NET Core o .NET Framework, sei pronto per partire.
3.  Libreria Aspose.Cells: devi installare la libreria Aspose.Cells. Puoi ottenerla da[Link per scaricare](https://releases.aspose.com/cells/net/) e aggiungilo al tuo progetto.
4. Nozioni di base sulle tabelle pivot: anche se non è necessario essere esperti, una minima conoscenza del funzionamento delle tabelle pivot sarà utile nel corso di questo tutorial.
5.  File Excel di esempio: avere un file Excel di esempio denominato`SamplePivotSort.xlsx` pronto nella tua directory di lavoro per i test.
## Importa pacchetti
Una volta ordinati tutti i prerequisiti, il primo passo è importare i pacchetti necessari. Per farlo, includi le seguenti righe all'inizio del tuo codice:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Questo pacchetto fornisce tutte le funzionalità necessarie per manipolare i file Excel utilizzando Aspose.Cells.

Bene, passiamo alla parte divertente! Analizzeremo il processo di creazione di una tabella pivot e di applicazione dell'ordinamento personalizzato in passaggi gestibili.
## Passaggio 1: impostare la cartella di lavoro
Per dare il via alle cose, dobbiamo impostare il nostro workbook. Ecco come fare:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
 In questo passaggio, inizializziamo un nuovo`Workbook` istanza con il percorso al nostro file Excel. Questo funge da canvas dove la nostra tabella pivot prenderà vita.
## Passaggio 2: accedi al foglio di lavoro
Ora dobbiamo accedere al foglio di lavoro in cui aggiungeremo la nostra tabella pivot.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
 Qui, prendiamo il primo foglio di lavoro nella nostra cartella di lavoro e chiamiamo il`PivotTableCollection`Questa raccolta ci consente di gestire tutte le tabelle pivot su questo foglio di lavoro.
## Passaggio 3: crea la tua prima tabella pivot
Adesso è il momento di creare la nostra tabella pivot.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Aggiungiamo una nuova tabella pivot al nostro foglio di lavoro, specificando l'intervallo di dati e la sua posizione. "E3" indica dove vogliamo che inizi la nostra tabella pivot. Quindi facciamo riferimento a questa nuova tabella pivot usando il suo indice.
## Passaggio 4: configurare le impostazioni della tabella pivot
Configuriamo la nostra tabella pivot! Ciò significa controllare aspetti come i totali generali e le disposizioni dei campi.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Ci assicuriamo che i totali generali per righe e colonne non vengano visualizzati, il che può rendere i dati più puliti. Quindi aggiungiamo il primo campo all'area delle righe, abilitando l'ordinamento automatico e un ordinamento ascendente.
## Passaggio 5: aggiungere colonne e campi dati
Una volta impostate le righe, aggiungiamo la colonna e i campi dati.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
Aggiungiamo il secondo campo come colonna e lo formattiamo come data. Di nuovo, abilitiamo l'ordinamento automatico e l'ordine crescente per mantenere le cose organizzate. Infine, dobbiamo aggiungere il terzo campo alla nostra area dati:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Passaggio 6: Aggiorna e calcola la tabella pivot
Dopo aver aggiunto tutti i campi necessari, assicuriamoci che la nostra tabella pivot sia aggiornata e pronta.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Questi metodi aggiornano i dati e li ricalcolano, assicurando che tutto sia aggiornato e visualizzato correttamente nella nostra tabella pivot.
## Passaggio 7: ordinamento personalizzato in base ai valori dei campi riga
Aggiungiamo un tocco di originalità ordinando la tabella pivot in base a valori specifici, come "SeaFood".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Ripetiamo il processo creando un'altra Tabella Pivot e impostandola in modo simile alla prima. Ora possiamo personalizzarla ulteriormente:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Passaggio 8: Personalizzazione aggiuntiva dell'ordinamentoProviamo un altro metodo di ordinamento basato su una data specifica:
```csharp
// Aggiungere un'altra tabella pivot per ordinare in base a una data
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Ripeti le impostazioni di riga e colonna in modo simile ai passaggi precedenti
```
Basta ripetere lo stesso processo, creando una terza tabella pivot con criteri di ordinamento personalizzati in base alle tue esigenze.
## Fase 9: Salva il quaderno di lavoroÈ il momento di salvare tutto il duro lavoro che abbiamo svolto!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
 Qui, salvi la cartella di lavoro come file Excel e PDF.`PdfSaveOptions` consente una formattazione migliore, assicurando che ogni foglio venga visualizzato su una pagina separata quando viene convertito.
## Fase 10: conclusioneConcludi il tutto facendo sapere all'utente che è tutto a posto.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Conclusione
questo punto, hai imparato come sfruttare la potenza di Aspose.Cells per creare e personalizzare le tabelle pivot nelle tue applicazioni .NET. Dalla configurazione iniziale all'ordinamento personalizzato, ogni passaggio si combina per offrire un'esperienza fluida. Che tu debba presentare dati di vendita annuali o monitorare le statistiche di inventario, queste competenze ti saranno molto utili!
## Domande frequenti
### Cos'è una tabella pivot?
Una tabella pivot è uno strumento di elaborazione dati in Excel che consente di riepilogare e analizzare i dati, offrendo un modo flessibile per estrarre facilmente informazioni.
### Come faccio a installare Aspose.Cells?
 Puoi installarlo tramite NuGet in Visual Studio o scaricarlo direttamente da[Link per scaricare](https://releases.aspose.com/cells/net/).
### Esiste una versione di prova di Aspose.Cells?
 Sì! Puoi provarlo gratuitamente visitando il[Link di prova gratuito](https://releases.aspose.com/).
### Posso ordinare più campi in una tabella pivot?
Assolutamente! Puoi aggiungere e ordinare più campi in base alle tue esigenze.
### Dove posso trovare supporto per Aspose.Cells?
 La comunità è piuttosto attiva e puoi porre domande sul loro forum[Qui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
