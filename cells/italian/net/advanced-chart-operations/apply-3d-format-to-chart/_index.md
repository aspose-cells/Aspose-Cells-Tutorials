---
title: Applica il formato 3D al grafico
linktitle: Applica il formato 3D al grafico
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come creare grafici 3D sbalorditivi in Excel usando Aspose.Cells per .NET. Segui la nostra semplice guida passo dopo passo.
weight: 10
url: /it/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Applica il formato 3D al grafico

## Introduzione

In un'epoca in cui la visualizzazione dei dati è fondamentale, il modo in cui presentiamo i nostri dati va oltre grafici e diagrammi di base. Con strumenti come Aspose.Cells per .NET, puoi migliorare le tue presentazioni di dati con straordinari grafici 3D che non solo catturano l'attenzione, ma trasmettono anche informazioni in modo efficace. Questa guida ti guiderà attraverso i passaggi per applicare un formato 3D a un grafico utilizzando Aspose.Cells, trasformando i tuoi dati grezzi in una visualizzazione accattivante.

## Prerequisiti

Prima di addentrarci nei dettagli dell'applicazione di un formato 3D a un grafico, assicuriamoci di avere tutto il necessario.

### Requisiti software

- Visual Studio: assicurati di aver installato Visual Studio per lavorare con le applicazioni .NET.
-  Aspose.Cells per .NET: se non l'hai ancora fatto, scarica e installa Aspose.Cells da[Qui](https://releases.aspose.com/cells/net/).

### Impostazione dell'ambiente di codifica

1. Crea un nuovo progetto .NET: apri Visual Studio, seleziona "Crea un nuovo progetto" e scegli un'applicazione console.
2. Aggiungere il riferimento ad Aspose.Cells: tramite NuGet Package Manager, aggiungere Aspose.Cells cercandolo o tramite la Package Manager Console:

```bash
Install-Package Aspose.Cells
```

3. Imposta directory di output: designa una directory di output in cui verranno salvati i file generati. Può trattarsi semplicemente di creare una cartella sul desktop.

Ora che hai impostato tutto, è il momento di passare al codice e creare dei fantastici grafici 3D!

## Importa pacchetti

Per iniziare, devi importare i namespace necessari. Questo ti aiuterà ad accedere alle classi e ai metodi forniti da Aspose.Cells. Ecco come fare:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Questa sezione suddividerà il processo in passaggi gestibili, fornendoti una chiara comprensione di ciascuna fase.

## Passaggio 1: inizializza la tua cartella di lavoro

 Per prima cosa, devi creare un'istanza di`Workbook` classe. Questo oggetto servirà come base per il tuo documento Excel.

```csharp
//Directory di output
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Pensa a questo`Workbook` come una tela bianca, pronta per essere riempita con dati colorati e visualizzazioni d'impatto.

## Passaggio 2: rinominare il primo foglio di lavoro

Ora, rinominiamo il primo foglio di lavoro. Questo fornisce chiarezza sui dati con cui stiamo lavorando.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

I nomi dovrebbero essere intuitivi. In questo caso, lo chiameremo "DataSheet" così sappiamo dove risiedono i nostri dati.

## Passaggio 3: creare i dati per il grafico

Ora aggiungeremo alcuni dati al nostro "DataSheet". Popoliamolo con i valori che verranno utilizzati nel nostro grafico.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Proprio come una ricetta dipende dagli ingredienti, l'efficacia del tuo grafico dipende dalla qualità e dall'organizzazione dei dati di input.

## Passaggio 4: imposta un nuovo foglio di lavoro grafico

È il momento di creare un nuovo foglio di lavoro per il grafico stesso. Questo aiuta a mantenere organizzata la visualizzazione dei dati.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Considera questo foglio di lavoro come il tuo palcoscenico, dove si sviluppano le prestazioni dei tuoi dati.

## Passaggio 5: aggiungere un grafico

Qui aggiungeremo un grafico a colonne al foglio di lavoro appena creato.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Stiamo definendo uno spazio per il nostro grafico e specificando di che tipo è. Immagina di selezionare il tipo di cornice per la tua opera d'arte.

## Passaggio 6: personalizzare l'aspetto del grafico

Adesso personalizziamo l'aspetto del nostro grafico impostando i colori di sfondo. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

Uno sfondo bianco pulito spesso fa risaltare i colori dei dati, migliorandone la visibilità.

## Passaggio 7: aggiungere serie di dati al grafico

È il momento di alimentare il nostro grafico con i dati. Aggiungeremo una serie di dati dal nostro "DataSheet" per assicurarci che il nostro grafico rifletta i dati di cui abbiamo bisogno.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Ciò è analogo a uno chef che prepara un piatto con ingredienti specifici. Ogni punto dati è importante!

## Passaggio 8: accedere e formattare la serie di dati

Ora che abbiamo collegato i nostri dati, prendiamo la serie di dati e iniziamo ad applicare alcuni effetti 3D.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Ci stiamo preparando ad aggiungere un tocco di stile al nostro piatto: pensiamolo come un condimento che ne esalta il sapore generale.

## Passaggio 9: applicare effetti smussati 3D

Successivamente aggiungeremo un effetto smussato per dare una certa dimensione al nostro grafico.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Proprio come uno scultore modella la pietra, noi creiamo la profondità che dà vita al nostro grafico!

## Fase 10: personalizzare il materiale della superficie e l'illuminazione

Facciamo risplendere il nostro grafico! Regoleremo il materiale della superficie e le impostazioni di illuminazione.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

L'illuminazione e il materiale giusti possono trasformare un oggetto piatto in un'immagine accattivante. Pensa a un set cinematografico illuminato in modo esperto per valorizzare ogni scena.

## Fase 11: Ritocchi finali all'aspetto della serie

Ora possiamo finalizzare l'aspetto della nostra serie di dati modificandone il colore.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Il colore giusto può evocare determinati sentimenti e reazioni: il marrone aggiunge un tocco di eleganza e raffinatezza.

## Passaggio 12: salva la tua cartella di lavoro

Infine, è il momento di salvare il tuo capolavoro! Non dimenticare di specificare la destinazione in cui vuoi salvarlo.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Salvare il tuo lavoro è come esporre la tua arte in una galleria: è un momento da custodire e condividere.

## Conclusione

Congratulazioni! Hai creato con successo un grafico 3D visivamente accattivante utilizzando Aspose.Cells per .NET. Seguendo questi passaggi, ora hai uno strumento potente per migliorare le tue presentazioni di dati, rendendole non solo informative ma anche visivamente accattivanti. Mentre perfezioni i tuoi grafici, ricorda che ogni visualizzazione è una storia: rendila coinvolgente, chiara e d'impatto!

## Domande frequenti

### Che cos'è Aspose.Cells per .NET?
Aspose.Cells per .NET è una potente libreria che consente agli sviluppatori di manipolare i documenti Excel a livello di programmazione, inclusa la creazione di grafici e diagrammi.

### Posso personalizzare i tipi di grafico in Aspose.Cells?
Sì! Aspose.Cells supporta vari tipi di grafici come Colonna, Linea, Torta e molti altri, che possono essere facilmente personalizzati.

### È disponibile una prova gratuita per Aspose.Cells?
 Assolutamente! Puoi scaricare una prova gratuita da[Qui](https://releases.aspose.com/).

### Posso applicare altri effetti ai grafici oltre ai formati 3D?
Sì, puoi applicare vari effetti, come ombre, sfumature e stili diversi, per migliorare i tuoi grafici oltre il 3D.

### Dove posso trovare supporto per Aspose.Cells?
 Per supporto, puoi visitare il[Forum di Aspose](https://forum.aspose.com/c/cells/9) per assistenza e aiuto alla comunità.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
