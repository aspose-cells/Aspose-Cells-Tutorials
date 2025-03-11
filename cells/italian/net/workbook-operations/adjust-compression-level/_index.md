---
title: Regola il livello di compressione nella cartella di lavoro
linktitle: Regola il livello di compressione nella cartella di lavoro
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come regolare il livello di compressione delle cartelle di lavoro di Excel usando Aspose.Cells per .NET con questa guida passo-passo. Ottimizza la gestione dei tuoi file.
weight: 14
url: /it/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Regola il livello di compressione nella cartella di lavoro

## Introduzione
Quando si tratta di gestire file Excel di grandi dimensioni, la compressione è un punto di svolta. Non solo fa risparmiare spazio di archiviazione, ma rende anche i trasferimenti di file più rapidi ed efficienti. Se lavori con Aspose.Cells per .NET, puoi facilmente regolare il livello di compressione delle tue cartelle di lavoro. In questa guida, ti guideremo passo dopo passo nel processo, assicurandoti di comprendere ogni parte del codice e il suo funzionamento.
## Prerequisiti
Prima di immergerti nel codice, ci sono alcuni prerequisiti che devi soddisfare:
1. Conoscenza di base di C#: la familiarità con la programmazione C# ti aiuterà a comprendere meglio i frammenti di codice.
2.  Libreria Aspose.Cells: devi avere installata la libreria Aspose.Cells. Puoi scaricarla da[Qui](https://releases.aspose.com/cells/net/).
3. Visual Studio: per eseguire il codice sarà necessario un ambiente di sviluppo come Visual Studio.
4. .NET Framework: assicurati che il tuo progetto sia configurato con una versione compatibile di .NET Framework.
## Importa pacchetti
Per iniziare, devi importare i pacchetti necessari nel tuo progetto C#. Ecco come puoi farlo:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Questi pacchetti sono essenziali per lavorare con file Excel utilizzando la libreria Aspose.Cells.`Aspose.Cells` namespace contiene tutte le classi necessarie per manipolare i file Excel, mentre`Aspose.Cells.Xlsb` fornisce le opzioni per salvare i file nel formato XLSB.
Ora, scomponiamo il processo di regolazione del livello di compressione in una cartella di lavoro in passaggi gestibili.
## Passaggio 1: definire le directory di origine e di output
Per prima cosa, devi specificare dove si trovano i tuoi file sorgente e dove vuoi salvare i file di output. Questo è fondamentale per garantire che il tuo programma sappia dove trovare i file con cui deve lavorare.
```csharp
// Elenco di origine
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Sostituire`"Your Document Directory"` con il percorso effettivo delle tue directory. Questo aiuterà il programma a localizzare i file che vuoi comprimere.
## Passaggio 2: caricare la cartella di lavoro
Poi, caricherai la cartella di lavoro che vuoi comprimere. È qui che inizia la magia!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
In questa riga, creiamo una nuova istanza di`Workbook` class e carica un file Excel esistente. Assicurati che il nome del file corrisponda a quello che hai nella directory di origine.
## Passaggio 3: imposta le opzioni di salvataggio
Ora è il momento di configurare le opzioni di salvataggio. Imposteremo il tipo di compressione per il file di output. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 IL`XlsbSaveOptions` La classe consente di specificare varie opzioni quando si salva la cartella di lavoro nel formato XLSB, inclusi i livelli di compressione.
## Fase 4: Misurare il tempo di compressione per il livello 1
Cominciamo con il primo livello di compressione. Misureremo quanto tempo ci vuole per salvare la cartella di lavoro con questo livello di compressione.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Qui, impostiamo il tipo di compressione su Livello 1, salviamo la cartella di lavoro e poi misuriamo il tempo trascorso. Questo ci dà un'idea di quanto tempo impiega il processo.
## Fase 5: Misurare il tempo di compressione per il livello 6
Vediamo ora come funziona la compressione di livello 6.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Questo passaggio è simile al precedente, ma modifichiamo il livello di compressione al Livello 6. Noterai che il tempo impiegato potrebbe variare in base alla complessità della cartella di lavoro.
## Fase 6: Misurare il tempo di compressione per il livello 9
Infine, diamo un'occhiata alle prestazioni con il livello di compressione più elevato.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
In questa fase, impostiamo il livello di compressione al Livello 9. È qui che solitamente si nota la riduzione più significativa delle dimensioni del file, ma l'elaborazione potrebbe richiedere più tempo.
## Fase 7: Output finale
Dopo aver eseguito tutti i livelli di compressione, è possibile visualizzare un messaggio che indica che il processo è stato completato correttamente.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Questa semplice riga di codice conferma che l'esecuzione del programma è stata completata senza intoppi.
## Conclusione
Regolare il livello di compressione delle tue cartelle di lavoro usando Aspose.Cells per .NET è un processo semplice che può portare a notevoli vantaggi in termini di dimensioni e prestazioni dei file. Seguendo i passaggi descritti in questa guida, puoi facilmente implementare la compressione nelle tue applicazioni e migliorare l'efficienza della gestione dei tuoi file Excel.
## Domande frequenti
### Che cos'è Aspose.Cells?  
Aspose.Cells è una potente libreria per .NET che consente agli sviluppatori di creare, manipolare e convertire file Excel senza dover utilizzare Microsoft Excel.
### Come faccio a installare Aspose.Cells?  
 Puoi scaricare e installare Aspose.Cells da[Sito web di Aspose](https://releases.aspose.com/cells/net/).
### Quali livelli di compressione sono disponibili?  
Aspose.Cells supporta più livelli di compressione, dal Livello 1 (compressione più bassa) al Livello 9 (compressione più alta).
### Posso provare Aspose.Cells gratuitamente?  
 Sì! Puoi ottenere una prova gratuita di Aspose.Cells[Qui](https://releases.aspose.com/).
### Dove posso trovare supporto per Aspose.Cells?  
 Per qualsiasi domanda o supporto, puoi visitare il forum di supporto di Aspose[Qui](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
