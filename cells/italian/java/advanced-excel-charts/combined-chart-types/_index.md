---
date: 2025-12-06
description: Scopri come aggiungere serie di dati, creare tipi di grafico combinati,
  salvare la cartella di lavoro Excel ed esportare il grafico in PNG con Aspose.Cells
  per Java.
language: it
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Aggiungi serie di dati per creare un grafico combinato con Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aggiungere serie di dati per creare un grafico combinato usando Aspose.Cells

In questo tutorial **aggiungerai serie di dati** a una cartella di lavoro Excel e imparerai a **creare grafici combinati** con Aspose.Cells for Java. Ti guideremo passo passo—dalla configurazione della cartella di lavoro, all'aggiunta delle serie, alla personalizzazione della leggenda, fino a **salvare il workbook Excel** e a esportare il **grafico in PNG**. Alla fine avrai un grafico combinato pronto all'uso da inserire in report o dashboard.

## Risposte rapide
- **Quale libreria crea grafici combinati?** Aspose.Cells for Java  
- **Come aggiungo una serie di dati?** Usa `chart.getNSeries().add(...)`  
- **Posso esportare il grafico come immagine?** Sì, con `chart.toImage(...)` (PNG)  
- **In quale formato file posso salvare il workbook?** Standard `.xlsx` (Excel)  
- **È necessaria una licenza per la produzione?** È richiesta una licenza valida di Aspose.Cells  

## Cos'è **aggiungere serie di dati** in Aspose.Cells?
Aggiungere una serie di dati indica al grafico quali celle contengono i valori da rappresentare. Ogni serie può rappresentare una linea, una colonna o qualsiasi altro tipo di grafico, e puoi combinarle per creare un **grafico combinato**.

## Perché creare un **grafico combinato**?
Un grafico combinato ti consente di visualizzare diversi set di dati con rappresentazioni visive distinte (ad esempio, una serie a linee sopra una serie a colonne) in un'unica vista. È perfetto per confrontare tendenze con totali, evidenziare correlazioni o fornire approfondimenti più ricchi in un formato compatto.

## Prerequisiti
- Java Development Kit (JDK) 8 o superiore  
- Libreria Aspose.Cells per Java (scarica dal link sotto)  
- Familiarità di base con la sintassi Java e i concetti di Excel  

## Iniziare

Per prima cosa, scarica la libreria Aspose.Cells per Java dal sito ufficiale:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Una volta aggiunto il JAR al classpath del tuo progetto, puoi iniziare a costruire il grafico.

### Passo 1: Importa le classi Aspose.Cells
```java
import com.aspose.cells.*;
```

### Passo 2: Crea un nuovo workbook
```java
Workbook workbook = new Workbook();
```

### Passo 3: Accedi al primo foglio di lavoro
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Passo 4: Aggiungi un oggetto grafico combinato  
Inizieremo con un grafico a linee e successivamente aggiungeremo altre serie per ottenere un effetto di **grafico combinato**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Aggiungere dati al grafico

Ora che il contenitore del grafico esiste, dobbiamo alimentarlo con i dati.

### Passo 5: Definisci gli intervalli di dati e **aggiungi serie di dati**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Consiglio:** Il primo parametro (`"A1:A5"`) è l'intervallo per la prima serie, e il secondo (`"B1:B5"`) crea una seconda serie che verrà combinata con la prima.

### Passo 6: Imposta i dati della categoria (asse X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizzare il grafico

Un buon grafico racconta una storia. Diamo al grafico titoli, etichette degli assi e una leggenda chiara.

### Passo 7: Imposta il titolo del grafico e le etichette degli assi
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Passo 8: **Aggiungi leggenda al grafico** e regola la sua posizione
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Salvataggio ed esportazione del grafico

Dopo la personalizzazione, vorrai **salvare il workbook Excel** e anche generare un'immagine.

### Passo 9: Salva il workbook come file Excel
```java
workbook.save("CombinedChart.xlsx");
```

### Passo 10: Esporta il **grafico in PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Il metodo `chart.toImage` **genera immagini del grafico Excel** che possono essere usate in pagine web, report o email.

## Problemi comuni e risoluzione

| Problema | Soluzione |
|----------|-----------|
| **Nessun dato appare** | Verifica che gli intervalli di celle (`A1:A5`, `B1:B5`, `C1:C5`) contengano effettivamente dati prima di creare il grafico. |
| **La leggenda si sovrappone al grafico** | Imposta `chart.getLegend().setOverlay(false)` o sposta la leggenda in una posizione diversa (ad esempio, `RIGHT`). |
| **Il file immagine è vuoto** | Assicurati che il grafico abbia almeno una serie e che `chart.toImage` sia chiamato dopo tutte le personalizzazioni. |
| **Il salvataggio genera un'eccezione** | Verifica di avere i permessi di scrittura nella directory di destinazione e che il file non sia aperto in Excel. |

## Domande frequenti

**D: Come installo Aspose.Cells per Java?**  
**R:** Scarica il JAR dal sito ufficiale e aggiungilo al classpath del tuo progetto. Il link per il download è: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**D: Posso creare altri tipi di grafico oltre a linea e colonna?**  
**R:** Sì, Aspose.Cells supporta grafici a barre, a torta, a dispersione, ad area e molti altri tipi. Consulta la documentazione API per l'elenco completo.

**D: È necessaria una licenza per l'uso in produzione?**  
**R:** È richiesta una licenza valida di Aspose.Cells per le distribuzioni in produzione. È disponibile una versione di prova gratuita per la valutazione.

**D: Come posso cambiare i colori di ciascuna serie?**  
**R:** Usa `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (o simile) dopo aver aggiunto le serie.

**D: Dove posso trovare altri esempi di codice?**  
**R:** Documentazione completa e ulteriori esempi sono disponibili sul sito di riferimento Aspose: [here](https://reference.aspose.com/cells/java/).

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**Ultimo aggiornamento:** 2025-12-06  
**Testato con:** Aspose.Cells for Java 24.12  
**Autore:** Aspose  

---