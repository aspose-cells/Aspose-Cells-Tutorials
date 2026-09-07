---
date: 2026-02-14
description: Scopri come esportare il grafico in PNG, aggiungere serie di dati, combinare
  un grafico a linee e colonne, salvare la cartella di lavoro in XLSX e aggiungere
  la legenda al grafico utilizzando Aspose.Cells per Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Esporta il grafico in PNG e aggiungi serie di dati per il grafico combinato
url: /it/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Esporta il grafico in PNG e aggiungi serie di dati per grafico combinato

In questo tutorial **aggiungere serie di dati** a una cartella di lavoro Excel, **combinare grafico a linee e colonne** elementi, e imparare come **esportare il grafico in PNG** usando Aspose.Cells per Java. Ti guideremo passo passo—dalla configurazione della cartella di lavoro, aggiungendo il grafico a un foglio di lavoro, personalizzando la legenda, fino a **salvare la cartella di lavoro come xlsx** e generare un'immagine PNG del grafico. Alla fine, avrai un grafico combinato pronto all'uso che potrai incorporare in report o dashboard.

## Risposte rapide
- **Quale libreria crea grafici combinati?** Aspose.Cells for Java  
- **Come aggiungo una serie di dati?** Usa `chart.getNSeries().add(...)`  
- **Come posso esportare il grafico in png?** Chiama `chart.toImage("file.png", ImageFormat.getPng())`  
- **In quale formato file posso salvare la cartella di lavoro?** Standard `.xlsx` (save workbook as xlsx)  
- **È necessaria una licenza per la produzione?** A valid Aspose.Cells license is required  

## Cos'è **export chart to PNG** in Aspose.Cells?
Esportare un grafico in PNG crea un'immagine raster del grafico Excel che può essere visualizzata in pagine web, report o email senza richiedere l'applicazione Excel.

## Perché creare un **combined line column chart**?
Un grafico combinato ti consente di visualizzare diversi set di dati con rappresentazioni visive distinte (ad esempio, una serie a linee sopra una serie a colonne) in un'unica vista. È perfetto per confrontare le tendenze con i totali, evidenziare correlazioni o fornire approfondimenti più ricchi in un formato compatto.

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

### Passo 2: Crea una nuova cartella di lavoro
```java
Workbook workbook = new Workbook();
```

### Passo 3: Accedi al primo foglio di lavoro
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Passo 4: Aggiungi un oggetto grafico combinato al foglio di lavoro  
Inizieremo con un grafico a linee e successivamente aggiungeremo una serie a colonne per ottenere un effetto **combined line column chart**.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Aggiungere dati al grafico

Ora che il contenitore del grafico esiste, dobbiamo alimentarlo con i dati.

### Passo 5: Definisci gli intervalli di dati e **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Suggerimento professionale:** Il primo parametro (`"A1:A5"`) è l'intervallo per la prima serie, e il secondo (`"B1:B5"`) crea una seconda serie che sarà combinata con la prima.

### Passo 6: Imposta i dati della categoria (asse X)
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Personalizzare il grafico

Un buon grafico racconta una storia. Diamo al grafico titoli, etichette degli assi e una leggenda chiara.

### Passo 7: **Set chart axis labels** e titolo
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Passo 8: **Add legend chart** e regola la sua posizione
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Salvataggio ed esportazione del grafico

Dopo la personalizzazione, vorrai **salvare la cartella di lavoro come xlsx** e generare anche un'immagine.

### Passo 9: Salva la cartella di lavoro come file Excel (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Passo 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Il metodo `chart.toImage` **genera immagini del grafico Excel** che possono essere usate in pagine web, report o email.

## Problemi comuni e risoluzione

| Problema | Soluzione |
|----------|----------|
| **Nessun dato appare** | Verifica che gli intervalli di celle (`A1:A5`, `B1:B5`, `C1:C5`) contengano effettivamente dati prima di creare il grafico. |
| **La leggenda si sovrappone al grafico** | Imposta `chart.getLegend().setOverlay(false)` o sposta la leggenda in una posizione diversa (ad es., `RIGHT`). |
| **Il file immagine è vuoto** | Assicurati che il grafico abbia almeno una serie e che `chart.toImage` sia chiamato dopo tutte le personalizzazioni. |
| **Il salvataggio genera un'eccezione** | Controlla di avere i permessi di scrittura nella directory di destinazione e che il file non sia aperto in Excel. |

## Domande frequenti

**D: Come installo Aspose.Cells per Java?**  
R: Scarica il JAR dal sito ufficiale e aggiungilo al classpath del tuo progetto. Il link per il download è: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**D: Posso creare altri tipi di grafico oltre a linee e colonne?**  
R: Sì, Aspose.Cells supporta grafici a barre, a torta, a dispersione, ad area e molti altri tipi. Consulta la documentazione API per l'elenco completo.

**D: È necessaria una licenza per l'uso in produzione?**  
R: È necessaria una licenza valida di Aspose.Cells per le distribuzioni in produzione. È disponibile una prova gratuita per la valutazione.

**D: Come posso cambiare i colori di ciascuna serie?**  
R: Usa `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (o simile) dopo aver aggiunto le serie.

**D: Dove posso trovare più esempi di codice?**  
R: Documentazione completa e ulteriori esempi sono disponibili sul sito di riferimento Aspose: [qui](https://reference.aspose.com/cells/java/).

---

**Ultimo aggiornamento:** 2026-02-14  
**Testato con:** Aspose.Cells per Java ultima versione  
**Autore:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}