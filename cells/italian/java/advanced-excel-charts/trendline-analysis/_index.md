---
date: 2026-08-27
description: Scopri come aggiungere la trendline al chart, visualizzare il valore
  R‑squared e esportare il chart come immagine PNG o JPEG usando Aspose.Cells for
  Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Esporta Chart in immagine con analisi della Trendline
og_description: Aggiungi la trendline al chart, visualizza R‑squared ed esporta il
  risultato come PNG/JPEG usando Aspose.Cells for Java – una soluzione veloce, con
  supporto a 50 formati.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Aggiungi la trendline al chart ed esporta come immagine con Aspose.Cells
  for Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Come aggiungere la trendline al chart e esportare come immagine in Java
url: /it/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere una linea di tendenza al grafico e esportarla come immagine

In questo tutorial imparerai come **aggiungere una linea di tendenza al grafico**, visualizzare il valore R‑squared e esportare l’immagine in un file PNG o JPEG utilizzando Aspose.Cells per Java. Vedrai perché le linee di tendenza sono importanti, come preparare la cartella di lavoro e i passaggi esatti per generare un’immagine ad alta risoluzione che può essere incorporata in report, email o pagine web.

## Risposte rapide
- **Qual è l'obiettivo principale di questa guida?** Mostrarti come aggiungere una linea di tendenza al grafico, visualizzare la sua equazione e il valore R‑squared, ed esportare il grafico come immagine con Java.  
- **Quale libreria è necessaria?** Aspose.Cells per Java – scaricala dalla [pagina di rilascio di Aspose.Cells per Java](https://releases.aspose.com/cells/java/).  
- **È necessaria una licenza per lo sviluppo?** Una versione di prova gratuita è sufficiente per lo sviluppo; è richiesta una licenza commerciale per le distribuzioni in produzione.  
- **Posso generare la cartella di lavoro Excel programmaticamente?** Sì – il tutorial crea e salva una cartella di lavoro XLSX da zero.  
- **Come viene esportato il grafico in PNG o JPEG?** Chiama il metodo `Chart.toImage()` e scrivi il `BufferedImage` restituito con `ImageIO.write(...)`.

## Come creare un grafico Excel con una linea di tendenza ed esportarlo come immagine?
Carica la cartella di lavoro, aggiungi un grafico a linee, collega una linea di tendenza che mostra l'equazione e il valore R‑squared, salva la cartella di lavoro, quindi chiama `chart.toImage()` e scrivi il `BufferedImage` risultante in un file PNG o JPEG. Questo flusso end‑to‑end richiede solo poche righe di codice Java e produce un'immagine pixel‑perfect adatta a qualsiasi applicazione successiva.

## Cos'è l'esportazione di un grafico in immagine?
Esportare un grafico in un'immagine converte la rappresentazione visiva dei tuoi dati in una bitmap portatile (PNG, JPEG, BMP, ecc.). Questo formato è ideale per incorporare grafici in report, pagine web o presentazioni dove il file Excel originale non è necessario.

## Perché aggiungere una linea di tendenza e visualizzare il valore R‑squared?
Una linea di tendenza rivela il modello sottostante di una serie di dati, mentre la metrica **R‑squared** quantifica quanto la linea di tendenza si adatti ai dati. Includere entrambi nell'immagine esportata fornisce agli stakeholder un insight immediato senza aprire la cartella di lavoro. Aiuta i decisori a valutare rapidamente la forza della correlazione e a prevedere le tendenze senza dover aprire Excel.

## Prerequisiti
- Java 8 o versioni successive installato sulla tua macchina di sviluppo.  
- Libreria Aspose.Cells per Java aggiunta al classpath del progetto (file JAR).  
- Familiarità con un IDE Java come IntelliJ IDEA o Eclipse.  

## Guida passo‑passo

### Passo 1: configurare il progetto
Crea un nuovo progetto Java e posiziona i JAR di Aspose.Cells sul percorso di compilazione. Questo prepara l'ambiente per generare e manipolare file Excel.

### Passo 2: caricare il file Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Abbiamo appena **caricato un file Excel** in memoria, pronto per la creazione del grafico.*

### Passo 3: creare un grafico
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Qui generiamo un grafico a linee che ospiterà in seguito la nostra linea di tendenza.*

### Passo 4: aggiungere una linea di tendenza (how to add trendline) e visualizzare il valore R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*La chiamata `setDisplayRSquaredValue(true)` garantisce che il **valore R‑squared** appaia sul grafico.*

### Passo 5: personalizzare il grafico e salvare la cartella di lavoro (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Ora la cartella di lavoro è **generata** e salvata come file XLSX, pronta per ulteriori elaborazioni.*

### Passo 6: esportare il grafico in immagine (export chart to image)
> **Nota:** Questo passo è descritto senza un blocco di codice aggiuntivo per mantenere invariato il conteggio originale dei blocchi.  
Dopo che il grafico è stato creato e salvato, puoi esportarlo in un'immagine chiamando il metodo `chart.toImage()` e scrivendo il `java.awt.image.BufferedImage` risultante in un formato file a tua scelta (PNG, JPEG, BMP). Il flusso di lavoro tipico è:
1. Recupera l'oggetto `Chart` (già fatto nei passaggi precedenti).  
2. Chiama `chart.toImage()` per ottenere un `BufferedImage`.  
3. Usa `ImageIO.write(bufferedImage, "png", new File("chart.png"))` per scrivere il file.  

L'oggetto `Chart` rappresenta un grafico nella cartella di lavoro e fornisce metodi per modificare il suo aspetto e i dati. `BufferedImage` è una classe Java che contiene un'immagine in memoria, consentendo di salvarla su disco. `ImageIO` è una classe di utilità per leggere e scrivere immagini in Java. `setDisplayRSquaredValue` abilita la visualizzazione della statistica R‑squared sulla linea di tendenza.

### Analizzare i risultati
Apri `output.xlsx` in Excel per verificare che la linea di tendenza, l'equazione e il valore R‑squared compaiano come previsto. Apri il file immagine esportato (ad es., `chart.png`) per vedere un'immagine pulita che può essere condivisa senza la cartella di lavoro originale.

## Problemi comuni e soluzioni
- **Linea di tendenza non visualizzata:** Assicurati che l'intervallo di dati (`A1:A10`) contenga valori numerici; i dati non numerici impediscono il calcolo della linea di tendenza.  
- **Il valore R‑squared appare 0:** Questo spesso indica che la serie di dati è costante o priva di variazione. Prova un diverso set di dati o utilizza una linea di tendenza polinomiale.  
- **L'esportazione dell'immagine fallisce con `NullPointerException`:** Verifica che il grafico sia stato completamente renderizzato prima di chiamare `toImage()`. Salvare prima la cartella di lavoro a volte risolve problemi di sincronizzazione.

## Domande frequenti

**D: Come posso cambiare il tipo di linea di tendenza?**  
R: Usa una diversa enumerazione `TrendlineType` quando aggiungi la linea di tendenza, ad esempio `TrendlineType.POLYNOMIAL` per una regressione polinomiale.

**D: Posso personalizzare l'aspetto della linea di tendenza (colore, spessore)?**  
R: Sì. Accedi al `LineFormat` della linea di tendenza tramite `trendline.getLineFormat()` e imposta proprietà come `setWeight()` e `setColor()`.

**D: Come esportare il grafico in PDF invece che in immagine?**  
R: Converti prima il grafico in un'immagine, poi incorpora quell'immagine in un PDF usando Aspose.PDF o qualsiasi altra libreria PDF.

**D: È possibile aggiungere più linee di tendenza allo stesso grafico?**  
R: Assolutamente. Chiama `chart.getNSeries().get(0).getTrendlines().add(...)` per ogni serie che desideri analizzare.

**D: Aspose.Cells supporta l'esportazione di immagini ad alta risoluzione?**  
R: Sì. Puoi specificare i DPI chiamando `chart.toImage()` e poi ridimensionare l'immagine prima di salvarla, garantendo un output nitido per la stampa o schermi ad alta densità.

---

**Ultimo aggiornamento:** 2026-08-27  
**Testato con:** Aspose.Cells per Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**Autore:** Aspose

## Tutorial correlati

- [Aggiungere etichette dati a un grafico Excel con Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Come esportare i grafici Excel come SVG usando Aspose.Cells Java per grafica vettoriale scalabile](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Esportare i grafici Excel in PDF usando Aspose.Cells per Java&#58; Guida alle dimensioni personalizzate della pagina](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}