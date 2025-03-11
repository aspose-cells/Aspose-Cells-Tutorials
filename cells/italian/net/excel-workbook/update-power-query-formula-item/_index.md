---
title: Aggiorna elemento formula Power Query
linktitle: Aggiorna elemento formula Power Query
second_title: Riferimento API Aspose.Cells per .NET
description: Aggiorna facilmente gli elementi della formula di Power Query in Excel utilizzando Aspose.Cells per .NET. Guida dettagliata per semplificare i processi di manipolazione dei dati.
weight: 160
url: /it/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiorna elemento formula Power Query

## Introduzione

Se hai mai lavorato con Excel, sai quanto può essere potente, soprattutto quando inizi a immergerti nelle Power Query. Sono l'ingrediente segreto che ti consente di trasformare, pulire e analizzare i tuoi dati senza sforzo. Un modo ingegnoso per manipolare le tue formule di Power Query in Excel è tramite Aspose.Cells per .NET. Oggi ti guideremo passo dopo passo nell'aggiornamento degli elementi della formula di Power Query. Quindi, prendi il tuo cappello da programmatore e iniziamo!

## Prerequisiti

Prima di immergerti nel codice, ci sono alcune cose che dovresti impostare:

1. Visual Studio: avrai bisogno di un ambiente di sviluppo integrato (IDE) per scrivere ed eseguire il tuo codice .NET. Visual Studio è la scelta giusta.
2.  Libreria Aspose.Cells: assicurati di avere la libreria Aspose.Cells disponibile nel tuo progetto. Puoi scaricarla da[sito](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: anche se affronteremo insieme questo argomento, avere una conoscenza di base di C# sarà sicuramente utile, soprattutto quando si esplorano classi e metodi diversi.
4. File Excel di esempio: ti serviranno i file Excel menzionati nel frammento di codice. Assicurati di avere:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: assicurati che il tuo progetto sia destinato a una versione compatibile di .NET Framework.

Ora che il nostro kit è pronto, possiamo passare alla parte divertente: scrivere il codice!

## Importa pacchetti

Per prima cosa, vorrai importare i namespace necessari. Ecco come fare:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Aggiungendo questi namespace, fai sapere al compilatore che intendi usare le classi e i metodi della libreria Aspose.Cells. Questo passaggio è cruciale perché getta le basi per il codice che segue.

Analizziamo il frammento di codice che hai fornito. Questo tutorial ti guiderà attraverso ogni parte, assicurandoti di capire cosa sta succedendo.

## Passaggio 1: impostare le directory di lavoro

In questo passaggio, definiremo dove si trovano i nostri file di origine e di output. Questo assicura che Aspose sappia dove cercare i tuoi file Excel.

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
 IL`Workbook` class è il tuo punto di ingresso nel file Excel. Passando il percorso del nostro file sorgente, stiamo creando un'istanza che ci consente di manipolarlo. Puoi immaginarlo come l'apertura di un libro: ti stai preparando a leggerne (o modificarne) il contenuto.

## Passaggio 3: accedere al Data Mashup

Successivamente, accederemo alle formule di Power Query memorizzate nel Data Mashup della cartella di lavoro.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 IL`DataMashup` classe contiene tutte le formule di Power Query associate alla tua cartella di lavoro. È qui che faremo il nostro lavoro pesante, proprio come quando apri una cassetta degli attrezzi per le riparazioni.

## Passaggio 4: scorrere le formule di Power Query

Ora arriva la parte in cui scorriamo le formule di Power Query per trovare quella specifica che vogliamo aggiornare.

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

-  Facciamo un giro attraverso ciascuno`PowerQueryFormula` In`mashupData`.
- All'interno di quel ciclo, ci immergiamo in ogni`PowerQueryFormulaItem`.
- Controlliamo se il nome dell'elemento corrisponde a "Source". In caso affermativo, aggiorniamo il suo valore per collegarlo al nostro nuovo file sorgente.

È un po' come trovare la pagina giusta in un manuale e poi apportare gli aggiornamenti necessari: è un processo semplice e meticoloso.

## Passaggio 5: salvare la cartella di lavoro aggiornata

Dopo aver effettuato gli aggiornamenti, è il momento di salvare le modifiche.

```csharp
// Salvare la cartella di lavoro di output.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 IL`Save` scrive la cartella di lavoro aggiornata nella directory di output specificata. È come sigillare le tue modifiche in una nuova versione del manuale, pronta per essere utilizzata da altri!

## Conclusione

Congratulazioni! Hai aggiornato con successo un elemento formula di Power Query usando Aspose.Cells per .NET. Con questo metodo, puoi automatizzare la modifica delle formule di Power Query nei tuoi file Excel, risparmiando tempo e fatica preziosi.

## Domande frequenti

### Che cos'è Aspose.Cells?
Aspose.Cells è una potente libreria per manipolare file Excel nelle applicazioni .NET senza dover installare Microsoft Excel.

### Ho bisogno di Microsoft Excel per eseguire Aspose.Cells?
No, Aspose.Cells consente di creare e modificare file Excel a livello di programmazione, senza dover installare Excel sul server o sulla macchina di sviluppo.

### Con quali tipi di file Excel posso lavorare con Aspose.Cells?
È possibile lavorare con .xlsx, .xls, .xlsm e molti altri formati Excel utilizzando Aspose.Cells.

### Esiste una versione di prova disponibile per Aspose.Cells?
 Sì, puoi scaricare una versione di prova gratuita da[Pagina di rilascio di Aspose Cells](https://releases.aspose.com/).

### Come posso ottenere supporto per Aspose.Cells?
 Puoi accedere al supporto tramite[Forum di Aspose](https://forum.aspose.com/c/cells/9), dove puoi porre domande e trovare risposte dalla community e dal team di Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
