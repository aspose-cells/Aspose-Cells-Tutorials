---
date: 2026-02-16
description: Scopri come impostare l'intervallo dei dati del grafico e creare un grafico
  a cascata in Java usando Aspose.Cells. Guida passo‑passo per aggiungere un grafico
  a serie di dati, personalizzarlo ed esportarlo in XLSX.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Imposta intervallo dati del grafico – Grafico a cascata Aspose.Cells per Java
url: /it/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafici a cascata

## Introduzione ai grafici a cascata usando Aspose.Cells per Java

In questo tutorial imparerai a **set chart data range** e a creare un **waterfall chart** con Aspose.Cells per Java. I grafici a cascata sono uno strumento essenziale nella visualizzazione dei dati perché consentono di vedere l'effetto cumulativo di una serie di valori positivi e negativi. Che tu stia preparando un bilancio finanziario, un report sulle performance di vendita o qualsiasi altra analisi basata sui dati, un grafico a cascata può trasformare i numeri grezzi in intuizioni chiare e azionabili.

## Risposte rapide
- **What is a waterfall chart?** Una visualizzazione che mostra come un valore iniziale venga aumentato e diminuito da una serie di valori intermedi, terminando con un totale finale.  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Can I save the file as XLSX?** Sì – usa `workbook.save("FileName.xlsx")`.  
- **Is it suitable for Java data visualization?** Assolutamente; Aspose.Cells fornisce funzionalità di grafico avanzate senza la necessità di Office installato.

## Cos'è un grafico a cascata?
Un grafico a cascata mostra contributi positivi e negativi sequenziali a un valore iniziale, aiutandoti a capire come ogni componente influisce sul risultato complessivo.

## Perché usare Aspose.Cells per Java per aggiungere un grafico a cascata?
- **No Microsoft Excel required** – genera grafici su qualsiasi server o pipeline CI.  
- **Full control over formatting** – colori, etichette dati e assi possono essere personalizzati programmaticamente.  
- **Supports multiple output formats** – XLSX, PDF, HTML e altro.  
- **High performance** – ideale per cartelle di lavoro di grandi dimensioni e reportistica automatizzata.

## Prerequisiti

Prima di immergerci nel codice, assicurati di avere i seguenti prerequisiti pronti:

- Aspose.Cells for Java: È necessario avere Aspose.Cells per Java installato. Puoi scaricarlo da [here](https://releases.aspose.com/cells/java/).

- Java Development Environment: Assicurati di avere Java installato sul tuo sistema.

Ora, iniziamo a creare il grafico a cascata passo dopo passo.

## Come impostare l'intervallo dei dati del grafico per un grafico a cascata in Java

### Passo 1: Importa Aspose.Cells

```java
import com.aspose.cells.*;
```

Per prima cosa, devi importare la libreria Aspose.Cells nel tuo progetto Java. Questa libreria fornisce funzionalità estese per lavorare con file Excel, inclusa la creazione di grafici.

### Passo 2: Inizializza Workbook e Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Crea una nuova cartella di lavoro e aggiungi un foglio di lavoro. Useremo questo foglio per inserire i nostri dati e **add chart to worksheet**.

### Passo 3: Inserisci i dati

Ora, popoliamo il foglio di lavoro con i dati che vogliamo rappresentare nel grafico a cascata.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

In questo esempio, abbiamo le categorie nella colonna A e i valori corrispondenti nella colonna B. Puoi sostituire questi dati con il tuo set di dati.

### Passo 4: Crea il grafico a cascata

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Abbiamo aggiunto un grafico a cascata al nostro foglio, specificato la serie di dati e i dati di categoria. Questo è il passaggio fondamentale che **adds waterfall chart** al tuo foglio. Nota come il metodo `add` utilizzi l'intervallo `"B2:B6"` – è qui che **set chart data range** per la serie. Puoi ulteriormente personalizzare l'aspetto del grafico (colori, etichette dati, ecc.) usando le proprietà dell'oggetto `Chart`.

### Passo 5: Salva la cartella di lavoro

```java
workbook.save("WaterfallChart.xlsx");
```

Salva la cartella di lavoro in un file. L'esempio utilizza il formato XLSX, ma Aspose.Cells ti consente anche di **export excel pdf java**‑compatible files come PDF, CSV e molti altri formati. Questo soddisfa il requisito **save workbook xlsx**.

## Problemi comuni e soluzioni

- **Chart appears blank** – Verifica che i riferimenti dell'intervallo di dati (`B2:B6` e `A2:A6`) corrispondano alle celle effettive contenenti i tuoi valori e le categorie.  
- **Negative values not displayed correctly** – Assicurati che il tipo di serie sia impostato su `ChartType.WATERFALL`; altri tipi di grafico trattano i valori negativi in modo diverso.  
- **File not opening in Excel** – Assicurati di utilizzare una versione recente di Aspose.Cells (l'ultima release) e che l'estensione del file corrisponda al formato (`.xlsx` per Excel).

## Domande frequenti

### Come posso personalizzare l'aspetto del mio grafico a cascata?

Puoi personalizzare l'aspetto del tuo grafico a cascata modificando proprietà come colori, etichette dati e etichette degli assi. Consulta la documentazione di Aspose.Cells per indicazioni dettagliate.

### Posso creare più grafici a cascata nello stesso foglio di lavoro?

Sì, puoi creare più grafici a cascata nello stesso foglio di lavoro seguendo gli stessi passaggi con intervalli di dati diversi.

### Aspose.Cells è compatibile con diversi ambienti di sviluppo Java?

Sì, Aspose.Cells per Java è compatibile con vari ambienti di sviluppo Java, inclusi Eclipse, IntelliJ IDEA e NetBeans.

### Posso aggiungere serie di dati aggiuntive al mio grafico a cascata?

Certamente, puoi aggiungere altre serie di dati al tuo grafico a cascata per rappresentare scenari di dati complessi in modo efficace. Questo è un esempio di come puoi **add data series chart** programmaticamente.

### Dove posso trovare più risorse ed esempi per Aspose.Cells per Java?

Puoi esplorare la documentazione di Aspose.Cells per Java su [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) per informazioni approfondite ed esempi di codice.

## FAQ

**Q: How do I set the chart data range for a financial waterfall chart?**  
A: Usa il metodo `add` sulla serie del grafico, passando l'intervallo di celle che contiene i tuoi valori, ad esempio `"B2:B6"`.

**Q: Can I export the workbook to PDF instead of XLSX?**  
A: Sì, chiama `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` per un output **export excel pdf java**‑compatible.

**Q: What if I need to create a financial waterfall chart with more categories?**  
A: Estendi l'intervallo di dati sia nella colonna dei valori che nella colonna delle categorie, quindi aggiorna le chiamate `add` e `setCategoryData` di conseguenza.

**Q: Is there a way to automatically format positive and negative bars?**  
A: Puoi iterare attraverso la collezione `Series` e impostare il colore `FillFormat` in base al segno di ogni valore.

**Q: Does Aspose.Cells support dynamic data updates for charts?**  
A: Sì, puoi modificare i valori delle celle dopo che il grafico è stato creato; il grafico rifletterà le modifiche quando la cartella di lavoro viene salvata.

---

**Ultimo aggiornamento:** 2026-02-16  
**Testato con:** Aspose.Cells for Java (latest)  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}