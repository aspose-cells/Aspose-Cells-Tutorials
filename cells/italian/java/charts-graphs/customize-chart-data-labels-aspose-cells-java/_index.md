---
date: '2026-10-17'
description: Scopri come impostare la forma delle etichette dei dati del grafico Excel
  in Java usando Aspose.Cells. Questa guida ti mostra come modificare le etichette
  dei grafici Excel rapidamente e in modo efficiente.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Scopri come impostare la forma delle etichette dei dati del grafico
  Excel in Java usando Aspose.Cells. Questa guida passo‑passo ti aiuta a modificare
  le etichette dei grafici Excel rapidamente.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Come impostare la forma delle etichette dei dati del grafico Excel in Java
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Come impostare la forma delle etichette dei dati del grafico Excel in Java
url: /it/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Padroneggiare la personalizzazione dei grafici in Java con Aspose.Cells: modificare le forme delle etichette dati

## Introduzione

Migliorare l'appeal visivo dei grafici Excel è fondamentale quando si preparano report o dashboard, soprattutto se si utilizza Java. Con Aspose.Cells—una potente libreria per la gestione e la manipolazione di fogli di calcolo—puoi **how to set shape** delle etichette dati di un grafico in poche righe di codice. Questo tutorial ti guiderà nella modifica della forma delle etichette dati in un grafico Excel usando Aspose.Cells per Java. Alla fine, saprai come:

- Accedere e modificare le etichette dei dati del grafico
- Impostare forme personalizzate per le etichette dei dati
- Salvare le modifiche al tuo workbook

## Risposte rapide
- **Qual è la classe principale per lavorare con i file Excel?** `Workbook` rappresenta un intero file Excel in memoria.  
- **Quale metodo imposta la forma dell'etichetta?** `setShapeType(DataLabelShapeType shape)` su un oggetto `DataLabel`.  
- **Ho bisogno di una licenza per lo sviluppo?** Una licenza temporanea gratuita funziona per la valutazione; è necessaria una licenza completa per la produzione.  
- **Posso applicare la forma a più serie?** Sì—itera su ogni serie e chiama `setShapeType`.  
- **Questo approccio è compatibile con workbook di grandi dimensioni?** Aspose.Cells elabora workbook di centinaia di pagine senza caricare l'intero file in memoria.

## Cos'è "how to set shape"?
La frase **how to set shape** si riferisce alla configurazione del contorno visivo di un'etichetta dati di un grafico, ad esempio trasformare un semplice rettangolo in un callout o un'ellisse. Cambiare la forma migliora la leggibilità e mette in evidenza i punti dati chiave. Selezionando una forma appropriata, puoi far risaltare l'etichetta, raggruppare punti correlati o aderire alle linee guida del brand aziendale, migliorando così la leggibilità complessiva del grafico.

## Perché usare Aspose.Cells per la personalizzazione delle etichette dei grafici?
Aspose.Cells supporta **50+ input and output formats**—inclusi XLSX, CSV, ODS e PDF—e può manipolare workbook contenenti **fino a 1 milione di righe** senza esaurire la memoria. La sua API consente di modificare i grafici programmaticamente, eliminando la necessità di interventi manuali in Excel e garantendo uno stile coerente nei report automatizzati.

## Prerequisiti

- **Aspose.Cells for Java Library**: è richiesta la versione 25.3 o successiva.  
- **Java Development Environment**: JDK installato sulla tua macchina.  
- **IDE Setup**: Usa un IDE come IntelliJ IDEA o Eclipse per scrivere ed eseguire il tuo codice.

### Librerie e dipendenze richieste

Per gli utenti Maven, includi la seguente dipendenza nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Gli utenti Gradle dovrebbero aggiungere questo al file `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisizione della licenza

Aspose.Cells offre una licenza di prova gratuita, che puoi ottenere dalla [Aspose temporary license page](https://purchase.aspose.com/temporary-license/). Questo consente l'accesso completo a tutte le funzionalità senza limitazioni per un periodo limitato.

## Configurazione di Aspose.Cells per Java

Una volta che l'ambiente è pronto, configuriamo Aspose.Cells. Ecco come iniziare:

### Passaggi di installazione

1. **Download the library**: Usa Maven o Gradle come mostrato sopra.  
2. **License configuration**:  
   - `License` è una classe che applica il file di licenza Aspose.Cells per abilitare la funzionalità completa.  
   - Scarica e applica una licenza temporanea usando questo frammento di codice dopo aver inizializzato l'oggetto `Workbook`:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Basic initialization**: Crea un'istanza `Workbook` per iniziare a lavorare con i file Excel.

## Come impostare la forma delle etichette dei dati in un grafico?

Carica il tuo workbook, individua il grafico target e applica la forma desiderata alle sue etichette dati. I passaggi seguenti completano l'operazione in meno di un minuto.

### Guida passo‑passo

#### Passo 1: carica il tuo workbook

La classe `Workbook` è l'oggetto di livello superiore di Aspose.Cells che rappresenta un singolo file Excel in memoria. Usa `new Workbook("input.xlsx")` per caricare il file da modificare.

#### Passo 2: accedi al grafico

`Worksheet` rappresenta un singolo foglio all'interno di un workbook.  
`Worksheet ws = workbook.getWorksheets().get(0);` recupera il primo foglio.  
`Chart` è un oggetto che rappresenta un grafico incorporato in un foglio.  
`Chart chart = ws.getCharts().get(0);` ottiene il primo grafico su quel foglio.

#### Passo 3: recupera le serie e modifica le etichette dei dati

`Series` rappresenta una serie di dati tracciata su un grafico.  
Ogni oggetto `Series` contiene una collezione `DataLabel`.  
`DataLabel` controlla l'aspetto di un'etichetta dati per una serie.  
`DataLabelShapeType` è un'enumerazione delle possibili forme per le etichette dati.  
Chiama `series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` per impostare la forma. L'enumerazione fornisce decine di opzioni, come `RECTANGLE`, `CLOUD` e `WEDGE_ELLIPSE_CALLOUT`.

#### Passo 4: salva il tuo workbook

Dopo aver applicato la forma, invoca `workbook.save("output.xlsx");` per scrivere le modifiche su disco.

## Suggerimenti per la risoluzione dei problemi

- **File path issues**: Verifica che il percorso del file sia assoluto o correttamente relativo alla directory di lavoro del tuo progetto.  
- **Library version mismatch**: Assicurati di utilizzare Aspose.Cells versione 25.3 o successiva; le versioni più vecchie non hanno il metodo `setShapeType`.  
- **Unsupported chart types**: Alcuni tipi di grafico legacy (ad es., radar) potrebbero non esporre le proprietà della forma dell'etichetta; passa a un tipo di grafico supportato come colonna o linea.

## Applicazioni pratiche

1. **Financial reporting** – Evidenzia i margini di profitto chiave con etichette in stile callout.  
2. **Educational content** – Usa etichette a forma di nuvola per attirare l'attenzione su punti dati importanti nei materiali didattici.  
3. **Marketing analytics** – Applica forme personalizzate per differenziare le metriche di performance delle campagne nei cruscotti.

Integrare Aspose.Cells con pipeline di dati o sistemi CRM consente di generare report completamente stilizzati automaticamente, riducendo lo sforzo manuale e garantendo visuali coerenti con il brand.

## Considerazioni sulle prestazioni

Quando si lavora con file Excel di grandi dimensioni:

- **Optimize memory usage**: Chiama `workbook.dispose();` dopo il salvataggio per rilasciare rapidamente le risorse native.  
- **Batch processing**: Elabora i grafici in gruppi anziché uno per volta per ridurre l'overhead di creazione degli oggetti.  
- **Efficient data handling**: Evita calcoli pesanti all'interno dei cicli che iterano migliaia di righe; calcola i valori in anticipo.

## Conclusione

Ora sai **how to set shape** delle etichette dati di un grafico Excel in Java usando Aspose.Cells. Questa capacità non solo migliora l'estetica dei grafici, ma anche la comprensione dei dati da parte degli utenti finali. Esplora ulteriori opzioni di personalizzazione—come colori delle etichette, caratteri e linee guida—per perfezionare ulteriormente le tue visualizzazioni.

Per qualsiasi domanda o assistenza, consulta il [Aspose support forum](https://forum.aspose.com/c/cells/9).

## Domande frequenti

**Q: Come cambio la forma di più etichette dati contemporaneamente?**  
A: Itera su ogni serie nel grafico e chiama `setShapeType` sull'oggetto `DataLabel` della serie.

**Q: Aspose.Cells per Java può gestire file Excel di grandi dimensioni in modo efficiente?**  
A: Sì. Con una corretta gestione della memoria, elabora workbook contenenti centinaia di migliaia di righe senza caricare l'intero file in memoria.

**Q: Quali sono i problemi comuni durante la configurazione di Aspose.Cells?**  
A: Dipendenze Maven mancanti, utilizzo di una versione della libreria obsoleta o fornitura di un file di licenza non valido sono ostacoli tipici.

**Q: Esiste un modo per ripristinare le forme delle etichette dati al valore predefinito?**  
A: Imposta il tipo di forma su `DataLabelShapeType.DEFAULT` per riportare l'aspetto originale.

**Q: Come posso applicare questa personalizzazione a più grafici in un workbook?**  
A: Itera su `ws.getCharts()` e applica la stessa logica `setShapeType` alla collezione di serie di ciascun grafico.

## Risorse

- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [Purchase a License](https://purchase.aspose.com/buy)
- [Free Trial License](https://releases.aspose.com/cells/java/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)

---  

**Last Updated:** 2026-10-17  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## Tutorial correlati

- [Modify Excel Chart Data Labels Using Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [How to Resize Labels in Excel Charts with Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Add Labels to Excel Charts with Aspose Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}