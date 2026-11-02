---
date: '2026-04-08'
description: Impara a generare un grafico a colonne in Java usando Aspose.Cells, coprendo
  la creazione del grafico in Java, l'aggiunta di un foglio grafico e l'esportazione
  della cartella di lavoro Excel.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Genera grafico a colonne con il tutorial Aspose.Cells Java
url: /it/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Genera un grafico a colonne con Aspose.Cells Java

Nelle applicazioni odierne guidate dai dati, **generating a column chart** rapidamente e in modo programmatico può trasformare numeri grezzi in chiare intuizioni visive. Che tu stia costruendo un cruscotto di reporting, uno strumento di analisi o una semplice funzionalità di esportazione, Aspose.Cells per Java ti offre un'API fluida per **create chart java** progetti senza dover interagire con l'interfaccia di Excel. In questo tutorial imparerai come configurare la libreria, **populate Excel cells**, aggiungere un **chart sheet**, personalizzare il **chart title** e infine **export workbook excel** in un file.

## Risposte rapide
- **Che cosa significa “generate column chart”?** Crea una visualizzazione a barre verticali a partire da dati tabulari.  
- **Quale libreria è necessaria?** Aspose.Cells for Java (prova gratuita disponibile).  
- **Ho bisogno di un'installazione di Excel?** No, la libreria funziona indipendentemente da Microsoft Excel.  
- **Posso esportare in formati diversi da XLS?** Sì – PDF, PNG, SVG, ecc., tramite `workbook.save()`.  
- **È obbligatoria una licenza per la produzione?** Sì, è necessaria una licenza acquistata o temporanea.

## Cos'è un grafico a colonne?
Un grafico a colonne visualizza le serie di dati come barre verticali, facilitando il confronto dei valori tra categorie come regioni, mesi o linee di prodotto. Aspose.Cells ti consente di costruire questo grafico interamente via codice, offrendoti il pieno controllo su dati, stile e formato di output.

## Perché usare Aspose.Cells per create chart java?
- **No COM interop** – funziona su qualsiasi OS con una JVM.  
- **Rich styling options** – immagini, gradienti, legende e font personalizzati.  
- **High performance** – adatto a grandi set di dati.  
- **Multiple export formats** – XLS, XLSX, PDF, PNG e altro.

## Prerequisiti
- **Java Development Kit (JDK) 8+** installato.  
- Conoscenza di base di Java e familiarità con i concetti di Excel.

### Librerie richieste
Aggiungi Aspose.Cells al tuo progetto usando uno dei frammenti qui sotto.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Acquisizione licenza
Aspose offre una prova gratuita e una licenza temporanea per test approfonditi.

- **Prova gratuita**: [Scarica gratuito](https://releases.aspose.com/cells/java/)  
- **Licenza temporanea**: [Richiedi qui](https://purchase.aspose.com/temporary-license/)

## Configurazione di Aspose.Cells per Java

Per prima cosa, crea un'istanza di `Workbook` – sarà la tela per i nostri dati e il grafico.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Guida passo‑passo

### 1. Crea e nomina un foglio di lavoro
Memorizzeremo i dati grezzi in un foglio chiamato **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Popola le celle di Excel
Inserisci i nomi delle regioni e le cifre di vendita che il grafico a colonne visualizzerà.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Aggiungi un foglio di grafico
Separare il grafico dai dati grezzi mantiene il workbook ordinato.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Crea un grafico a colonne
Ora creiamo effettivamente gli oggetti **generate column chart**.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Imposta immagine come riempimento di sfondo nell'area del grafico
Un'immagine di sfondo può far risaltare il grafico.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Imposta il titolo del grafico
Personalizzare il **set chart title** migliora la leggibilità.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Configura i dati della serie e la legenda
Collega l'intervallo di dati al grafico e posiziona la legenda.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Esporta il workbook Excel
Infine, **export workbook excel** in un file XLS (o in qualsiasi formato supportato).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Applicazioni pratiche
- **Business Reports** – Genera automaticamente grafici di vendite per PDF mensili.  
- **Data Analysis Tools** – Inserisci grafici dinamici in cruscotti di analisi personalizzati.  
- **Enterprise Dashboards** – Aggiorna le immagini dei grafici al volo per il monitoraggio in tempo reale.

## Considerazioni sulle prestazioni
- Aggiorna le celle in batch quando lavori con grandi set di dati per ridurre l'overhead.  
- Rilascia le risorse (`workbook.dispose()`) se elabori molti workbook in un ciclo.  

## Problemi comuni e soluzioni
- **Image not showing** – Verifica il percorso del file e che il formato immagine (PNG, JPEG) sia supportato.  
- **Chart appears blank** – Assicurati che i riferimenti dell'intervallo di dati (`Data!B2:B8`) corrispondano alle celle popolate.  
- **Out‑of‑memory errors** – Elabora i dati a blocchi e chiama `System.gc()` dopo salvataggi di grandi dimensioni.

## Domande frequenti

**Q: Come aggiungere più serie a un grafico a colonne?**  
A: Chiama `chart.getNSeries().add()` ripetutamente con diversi intervalli di dati, ad esempio, `"Data!C2:C8"` per una seconda serie.

**Q: Posso cambiare le etichette degli assi?**  
A: Sì. Usa `chart.getCategoryAxis().setTitle("Regions")` e `chart.getValueAxis().setTitle("Sales")`.

**Q: Quali formati posso esportare oltre a XLS?**  
A: Usa `workbook.save("chart.pdf")`, `workbook.save("chart.png")` o `workbook.save("chart.xlsx")` per PDF, PNG e XLSX rispettivamente.

**Q: È necessaria una licenza per le build di sviluppo?**  
A: Una prova gratuita funziona per la valutazione, ma è necessaria una licenza permanente o temporanea per le distribuzioni in produzione.

**Q: Come posso migliorare la velocità di rendering per migliaia di righe?**  
A: Popola le celle usando `cells.importArray()` e riduci i ridisegni del grafico creando il grafico solo dopo aver caricato tutti i dati.

---

**Last Updated:** 2026-04-08  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

## Risorse

- [Documentazione Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Scarica Aspose.Cells](https://releases.aspose.com/cells/java/)
- [Acquista una licenza](https://purchase.aspose.com/buy)
- [Prova gratuita](https://releases.aspose.com/cells/java/)
- [Richiesta licenza temporanea](https://purchase.aspose.com/temporary-license/)
- [Forum di supporto](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}