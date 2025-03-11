---
title: Conversione del foglio di lavoro in SVG in .NET
linktitle: Conversione del foglio di lavoro in SVG in .NET
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come convertire un foglio di lavoro Excel in SVG usando Aspose.Cells per .NET con questa guida passo-passo. Perfetto per gli sviluppatori .NET che vogliono eseguire il rendering di Excel in SVG.
weight: 11
url: /it/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Conversione del foglio di lavoro in SVG in .NET

## Introduzione

Se stai cercando di convertire un foglio di lavoro Excel in formato SVG, sei nel posto giusto! Aspose.Cells per .NET è un potente strumento che consente agli sviluppatori di manipolare file Excel e convertirli in vari formati, tra cui l'SVG (Scalable Vector Graphics) ampiamente supportato. Questo tutorial ti guiderà attraverso il processo di conversione di un foglio di lavoro in un SVG in .NET, suddividendolo passo dopo passo, in modo che anche i principianti possano seguire con facilità.

## Prerequisiti

Prima di immergerci nel codice, assicuriamoci di avere tutto ciò di cui hai bisogno:

1.  Aspose.Cells per .NET: Scarica e installa l'ultima versione di Aspose.Cells per .NET da[Aspose.Cells per .NET](https://releases.aspose.com/cells/net/).
2. Ambiente di sviluppo .NET: sarà necessario avere installato Visual Studio o qualsiasi altro IDE .NET.
3. Conoscenza di base di C#: è richiesta familiarità con C#, ma non preoccuparti, spiegheremo tutto in modo chiaro.
4. File Excel: tieni pronto un file Excel che vorresti convertire in formato SVG.

## Importazione dei pacchetti necessari

Prima di passare alla parte di codifica, assicurati di includere gli spazi dei nomi richiesti all'inizio del tuo file C#.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Questi pacchetti sono necessari per lavorare con Aspose.Cells e gestire le opzioni di rendering come l'esportazione SVG.

Ora che abbiamo affrontato le nozioni di base, passiamo ai passaggi effettivi per convertire un foglio di lavoro Excel in un'immagine SVG.

## Passaggio 1: imposta il percorso della directory dei documenti

La prima cosa di cui abbiamo bisogno è definire il percorso della cartella in cui si trova il tuo file Excel. Questo è fondamentale perché il tuo codice farà riferimento alla directory per caricare e salvare i file.

```csharp
// Il percorso verso la directory dei documenti
string dataDir = "Your Document Directory";
```

 Assicurati di sostituire`"Your Document Directory"`con il percorso effettivo in cui risiede il file Excel.

##  Passaggio 2: caricare il file Excel utilizzando`Workbook`

 Successivamente, dobbiamo caricare il file Excel in un'istanza di`Workbook` classe. La`Workbook` La classe rappresenta l'intero file Excel, inclusi tutti i fogli di lavoro in esso contenuti.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Qui,`"Template.xlsx"` è il nome del file Excel con cui stai lavorando. Assicurati che questo file esista nella directory specificata, altrimenti incontrerai degli errori.

## Passaggio 3: impostare le opzioni di immagine o stampa per la conversione SVG

 Prima di poter convertire il foglio di lavoro in formato SVG, dobbiamo specificare le opzioni dell'immagine.`ImageOrPrintOptions` classe consente di controllare come il foglio di lavoro verrà convertito. In particolare, dobbiamo impostare la`SaveFormat` A`SVG` e assicurarsi che ogni foglio di lavoro venga convertito in una singola pagina.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 IL`SaveFormat.Svg` l'opzione assicura che il formato di output sarà SVG, mentre`OnePagePerSheet` garantisce che ogni foglio di lavoro venga visualizzato su una singola pagina.

## Passaggio 4: scorrere ogni foglio di lavoro nella cartella di lavoro

Ora dobbiamo scorrere tutti i fogli di lavoro nel file Excel. Ogni foglio di lavoro verrà convertito individualmente.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Elaboreremo ogni foglio di lavoro uno per uno
}
```

Questo ciclo garantisce che, indipendentemente dal numero di fogli di lavoro presenti nella cartella di lavoro, ognuno di essi verrà gestito.

##  Passaggio 5: creare un`SheetRender` Object for Rendering

 Per ogni foglio di lavoro, creeremo un`SheetRender` oggetto. Questo oggetto è responsabile della conversione del foglio di lavoro nel formato immagine desiderato, che in questo caso è SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 IL`SheetRender` object accetta due argomenti: il foglio di lavoro che stai convertendo e le opzioni immagine definite in precedenza.

## Passaggio 6: convertire il foglio di lavoro in SVG

 Infine, all'interno del ciclo, convertiremo ogni foglio di lavoro in formato SVG. Utilizziamo un ciclo nidificato per scorrere le pagine (anche se in questo caso c'è solo una pagina per foglio di lavoro, grazie al`OnePagePerSheet` opzione).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Esportare il foglio di lavoro in formato immagine Svg
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Questo codice salverà il foglio di lavoro come file SVG nella stessa directory del file Excel. Ogni file SVG verrà denominato in base al nome del foglio di lavoro e a un numero di indice per evitare conflitti di denominazione.

## Conclusione

Ed ecco fatto! Hai convertito con successo un foglio di lavoro Excel in formato SVG usando Aspose.Cells per .NET. Questo processo ti consente di mantenere il layout e il design del tuo foglio di lavoro rendendolo visualizzabile in qualsiasi browser o dispositivo che supporti SVG, ovvero praticamente tutti. Sia che tu stia lavorando con file Excel complessi o semplicemente con una semplice tabella, questo metodo assicura che i tuoi dati siano splendidamente resi in un formato web-friendly.

## Domande frequenti

### Cos'è SVG e perché dovrei utilizzarlo?
SVG (Scalable Vector Graphics) è un formato web-friendly che può essere ridimensionato all'infinito senza perdere qualità. È perfetto per grafici, diagrammi e immagini che devono essere visualizzati in varie dimensioni.

### Aspose.Cells può gestire file Excel di grandi dimensioni per la conversione?
Sì, Aspose.Cells può gestire in modo efficiente file Excel di grandi dimensioni e convertirli in SVG senza significativi problemi di prestazioni.

### Esiste un limite al numero di fogli di lavoro che posso convertire in SVG?
No, non c'è alcun limite intrinseco in Aspose.Cells per la conversione di più fogli di lavoro. L'unico vincolo sarebbe la memoria e le prestazioni del tuo sistema.

### Ho bisogno di una licenza per utilizzare Aspose.Cells?
 Sì, Aspose.Cells richiede una licenza per l'uso in produzione. Puoi ottenere una licenza temporanea[Qui](https://purchase.aspose.com/temporary-license/) o esplora il[prova gratuita](https://releases.aspose.com/).

### Posso personalizzare l'output SVG?
 Sì, puoi modificare il`ImageOrPrintOptions` per personalizzare vari aspetti dell'output SVG, come la risoluzione e il ridimensionamento.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
