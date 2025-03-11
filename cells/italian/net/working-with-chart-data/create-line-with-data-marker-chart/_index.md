---
title: Crea una linea con il grafico dei marcatori dei dati
linktitle: Crea una linea con il grafico dei marcatori dei dati
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come creare un grafico Line with Data Markers in Excel usando Aspose.Cells per .NET. Segui questa guida passo passo per generare e personalizzare facilmente i grafici.
weight: 10
url: /it/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea una linea con il grafico dei marcatori dei dati

## Introduzione

Ti sei mai chiesto come creare grafici sbalorditivi in Excel a livello di programmazione? Bene, allacciati le cinture, perché oggi ci immergiamo nella creazione di un grafico Line with Data Marker usando Aspose.Cells per .NET. Questo tutorial ti guiderà attraverso ogni passaggio, assicurandoti di avere una solida conoscenza della generazione di grafici, anche se hai appena iniziato con Aspose.Cells.

## Prerequisiti

Prima di iniziare, assicurati di avere tutto a posto per procedere senza intoppi.

1. Aspose.Cells per la libreria .NET – Dovrai installarla. Puoi scaricarla[Qui](https://releases.aspose.com/cells/net/).
2. .NET Framework: assicurati che il tuo ambiente di sviluppo sia configurato con la versione più recente di .NET.
3. IDE (Integrated Development Environment): si consiglia Visual Studio.
4.  Una licenza Aspose.Cells valida: se non ne hai una, puoi richiederne una[licenza temporanea](https://purchase.aspose.com/temporary-license/) o dai un'occhiata al loro[prova gratuita](https://releases.aspose.com/).

Pronti a partire? Analizziamolo nel dettaglio!

## Importazione dei pacchetti necessari

Per iniziare, assicurati di importare i seguenti namespace nel tuo progetto. Questi forniranno le classi e i metodi necessari per creare il tuo grafico.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Una volta capito questo, possiamo iniziare a programmare!

## Passaggio 1: imposta la cartella di lavoro e il foglio di lavoro

Per prima cosa, devi creare una nuova cartella di lavoro e accedere al primo foglio di lavoro.

```csharp
//Directory di output
static string outputDir = "Your Document Directory";
		
// Creare un'istanza di una cartella di lavoro
Workbook workbook = new Workbook();

// Accedi al primo foglio di lavoro
Worksheet worksheet = workbook.Worksheets[0];
```

Pensa alla cartella di lavoro come al tuo file Excel e al foglio di lavoro come al foglio specifico al suo interno. In questo caso, stiamo lavorando con il primo foglio.

## Passaggio 2: popolare il foglio di lavoro con i dati

Ora che abbiamo il nostro foglio di lavoro, riempiamolo con alcuni dati. Stiamo creando punti dati casuali per due serie di valori.

```csharp
// Imposta il titolo delle colonne
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Dati casuali per la generazione del grafico
Random R = new Random();

// Crea dati casuali e salvali nelle celle
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Qui utilizziamo numeri casuali per simulare i dati, ma nelle applicazioni reali è possibile inserirvi valori effettivi dal proprio set di dati.

## Passaggio 3: aggiungere il grafico al foglio di lavoro

Successivamente, aggiungiamo il grafico al foglio di lavoro e scegliamo il tipo, in questo caso un grafico a linee con indicatori di dati.

```csharp
// Aggiungere un grafico al foglio di lavoro
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Accedi al grafico appena creato
Chart chart = worksheet.Charts[idx];
```

Questo frammento aggiunge un grafico a linee con marcatori di dati al foglio di lavoro, posizionandolo in un intervallo specifico (da 1,3 a 20,20). Semplice, vero?

## Passaggio 4: personalizzare l'aspetto del grafico

Una volta creato il grafico, puoi personalizzarlo a tuo piacimento. Cambiamo lo sfondo, il titolo e lo stile del grafico.

```csharp
// Imposta lo stile del grafico
chart.Style = 3;

// Imposta il valore di ridimensionamento automatico su vero
chart.AutoScaling = true;

// Imposta il colore di primo piano su bianco
chart.PlotArea.Area.ForegroundColor = Color.White;

//Imposta le proprietà del titolo del grafico
chart.Title.Text = "Sample Chart";

// Imposta il tipo di grafico
chart.Type = ChartType.LineWithDataMarkers;
```

Qui diamo al grafico un aspetto pulito impostando uno sfondo bianco, applicando il ridimensionamento automatico e assegnandogli un titolo significativo.

## Passaggio 5: definire le serie e tracciare i punti dati

Ora che il nostro grafico è pronto, dobbiamo definire le serie di dati che verranno tracciate.

```csharp
// Imposta le proprietà del titolo dell'asse della categoria
chart.CategoryAxis.Title.Text = "Units";

// Definisci due serie per il grafico
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Queste serie corrispondono agli intervalli di punti dati che abbiamo popolato in precedenza.

## Passaggio 6: aggiungere colori e personalizzare i marcatori di serie

Rendiamo questo grafico ancora più accattivante aggiungendo colori personalizzati ai nostri marcatori di dati.

```csharp
// Personalizza la prima serie
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Personalizza la seconda serie
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Personalizzando i colori, il grafico non sarà solo funzionale, ma anche visivamente accattivante!

## Passaggio 7: impostare i valori X e Y per ciascuna serie

Infine, assegniamo i valori X e Y a ciascuna delle nostre serie.

```csharp
// Imposta i valori X e Y della prima serie
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Imposta i valori X e Y della seconda serie
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

valori si basano sui dati che abbiamo inserito nel passaggio 2.

## Passaggio 8: salvare la cartella di lavoro

Ora che tutto è impostato, salviamo la cartella di lavoro, così possiamo vedere il grafico in azione.

```csharp
// Salvare la cartella di lavoro
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Ed ecco fatto! Hai appena creato un grafico a linee con marcatori di dati usando Aspose.Cells per .NET.

## Conclusione

Creare grafici a livello di programmazione in Excel può sembrare scoraggiante, ma con Aspose.Cells per .NET è facile come seguire una ricetta passo dopo passo. Dall'impostazione della cartella di lavoro alla personalizzazione dell'aspetto del grafico, questa potente libreria gestisce tutto. Che tu stia creando report, dashboard o visualizzazioni di dati, Aspose.Cells ti consente di farlo in un attimo.

## Domande frequenti

### Posso personalizzare ulteriormente il grafico?  
Assolutamente! Aspose.Cells offre un sacco di opzioni di personalizzazione, dai font alle griglie e altro ancora.

### Ho bisogno di una licenza per utilizzare Aspose.Cells?  
 Sì, è richiesta una licenza per la piena funzionalità. Puoi ottenere una[licenza temporanea](https://purchase.aspose.com/temporary-license/) o iniziare con un[prova gratuita](https://releases.aspose.com/).

### Come posso aggiungere altre serie di dati?  
 Basta aggiungere altre serie utilizzando il`NSeries.Add` metodo, specificando gli intervalli di celle per i nuovi dati.

### Posso esportare il grafico come immagine?  
 Sì, puoi esportare i grafici direttamente come immagini utilizzando`Chart.ToImage` metodo.

### Aspose.Cells supporta grafici 3D?  
Sì, Aspose.Cells supporta un'ampia gamma di tipi di grafici, inclusi i grafici 3D.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
