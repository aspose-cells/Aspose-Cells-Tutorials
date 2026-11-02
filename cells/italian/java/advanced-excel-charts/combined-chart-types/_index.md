---
date: 2026-09-02
description: Scopri come esportare un grafico in PNG, aggiungere serie di dati, combinare
  un grafico a linee e colonne, salvare la cartella di lavoro come XLSX e aggiungere
  la legenda al grafico utilizzando Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Esporta il grafico in PNG e aggiungi serie di dati per il grafico combinato
og_description: Esporta un grafico in PNG con Aspose.Cells for Java, combina un grafico
  a linee e colonne, aggiungi serie di dati e salva la cartella di lavoro come XLSX
  in un unico tutorial.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Esporta il grafico in PNG e aggiungi serie di dati per il grafico combinato
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Esporta il grafico in PNG e aggiungi serie di dati per il grafico combinato
url: /it/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Esporta il grafico in PNG e aggiungi serie di dati per un grafico combinato

In questo tutorial **aggiungerai serie di dati** a una cartella di lavoro Excel, **combinerai elementi di grafico a linee e a colonne**, e imparerai come **esportare il grafico in PNG** usando Aspose.Cells per Java. Ti guideremo passo passo—dalla configurazione della cartella di lavoro, all'aggiunta del grafico a un foglio di lavoro, alla personalizzazione della legenda, fino a **salvare la cartella di lavoro come XLSX** e generare un'immagine PNG del grafico. Alla fine, avrai un grafico combinato pronto all'uso che potrai incorporare in report o dashboard.

## Risposte rapide
- **Quale libreria crea grafici combinati?** Aspose.Cells for Java.  
- **Come aggiungo una serie di dati?** Chiama `chart.getNSeries().add(...)` con l'intervallo appropriato.  
- **Come posso esportare il grafico in PNG?** Usa `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **In quale formato file posso salvare la cartella di lavoro?** Standard `.xlsx` (salva la cartella di lavoro come XLSX).  
- **È necessaria una licenza per la produzione?** Sì – è richiesta una licenza valida di Aspose.Cells per le distribuzioni in produzione.

## Cos'è l'esportazione di un grafico in PNG in Aspose.Cells?
Esportare un grafico in PNG crea un'immagine raster del grafico Excel che può essere visualizzata in pagine web, report o email senza richiedere l'applicazione Excel. Questo metodo cattura l'esatta disposizione visiva, i colori e i marcatori dei dati, producendo un file immagine portatile.

## Perché creare un grafico combinato a linee e colonne?
Un grafico combinato a linee e colonne consente di visualizzare diversi set di dati con rappresentazioni visive distinte (ad esempio, una serie a linee sopra una serie a colonne) in un'unica vista. Questo approccio è ideale per confrontare le tendenze con i totali, evidenziare correlazioni o fornire approfondimenti più ricchi mantenendo una piccola impronta visiva.

## Prerequisiti
- Java Development Kit (JDK) 8 o superiore  
- Libreria Aspose.Cells per Java (scarica dal link qui sotto)  
- Familiarità di base con la sintassi Java e i concetti di Excel  

## Iniziare

Prima, scarica la libreria Aspose.Cells per Java dal sito ufficiale:

[Scarica Aspose.Cells per Java](https://releases.aspose.com/cells/java/)

Una volta aggiunto il JAR al classpath del tuo progetto, puoi iniziare a costruire il grafico.

### Passo 1: importa le classi aspose.cells
`Workbook` è l'oggetto principale di Aspose.Cells che rappresenta un intero file Excel in memoria.  
```java
import com.aspose.cells.*;
```

### Passo 2: crea una nuova cartella di lavoro
`Worksheet` rappresenta un singolo foglio all'interno di un `Workbook` e fornisce l'accesso a celle, righe e grafici.  
```java
Workbook workbook = new Workbook();
```

### Passo 3: accedi al primo foglio di lavoro
`Chart` è l'oggetto che contiene tutte le impostazioni relative al grafico, le serie e le opzioni di rendering.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Passo 4: aggiungi un oggetto grafico combinato al foglio di lavoro  
Inizieremo con un grafico a linee e successivamente aggiungeremo una serie a colonne per ottenere l'effetto di un **grafico combinato a linee e colonne**.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Aggiungere dati al grafico

Ora che il contenitore del grafico esiste, dobbiamo alimentarlo con i dati.

### Passo 5: definisci gli intervalli di dati e aggiungi le serie di dati
`NSeries` è la collezione che memorizza ogni serie di dati per un grafico. Aggiungere una serie collega un intervallo di celle al grafico.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Suggerimento:** Il primo parametro (`"A1:A5"`) è l'intervallo per la prima serie, e il secondo (`"B1:B5"`) crea una seconda serie che verrà combinata con la prima.

### Passo 6: imposta i dati della categoria (asse X)
`CategoryAxis` rappresenta l'asse orizzontale del grafico, controllando le etichette visualizzate lungo l'asse X.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizzare il grafico

Un buon grafico racconta una storia. Diamo al grafico titoli, etichette degli assi e una legenda chiara.

### Passo 7: imposta le etichette degli assi del grafico e il titolo
`Title` imposta il titolo principale del grafico, e gli oggetti `Axis` rappresentano gli assi X e Y.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Passo 8: aggiungi la legenda al grafico e regola la sua posizione
`Legend` controlla la posizione e l'aspetto della legenda delle serie nel grafico.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Salvataggio ed esportazione del grafico

Dopo la personalizzazione, vorrai **salvare la cartella di lavoro come XLSX** e generare anche un'immagine.

### Passo 9: salva la cartella di lavoro come file Excel (XLSX)
`Workbook.save` scrive la cartella di lavoro in memoria su un file nel formato specificato.  
```java
workbook.save("CombinedChart.xlsx");
```

### Passo 10: esporta il grafico in PNG
`Chart.toImage` rende il grafico come file immagine nel formato scelto.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Il metodo `chart.toImage` **genera immagini del grafico Excel** che possono essere usate in pagine web, report o email.

## Problemi comuni e risoluzione

| Problema | Soluzione |
|----------|-----------|
| **Nessun dato visualizzato** | Verifica che gli intervalli di celle (`A1:A5`, `B1:B5`, `C1:C5`) contengano effettivamente dati prima di creare il grafico. |
| **La legenda si sovrappone al grafico** | Imposta `chart.getLegend().setOverlay(false)` o sposta la legenda in una posizione diversa (ad es., `RIGHT`). |
| **Il file immagine è vuoto** | Assicurati che il grafico abbia almeno una serie e che `chart.toImage` sia chiamato dopo tutte le personalizzazioni. |
| **Il salvataggio genera un'eccezione** | Verifica di avere i permessi di scrittura sulla directory di destinazione e che il file non sia aperto in Excel. |

## Domande frequenti

**D: Come installo Aspose.Cells per Java?**  
R: Scarica il JAR dal sito ufficiale e aggiungilo al classpath del tuo progetto. Il link per il download è: [Scarica Aspose.Cells per Java](https://releases.aspose.com/cells/java/).

**D: Posso creare altri tipi di grafico oltre a linee e colonne?**  
R: Sì, Aspose.Cells supporta grafici a barre, a torta, a dispersione, ad area e molti altri tipi di grafico. Consulta la documentazione API per l'elenco completo.

**D: È necessaria una licenza per l'uso in produzione?**  
R: È richiesta una licenza valida di Aspose.Cells per le distribuzioni in produzione. È disponibile una prova gratuita per la valutazione.

**D: Come posso cambiare i colori di ogni serie?**  
R: Usa `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (o simile) dopo aver aggiunto le serie.

**D: Dove posso trovare altri esempi di codice?**  
R: Documentazione completa e ulteriori esempi sono disponibili sul sito di riferimento Aspose: [Documentazione di riferimento Aspose Cells Java](https://reference.aspose.com/cells/java/).

---

**Ultimo aggiornamento:** 2026-09-02  
**Testato con:** Aspose.Cells per Java ultima versione  
**Autore:** Aspose

## Tutorial correlati

- [Come aggiungere etichette ai grafici Excel usando Aspose.Cells per Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Come creare un grafico Excel con linea di tendenza ed esportarlo in immagine usando Aspose.Cells per Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Esporta grafici Excel in PDF usando Aspose.Cells per Java: Guida alle dimensioni personalizzate della pagina](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}