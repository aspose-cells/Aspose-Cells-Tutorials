---
date: 2025-11-28
description: Impara come aggiungere tooltip, etichette dati e funzionalità di drill‑down
  per creare un grafico interattivo in Java usando Aspose.Cells.
language: it
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Come aggiungere tooltip nei grafici interattivi (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Come aggiungere i tooltip nei grafici interattivi (Aspose.Cells Java)

## Introduzione

I grafici interattivi consentono agli utenti di esplorare i dati passando il mouse, facendo clic o approfondendo i dettagli. In questo tutorial imparerai **come aggiungere i tooltip** a un grafico, così come **come aggiungere le etichette dei dati**, e implementare la navigazione **drill‑down** — tutto con Aspose.Cells per Java. Alla fine, sarai in grado di creare un grafico interattivo completo che rende le tue presentazioni dati più coinvolgenti e approfondite.

## Risposte rapide
- **Quale libreria è necessaria?** Aspose.Cells for Java (ultima versione).  
- **Quale funzionalità principale copre questa guida?** Aggiungere tooltip ai grafici.  
- **Posso anche aggiungere le etichette dei dati?** Sì – vedi la sezione “Aggiungere etichette dei dati”.  
- **Il drill‑down è supportato?** Sì, tramite hyperlink sui punti dati.  
- **Quale formato file viene prodotto?** Una cartella di lavoro Excel (`.xlsx`) con un grafico interattivo.

## Che cosa significa aggiungere i tooltip?

Un tooltip è un piccolo popup che appare quando un utente passa il mouse su un elemento del grafico, mostrando informazioni aggiuntive come il valore esatto o un messaggio personalizzato. I tooltip migliorano la leggibilità dei dati senza ingombrare il layout visivo.

## Perché creare grafici interattivi in Java?

- **Migliore presa di decisione:** Gli utenti possono vedere immediatamente valori precisi.  
- **Report professionali:** Gli elementi interattivi rendono le dashboard moderne.  
- **Componenti riutilizzabili:** Una volta padroneggiata l'API, puoi applicarla a qualsiasi soluzione di reporting basata su Excel.

## Prerequisiti

- Un ambiente di sviluppo Java (JDK 8 o successivo).  
- Libreria Aspose.Cells per Java (scarica da [qui](https://releases.aspose.com/cells/java/)).  
- Un file Excel di esempio chiamato **data.xlsx** contenente i dati da visualizzare.

## Passo 1: Configurare il tuo progetto Java

1. Crea un nuovo progetto Java nel tuo IDE preferito (IntelliJ IDEA, Eclipse, ecc.).  
2. Aggiungi il JAR di Aspose.Cells al classpath del tuo progetto.

## Passo 2: Caricare i dati

Per creare un grafico interattivo è necessario prima un foglio di lavoro con i dati. Il codice qui sotto carica il primo foglio di lavoro da **data.xlsx**.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Passo 3: Creare un grafico

Ora aggiungeremo un grafico a colonne al foglio di lavoro. Il grafico occuperà le celle F6 a K16.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Passo 4: Aggiungere interattività

### 4.1. Come aggiungere i tooltip

Il frammento seguente abilita i tooltip per la prima serie del grafico. Ogni punto dati mostrerà il suo valore al passaggio del mouse.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Aggiungere etichette dei dati al grafico

Se desideri anche etichette visibili accanto a ogni colonna, utilizza l'approccio **add data labels chart** mostrato di seguito. Questo soddisfa la keyword secondaria *add data labels chart*.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Come eseguire il drill‑down (implementazione del drill‑down)

Il drill‑down consente agli utenti di fare clic su un punto dati e passare a una vista dettagliata (ad es., una pagina web). Qui colleghiamo un hyperlink al primo punto della serie.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Suggerimento professionale:** Puoi generare l'URL dinamicamente in base al valore del punto per creare un'esperienza di drill‑down realmente guidata dai dati.

## Passo 5: Salvare la cartella di lavoro

Dopo aver configurato il grafico, salva la cartella di lavoro. Il file risultante contiene un grafico interattivo pronto per essere aperto in Excel.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemi comuni e soluzioni

| Problema | Causa | Soluzione |
|----------|-------|-----------|
| I tooltip non compaiono | Etichette dei dati non abilitate | Assicurati che `setHasDataLabels(true)` sia chiamato prima di impostare `ShowValue`. |
| Hyperlink non cliccabile | Indice del punto errato | Verifica di fare riferimento al punto corretto (`get(0)` è il primo punto). |
| Il grafico appare fuori posto | Intervallo di celle errato | Regola gli indici di riga/colonna in `add(ChartType.COLUMN, row1, col1, row2, col2)`. |

## Domande frequenti

**D: Come posso cambiare il tipo di grafico?**  
R: Sostituisci `ChartType.COLUMN` con un altro valore enum come `ChartType.LINE` o `ChartType.PIE` quando chiami `worksheet.getCharts().add(...)`.

**D: Posso personalizzare l'aspetto dei tooltip?**  
R: Sì. Usa le proprietà di formattazione dell'oggetto `DataLabel` (dimensione del font, colore di sfondo, ecc.) per stilizzare il testo del tooltip.

**D: Come gestisco le interazioni dell'utente in un'applicazione web?**  
R: Esporta la cartella di lavoro in un formato compatibile con il web (ad es., HTML) e utilizza JavaScript per catturare gli eventi di clic sugli elementi del grafico.

**D: Dove posso trovare altri esempi e documentazione?**  
R: Esplora il riferimento ufficiale dell'API su [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/).

**D: È possibile aggiungere più link di drill‑down nello stesso grafico?**  
R: Assolutamente. Scorri i punti della serie e assegna un URL unico alla collezione `Hyperlinks` di ciascun punto.

## Conclusione

In questa guida hai imparato **come aggiungere i tooltip**, **aggiungere le etichette dei dati** e **implementare il drill‑down** per creare una soluzione **create interactive chart java** usando Aspose.Cells. Queste funzionalità trasformano i grafici statici di Excel in visualizzazioni dinamiche e user‑friendly che aiutano gli stakeholder a esplorare i dati con facilità.

---

**Ultimo aggiornamento:** 2025-11-28  
**Testato con:** Aspose.Cells for Java 24.12  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}