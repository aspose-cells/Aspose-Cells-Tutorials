---
title: Separare le celle unite in Excel
linktitle: Separare le celle unite in Excel
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Separa facilmente le celle unite in Excel usando Aspose.Cells per .NET. Segui la nostra guida passo passo per creare fogli di calcolo migliori.
weight: 10
url: /it/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Separare le celle unite in Excel

## Introduzione

Sei stanco di dover gestire celle unite nei tuoi fogli di calcolo Excel? Non sei il solo! Le celle unite possono essere una funzionalità utile per la formattazione, ma possono spesso causare mal di testa quando si tratta di manipolazione e analisi dei dati. Ma indovina un po'? Separare quelle fastidiose celle è più facile di quanto pensi, soprattutto quando usi Aspose.Cells per .NET. In questo articolo, ti guiderò passo dopo passo attraverso come separare le celle unite, assicurandoti che i tuoi dati siano puliti, ordinati e pronti per l'azione! Quindi, prendi il tuo cappello da programmatore e tuffiamoci nel mondo di Aspose.Cells.

## Prerequisiti

Prima di sporcarci le mani, ecco alcuni elementi essenziali che dovrai avere a portata di mano:

### Conoscenza di base di C# e .NET Framework
Se hai familiarità con la programmazione C# e hai una conoscenza di base del framework .NET, sei già partito alla grande. In caso contrario, non preoccuparti! Questo tutorial è progettato per essere semplice, quindi imparerai i concetti necessari strada facendo.

### Libreria Aspose.Cells
Assicurati di avere la libreria Aspose.Cells installata nel tuo ambiente .NET. Puoi ottenerla facilmente visitando il sito[Pagina di download di Aspose.Cells](https://releases.aspose.com/cells/net/).

### Configurazione IDE
Dovresti avere impostato un ambiente di sviluppo, come Visual Studio, in cui puoi scrivere ed eseguire il codice C#.

### Esempio di file Excel
Prendi un file Excel di esempio che contiene alcune celle unite: userai questo file per esercitarti a separare le celle.

Una volta soddisfatti tutti questi prerequisiti, possiamo passare alla parte più entusiasmante: la codifica della nostra soluzione!

## Importa pacchetti

Per prima cosa, importiamo i pacchetti necessari. Con Aspose.Cells, interagirai con varie classi per gestire efficacemente i tuoi file Excel. Ecco cosa devi includere all'inizio del tuo file C#:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Includendo questo pacchetto avrai accesso a tutte le funzionalità offerte da Aspose.Cells.

Analizziamo il processo di unmerging in passaggi gestibili. Ogni passaggio sarà chiaramente definito in modo che tu possa seguirlo facilmente.

## Passaggio 1: definire le directory

Il primo passo è definire le directory in cui si trovano il file Excel di input (quello con le celle unite) e il file di output (quello in cui verranno salvati i dati non uniti). Ecco come impostarlo:

```csharp
// Elenco di origine
string sourceDir = "Your Document Directory"; 

// Directory di uscita
string outputDir = "Your Document Directory"; 
```

 Assicurati di sostituire`"Your Document Directory"` con il percorso effettivo dei tuoi file.

## Passaggio 2: creare una cartella di lavoro

Ora che hai impostato le directory, è il momento di creare un oggetto Workbook. Questo oggetto ti consentirà di manipolare il file Excel. Puoi farlo con il seguente codice:

```csharp
// Crea una cartella di lavoro
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Questa riga di codice legge il file Excel di esempio e lo prepara per l'elaborazione. 

## Passaggio 3: accedi al foglio di lavoro

Ogni cartella di lavoro è composta da fogli. Devi accedere al foglio di lavoro specifico in cui vuoi separare le celle. Ecco come fare:

```csharp
// Crea un foglio di lavoro e ottieni il primo foglio
Worksheet worksheet = wbk.Worksheets[0];
```

Questo codice cattura il primo foglio di lavoro. Se le celle unite sono su un foglio diverso, aggiorna l'indice di conseguenza.

## Passaggio 4: accedere alle celle nel foglio di lavoro

Successivamente, dovrai ottenere un riferimento alle celle nel tuo foglio di lavoro. Questo può essere ottenuto usando:

```csharp
//Crea un oggetto Celle per recuperare tutte le celle
Cells cells = worksheet.Cells;
```

Grazie a questa riga, ora hai accesso a tutte le celle del foglio di lavoro, potendo così manipolarle a seconda delle tue esigenze.

## Passaggio 5: separare le celle

Ecco il passaggio cruciale: separare le celle! Dovrai specificare l'intervallo delle celle unite che desideri separare. Utilizza il seguente codice:

```csharp
// Separare le celle
cells.UnMerge(5, 2, 2, 3);
```

 In questo esempio, il`UnMerge` Il metodo accetta quattro parametri: l'indice di riga iniziale (5), l'indice di colonna iniziale (2), il numero di righe da dividere (2) e il numero di colonne da dividere (3). Adatta questi parametri in modo che corrispondano alle celle unite specifiche nel tuo file Excel.

## Passaggio 6: salvare la cartella di lavoro

Dopo aver eseguito l'unmerging, vorrai salvare le modifiche in un nuovo file Excel. Ecco come fare:

```csharp
// Salva il file
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Questa riga salva i tuoi dati non uniti nella directory di output specificata. Semplice!

## Passaggio 7: confermare il processo

Infine, è una buona idea confermare che tutto è andato liscio. Puoi stampare un messaggio sulla console per farti sapere che l'operazione è stata eseguita correttamente:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

Ed ecco fatto! Hai unito con successo le celle in un file Excel usando Aspose.Cells per .NET.

## Conclusione

Separare le celle potrebbe sembrare noioso, soprattutto se si ha a che fare con grandi fogli di calcolo, ma con Aspose.Cells per .NET è un gioco da ragazzi! Questo tutorial ti ha guidato attraverso tutto, dall'impostazione del tuo ambiente all'esecuzione del codice necessario per separare le celle in modo efficace. La flessibilità offerta dalla libreria Aspose.Cells ti consente di elaborare i fogli di calcolo in modo efficiente, rendendola una scelta ideale per gli sviluppatori che lavorano con file Excel. Quindi, tuffati e inizia a goderti fogli di calcolo più puliti e gestibili.

## Domande frequenti

### Che cos'è Aspose.Cells?  
Aspose.Cells è una potente libreria per creare, manipolare e convertire documenti Excel nelle applicazioni .NET.

### Ho bisogno di una licenza per utilizzare Aspose.Cells?  
 Mentre Aspose.Cells offre una prova gratuita, è richiesta una licenza per un utilizzo completo. Puoi ottenere una[licenza temporanea qui](https://purchase.aspose.com/temporary-license/).

### Posso dividere le celle di più fogli contemporaneamente?  
Sì, è possibile scorrere più fogli di lavoro all'interno di una cartella di lavoro e dividere le celle in base alle esigenze.

### Aspose.Cells è compatibile con .NET Core?  
Sì, Aspose.Cells è compatibile con .NET Core, il che lo rende versatile per varie applicazioni .NET.

### Dove posso trovare ulteriore documentazione su Aspose.Cells?  
 Puoi esplorare la documentazione completa su[Pagina di riferimento Aspose.Cells](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
