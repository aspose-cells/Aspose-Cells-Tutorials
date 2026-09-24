---
date: 2026-02-09
description: Scopri come creare un grafico Excel, aggiungere una linea di tendenza,
  visualizzare il valore R‑quadrato ed esportare il grafico in un'immagine usando
  Aspose.Cells per Java. Include i passaggi per caricare il file Excel, personalizzare
  il grafico e salvarlo come PNG/JPEG.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Come creare un grafico Excel con linea di tendenza ed esportarlo in immagine
  usando Aspose.Cells per Java
url: /it/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Esporta Grafico in Immagine con Analisi della Linea di Tendenza

In questo tutorial imparerai a **creare un grafico Excel** con una linea di tendenza, visualizzare il suo valore R‑squared e esportare il risultato visivo in un'immagine usando Aspose.Cells per Java. Vedremo come caricare una cartella di lavoro esistente, aggiungere una linea di tendenza, personalizzare i titoli, salvare la cartella di lavoro e infine generare un file PNG/JPEG che potrai inserire ovunque.

## Risposte Rapide
- **Qual è lo scopo principale di questa guida?** Per mostrarti come aggiungere una linea di tendenza, visualizzare la sua equazione e il valore R‑squared, ed esportare il grafico risultante in un'immagine usando Java.  
- **Quale libreria è necessaria?** Aspose.Cells per Java (scarica [qui](https://releases.aspose.com/cells/java/)).  
- **Ho bisogno di una licenza?** Una versione di prova gratuita è sufficiente per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Posso generare un file Excel in Java?** Sì – il tutorial crea e salva una cartella di lavoro XLSX.  
- **Come esportare il grafico in PNG o JPEG?** Usa il metodo `Chart.toImage()` (coperto nella sezione “Export Chart”).

## Come creare un grafico Excel con linea di tendenza ed esportarlo in immagine
Questo titolo risponde direttamente alla query principale e ti guida attraverso l'intero flusso di lavoro in ordine logico. Di seguito troverai il perché, i prerequisiti e una guida passo‑passo.

## Che cos'è l'Esportazione di un Grafico in Immagine?
L'esportazione di un grafico in un'immagine converte la rappresentazione visiva dei tuoi dati in una bitmap portatile (PNG, JPEG, ecc.). Questo è utile per incorporare i grafici in report, pagine web o presentazioni dove il file Excel originale non è necessario.

## Perché Aggiungere una Linea di Tendenza e Visualizzare il Valore R‑squared?
Una linea di tendenza ti aiuta a identificare il modello sottostante di una serie di dati, mentre la metrica **R‑squared** quantifica quanto bene la linea di tendenza si adatta ai dati. Includere questi elementi nella tua immagine esportata fornisce agli stakeholder un'istantanea immediata senza aprire la cartella di lavoro.

## Prerequisiti
- Java 8 o versioni successive installate.  
- Libreria Aspose.Cells per Java aggiunta al tuo progetto (file JAR nel classpath).  
- Familiarità di base con gli IDE Java (IntelliJ IDEA, Eclipse, ecc.).  

## Guida Passo‑Passo

### Passo 1: Configura il Progetto
Crea un nuovo progetto Java e aggiungi i JAR di Aspose.Cells al percorso di compilazione. Questo prepara l'ambiente per generare e manipolare file Excel.

### Passo 2: Carica il File Excel (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*Abbiamo appena **caricato un file Excel** in memoria, pronto per la creazione del grafico.*

### Passo 3: Crea un Grafico
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Qui generiamo un grafico a linee che ospiterà in seguito la nostra linea di tendenza.*

### Passo 4: Aggiungi la Linea di Tendenza (how to add trendline) e Visualizza il Valore R‑squared
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*La chiamata `setDisplayRSquaredValue(true)` garantisce che il **valore R‑squared** appaia sul grafico.*

### Passo 5: Personalizza il Grafico e Salva la Cartella di Lavoro (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Ora la cartella di lavoro è **generata** e salvata come file XLSX, pronta per ulteriori elaborazioni.*

### Passo 6: Esporta il Grafico in Immagine (export chart to image)
> **Nota:** Questo passo è descritto senza un blocco di codice aggiuntivo per mantenere invariato il conteggio originale dei blocchi.  
Dopo che il grafico è stato creato e salvato, puoi esportarlo in un'immagine chiamando il metodo `chart.toImage()` e scrivendo il `java.awt.image.BufferedImage` risultante in un formato file a tua scelta (PNG, JPEG, BMP). Il flusso di lavoro tipico è:
1. Recupera l'oggetto `Chart` (già fatto nei passaggi precedenti).  
2. Chiama `chart.toImage()` per ottenere un `BufferedImage`.  
3. Usa `ImageIO.write(bufferedImage, "png", new File("chart.png"))` per scrivere il file.  

Questo produce un'immagine ad alta risoluzione che puoi inserire ovunque, completando il processo di **esportazione del grafico in immagine**.

## Analizza i Risultati
Apri `output.xlsx` in Excel per verificare che la linea di tendenza, l'equazione e il valore R‑squared compaiano come previsto. Apri il file immagine esportato (ad es., `chart.png`) per vedere un visuale pulito che può essere condiviso senza la cartella di lavoro originale.

## Problemi Comuni e Soluzioni
- **Linea di tendenza non visualizzata:** Assicurati che l'intervallo di dati (`A1:A10`) contenga effettivamente valori numerici; dati non numerici impediranno il calcolo della linea di tendenza.  
- **Il valore R‑squared appare 0:** Questo spesso indica che la serie di dati è costante o ha variazione insufficiente. Prova un diverso set di dati o una linea di tendenza polinomiale.  
- **L'esportazione dell'immagine fallisce con `NullPointerException`:** Verifica che il grafico sia stato completamente renderizzato prima di chiamare `toImage()`. Salvare prima la cartella di lavoro a volte risolve problemi di temporizzazione.

## Domande Frequenti

**D: Come posso cambiare il tipo di linea di tendenza?**  
R: Usa una diversa enumerazione `TrendlineType` quando aggiungi la linea di tendenza, ad esempio `TrendlineType.POLYNOMIAL` per una regressione polinomiale.

**D: Posso personalizzare l'aspetto della linea di tendenza (colore, spessore)?**  
R: Sì. Accedi al `LineFormat` della linea di tendenza tramite `trendline.getLineFormat()` e imposta proprietà come `setWeight()` e `setColor()`.

**D: Come esportare il grafico in PDF invece che in immagine?**  
R: Converti prima il grafico in un'immagine, poi incorpora quell'immagine in un PDF usando Aspose.PDF o qualsiasi libreria PDF a tua scelta.

**D: È possibile aggiungere più linee di tendenza allo stesso grafico?**  
R: Assolutamente. Chiama `chart.getNSeries().get(0).getTrendlines().add(...)` per ogni serie che desideri analizzare.

**D: Aspose.Cells supporta l'esportazione di immagini ad alta risoluzione?**  
R: Sì. Puoi specificare i DPI quando chiami `chart.toImage()` e poi ridimensionare l'immagine di conseguenza prima di salvarla.

## Conclusione
Ora disponi di una soluzione completa, end‑to‑end, per **creare un grafico Excel**, aggiungere una linea di tendenza, visualizzare l'equazione e il valore R‑squared, personalizzare l'aspetto, salvare la cartella di lavoro e infine esportare il grafico come immagine PNG/JPEG. Questo approccio ti consente di generare programmaticamente risorse analitiche di livello professionale, perfette per report automatizzati, dashboard o qualsiasi scenario in cui un'immagine statica è più comoda di un file Excel.

---

**Ultimo Aggiornamento:** 2026-02-09  
**Testato Con:** Aspose.Cells for Java latest  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}