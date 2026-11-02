---
date: 2026-09-02
description: Scopri come creare un grafico a cascata Excel in Java con Aspose.Cells,
  impostare l'intervallo di dati del grafico, personalizzare le etichette e esportare
  in XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Grafici a cascata
og_description: Crea un grafico a cascata Excel utilizzando Aspose.Cells per Java
  – imposta l'intervallo di dati del grafico, aggiungi le etichette dei dati e esporta
  in XLSX in pochi passaggi.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Crea un grafico a cascata Excel con Aspose.Cells per Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Crea un grafico a cascata Excel con Aspose.Cells per Java
url: /it/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafici a cascata

## Introduzione ai grafici a cascata usando Aspose.Cells per Java

In questo tutorial imparerai a **creare un grafico a cascata in Excel** e a **impostare l'intervallo dati del grafico** con Aspose.Cells per Java. I grafici a cascata trasformano una serie di numeri positivi e negativi in una chiara storia visiva, rendendoli ideali per bilanci finanziari, revisioni delle performance di vendita e qualsiasi scenario in cui sia necessario vedere come gli elementi individuali contribuiscono a un totale.

## Risposte rapide
- **Cos'è un grafico a cascata?** Un visual che mostra come un valore iniziale viene aumentato e diminuito da una serie di valori intermedi, terminando con un totale finale.  
- **Quale libreria viene utilizzata?** Aspose.Cells per Java.  
- **È necessaria una licenza?** Una prova gratuita funziona per lo sviluppo; è necessaria una licenza commerciale per la produzione.  
- **Posso salvare il file come XLSX?** Sì – usa `workbook.save("FileName.xlsx")`.  
- **È adatto per la visualizzazione dei dati in Java?** Assolutamente; Aspose.Cells fornisce funzionalità di grafico avanzate senza bisogno di Office installato.

## Cos'è un grafico a cascata?
Un grafico a cascata visualizza contributi sequenziali positivi e negativi a un valore di partenza, aiutandoti a capire come ogni componente influisce sul risultato complessivo. Visualizzando guadagni e perdite fianco a fianco, rende i flussi finanziari complessi immediatamente leggibili.

## Perché usare Aspose.Cells per Java per aggiungere un grafico a cascata?
Aspose.Cells ti consente di generare grafici Excel su qualsiasi server, pipeline CI o desktop senza necessità di Microsoft Excel. Supporta **15+ formati di output** (XLSX, PDF, HTML, CSV e altri), elabora workbook con **500+ righe** in meno di un secondo e offre controllo programmatico su ogni elemento del grafico—dai colori alle etichette dei dati.

## Prerequisiti

Prima di immergerci nel codice, assicurati di avere i seguenti prerequisiti:

- Aspose.Cells per Java: dovrai avere Aspose.Cells per Java installato. Puoi scaricarlo dalla pagina di rilascio di Aspose.Cells per Java: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Ambiente di sviluppo Java: assicurati di avere Java installato sul tuo sistema e uno strumento di build (Maven/Gradle) pronto.

Ora, iniziamo a creare il grafico a cascata passo dopo passo.

## Come impostare l'intervallo dati del grafico per un grafico a cascata in Java
Carica un nuovo workbook, popolalo con dati, aggiungi un oggetto `Chart`, definisci l'intervallo della serie e infine salva il file. Questo processo è lineare: crei un workbook, riempi le celle con categorie e valori, crei un grafico, associ gli intervalli dati e poi esporti il workbook. Il risultato è un grafico a cascata pienamente funzionale pronto per l'uso in report o dashboard.

### Passo 1: importare Aspose.Cells
Il pacchetto `com.aspose.cells` contiene tutte le classi necessarie per la manipolazione di Excel, inclusa la creazione di workbook, la gestione dei worksheet e la generazione di grafici.

### Passo 2: inizializzare workbook e worksheet
Un **Workbook** rappresenta un file Excel, e un **Worksheet** è un singolo foglio all'interno di quel file. Creare questi oggetti fornisce la tela sia per i dati grezzi sia per il grafico.

### Passo 3: inserire dati
La colonna A contiene le etichette delle categorie, mentre la colonna B contiene i valori numerici per il grafico a cascata. Questa disposizione corrisponde al tipico flusso di profitto‑e‑perdita usato nell'analisi finanziaria.

### Passo 4: creare il grafico a cascata
L'oggetto **Chart** crea una rappresentazione visiva; impostando il suo tipo su `ChartType.WATERFALL` lo configura come grafico a cascata. Usa il metodo `add` per impostare l'intervallo dati del grafico per la serie (`"B2:B6"`), e collega l'asse delle categorie a `"A2:A6"`.

### Passo 5: salvare il workbook
Salvare il workbook scrive il grafico e i dati nel formato file specificato. Chiama `workbook.save("WaterfallChart.xlsx")` per generare un file XLSX, o modifica il parametro di formato per esportare in PDF, CSV o HTML.

## Problemi comuni e soluzioni

- **Il grafico appare vuoto** – Verifica che i riferimenti dell'intervallo dati (`B2:B6` e `A2:A6`) corrispondano alle celle effettive contenenti i tuoi valori e le categorie.  
- **Valori negativi non visualizzati correttamente** – Assicurati che il tipo di serie sia impostato su `ChartType.WATERFALL`; altri tipi di grafico trattano i negativi in modo diverso.  
- **Il file non si apre in Excel** – Usa l'ultima versione di Aspose.Cells e conferma che l'estensione del file corrisponda al formato (`.xlsx` per Excel).

## Domande frequenti

### Come posso personalizzare l'aspetto del mio grafico a cascata?
Puoi modificare proprietà come `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` per cambiare i colori delle barre, abilitare le etichette dei dati con `setShowDataLabels(true)`, e regolare i titoli degli assi tramite `getCategoryAxis().setTitle("Stage")`. Il riferimento API di Aspose.Cells fornisce un elenco completo delle opzioni personalizzabili.

### Posso creare più grafici a cascata nello stesso foglio di lavoro?
Sì. Dopo aver aggiunto il primo grafico, ripeti i passaggi di creazione del grafico con un intervallo dati diverso e un nuovo oggetto `Chart`. Ogni grafico è indipendente e può essere posizionato ovunque nel foglio.

### Aspose.Cells è compatibile con diversi ambienti di sviluppo Java?
Assolutamente. La libreria funziona con Eclipse, IntelliJ IDEA, NetBeans e qualsiasi sistema di build che supporti Maven o Gradle. Non sono richiesti plugin aggiuntivi.

### Posso aggiungere serie di dati aggiuntive al mio grafico a cascata?
Puoi aggiungere altre serie chiamando `chart.getNSeries().add("C2:C6", true)` e configurando ciascuna serie separatamente. Questo ti consente di confrontare più scenari fianco a fianco.

### Dove posso trovare più risorse ed esempi per Aspose.Cells per Java?
Esplora la documentazione completa al riferimento API di Aspose.Cells Java: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**D: Come imposto l'intervallo dati del grafico per un grafico a cascata finanziario?**  
R: Usa il metodo `add` sulla serie del grafico, passando l'intervallo di celle che contiene i tuoi valori, ad esempio `"B2:B6"`.

**D: Posso esportare il workbook in PDF invece di XLSX?**  
R: Sì, chiama `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` per generare una versione PDF.

**D: Cosa fare se devo creare un grafico a cascata con più categorie?**  
R: Estendi l'intervallo dati sia nella colonna dei valori sia nella colonna delle categorie, quindi aggiorna le chiamate `add` e `setCategoryData` di conseguenza.

**D: Esiste un modo per formattare automaticamente le barre positive e negative?**  
R: Itera attraverso la collezione `Series` e imposta il colore `FillFormat` in base al segno di ciascun valore; Aspose.Cells consente di applicare formattazione condizionale programmaticamente.

**D: Aspose.Cells supporta aggiornamenti dinamici dei dati per i grafici?**  
R: Sì. Dopo aver modificato i valori delle celle, basta risalvare il workbook—il grafico rifletterà automaticamente i nuovi dati.

---

**Ultimo aggiornamento:** 2026-09-02  
**Testato con:** Aspose.Cells per Java (ultima versione)  
**Autore:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

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

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Tutorial correlati

- [Personalizza le etichette dei dati del grafico Excel usando Aspose.Cells per Java: Guida passo passo](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aggiungi etichette dati a un grafico Excel con Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Come creare ed esportare grafici in Java usando Aspose.Cells: Guida completa](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}