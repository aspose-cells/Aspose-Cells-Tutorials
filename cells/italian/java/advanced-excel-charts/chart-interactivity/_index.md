---
date: 2025-12-01
description: Scopri come modificare il tipo di grafico di Excel e aggiungere funzionalità
  interattive come tooltip, etichette dati e drill‑down utilizzando Aspose.Cells per
  Java.
language: it
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Modifica il tipo di grafico Excel e aggiungi interattività – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Modifica il tipo di grafico Excel e aggiungi interattività

## Introduzione

I grafici interattivi consentono al tuo pubblico di esplorare i dati al volo, mentre la possibilità di **change Excel chart type** ti offre la flessibilità di presentare le informazioni nel formato visivo più efficace. In questo tutorial imparerai a usare Aspose.Cells per Java per modificare il tipo di un grafico, aggiungere tooltip, incorporare etichette dati e persino creare collegamenti drill‑down — tutto senza uscire dal tuo codice Java. Alla fine, avrai una cartella di lavoro Excel completamente funzionale e interattiva che potrai incorporare in report, dashboard o applicazioni web.

## Risposte rapide
- **Posso modificare il tipo di grafico programmaticamente?** Sì – usa l'enumerazione `ChartType` quando crei o aggiorni un grafico.  
- **Come aggiungo tooltip a un grafico?** Abilita le etichette dati e imposta `ShowValue` su true.  
- **Qual è il modo più semplice per aggiungere collegamenti drill‑down?** Allega un hyperlink a un punto dati tramite `getHyperlinks().add(url)`.  
- **Ho bisogno di una licenza per Aspose.Cells?** Una versione di prova gratuita funziona per lo sviluppo; è necessaria una licenza per la produzione.  
- **Quale versione di Java è supportata?** Java 8 e successive sono pienamente supportate.

## Che cosa è “change Excel chart type”?

Modificare il tipo di grafico significa scambiare la rappresentazione visiva (ad esempio, da un grafico a colonne a un grafico a linee) mantenendo intatti i dati sottostanti. Questo è utile quando scopri che un grafico diverso comunica meglio tendenze, confronti o distribuzioni.

## Perché aggiungere interattività ai grafici Excel?

- **Migliore comprensione dei dati:** Tooltip ed etichette dati consentono agli utenti di vedere i valori esatti senza scorrere.  
- **Presentazioni coinvolgenti:** Gli elementi interattivi mantengono l'interesse degli spettatori.  
- **Capacità di drill‑down:** Gli hyperlink consentono agli utenti di passare a fogli di lavoro dettagliati o a risorse esterne.  
- **Asset riutilizzabili:** Una cartella di lavoro può servire a più scenari di reporting semplicemente cambiando i tipi di grafico.

## Prerequisiti

- Ambiente di sviluppo Java (JDK 8+)
- Libreria Aspose.Cells per Java (scarica da [qui](https://releases.aspose.com/cells/java/))
- Un file Excel di esempio (`data.xlsx`) contenente i dati che desideri visualizzare

## Guida passo‑passo

### Passo 1: Configura il tuo progetto Java

1. Crea un nuovo progetto Java nel tuo IDE preferito (IntelliJ IDEA, Eclipse, VS Code, ecc.).  
2. Aggiungi il JAR di Aspose.Cells al classpath del tuo progetto.

### Passo 2: Carica la cartella di lavoro di origine

Iniziamo caricando una cartella di lavoro esistente che contiene i dati per il nostro grafico.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Passo 3: Crea un grafico e **cambia il suo tipo**

Di seguito creiamo un grafico a colonne, per poi dimostrare immediatamente come potresti cambiarlo in un grafico a linee se necessario.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Suggerimento professionale:** Cambiare il tipo di grafico dopo la creazione è semplice come chiamare `setChartType(...)`. Questo soddisfa la parola chiave principale **change Excel chart type** senza richiedere un nuovo oggetto grafico.

### Passo 4: Aggiungi interattività

#### 4.1 Aggiungi tooltip al grafico

I tooltip vengono visualizzati quando l'utente passa il mouse su un punto dati. In Aspose.Cells sono implementati tramite etichette dati.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Aggiungi etichette dati ( **add data labels chart** )

Le etichette dati possono mostrare il valore esatto, il nome della categoria o entrambi. Qui utilizziamo uno stile callout.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Implementa drill‑down ( **add drill down excel** )

Un collegamento drill‑down consente agli utenti di fare clic su un punto e passare a una vista dettagliata, sia all'interno della cartella di lavoro che su una pagina web.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Passo 5: Salva la cartella di lavoro

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemi comuni e soluzioni

| Problema | Motivo | Soluzione |
|----------|--------|----------|
| Tooltip non visualizzati | `HasDataLabels` non abilitato | Assicurati che `setHasDataLabels(true)` sia chiamato prima di configurare `ShowValue`. |
| Il collegamento drill‑down non funziona | URL dell'hyperlink malformato | Verifica che l'URL inizi con `http://` o `https://`. |
| Il tipo di grafico non cambia | Uso di una versione più vecchia di Aspose.Cells | Aggiorna all'ultima versione (testata con 24.12). |

## Domande frequenti

**D: Come posso cambiare il tipo di grafico dopo che è stato creato?**  
R: Chiama `chart.setChartType(ChartType.YOUR_CHOICE)` sull'oggetto `Chart` esistente. Questo risponde direttamente al requisito **change Excel chart type**.

**D: Posso personalizzare l'aspetto dei tooltip?**  
R: Sì. Usa `chart.getNSeries().get(0).getPoints().getDataLabels()` per impostare la dimensione del carattere, il colore e lo sfondo.

**D: È possibile aggiungere più collegamenti drill‑down in un unico grafico?**  
R: Assolutamente. Scorri i punti e chiama `getHyperlinks().add(url)` per ogni punto che desideri collegare.

**D: Aspose.Cells supporta altri tipi di grafico come torta o radar?**  
R: Tutti i tipi di grafico definiti nell'enumerazione `ChartType` sono supportati, inclusi `PIE`, `RADAR`, `AREA`, ecc.

**D: Dove posso trovare più esempi?**  
R: Visita il [Riferimento API Java di Aspose.Cells](https://reference.aspose.com/cells/java/) ufficiale per un elenco completo dei metodi relativi ai grafici.

## Conclusione

Ora sai come **change Excel chart type**, incorporare **tooltip**, aggiungere **etichette dati** e creare collegamenti **drill‑down** usando Aspose.Cells per Java. Queste funzionalità interattive trasformano i fogli di calcolo statici in strumenti dinamici di esplorazione dei dati, perfetti per dashboard, report e analisi basate sul web.

---

**Ultimo aggiornamento:** 2025-12-01  
**Testato con:** Aspose.Cells 24.12 per Java  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}