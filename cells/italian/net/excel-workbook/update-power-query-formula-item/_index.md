---
"description": "Aggiorna facilmente gli elementi delle formule di Power Query in Excel utilizzando Aspose.Cells per .NET. Guida dettagliata per semplificare i processi di manipolazione dei dati."
"linktitle": "Aggiorna elemento formula Power Query"
"second_title": "Riferimento API Aspose.Cells per .NET"
"title": "Aggiorna elemento formula Power Query"
"url": "/it/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiorna elemento formula Power Query

## Introduzione

Se hai mai lavorato con Excel, sai quanto può essere potente, soprattutto quando inizi a immergerti nelle Power Query. Sono l'ingrediente segreto che ti permette di trasformare, pulire e analizzare i tuoi dati senza sforzo. Un modo ingegnoso per manipolare le formule di Power Query in Excel è tramite Aspose.Cells per .NET. Oggi ti guideremo passo dopo passo nell'aggiornamento degli elementi delle formule di Power Query. Quindi, prendi il tuo cappello da programmatore e iniziamo!

## Prerequisiti

Prima di immergerti nel codice, ci sono alcune cose che dovresti impostare:

1. Visual Studio: per scrivere ed eseguire il codice .NET avrai bisogno di un ambiente di sviluppo integrato (IDE). Visual Studio è la scelta ideale.
2. Libreria Aspose.Cells: assicurati di avere la libreria Aspose.Cells disponibile nel tuo progetto. Puoi scaricarla da [sito](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: anche se approfondiremo insieme questo argomento, avere una conoscenza di base di C# sarà sicuramente utile, soprattutto quando si esplorano classi e metodi diversi.
4. File Excel di esempio: avrai bisogno dei file Excel menzionati nel frammento di codice. Assicurati di avere:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: assicurati che il tuo progetto sia destinato a una versione compatibile di .NET Framework.

Ora che il nostro kit è pronto, possiamo passare alla parte divertente: scrivere il codice!

## Importa pacchetti

Per prima cosa, dovrai importare gli spazi dei nomi necessari. Ecco come fare:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Aggiungendo questi namespace, si comunica al compilatore che si intende utilizzare le classi e i metodi della libreria Aspose.Cells. Questo passaggio è fondamentale in quanto getta le basi per il codice che segue.

Analizziamo il frammento di codice che hai fornito. Questo tutorial ti guiderà passo passo, assicurandoti di capire cosa sta succedendo.

## Passaggio 1: impostare le directory di lavoro

In questa fase, definiremo dove si trovano i file sorgente e di output. Questo garantirà ad Aspose dove cercare i file Excel.

```csharp
// Directory di lavoro
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Passaggio 2: caricare la cartella di lavoro

Carichiamo ora il file Excel in cui risiede Power Query.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
IL `Workbook` La classe è il punto di ingresso nel file Excel. Passando il percorso del nostro file sorgente, creiamo un'istanza che ci permette di manipolarlo. Puoi immaginarlo come se stessi aprendo un libro: ti stai preparando a leggerne (o modificarne) il contenuto.

## Passaggio 3: accedere al Data Mashup

Successivamente, accederemo alle formule di Power Query memorizzate nel Data Mashup della cartella di lavoro.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
IL `DataMashup` La classe contiene tutte le formule di Power Query associate alla cartella di lavoro. È qui che faremo il grosso del lavoro, proprio come quando si apre una cassetta degli attrezzi per le riparazioni.

## Passaggio 4: scorrere le formule di Power Query

Ora arriva la parte in cui esaminiamo le formule di Power Query per trovare quella specifica che vogliamo aggiornare.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- Facciamo un giro attraverso ciascuno `PowerQueryFormula` In `mashupData`.
- All'interno di questo ciclo, ci immergiamo in ogni `PowerQueryFormulaItem`.
- Controlliamo se il nome dell'elemento corrisponde a "Source". In tal caso, aggiorniamo il suo valore per collegarlo al nostro nuovo file sorgente.

È un po' come trovare la pagina giusta in un manuale e poi apportare gli aggiornamenti necessari: è un processo semplice e meticoloso.

## Passaggio 5: salvare la cartella di lavoro aggiornata

Dopo aver effettuato gli aggiornamenti, è il momento di salvare le modifiche.

```csharp
// Salvare la cartella di lavoro di output.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
IL `Save` Il metodo scrive la cartella di lavoro aggiornata nella directory di output specificata. È come sigillare le modifiche in una nuova versione del manuale, pronta per essere utilizzata da altri!

## Conclusione

Congratulazioni! Hai aggiornato correttamente un elemento formula di Power Query utilizzando Aspose.Cells per .NET. Con questo metodo, puoi automatizzare la modifica delle formule di Power Query nei tuoi file Excel, risparmiando tempo e fatica.

## Domande frequenti

### Che cosa è Aspose.Cells?
Aspose.Cells è una potente libreria per manipolare file Excel nelle applicazioni .NET senza dover installare Microsoft Excel.

### Ho bisogno di Microsoft Excel per eseguire Aspose.Cells?
No, Aspose.Cells consente di creare e modificare file Excel a livello di programmazione, senza dover installare Excel sul server o sulla macchina di sviluppo.

### Con quali tipi di file Excel posso lavorare utilizzando Aspose.Cells?
È possibile lavorare con .xlsx, .xls, .xlsm e molti altri formati Excel utilizzando Aspose.Cells.

### Esiste una versione di prova disponibile per Aspose.Cells?
Sì, puoi scaricare una versione di prova gratuita da [Pagina di rilascio di Aspose Cells](https://releases.aspose.com/).

### Come posso ottenere supporto per Aspose.Cells?
Puoi accedere al supporto tramite [Forum di Aspose](https://forum.aspose.com/c/cells/9), dove puoi porre domande e trovare risposte dalla community e dal team Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}