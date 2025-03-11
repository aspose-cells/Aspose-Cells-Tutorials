---
title: Recuperare dati dalle celle in Excel
linktitle: Recuperare dati dalle celle in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come recuperare dati dalle celle di Excel utilizzando Aspose.Cells per .NET in questo tutorial dettagliato, perfetto sia per i principianti che per gli sviluppatori esperti.
weight: 10
url: /it/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Recuperare dati dalle celle in Excel

## Introduzione

Quando si tratta di gestire dati in Excel, la capacità di leggere e recuperare informazioni dalle celle è fondamentale. Aspose.Cells per .NET è una potente libreria che consente agli sviluppatori di manipolare i file Excel senza problemi. In questo tutorial, approfondiremo come recuperare dati dalle celle in una cartella di lavoro Excel utilizzando Aspose.Cells. Che tu sia uno sviluppatore esperto o alle prime armi, questa guida ti guiderà passo dopo passo nel processo.

## Prerequisiti

Prima di passare al codice, è necessario soddisfare alcuni prerequisiti:

1. Visual Studio: assicurati di avere Visual Studio installato sul tuo computer. È l'IDE che useremo per scrivere ed eseguire il nostro codice.
2.  Aspose.Cells per .NET: è necessario avere la libreria Aspose.Cells. È possibile scaricarla da[Sito web di Aspose](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio gli esempi.
4. File Excel: avere pronto un file Excel (ad esempio,`book1.xls`) che utilizzerai per questo tutorial.

Una volta soddisfatti questi prerequisiti, possiamo iniziare a scoprire come recuperare i dati dalle celle di Excel.

## Importa pacchetti

Per iniziare, devi importare i namespace necessari nel tuo progetto C#. Questo ti consentirà di utilizzare le classi e i metodi forniti da Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Con questi namespace importati, sei pronto per iniziare a programmare. Suddividiamo il processo in passaggi gestibili.

## Passaggio 1: imposta la directory dei documenti

Il primo passo è definire il percorso alla directory dei documenti in cui si trova il file Excel. Questo è fondamentale perché indica all'applicazione dove trovare il file con cui vuoi lavorare.


```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
```

 Sostituire`"Your Document Directory"` con il percorso effettivo in cui ti trovi`book1.xls` file è memorizzato. Questo è il percorso in cui Aspose.Cells cercherà il file quando proverai ad aprirlo.

## Passaggio 2: aprire la cartella di lavoro esistente

Ora che hai impostato la directory dei documenti, il passo successivo è aprire la cartella di lavoro (file Excel) con cui vuoi lavorare.


```csharp
//Apertura di una cartella di lavoro esistente
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

 Qui creiamo un`Workbook` oggetto passando il percorso completo del file Excel. Questo passaggio inizializza la cartella di lavoro e la rende pronta per il recupero dei dati.

## Passaggio 3: accedi al primo foglio di lavoro

Dopo aver aperto la cartella di lavoro, vorrai accedere al foglio di lavoro specifico da cui vuoi recuperare i dati. In questo caso, accederemo al primo foglio di lavoro.


```csharp
// Accesso al primo foglio di lavoro
Worksheet worksheet = workbook.Worksheets[0];
```

 IL`Worksheets` la raccolta consente di accedere a diversi fogli nella cartella di lavoro. L'indice`[0]` si riferisce al primo foglio di lavoro. Se vuoi accedere ai fogli successivi, puoi modificare l'indice di conseguenza.

## Passaggio 4: scorrere le celle

Ora che hai il foglio di lavoro, è il momento di scorrere ogni cella per recuperare i dati. È qui che avviene la magia!


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // Variabili per memorizzare valori di diversi tipi di dati
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // Passaggio del tipo di dati contenuti nella cella per la valutazione
    switch (cell1.Type)
    {
        // Valutazione del tipo di dati della cella per il valore stringa
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // Valutazione del tipo di dati della cella dati per il valore double
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        //Valutazione del tipo di dati della cella per il valore booleano
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // Valutazione del tipo di dati della cella per il valore data/ora
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // Valutazione del tipo di dati sconosciuto dei dati della cella
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // Terminare il controllo del tipo di tipo di dati della cella è null
        case CellValueType.IsNull:
            break;
    }
}
```

 In questo passaggio, eseguiamo un ciclo su ogni cella del foglio di lavoro. Per ogni cella, controlliamo il suo tipo di dati utilizzando un`switch` istruzione. A seconda del tipo, recuperiamo il valore e lo stampiamo sulla console. Ecco una ripartizione dei casi:

-  IsString: se la cella contiene una stringa, la recuperiamo utilizzando`StringValue`.
-  IsNumeric: per i valori numerici, utilizziamo`DoubleValue`.
-  IsBool: se la cella contiene un valore booleano, vi si accede utilizzando`BoolValue`.
-  IsDateTime: per i valori di data e ora, utilizziamo`DateTimeValue`.
- IsUnknown: se il tipo di dati è sconosciuto, recuperiamo comunque la rappresentazione della stringa.
- IsNull: se la cella è vuota, semplicemente la saltiamo.

## Conclusione

Recuperare dati da celle Excel usando Aspose.Cells per .NET è un processo semplice. Seguendo questi passaggi, puoi estrarre in modo efficiente vari tipi di dati dai tuoi file Excel. Che tu stia creando uno strumento di reporting, automatizzando l'immissione di dati o semplicemente avendo bisogno di analizzare i dati, Aspose.Cells fornisce la flessibilità e la potenza di cui hai bisogno per portare a termine il lavoro.

## Domande frequenti

### Che cos'è Aspose.Cells?  
Aspose.Cells è una libreria .NET che consente agli sviluppatori di creare, manipolare e convertire file Excel senza dover installare Microsoft Excel.

### Posso usare Aspose.Cells gratuitamente?  
 Sì, Aspose.Cells offre una prova gratuita che puoi usare per testare le sue funzionalità. Puoi scaricarlo[Qui](https://releases.aspose.com/).

### Quali tipi di dati posso recuperare dalle celle di Excel?  
È possibile recuperare vari tipi di dati, tra cui stringhe, numeri, valori booleani e valori di data/ora.

### Come posso ottenere supporto per Aspose.Cells?  
 Puoi ottenere supporto visitando il[Forum di Aspose](https://forum.aspose.com/c/cells/9) dove puoi porre domande e ricevere aiuto dalla comunità.

### È disponibile una licenza temporanea?  
 Sì, Aspose offre una licenza temporanea a scopo di valutazione. Puoi trovare maggiori informazioni[Qui](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
