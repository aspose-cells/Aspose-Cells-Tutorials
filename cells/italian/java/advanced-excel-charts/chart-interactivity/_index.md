---
date: 2026-08-21
description: Scopri come aggiungere tooltip, data labels e modificare il chart type
  nei grafici Excel utilizzando Aspose.Cells for Java – guida passo‑passo con esempi
  interattivi.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Modifica Chart Type di Excel
og_description: Scopri come aggiungere tooltip, data labels e modificare il chart
  type nei grafici Excel utilizzando Aspose.Cells for Java – guida passo‑passo con
  esempi interattivi.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Come aggiungere tooltip e data labels ai grafici Excel in Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Come aggiungere tooltip e data labels ai grafici Excel in Java
url: /it/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere etichette dati al grafico Excel e modificare il tipo di grafico – Aspose.Cells Java

I grafici interattivi conferiscono ai tuoi report Excel un nuovo livello di approfondimento, e **come aggiungere tooltip** rende le informazioni immediatamente leggibili. In questo tutorial imparerai a **aggiungere etichette dati al grafico Excel**, **modificare il tipo di grafico**, e a creare soluzioni Java interattive con Aspose.Cells. Ti mostreremo anche come aggiungere tooltip e un semplice collegamento ipertestuale drill‑down affinché il tuo pubblico possa esplorare i dati in profondità.

## Risposte rapide
- **Quale libreria viene utilizzata?** Aspose.Cells for Java  
- **Posso modificare il tipo di grafico?** Sì – basta modificare l’enum `ChartType` quando crei il grafico.  
- **Come aggiungo tooltip a un grafico?** Usa l’API data‑label (`setHasDataLabels(true)`) e abilita la visualizzazione del valore.  
- **Il drill‑down è supportato?** Puoi allegare hyperlink ai punti dati per un comportamento drill‑down di base.  
- **Prerequisiti?** IDE Java, Aspose.Cells JAR e un file Excel con dati di esempio.

## Che cosa significa aggiungere tooltip?

**How to add tooltips** si riferisce al processo di abilitare il testo a comparsa che mostra il valore di un punto dati o informazioni personalizzate su un grafico Excel. In Aspose.Cells ciò avviene tramite le impostazioni delle etichette dati del grafico. I tooltip aiutano gli utenti a comprendere rapidamente i dati senza ingombrare il grafico e possono essere personalizzati per carattere, colore e formato.

## Perché utilizzare grafici interattivi con Aspose.Cells?

Aspose.Cells supporta **oltre 50 formati di input e output** — inclusi XLSX, CSV, PDF e HTML — e può elaborare cartelle di lavoro con **oltre 1 000 fogli** senza caricare l’intero file in memoria, offrendo una generazione rapida di grafici lato server per report aziendali. I grafici interattivi consentono inoltre l’inserimento di hyperlink, aggiornamenti dinamici dei dati e l’esportazione in formati web‑friendly, rendendoli ideali per dashboard e portali di reporting.

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

- Ambiente di sviluppo Java (JDK 8+ consigliato)  
- Libreria Aspose.Cells per Java (scarica dalla [pagina di download di Aspose.Cells per Java](https://releases.aspose.com/cells/java/))  
- Un workbook di esempio (`data.xlsx`) contenente i dati che desideri visualizzare  

## Passo 1: configurare il tuo progetto Java

1. Crea un nuovo progetto Java nel tuo IDE preferito (IntelliJ IDEA, Eclipse, ecc.).  
2. Aggiungi il JAR di Aspose.Cells al percorso di compilazione del tuo progetto o alle dipendenze Maven/Gradle.

## Passo 2: caricare i dati

Per lavorare con i grafici è necessario prima caricare un workbook in memoria.

La classe `Workbook` rappresenta un file Excel, e `Worksheet` rappresenta un singolo foglio all’interno di quel file.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Come modificare il tipo di grafico in Aspose.Cells?

Crea un nuovo grafico con l’enum `ChartType` desiderato; Aspose.Cells non modifica il tipo di un grafico esistente in‑place, quindi devi aggiungere un nuovo grafico del tipo corretto e, facoltativamente, rimuovere quello vecchio. Questo approccio garantisce che tutte le serie e gli assi vengano ricostruiti correttamente per la nuova rappresentazione visiva.

## Passo 3: creare un grafico (e cambiarne il tipo)

Puoi scegliere qualsiasi tipo di grafico che si adatti alla tua analisi. Di seguito creiamo un **grafico a colonne**, ma puoi facilmente passare a un grafico a linee, a torta o a barre modificando l’enum `ChartType`.

L’oggetto `Chart` fornisce metodi per configurare la rappresentazione visiva dei dati nel foglio.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Consiglio professionale:** Per **modificare il tipo di grafico Excel**, sostituisci `ChartType.COLUMN` con `ChartType.LINE`, `ChartType.PIE`, ecc.

## Come aggiungere tooltip a un grafico Excel?

Carica il tuo grafico, abilita le etichette dati e imposta il flag `showValue`. Il tooltip mostrerà quindi il valore della cella sottostante ogni volta che l’utente passa il mouse su un punto dati nel file Excel renderizzato o nella vista HTML. Puoi anche personalizzare il carattere, il colore e lo sfondo del tooltip per adattarlo allo stile del tuo report.

La classe `DataLabel` controlla l’aspetto e il contenuto delle etichette dati, che fungono anche da tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Passo 4: aggiungere interattività

### 4.1. Aggiungere tooltip (aggiungere tooltip al grafico)

I tooltip compaiono quando l’utente passa il mouse su un punto dati. Il codice seguente abilita le etichette dati e mostra il valore come tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Aggiungere etichette dati – **add data labels to excel chart**

Le etichette dati forniscono un’indicazione visiva permanente sul grafico stesso. Puoi visualizzarle come callout per una migliore leggibilità.

La classe `DataLabel` controlla l’aspetto delle etichette su ciascuna serie. Chiamando `setHasDataLabels(true)` e configurando proprietà come `setShowValue(true)`, inserisci direttamente il valore numerico sul grafico, rendendolo immediatamente visibile senza alcuna interazione. Opzioni aggiuntive consentono di mostrare i nomi delle serie, le percentuali o testo personalizzato per un contesto più ricco.

> **Perché aggiungere etichette dati?** Includere le etichette dati direttamente sul grafico elimina la necessità per gli utenti di passare il mouse o indovinare i valori, migliorando la chiarezza del report.

### 4.3. Implementare drill‑down (hyperlink su un punto dati)

Un modo semplice per aggiungere la capacità di drill‑down è allegare un hyperlink a un punto specifico. Cliccando sul punto si apre una pagina web con informazioni dettagliate.

La classe `Hyperlink` allega un collegamento cliccabile a un elemento del grafico, abilitando la navigazione drill‑down.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Come aggiungere etichette dati a un grafico Excel?

La classe `DataLabel` controlla l’aspetto delle etichette su ciascuna serie. Chiamando `setHasDataLabels(true)` e configurando proprietà come `setShowValue(true)`, inserisci direttamente il valore numerico sul grafico, rendendolo immediatamente visibile senza alcuna interazione. Opzioni aggiuntive consentono di mostrare i nomi delle serie, le percentuali o testo personalizzato per un contesto più ricco.

## Passo 5: salvare il workbook

Dopo aver configurato il grafico, persisti il workbook in modo che le funzionalità interattive siano memorizzate nel file di output.

Chiamando `workbook.save` il workbook modificato viene scritto su disco nel formato scelto.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Tooltip non visualizzati** | Assicurati che `setHasDataLabels(true)` sia chiamato prima di configurare `setShowValue(true)`. |
| **Hyperlink non cliccabile** | Verifica che il formato di output supporti gli hyperlink (ad es., XLSX, non CSV). |
| **Il tipo di grafico non cambia** | Controlla di aver modificato l’enum `ChartType` corretto quando aggiungi il grafico. |

## Domande frequenti

**D: Come posso cambiare il tipo di grafico dopo averlo creato?**  
R: È necessario creare un nuovo grafico con il `ChartType` desiderato. Aspose.Cells non fornisce una conversione in‑place del tipo, quindi rimuovi il grafico vecchio e aggiungi quello nuovo.

**D: Posso personalizzare l’aspetto dei tooltip?**  
R: Sì. Usa le proprietà della classe `DataLabel` come `setFontSize`, `setFontColor` e `setBackgroundColor` per stilizzare il testo del tooltip.

**D: Come gestisco le interazioni dell’utente in un’applicazione web?**  
R: Esporta il workbook in un file HTML o XLSX e utilizza JavaScript sul lato client per catturare gli eventi di click sugli elementi del grafico.

**D: Dove posso trovare altri esempi e documentazione?**  
R: Visita la [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) per un elenco completo delle classi e dei metodi relativi ai grafici.

## Conclusione

Ora sai come **aggiungere etichette dati al grafico Excel**, **modificare il tipo di grafico Excel**, **creare soluzioni Java per grafici interattivi**, e arricchirli con tooltip, etichette dati e hyperlink drill‑down usando Aspose.Cells per Java. Questi miglioramenti rendono i tuoi report Excel molto più coinvolgenti e informativi per gli utenti finali.

---

**Ultimo aggiornamento:** 2026-08-21  
**Testato con:** Aspose.Cells for Java 24.12  
**Autore:** Aspose

## Tutorial correlati

- [Come modificare i grafici Excel e le etichette dati usando Aspose.Cells per Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Estrarre le etichette degli assi dei grafici Excel usando Aspose.Cells Java: Guida completa](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Creare grafici a bolle in Excel usando Aspose.Cells per Java: Guida passo‑passo](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}