---
"description": "Scopri come unire le celle in un intervallo denominato utilizzando Aspose.Cells per .NET in questo tutorial passo passo. Scopri come formattare, applicare stili e automatizzare i report di Excel."
"linktitle": "Unisci celle in un intervallo denominato in Excel"
"second_title": "API di elaborazione Excel .NET Aspose.Cells"
"title": "Unisci celle in un intervallo denominato in Excel"
"url": "/it/net/excel-advanced-named-ranges/merge-cells-in-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Unisci celle in un intervallo denominato in Excel

## Introduzione

Quando si lavora con file Excel a livello di programmazione, una delle attività più comuni è l'unione di celle all'interno di un intervallo denominato. Che si tratti di automatizzare la generazione di report, creare dashboard o semplicemente gestire dataset di grandi dimensioni, l'unione di celle è una tecnica essenziale. In questo tutorial, esploreremo come unire celle in un intervallo denominato utilizzando Aspose.Cells per .NET, una potente libreria che consente agli sviluppatori di manipolare file Excel senza dover installare Microsoft Excel.

## Prerequisiti

Prima di iniziare, assicurati di avere pronto quanto segue:

- Aspose.Cells per .NET: puoi scaricarlo da [Pagina delle release di Aspose.Cells](https://releases.aspose.com/cells/net/).
- .NET Framework installato sul computer.
- Conoscenza di base di C#: sarà utile avere familiarità con concetti quali classi, metodi e oggetti.

## Importa pacchetti

Prima di iniziare a scrivere codice, è necessario importare i namespace necessari. Questi namespace daranno accesso alle funzionalità della libreria Aspose.Cells.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Ora che abbiamo chiarito i prerequisiti e i pacchetti, passiamo alla parte divertente: la codifica!

Ecco una spiegazione dettagliata di come unire le celle in un intervallo denominato in un foglio Excel utilizzando Aspose.Cells per .NET.

## Passaggio 1: creare una nuova cartella di lavoro

La prima cosa di cui abbiamo bisogno è una cartella di lavoro. Una cartella di lavoro, in termini Excel, è l'equivalente di un file Excel. Creiamone una.

```csharp
// Crea una nuova cartella di lavoro.
Workbook wb1 = new Workbook();
```

Inizializzando una nuova cartella di lavoro, abbiamo ora un file Excel vuoto pronto per essere elaborato. È come iniziare da una tela bianca!

## Passaggio 2: accedi al primo foglio di lavoro

Ogni cartella di lavoro contiene dei fogli di lavoro e, in questo caso, vogliamo lavorare con il primo. Prendiamolo!

```csharp
// Ottieni il primo foglio di lavoro nella cartella di lavoro.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Considerate il foglio di lavoro come le singole schede di un file Excel in cui sono memorizzati i dati. Per impostazione predefinita, accediamo alla prima scheda.

## Passaggio 3: creare un intervallo di celle

Ora che abbiamo il nostro foglio di lavoro, è il momento di creare un intervallo. Un intervallo è un blocco di celle, che può estendersi su più righe e colonne.

```csharp
// Crea un intervallo.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Qui selezioniamo le celle da D6 a I12, un blocco che comprende più righe e colonne. Presto uniremo questo intervallo!

## Passaggio 4: Assegna un nome all'intervallo

Assegnare un nome a un intervallo semplifica il successivo riferimento, soprattutto quando si gestiscono set di dati di grandi dimensioni.

```csharp
// Assegna un nome all'intervallo.
mrange.Name = "TestRange";
```

Chiamando questo intervallo "TestRange", possiamo recuperarlo rapidamente in seguito nel codice, senza dover specificare nuovamente le coordinate della cella.

## Passaggio 5: unire l'intervallo di celle

Ora arriva la magia: unire le celle all'interno dell'intervallo appena creato!

```csharp
// Unisci le celle dell'intervallo.
mrange.Merge();
```

Questo passaggio unisce tutte le celle da D6 a I12 in un'unica cella. Perfetto per titoli o riassunti!

## Passaggio 6: recuperare l'intervallo denominato

Una volta unite le celle, potremmo voler applicare un po' di formattazione. Per prima cosa, recuperiamo il nostro intervallo denominato.

```csharp
// Ottieni la gamma.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Recuperando l'intervallo in base al nome possiamo eseguire ulteriori operazioni, come l'aggiunta di stili o l'inserimento di dati.

## Passaggio 7: definire uno stile per le celle unite

A cosa serve una cella unita se non ha un aspetto curato? Creiamo un oggetto stile per allineare il testo e applicare un colore di sfondo.

```csharp
// Definisci un oggetto stile.
Style style = wb1.CreateStyle();

// Imposta l'allineamento.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Qui allineiamo il testo sia orizzontalmente che verticalmente al centro, e impostiamo uno sfondo azzurro (acqua). Elegante, vero?

## Passaggio 8: applicare lo stile all'intervallo

Dopo aver definito lo stile, è il momento di applicarlo all'intervallo unito.

```csharp
// Crea un oggetto StyleFlag.
StyleFlag flag = new StyleFlag();

// Imposta su ON l'attributo di stile relativo.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Applica lo stile all'intervallo.
range1.ApplyStyle(style, flag);
```

IL `StyleFlag` indica ad Aspose.Cells quali proprietà di stile applicare: allineamento, ombreggiatura, ecc. Ciò fornisce un controllo granulare su come viene applicato lo stile.

## Passaggio 9: immettere i dati nell'intervallo unito

Cos'è un intervallo formattato senza contenuto? Aggiungiamo del testo.

```csharp
// Inserire i dati nell'intervallo.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Questo inserisce il testo "Benvenuti nelle API di Aspose" nella prima cella del nostro intervallo unito. Con la cella unita, questo testo si estenderà a tutte le celle da D6 a I12.

## Passaggio 10: salvare il file Excel

Infine, salviamo la cartella di lavoro come file Excel.

```csharp
// Salvare il file Excel.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Qui la cartella di lavoro viene salvata con il nome "outputMergeCellsInNamedRange.xlsx" nella directory specificata.

## Conclusione

Ed ecco fatto! Hai unito con successo le celle in un intervallo denominato, applicato una splendida formattazione e persino inserito dei dati, il tutto con Aspose.Cells per .NET. Che tu stia automatizzando report, manipolando file Excel o semplicemente imparando nuove tecniche, questa guida passo passo dovrebbe fornirti le basi necessarie.

## Domande frequenti

### Posso unire più intervalli non contigui in Aspose.Cells?  
No, in Aspose.Cells è possibile unire solo celle contigue.

### Posso annullare un'operazione di unione a livello di codice?  
Una volta unite le celle, è possibile separarle utilizzando `UnMerge()` metodo in Aspose.Cells.

### L'unione delle celle rimuove i dati in esse contenuti?  
Se nelle celle prima dell'unione sono presenti dati, verranno mantenuti i dati della prima cella dell'intervallo.

### Posso applicare stili diversi alle singole celle all'interno di un intervallo unito?  
No, un intervallo unito funziona come una singola cella, quindi non è possibile applicare stili diversi alle singole celle al suo interno.

### Come posso accedere a una cella unita dopo averla unita?  
Dopo l'unione, è ancora possibile accedere alla cella unita utilizzando le coordinate dell'angolo in alto a sinistra.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}