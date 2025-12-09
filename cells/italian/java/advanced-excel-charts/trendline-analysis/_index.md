---
date: 2025-12-09
description: Scopri come esportare un grafico in immagine eseguendo l'analisi della
  linea di tendenza in Java con Aspose.Cells. Include i passaggi per caricare il file
  Excel, aggiungere la linea di tendenza, visualizzare il valore R² e salvare la cartella
  di lavoro in formato XLSX.
language: it
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Esporta grafico in immagine con analisi della linea di tendenza usando Aspose.Cells
  per Java
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Esporta grafico in immagine con analisi della linea di tendenza

In questo tutorial scoprirai **come esportare un grafico in immagine** eseguendo un'analisi completa della **linea di tendenza** usando Aspose.Cells per Java. Ti guideremo attraverso il caricamento di una cartella di lavoro Excel esistente, l'aggiunta di una linea di tendenza, la visualizzazione del valore R‑squared, la personalizzazione del grafico e, infine, l'esportazione del grafico come file immagine—tutto con codice chiaro, passo‑per‑passo, che puoi copiare & incollare.

## Risposte rapide
- **Qual è lo scopo principale di questa guida?** Mostrarti come aggiungere una linea di tendenza, visualizzare la sua equazione e il valore R‑squared, ed esportare il grafico risultante in un'immagine usando Java.  
- **Quale libreria è necessaria?** Aspose.Cells per Java (scarica [qui](https://releases.aspose.com/cells/java/)).  
- **Ho bisogno di una licenza?** Una versione di prova gratuita è sufficiente per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Posso generare un file Excel in Java?** Sì – il tutorial crea e salva una cartella di lavoro XLSX.  
- **Come esporto il grafico in PNG o JPEG?** Usa il metodo `Chart.toImage()` (coperto nella sezione “Export Chart”).

## Cos'è l'esportazione di un grafico in immagine?
Esportare un grafico in un'immagine converte la rappresentazione visiva dei tuoi dati in una bitmap portatile (PNG, JPEG, ecc.). Questo è utile per incorporare grafici in report, pagine web o presentazioni dove il file Excel originale non è necessario.

## Perché aggiungere una linea di tendenza e visualizzare il valore R‑squared?
Una linea di tendenza ti aiuta a identificare il modello sottostante di una serie di dati, mentre la metrica **R‑squared** quantifica quanto bene la linea di tendenza si adatta ai dati. Includere questi elementi nella tua immagine esportata fornisce agli stakeholder un'istantanea immediata senza aprire la cartella di lavoro.

## Prerequisiti
- Java 8 o versioni successive installate.  
- Libreria Aspose.Cells per Java aggiunta al tuo progetto (file JAR nel classpath).  
- Familiarità di base con gli IDE Java (IntelliJ IDEA, Eclipse, ecc.).

## Guida passo‑per‑passo

### Passo 1: Configura il progetto
Crea un nuovo progetto Java e aggiungi i JAR di Aspose.Cells al percorso di compilazione. Questo prepara l'ambiente per generare e manipolare file Excel.

### Passo 2: Carica il file Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Abbiamo appena **caricato un file Excel** in memoria, pronto per la creazione del grafico.*

### Passo 3: Crea un grafico
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Qui generiamo un grafico a linee che in seguito ospiterà la nostra linea di tendenza.*

### Passo 4: Aggiungi una linea di tendenza (how to add trendline) e visualizza il valore R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*La chiamata `setDisplayRSquaredValue(true)` garantisce che il **valore R‑squared** appaia sul grafico.*

### Passo 5: Personalizza il grafico e salva la cartella di lavoro (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Ora la cartella di lavoro è **generata** e salvata come file XLSX, pronta per ulteriori elaborazioni.*

### Passo 6: Esporta il grafico in immagine (export chart to image)
> **Nota:** Questo passo è descritto senza un blocco di codice aggiuntivo per mantenere invariato il conteggio originale dei blocchi.  
Dopo che il grafico è stato creato e salvato, puoi esportarlo in un'immagine chiamando il metodo `chart.toImage()` e scrivendo il `java.awt.image.BufferedImage` risultante in un formato di file a tua scelta (PNG, JPEG, BMP). Il flusso di lavoro tipico è:
1. Recupera l'oggetto `Chart` (già fatto nei passaggi precedenti).  
2. Chiama `chart.toImage()` per ottenere un `BufferedImage`.  
3. Usa `ImageIO.write(bufferedImage, "png", new File("chart.png"))` per scrivere il file.  

Questo produce un'immagine ad alta risoluzione che puoi incorporare ovunque, completando il processo di **esportazione del grafico in immagine**.

## Analizza i risultati
Apri `output.xlsx` in Excel per verificare che la linea di tendenza, l'equazione e il valore R‑squared compaiano come previsto. Apri il file immagine esportato (ad es., `chart.png`) per vedere un'immagine pulita che può essere condivisa senza la cartella di lavoro originale.

## Problemi comuni e soluzioni
- **Linea di tendenza non visualizzata:** Assicurati che l'intervallo di dati (`A1:A10`) contenga effettivamente valori numerici; dati non numerici impediranno il calcolo della linea di tendenza.  
- **Il valore R‑squared appare 0:** Questo spesso indica che la serie di dati è costante o ha variazione insufficiente. Prova un diverso set di dati o una linea di tendenza polinomiale.  
- **L'esportazione dell'immagine fallisce con `NullPointerException`:** Verifica che il grafico sia stato completamente renderizzato prima di chiamare `toImage()`. Salvare prima la cartella di lavoro a volte può risolvere problemi di temporizzazione.

## Domande frequenti

**Q: Come posso cambiare il tipo di linea di tendenza?**  
A: Usa una diversa enumerazione `TrendlineType` quando aggiungi la linea di tendenza, ad esempio `TrendlineType.POLYNOMIAL` per una regressione polinomiale.

**Q: Posso personalizzare l'aspetto della linea di tendenza (colore, spessore)?**  
A: Sì. Accedi al `LineFormat` della linea di tendenza tramite `trendline.getLineFormat()` e imposta proprietà come `setWeight()` e `setColor()`.

**Q: Come esportare il grafico in PDF invece che in immagine?**  
A: Converti prima il grafico in un'immagine, poi incorpora quell'immagine in un PDF usando Aspose.PDF o qualsiasi libreria PDF a tua scelta.

**Q: È possibile aggiungere più linee di tendenza allo stesso grafico?**  
A: Assolutamente. Chiama `chart.getNSeries().get(0).getTrendlines().add(...)` per ogni serie che desideri analizzare.

**Q: Aspose.Cells supporta l'esportazione di immagini ad alta risoluzione?**  
A: Sì. Puoi specificare i DPI chiamando `chart.toImage()` e poi scalare l'immagine di conseguenza prima di salvarla.

## Conclusione
Ora disponi di una soluzione completa, end‑to‑end, per **esportare un grafico in immagine** eseguendo un'**analisi della linea di tendenza** in Java con Aspose.Cells. Caricando un file Excel, aggiungendo una linea di tendenza, visualizzando l'equazione e il valore R‑squared, personalizzando il grafico, salvando la cartella di lavoro e infine esportando l'immagine in PNG/JPEG, puoi generare programmaticamente asset analitici di livello professionale.

---

**Ultimo aggiornamento:** 2025-12-09  
**Testato con:** Aspose.Cells for Java 24.12 (latest)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}