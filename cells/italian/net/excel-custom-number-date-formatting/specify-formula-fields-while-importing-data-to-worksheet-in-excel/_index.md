---
"description": "In questo tutorial dettagliato scoprirai come importare dati in fogli Excel con campi formula specificati utilizzando Aspose.Cells per .NET."
"linktitle": "Specificare i campi formula durante l'importazione di dati in un foglio Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Specificare i campi formula durante l'importazione di dati in un foglio Excel"
"url": "/it/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specificare i campi formula durante l'importazione di dati in un foglio Excel

## Introduzione

Quando si tratta di gestire file Excel a livello di codice, Aspose.Cells per .NET è uno strumento prezioso. Offre funzionalità affidabili per creare, modificare e manipolare fogli di calcolo Excel con facilità. Una delle funzionalità più interessanti è la possibilità di specificare campi formula durante l'importazione di dati in un foglio Excel. Immagina di lavorare a un report finanziario e di dover calcolare automaticamente i totali in base all'input dell'utente. Questo tutorial ti guiderà passo dopo passo nel raggiungimento di questo obiettivo con un approccio semplice e diretto.

## Prerequisiti

Prima di immergerci nel codice, assicuriamoci di avere tutto ciò di cui hai bisogno. 

1. Visual Studio o qualsiasi ambiente di sviluppo integrato (IDE) .NET: assicurati di disporre di un IDE adatto per scrivere ed eseguire il codice C#.
2. Aspose.Cells per .NET: dovrai scaricare e fare riferimento alla libreria Aspose.Cells nel tuo progetto. Puoi scaricarla da [Rilasci di Aspose](https://releases.aspose.com/cells/net/).
3. Conoscenza di base di C#: la familiarità con C# e con i concetti di programmazione orientata agli oggetti ti aiuterà a comprendere meglio gli esempi.
4. .NET Framework: in questo tutorial si presuppone che si utilizzi .NET Framework 4.5 o versione successiva.

Una volta soddisfatti i prerequisiti, procediamo a importare alcuni dati in un foglio Excel con campi formula specificati.

## Importa pacchetti

Prima di iniziare a scrivere il codice, è necessario importare lo spazio dei nomi Aspose.Cells necessario. Questa operazione viene in genere eseguita all'inizio del file C#:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Ciò consente di utilizzare le classi e i metodi forniti dalla libreria Aspose.Cells senza dover ogni volta anteporre loro lo spazio dei nomi.

Scomponiamo l'intero processo in passaggi gestibili:

## Passaggio 1: definire la directory di output

Per prima cosa, devi stabilire dove vuoi salvare il file Excel. Ecco come fare:

```csharp
static string outputDir = "Your Document Directory"; // specifica qui la directory dei tuoi documenti
```

Sostituire `"Your Document Directory"` Con il percorso effettivo del file. È qui che verrà salvato il file Excel generato.

## Passaggio 2: creare una classe definita dall'utente per gli elementi dati

Ora definiremo una classe per strutturare i dati che intendiamo importare.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

Questo `DataItems` La classe conterrà i numeri interi grezzi e le formule che scriveremo nel foglio Excel. 

## Passaggio 3: inizializzare un elenco per contenere gli elementi dati

Utilizzeremo un elenco per contenere più istanze del nostro `DataItems` classe.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Passaggio 4: aggiungere elementi dati all'elenco

Ora aggiungiamo alcune voci alla nostra lista. Ogni voce conterrà due numeri e due formule.

```csharp
// Definisci e aggiungi ogni elemento dati
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Sito web Aspose\")";
dis.Add(di);

// Ripetere per ulteriori elementi di dati
```

Assicurati di personalizzare ogni `DataItems` istanza con valori e formule univoci.

## Passaggio 5: creare una cartella di lavoro e un foglio di lavoro di Access

Successivamente, creiamo la cartella di lavoro e accediamo al primo foglio di lavoro in cui importeremo i dati.

```csharp
Workbook wb = new Workbook(); // creare una nuova cartella di lavoro
Worksheet ws = wb.Worksheets[0]; // accedi al primo foglio di lavoro
```

## Passaggio 6: specificare le opzioni della tabella di importazione

È qui che avviene la magia. Devi specificare quali campi nei tuoi dati corrispondono alle formule. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

In questo esempio, gli ultimi due campi contengono formule, il che è indicato da `true`, mentre i primi due campi sono impostati su `false`.

## Passaggio 7: importare oggetti personalizzati

Ora che tutto è impostato, importiamo l'elenco dei dati nel foglio di lavoro.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Questa riga importa di fatto i dati a partire dalla cella A1.

## Passaggio 8: calcolare le formule

Poiché abbiamo importato alcune formule, è fondamentale calcolarle.

```csharp
wb.CalculateFormula();
```

Questo metodo garantisce che le formule vengano valutate in base alle loro dipendenze.

## Passaggio 9: Adattamento automatico delle colonne

Per assicurarti che i tuoi dati siano facili da visualizzare, puoi adattare automaticamente le colonne in base al contenuto.

```csharp
ws.AutoFitColumns();
```

Questo passaggio ottimizza il layout del file Excel. 

## Passaggio 10: salva il file Excel

Infine, è il momento di salvare il file Excel appena creato. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Assicurati che il nome del file di output sia pertinente e descrittivo!

## Fase 11: Verifica dell'esecuzione

Per confermare in modo semplice che tutto sia andato a buon fine, potresti voler stampare un messaggio.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

In questo modo avrai subito la conferma che il codice ha funzionato senza problemi.

## Conclusione

Ed ecco fatto! Hai importato correttamente i dati in un foglio Excel utilizzando Aspose.Cells per .NET e specificando i campi formula. Seguendo questi passaggi, puoi applicare tecniche simili per automatizzare le attività di elaborazione dati in base alle tue esigenze. Che tu stia elaborando numeri per report o semplicemente gestendo dati, padroneggiare l'arte della manipolazione di Excel con Aspose è un'abilità che vale la pena acquisire.

## Domande frequenti

### Che cosa è Aspose.Cells?
Aspose.Cells è una libreria .NET progettata per creare, manipolare e convertire file Excel a livello di programmazione.

### Come faccio a installare Aspose.Cells per .NET?
Puoi scaricarlo da [Rilasci di Aspose](https://releases.aspose.com/cells/net/) e farvi riferimento nel vostro progetto.

### Posso usare Aspose.Cells gratuitamente?
Sì, Aspose offre una prova gratuita disponibile su [questo collegamento](https://releases.aspose.com/).

### Dove posso trovare altri esempi?
Ulteriori esempi e documentazione possono essere trovati su [Pagina di documentazione di Aspose](https://reference.aspose.com/cells/net/).

### Cosa succede se riscontro problemi durante l'utilizzo di Aspose?
Puoi cercare aiuto nel forum di supporto di Aspose [Qui](https://forum.aspose.com/c/cells/9).
 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}