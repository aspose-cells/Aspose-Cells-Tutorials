---
date: '2026-09-27'
description: Scopri come creare un pie chart java usando Aspose.Cells. Guida step‑by‑step
  per personalizzare il pie chart di Excel, configurare la dipendenza Maven e generare
  grafici professionali.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Crea un pie chart java usando Aspose.Cells per Java. Scopri come personalizzare
  il pie chart di Excel, aggiungere la dipendenza Maven e generare grafici professionali
  in pochi minuti.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Crea un pie chart java con Aspose.Cells – Guida completa Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Come creare un pie chart java con Aspose.Cells
url: /it/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare un grafico a torta java con Aspose.Cells

## Introduzione
Creare un **grafico a torta** programmaticamente spesso sembra un puzzle, soprattutto quando è necessario un controllo dettagliato su colori, legende e titoli. In questa guida imparerai come **creare un grafico a torta java** usando Aspose.Cells, per poi personalizzare il grafico a torta di Excel in modo da corrispondere al tuo brand o allo stile di reporting. Percorreremo la configurazione dell'ambiente, il popolamento dei dati, la generazione del grafico e le regolazioni visive—tutto senza uscire dal tuo IDE Java.

**Cosa imparerai**
- Aggiungi la **dipendenza Maven Aspose.Cells** al tuo progetto.
- Crea una cartella di lavoro, riempi le celle con i dati e genera un grafico a torta.
- Applica colori personalizzati, titoli e legende al grafico.
- Esporta la cartella di lavoro in un file XLSX pronto per la condivisione.

Prima di iniziare, dovresti avere familiarità con la sintassi di base di Java e avere Maven o Gradle installati.

## Risposte rapide
- **Quale libreria crea grafici a torta in Java?** Aspose.Cells for Java.
- **Ho bisogno di una licenza?** Una versione di prova gratuita funziona per lo sviluppo; è necessaria una licenza a pagamento per la produzione.
- **Quali coordinate Maven sono richieste?** `com.aspose:aspose-cells:24.10`.
- **Posso cambiare i colori delle fette?** Sì, tramite il metodo `setAreaColor` su ogni serie.
- **Il grafico è esportabile in XLSX?** Assolutamente—basta chiamare `workbook.save("output.xlsx")`.

## Cos'è un grafico a torta in Excel?
Un grafico a torta visualizza una singola serie di dati come fette proporzionali di un cerchio, facilitando il confronto delle parti di un tutto. L'angolo di ciascuna fetta corrisponde al suo valore rispetto al totale, consentendo una rapida comprensione della distribuzione tra categorie come quota di mercato, allocazione del budget o percentuali demografiche.

## Perché usare Aspose.Cells per creare un grafico a torta java?
Aspose.Cells supporta oltre 50 tipi di grafico e può gestire fogli di lavoro con fino a un milione di righe senza caricare l'intero file in memoria. Questo vantaggio di prestazioni ti consente di generare grandi report su hardware modesto, offrendo al contempo un controllo dettagliato sull'aspetto del grafico, sul binding dei dati e sui formati di esportazione, rendendolo una scelta superiore rispetto a molte librerie open‑source.

## Prerequisiti
- **Java Development Kit (JDK)** 8 o superiore.
- **IDE** come IntelliJ IDEA o Eclipse.
- **Maven** o **Gradle** per la gestione delle dipendenze.
- Una licenza Aspose.Cells di **prova o acquistata**.

### Librerie e dipendenze richieste
Aggiungi l'artifact Maven di Aspose.Cells al tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Oppure l'equivalente Gradle:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Passaggi per l'acquisizione della licenza
Aspose.Cells per Java è commerciale, ma puoi iniziare con una versione di prova gratuita. Visita la [pagina di acquisto](https://purchase.aspose.com/buy) per ottenere una chiave di licenza temporanea.

## Configurazione di Aspose.Cells per Java
Prima di tutto, assicurati che la libreria sia nel tuo classpath. Dopo aver aggiunto la dipendenza, puoi inizializzare l'API come mostrato di seguito.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Guida all'implementazione

### Creare e configurare una cartella di lavoro
La classe `Workbook` rappresenta un intero file Excel in memoria.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Passo 1: istanziare una cartella di lavoro
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Questo crea una nuova cartella di lavoro vuota che puoi subito iniziare a popolare.

### Accedere o modificare le celle del foglio di lavoro
Un `Worksheet` rappresenta un singolo foglio all'interno della cartella di lavoro, contenente celle, righe e colonne.  
Scriverai i dati che alimentano il grafico a torta in un foglio di lavoro.

#### Passo 2: ottenere il primo foglio di lavoro e le sue celle
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Popola le celle con i nomi delle categorie e i valori che il grafico utilizzerà.

### Creare un grafico a torta
Gli oggetti `Chart` visualizzano i dati in un foglio di lavoro e supportano vari tipi come torta, colonna e linea.

#### Passo 3: aggiungere un grafico a torta al foglio di lavoro
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Configurare le serie e i dati del grafico a torta
`Series` definisce l'intervallo di dati e la formattazione per un grafico, collegando le celle del foglio di lavoro agli elementi visivi.

#### Passo 4: impostare le serie per il grafico
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Configurare l'aspetto della leggenda e del titolo del grafico
Una `Legend` del grafico mostra i nomi delle serie e i colori, aiutando i lettori a identificare ogni fetta.

#### Passo 5: personalizzare la leggenda e il titolo del grafico
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Personalizzare i colori delle serie del grafico
`setAreaColor` imposta il colore di riempimento di una fetta della serie del grafico usando un valore RGB.

#### Passo 6: cambiare i colori dei segmenti della torta
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Adattare automaticamente le colonne e salvare la cartella di lavoro
`autoFitColumns` regola automaticamente la larghezza delle colonne per adattarsi al contenuto delle celle.

#### Passo 7: regolare la larghezza delle colonne e salvare il file
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Casi d'uso comuni
- **Analisi demografica:** mostrare la distribuzione della popolazione tra le regioni.
- **Report sulla quota di mercato:** visualizzare la quota di ciascun concorrente in un colpo d'occhio.
- **Allocazione del budget:** evidenziare come i fondi sono suddivisi tra i dipartimenti.

## Considerazioni sulle prestazioni
- Rilascia gli oggetti (`workbook.dispose()`) quando non sono più necessari per liberare la memoria nativa.
- Per set di dati massivi, usa `WorkbookDesigner` per trasmettere i dati invece di caricarli tutti in una volta.
- Esegui il profiling con Java Flight Recorder per individuare eventuali colli di bottiglia nella generazione del grafico.

## Domande frequenti

**D: Posso generare più grafici a torta nello stesso workbook?**  
R: Sì, ripeti i passaggi di creazione del grafico per ogni intervallo di dati; ogni grafico è indipendente.

**D: Aspose.Cells supporta grafici a torta 3‑D?**  
R: Sì; imposta il tipo di grafico su `ChartType.PIE_3D` quando aggiungi il grafico.

**D: Come applico un tema personalizzato a tutti i grafici?**  
R: Usa il metodo `Workbook.setDefaultTheme` prima di creare qualsiasi grafico.

**D: In quali formati posso esportare il workbook?**  
R: Oltre 30 formati, inclusi XLSX, CSV, PDF e HTML.

**D: È necessaria una licenza per il deployment commerciale?**  
R: Sì, una licenza valida rimuove i watermark di valutazione e sblocca tutte le funzionalità.

## Conclusione
Ora hai una ricetta completa, end‑to‑end, per **creare un grafico a torta java** con Aspose.Cells. Seguendo i passaggi sopra potrai generare grafici a torta Excel curati, personalizzare colori e titoli e integrarli in qualsiasi pipeline di reporting. Esplora altri tipi di grafico—colonna, linea, radar—per ampliare il tuo toolkit di visualizzazione dei dati.

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## Tutorial correlati

- [Customize Excel Chart Data Labels Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Create and Customize Excel Workbooks Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}