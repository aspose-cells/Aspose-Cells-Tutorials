---
date: 2025-12-06
description: Scopri come cambiare il tipo di grafico in Excel e creare grafici interattivi
  con Java usando Aspose.Cells. Aggiungi tooltip al grafico, etichette dei dati e
  drill‑down per una visualizzazione dei dati più ricca.
language: it
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Cambia il tipo di grafico Excel con Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambia il tipo di grafico Excel e aggiungi interattività

## Introduzione

I grafici interattivi offrono ai tuoi report Excel un nuovo livello di approfondimento, consentendo agli utenti di passare il mouse, fare clic ed esplorare i punti dati direttamente. In questo tutorial **cambierai il tipo di grafico Excel** e **creerai soluzioni Java per grafici interattivi** con Aspose.Cells per Java. Ti guideremo nell'aggiungere tooltip al grafico, etichette dati e un semplice collegamento ipertestuale di drill‑down affinché il tuo pubblico possa approfondire i numeri.

## Risposte rapide
- **Quale libreria viene utilizzata?** Aspose.Cells for Java  
- **Posso cambiare il tipo di grafico?** Sì – basta modificare l'enumerazione `ChartType` quando crei il grafico.  
- **Come aggiungo tooltip a un grafico?** Usa l'API delle etichette dati (`setHasDataLabels(true)`) e abilita la visualizzazione del valore.  
- **Il drill‑down è supportato?** Puoi allegare collegamenti ipertestuali ai punti dati per un comportamento di drill‑down di base.  
- **Prerequisiti?** IDE Java, JAR Aspose.Cells e un file Excel con dati di esempio.

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

- Ambiente di sviluppo Java (JDK 8+ consigliato)  
- Libreria Aspose.Cells per Java (scarica da [qui](https://releases.aspose.com/cells/java/))  
- Un cartella di lavoro di esempio (`data.xlsx`) contenente i dati che desideri visualizzare  

## Passo 1: Configurare il tuo progetto Java

1. Crea un nuovo progetto Java nel tuo IDE preferito (IntelliJ IDEA, Eclipse, ecc.).  
2. Aggiungi il JAR Aspose.Cells al percorso di compilazione del tuo progetto o alle dipendenze Maven/Gradle.

## Passo 2: Caricare i dati

Per lavorare con i grafici è necessario prima caricare una cartella di lavoro in memoria.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Passo 3: Creare un grafico (e cambiarne il tipo)

Puoi scegliere qualsiasi tipo di grafico che si adatti alla tua analisi. Di seguito creiamo un **grafico a colonne**, ma puoi facilmente passare a un grafico a linee, a torta o a barre modificando l'enumerazione `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Consiglio professionale:** Per **cambiare il tipo di grafico Excel**, sostituisci `ChartType.COLUMN` con `ChartType.LINE`, `ChartType.PIE`, ecc.

## Passo 4: Aggiungere interattività

### 4.1. Aggiungere tooltip (Aggiungi tooltip al grafico)

I tooltip compaiono quando l'utente passa il mouse su un punto dati. Il codice seguente abilita le etichette dati e mostra il valore come tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Aggiungere etichette dati

Le etichette dati forniscono un'indicazione visiva permanente sul grafico stesso. Puoi visualizzarle come callout per una migliore leggibilità.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Implementare drill‑down (Collegamento ipertestuale su un punto dati)

Un modo semplice per aggiungere la funzionalità di drill‑down è allegare un collegamento ipertestuale a un punto specifico. Cliccando sul punto si apre una pagina web con informazioni dettagliate.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Passo 5: Salvare la cartella di lavoro

Dopo aver configurato il grafico, persisti la cartella di lavoro in modo che le funzionalità interattive siano memorizzate nel file di output.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemi comuni e soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Tooltip non visualizzati** | Assicurati che `setHasDataLabels(true)` sia chiamato prima di configurare `setShowValue(true)`. |
| **Collegamento ipertestuale non cliccabile** | Verifica che il formato di output supporti i collegamenti ipertestuali (ad es., XLSX, non CSV). |
| **Il tipo di grafico non cambia** | Controlla di aver modificato l'enumerazione `ChartType` corretta quando aggiungi il grafico. |

## Domande frequenti

**D: Come posso cambiare il tipo di grafico dopo che è stato creato?**  
R: Devi creare un nuovo grafico con il `ChartType` desiderato. Aspose.Cells non fornisce una conversione in‑place del tipo, quindi rimuovi il vecchio grafico e aggiungi uno nuovo.

**D: Posso personalizzare l'aspetto dei tooltip?**  
R: Sì. Usa le proprietà `DataLabel` come `setFontSize`, `setFontColor` e `setBackgroundColor` per stilizzare il testo del tooltip.

**D: Come gestisco le interazioni dell'utente in un'applicazione web?**  
R: Esporta la cartella di lavoro in un file HTML o XLSX e utilizza JavaScript sul lato client per catturare gli eventi di click sugli elementi del grafico.

**D: Dove posso trovare più esempi e documentazione?**  
R: Visita il [Riferimento API Java di Aspose.Cells](https://reference.aspose.com/cells/java/) per un elenco completo delle classi e dei metodi relativi ai grafici.

## Conclusione

Ora sai come **cambiare il tipo di grafico Excel**, **creare soluzioni Java per grafici interattivi**, e arricchirli con tooltip, etichette dati e collegamenti ipertestuali di drill‑down usando Aspose.Cells per Java. Questi miglioramenti rendono i tuoi report Excel molto più coinvolgenti e informativi per gli utenti finali.

---

**Ultimo aggiornamento:** 2025-12-06  
**Testato con:** Aspose.Cells for Java 24.12  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}