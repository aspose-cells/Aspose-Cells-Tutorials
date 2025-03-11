---
title: Crea grafico a torta
linktitle: Crea grafico a torta
second_title: API di elaborazione Excel .NET Aspose.Cells
description: Scopri come creare un grafico a torta in Excel usando Aspose.Cells per .NET con questa guida passo-passo. Visualizza i tuoi dati senza sforzo.
weight: 12
url: /it/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crea grafico a torta

## Introduzione

Creare grafici è essenziale per rappresentare visivamente i dati e i grafici a torta sono uno dei modi più popolari per illustrare come le parti costituiscono un tutto. Con Aspose.Cells per .NET, puoi facilmente automatizzare la generazione di grafici a torta nei file Excel. In questo tutorial, approfondiremo come creare un grafico a torta da zero utilizzando Aspose.Cells per .NET, con una guida passo passo per rendere il processo fluido e diretto. Che tu sia un novizio dello strumento o che tu stia cercando di migliorare le tue competenze di automazione Excel, questa guida ti coprirà!

## Prerequisiti

Prima di immergerti nel codice, assicurati di aver impostato quanto segue:

1.  Aspose.Cells per la libreria .NET: assicurati di avere Aspose.Cells installato nel tuo progetto. Se non lo hai ancora installato, puoi scaricarlo da[Qui](https://releases.aspose.com/cells/net/).
2. Ambiente di sviluppo .NET: assicurati che il tuo progetto sia configurato per utilizzare .NET Framework o .NET Core.
3. Conoscenza di base di C#: dovresti avere dimestichezza con la programmazione C#, in particolare con la programmazione orientata agli oggetti (OOP).

 Per gli utenti avanzati, è possibile applicare una licenza temporanea per sbloccare tutte le funzionalità di Aspose.Cells. È possibile richiederne una da[Qui](https://purchase.aspose.com/temporary-license/).

## Importa pacchetti

Per iniziare, importa i namespace e i pacchetti necessari per questo tutorial. Questi includono le operazioni I/O di base e il pacchetto Aspose.Cells.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Passaggio 1: creare una nuova cartella di lavoro

 Per prima cosa, dobbiamo creare un'istanza di`Workbook` classe, che rappresenta il file Excel. Una cartella di lavoro contiene più fogli e, per il nostro esempio, lavoreremo con due fogli, uno per i dati e uno per il grafico a torta.

```csharp
Workbook workbook = new Workbook();
```

Questo inizializza una nuova cartella di lavoro Excel. Ma dove vanno i dati? Ce ne occuperemo nel passaggio successivo.

## Passaggio 2: aggiungere dati al foglio di lavoro

Una volta creata la cartella di lavoro, dobbiamo accedere al primo foglio di lavoro e dargli un nome. È qui che inseriremo i dati richiesti per il grafico a torta.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Ora possiamo inserire alcuni dati di vendita fittizi che rappresentano diverse regioni:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Qui, stiamo aggiungendo due colonne: una per le regioni e un'altra per le cifre di vendita. Questi dati saranno rappresentati nel grafico a torta.

## Passaggio 3: aggiungere un foglio grafico

Ora aggiungiamo un foglio di lavoro separato per contenere il grafico a torta.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Questo nuovo foglio ospiterà il grafico a torta. Dandogli un nome come "Grafico" si garantisce che gli utenti sappiano cosa aspettarsi quando aprono il file.

## Passaggio 4: creare il grafico a torta

Ora è il momento di creare il grafico vero e proprio. Specifichiamo che vogliamo un grafico a torta e definiamo la sua posizione sul foglio.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Il metodo`Add()`accetta parametri per il tipo di grafico (in questo caso,`ChartType.Pie`), e la sua posizione sul foglio di lavoro. I numeri rappresentano le posizioni di riga e colonna.

## Passaggio 5: personalizzare l'aspetto del grafico

Un grafico a torta non sarebbe completo senza un po' di personalizzazione! Rendiamo il nostro grafico visivamente accattivante modificando i colori, le etichette e il titolo.

### Imposta il titolo del grafico
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Personalizza l'area del grafico
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Impostiamo il riempimento sfumato per l'area del grafico e nascondiamo il bordo per un aspetto più pulito.

## Passaggio 6: definire i dati del grafico

 È il momento di collegare il grafico ai nostri dati.`NSeries` proprietà del grafico associa le cifre di vendita e le regioni al grafico a torta.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 La prima riga specifica che stiamo utilizzando i dati di vendita dalle celle`B2:B8` . Diciamo anche al grafico di usare i nomi delle regioni da`A2:A8` come etichette di categoria.

## Passaggio 7: aggiungere etichette dati

Aggiungere etichette direttamente ai segmenti del grafico può renderlo più facile da capire. Includiamo i nomi delle regioni e i valori delle vendite all'interno delle fette del grafico a torta.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Passaggio 8: personalizzare l'area del grafico e la legenda

Infine, diamo qualche ultimo tocco all'area del grafico e alla legenda. Ciò migliora la presentazione complessiva del grafico.

### Area del grafico
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Leggenda
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Passaggio 9: Salvare la cartella di lavoro

Infine, salviamo la cartella di lavoro in un file Excel. Puoi specificare la directory di output e il nome del file a seconda delle tue esigenze.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusione

Creare un grafico a torta con Aspose.Cells per .NET è un processo semplice e personalizzabile. Seguendo questa guida, puoi generare un grafico dall'aspetto professionale che trasmette informazioni preziose in pochi passaggi. Che si tratti di reporting aziendale o scopi educativi, padroneggiare la creazione di grafici migliorerà le tue competenze di automazione Excel. Ricorda, Aspose.Cells fornisce la flessibilità di cui hai bisogno per creare file Excel sbalorditivi e basati sui dati senza sforzo.

## Domande frequenti

### Posso creare altri tipi di grafici utilizzando Aspose.Cells per .NET?
Sì! Aspose.Cells supporta vari tipi di grafici, tra cui grafici a barre, grafici a linee e grafici a dispersione.

### Ho bisogno di una licenza a pagamento per utilizzare Aspose.Cells per .NET?
Puoi usare la versione gratuita con alcune limitazioni. Per le funzionalità complete, avrai bisogno di una licenza, che puoi acquistare[Qui](https://purchase.aspose.com/buy).

### Posso esportare il grafico in formati come PDF o immagini?
Assolutamente! Aspose.Cells consente di esportare grafici in vari formati, tra cui PDF e PNG.

### È possibile decorare ogni fetta di torta con colori diversi?
 Sì, puoi applicare colori diversi a ogni fetta impostando l'`IsColorVaried` proprietà a`true`, come mostrato nel tutorial.

### Posso automatizzare la generazione di più grafici in un'unica cartella di lavoro?
Sì, puoi creare e personalizzare tutti i grafici che desideri all'interno di un singolo file Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
