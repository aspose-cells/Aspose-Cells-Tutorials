---
date: 2026-02-09
description: Scopri come aggiungere etichette dati a un grafico Excel e cambiare il
  tipo di grafico usando Aspose.Cells per Java, oltre a tooltip e interattività drill‑down.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Aggiungi etichette dati al grafico Excel con Aspose.Cells Java
url: /it/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

Last Updated:" etc.

Let's produce.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere Etichette Dati a un Grafico Excel e Modificare il Tipo di Grafico – Aspose.Cells Java

I grafici interattivi conferiscono ai tuoi report Excel un nuovo livello di approfondimento, e **l'aggiunta di etichette dati a un grafico Excel** rende le informazioni immediatamente leggibili. In questo tutorial imparerai come **aggiungere etichette dati a un grafico Excel**, cambiare il tipo di grafico e creare soluzioni Java interattive con Aspose.Cells. Ti mostreremo anche come aggiungere tooltip e un semplice collegamento ipertestuale per il drill‑down, così il tuo pubblico potrà esplorare i dati in profondità.

## Risposte Rapide
- **Quale libreria viene utilizzata?** Aspose.Cells per Java  
- **Posso cambiare il tipo di grafico?** Sì – basta modificare l’enumerazione `ChartType` quando crei il grafico.  
- **Come aggiungo tooltip a un grafico?** Usa l’API delle etichette dati (`setHasDataLabels(true)`) e abilita la visualizzazione del valore.  
- **Il drill‑down è supportato?** Puoi collegare hyperlink ai punti dati per un comportamento di drill‑down di base.  
- **Prerequisiti?** IDE Java, JAR di Aspose.Cells e un file Excel con dati di esempio.

## Prerequisiti

Prima di iniziare, assicurati di avere quanto segue:

- Ambiente di sviluppo Java (JDK 8+ consigliato)  
- Libreria Aspose.Cells per Java (scaricabile da [qui](https://releases.aspose.com/cells/java/))  
- Un cartella di lavoro di esempio (`data.xlsx`) contenente i dati che desideri visualizzare  

## Passo 1: Configurare il Progetto Java

1. Crea un nuovo progetto Java nel tuo IDE preferito (IntelliJ IDEA, Eclipse, ecc.).  
2. Aggiungi il JAR di Aspose.Cells al percorso di compilazione del progetto o alle dipendenze Maven/Gradle.

## Passo 2: Caricare i Dati

Per lavorare con i grafici è necessario prima caricare una cartella di lavoro in memoria.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Passo 3: Creare un Grafico (e Cambiarne il Tipo)

Puoi scegliere qualsiasi tipo di grafico che si adatti alla tua analisi. Di seguito creiamo un **grafico a colonne**, ma puoi facilmente passare a un grafico a linee, a torta o a barre modificando l’enumerazione `ChartType`.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Consiglio professionale:** Per **cambiare il tipo di grafico Excel**, sostituisci `ChartType.COLUMN` con `ChartType.LINE`, `ChartType.PIE`, ecc.

## Passo 4: Aggiungere Interattività

### 4.1. Aggiungere Tooltip (Add Tooltips to Chart)

I tooltip appaiono quando l’utente passa il mouse su un punto dati. Il codice seguente abilita le etichette dati e mostra il valore come tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Aggiungere Etichette Dati – **add data labels to excel chart**

Le etichette dati forniscono un’indicazione visiva permanente sul grafico stesso. Puoi visualizzarle come callout per una migliore leggibilità.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Perché aggiungere etichette dati?** Inserire le etichette dati direttamente sul grafico elimina la necessità che gli utenti passino il mouse o indovinino i valori, migliorando la chiarezza del report.

### 4.3. Implementare Drill‑Down (Hyperlink su un Punto Dato)

Un modo semplice per aggiungere la funzionalità di drill‑down è collegare un hyperlink a un punto specifico. Cliccando sul punto si apre una pagina web con informazioni dettagliate.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Passo 5: Salvare la Cartella di Lavoro

Dopo aver configurato il grafico, salva la cartella di lavoro in modo che le funzionalità interattive vengano memorizzate nel file di output.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Problemi Comuni & Soluzioni

| Problema | Soluzione |
|----------|-----------|
| **Tooltip non visualizzati** | Assicurati che `setHasDataLabels(true)` sia chiamato prima di configurare `setShowValue(true)`. |
| **Hyperlink non cliccabile** | Verifica che il formato di output supporti gli hyperlink (ad esempio XLSX, non CSV). |
| **Il tipo di grafico non cambia** | Controlla di aver modificato l’enumerazione `ChartType` corretta al momento dell’aggiunta del grafico. |

## Domande Frequenti

**D: Come posso cambiare il tipo di grafico dopo averlo creato?**  
R: È necessario creare un nuovo grafico con il `ChartType` desiderato. Aspose.Cells non fornisce una conversione in‑place, quindi rimuovi il grafico vecchio e aggiungi quello nuovo.

**D: Posso personalizzare l’aspetto dei tooltip?**  
R: Sì. Usa le proprietà di `DataLabel` come `setFontSize`, `setFontColor` e `setBackgroundColor` per stilizzare il testo del tooltip.

**D: Come gestisco le interazioni dell’utente in un’applicazione web?**  
R: Esporta la cartella di lavoro in un file HTML o XLSX e utilizza JavaScript lato client per catturare gli eventi di click sugli elementi del grafico.

**D: Dove posso trovare altri esempi e documentazione?**  
R: Visita il [Riferimento API Aspose.Cells Java](https://reference.aspose.com/cells/java/) per un elenco completo delle classi e dei metodi relativi ai grafici.

## Conclusione

Ora sai come **aggiungere etichette dati a un grafico Excel**, **cambiare il tipo di grafico Excel**, **creare soluzioni Java per grafici interattivi**, e arricchirli con tooltip, etichette dati e hyperlink per il drill‑down usando Aspose.Cells per Java. Questi miglioramenti rendono i tuoi report Excel molto più coinvolgenti e informativi per gli utenti finali.

---

**Ultimo aggiornamento:** 2026-02-09  
**Testato con:** Aspose.Cells per Java 24.12  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}