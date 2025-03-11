---
title: Calcola il colore scelto da MS Excel tramite programmazione
linktitle: Calcola il colore scelto da MS Excel tramite programmazione
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come calcolare il colore scelto da MS Excel usando Aspose.Cells per .NET. Segui questa guida passo passo per accedere al colore di formattazione condizionale di Excel a livello di programmazione.
weight: 10
url: /it/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Calcola il colore scelto da MS Excel tramite programmazione

## Introduzione
Hai mai lavorato con file Excel e ti sei chiesto come certi colori vengono selezionati automaticamente per la formattazione? Non sei il solo. La formattazione condizionale di Excel può essere un po' un mistero, specialmente quando si cerca di estrarre il colore esatto che Excel assegna. Ma non preoccuparti, ci pensiamo noi! In questo tutorial, approfondiremo come calcolare a livello di programmazione il colore scelto da MS Excel usando Aspose.Cells per .NET. Lo scomporremo passo dopo passo, così potrai seguirlo e applicarlo ai tuoi progetti con facilità. Cominciamo!
## Prerequisiti
Prima di immergerci nel codice, vediamo cosa ti servirà per seguire questo tutorial:
-  Aspose.Cells per .NET installato. Se non lo hai ancora, puoi[scaricalo qui](https://releases.aspose.com/cells/net/).
- Conoscenza pratica di C# e del framework .NET.
- Un file Excel di esempio (Book1.xlsx) con formattazione condizionale applicata.
Puoi anche provare la versione di prova gratuita di Aspose.Cells per .NET se non hai ancora una licenza. Scarica la versione di prova[Qui](https://releases.aspose.com/).
## Importa pacchetti
Prima di iniziare a scrivere codice, dobbiamo importare i pacchetti necessari per garantire che tutto funzioni senza intoppi. Assicurati di includere i seguenti namespace nel tuo progetto:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Queste importazioni forniscono l'accesso alle classi principali di Aspose.Cells e alla libreria di disegno di sistema nativa di .NET per la gestione dei colori.

Ora che abbiamo tutto a posto, suddividiamo questo compito in passaggi digeribili:
## Passaggio 1: impostare l'oggetto cartella di lavoro
 La prima cosa che dobbiamo fare è creare un'istanza di`Workbook` oggetto e caricare il file Excel con cui vogliamo lavorare. È qui che inizia il viaggio!
```csharp
// Percorso verso la directory dei documenti.
string dataDir = "Your Document Directory";
// Crea un'istanza di un oggetto cartella di lavoro e apri il file modello
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
 In questo passaggio, creiamo una nuova istanza di`Workbook` classe da Aspose.Cells. La`Workbook`La classe rappresenta un file Excel e, specificando il percorso al nostro file, possiamo caricarlo facilmente per ulteriori manipolazioni.
## Passaggio 2: accedi al primo foglio di lavoro
Una volta caricata la cartella di lavoro, dobbiamo accedere al foglio di lavoro specifico in cui vogliamo estrarre il colore. In questo esempio, lavoreremo con il primo foglio.
```csharp
// Ottieni il primo foglio di lavoro
Worksheet worksheet = workbook.Worksheets[0];
```
 Qui, stiamo recuperando il primo foglio di lavoro nella cartella di lavoro utilizzando il`Worksheets[0]` indice. Aspose.Cells consente di accedere a qualsiasi foglio di lavoro nel file Excel tramite il suo indice o nome.
## Passaggio 3: selezionare la cella di interesse
Successivamente, sceglieremo una cella specifica nel foglio di lavoro. Per questo tutorial, ci concentreremo sulla cella "A1", ma puoi selezionare qualsiasi cella con formattazione condizionale applicata.
```csharp
// Ottieni la cella A1
Cell a1 = worksheet.Cells["A1"];
```
 Noi utilizziamo il`Cells` proprietà per fare riferimento a una cella specifica tramite il suo indirizzo. In questo caso, selezioniamo la cella "A1" perché vogliamo estrarre i risultati della formattazione condizionale applicati a questa cella.
## Passaggio 4: recuperare il risultato della formattazione condizionale
Ora, ecco dove avviene la magia! Utilizzeremo Aspose.Cells per catturare il risultato della formattazione condizionale per la cella selezionata. Ecco come Excel calcola la formattazione dinamicamente, inclusi i colori.
```csharp
// Ottieni l'oggetto risultante della formattazione condizionale
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
 IL`GetConditionalFormattingResult()` metodo è cruciale in questo passaggio. Restituisce un oggetto che contiene i risultati di qualsiasi formattazione condizionale applicata alla cella. È qui che iniziamo a sfruttare le informazioni sul colore che Excel sta utilizzando.
## Passaggio 5: accedi a ColorScaleResult
Una volta ottenuto il risultato della formattazione condizionale, possiamo approfondire l'argomento e accedere alla scala di colori utilizzata da Excel per questa particolare cella.
```csharp
// Ottieni l'oggetto colore risultante ColorScale
Color c = cfr1.ColorScaleResult;
```
La formattazione condizionale in Excel spesso si basa su scale di colori. Questa riga ci consente di estrarre il colore risultante che è stato applicato in base alle regole di formattazione condizionale.
## Passaggio 6: emissione delle informazioni sul colore
Infine, vogliamo vedere il colore applicato da Excel. Stampiamo i dettagli del colore in un formato facile da capire, includendo sia il suo valore ARGB che il suo nome.
```csharp
// Leggi il colore
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
 IL`ToArgb()` il metodo ci fornisce il colore in formato ARGB (Alpha, Red, Green, Blue), mentre il`Name` property fornisce il nome del colore in un formato più leggibile. Puoi usare questi dettagli di colore per abbinarli in altre applicazioni o modificare i tuoi file Excel a livello di programmazione.

## Conclusione
Ed ecco fatto! Seguendo questi passaggi, hai appena imparato come calcolare a livello di programmazione il colore scelto da MS Excel usando Aspose.Cells per .NET. Questo approccio può essere incredibilmente utile per automatizzare le attività basate su Excel, specialmente quando si ha a che fare con una formattazione condizionale complessa. Ora, la prossima volta che incontrerai un colore misterioso in Excel, saprai esattamente come rivelarne i segreti.
## Domande frequenti
### Posso applicare la formattazione condizionale a livello di programmazione utilizzando Aspose.Cells?
Sì, Aspose.Cells consente di applicare, modificare e persino rimuovere la formattazione condizionale nei file Excel a livello di programmazione.
### Aspose.Cells supporta tutte le versioni di Excel?
Assolutamente! Aspose.Cells supporta Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) e altri formati, tra cui PDF, HTML e CSV.
### Aspose.Cells è disponibile anche per piattaforme diverse da .NET?
Sì, Aspose.Cells è disponibile per diverse piattaforme, tra cui Java, C++e Android tramite Java.
### Come posso ottenere una prova gratuita di Aspose.Cells?
 Puoi scaricare una versione di prova gratuita di Aspose.Cells per .NET da[Qui](https://releases.aspose.com/).
### Come posso gestire file Excel di grandi dimensioni con Aspose.Cells?
Aspose.Cells è ottimizzato per le prestazioni, anche quando si tratta di file di grandi dimensioni. Puoi utilizzare le API di streaming per gestire in modo efficiente grandi dati.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
