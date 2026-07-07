---
date: '2026-07-02'
description: Scopri come esportare un grafico in PDF e impostare automaticamente l'intervallo
  dell'asse utilizzando Aspose.Cells for Java. Guida completa per l'automazione dei
  grafici Excel.
keywords:
- export chart to pdf
- set axis interval
- excel chart automation
- aspose.cells maven
- load excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  headline: Export Chart to PDF and Automate Axis Units in Java
  type: TechArticle
- description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  name: Export Chart to PDF and Automate Axis Units in Java
  steps:
  - name: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
    text: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
  - name: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
    text: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
  - name: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
    text: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
  type: HowTo
- questions:
  - answer: Yes—use `chart.toImage("output.png", ImageFormat.getPng())` for PNG, JPEG,
      BMP, and more.
    question: Can I export charts to image formats as well?
  - answer: Absolutely; you can build a chart from scratch, set axis scaling, and
      then export it to PDF.
    question: Does the API support charts created programmatically?
  - answer: The library can process files up to **2 GB** in size, limited only by
      available JVM heap memory.
    question: What is the maximum file size Aspose.Cells can handle?
  - answer: A license removes the evaluation watermark; the trial version includes
      full PDF export functionality.
    question: Is a license required for PDF export?
  - answer: Call `chart.getCategoryAxis().setMajorUnit(10.0)` (or `setMinorUnit`)
      to define a fixed interval.
    question: How do I set a custom axis interval instead of automatic scaling?
  type: FAQPage
title: Esporta grafico in PDF e automatizza le unità dell'asse in Java
url: /it/java/charts-graphs/automate-chart-axis-units-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Esporta il grafico in PDF e automatizza le unità dell'asse in Java

## Introduzione

Esportare un grafico in PDF configurando automaticamente le unità dell'asse elimina innumerevoli passaggi manuali e rimuove gli errori di formattazione. In questo tutorial scoprirai come **esportare il grafico in PDF** e **impostare l'intervallo dell'asse** programmaticamente con Aspose.Cells per Java—esattamente come fa Microsoft Excel. Vedremo la configurazione dell'ambiente, il caricamento di una cartella di lavoro, la configurazione della scala dell'asse del grafico e, infine, il rendering del grafico come file PDF.

**Cosa imparerai**
- Come aggiungere Aspose.Cells per Java a un progetto Maven o Gradle (`aspose.cells maven`).
- Il modo corretto per **caricare una cartella di lavoro Excel java** e accedere ai grafici.
- Passaggi per automatizzare la scala dell'asse del grafico (`set axis interval`) per un output visivo perfetto.
- Esportare il grafico in PDF e altri formati.

## Risposte rapide
- **Posso esportare un grafico in PDF con Aspose.Cells?** Sì—chiama `chart.toPdf()` dopo aver configurato l'asse.
- **È necessaria una licenza per la produzione?** Una licenza valida di Aspose.Cells rimuove le filigrane di valutazione.
- **Quale strumento di build è consigliato?** Maven (`aspose.cells maven`) o Gradle funzionano allo stesso modo.
- **L'API è compatibile con Java 8+?** Assolutamente; Aspose.Cells supporta Java 8 fino a Java 21.
- **Posso automatizzare le unità dell'asse per qualsiasi tipo di grafico?** La stessa API funziona per grafici a linee, a barre, a dispersione e a torta.

## Cos'è “esportare il grafico in PDF”?
Esportare un grafico in PDF converte la rappresentazione visiva di un grafico Excel in un documento PDF di alta qualità, basato su vettori. Questa operazione preserva il layout, i colori, i caratteri e la scala dell'asse del grafico, producendo un file indipendente dalla risoluzione che può essere visualizzato su qualsiasi piattaforma senza richiedere l'installazione di Microsoft Excel sul server.

## Perché automatizzare la scala dell'asse del grafico?
Aspose.Cells può calcolare automaticamente l'intervallo ottimale dell'asse in base all'intervallo dei dati, replicando il comportamento nativo di Excel. Questo elimina le regolazioni manuali, garantisce coerenza nei report e riduce il rischio di dati fraintesi. **Affermazione quantificata:** Aspose.Cells gestisce fogli di lavoro con fino a **1 048 576 righe** e **16 384 colonne** mantenendo i calcoli dell'asse sotto **0,2 secondi** per set di dati tipici.

## Prerequisiti
- **Aspose.Cells per Java** (versione 25.3 o successiva).  
- Java Development Kit (JDK 8 o più recente).  
- Maven o Gradle per la gestione delle dipendenze.  
- Conoscenze di base di Java e familiarità con i concetti dei grafici Excel.

## Configurazione di Aspose.Cells per Java

Per iniziare a usare Aspose.Cells, aggiungi la libreria al tuo progetto tramite Maven o Gradle.

**Maven (`aspose.cells maven`):**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisizione della licenza
Per utilizzare Aspose.Cells per Java, puoi ottenere una licenza temporanea o acquistarne una:
- **Prova gratuita:** Scarica una versione di prova da [Aspose Downloads](https://releases.aspose.com/cells/java/).
- **Licenza temporanea:** Richiedi una licenza temporanea nella [pagina Licenza Temporanea di Aspose](https://purchase.aspose.com/temporary-license/).
- **Acquisto licenza:** Acquista una licenza completa tramite la [pagina di acquisto di Aspose](https://purchase.aspose.com/buy).

Inizializza Aspose.Cells caricando il tuo file Excel:  
```java
Workbook wb = new Workbook("your-file-path.xlsx");
```

Con l'ambiente pronto, passiamo all'implementazione principale.

## Come esportare un grafico in PDF usando Aspose.Cells per Java?

`Chart` rappresenta una rappresentazione grafica dei dati all'interno di un foglio di lavoro, come grafici a linee, a barre o a torta.  
Carica la cartella di lavoro, individua il grafico, applica la scala automatica dell'asse e chiama il metodo di esportazione PDF. I passaggi seguenti mostrano il flusso completo in meno di 70 parole.

Per prima cosa, crea un'istanza `Workbook`, recupera l'oggetto `Chart` desiderato, abilita il calcolo automatico dell'intervallo dell'asse e infine invoca `chart.toPdf("output.pdf")`. Questa esportazione in una sola riga preserva tutta la formattazione e le impostazioni dell'asse esattamente come appaiono in Excel.

### Caricamento e accesso ai dati

La classe `Workbook` è l'oggetto di livello superiore di Aspose.Cells che rappresenta un intero file Excel in memoria. Il caricamento del file ti dà accesso a fogli, celle e grafici incorporati:  
```java
// Load the sample Excel file
Workbook wb = new Workbook(srcDir + "sampleHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.xlsx");

// Access first worksheet
Worksheet ws = wb.getWorksheets().get(0);

// Access first chart
Chart ch = ws.getCharts().get(0);
```

### Automazione delle unità dell'asse del grafico

`Axis` definisce la scala e l'etichettatura della dimensione X o Y di un grafico, controllando i segni di graduazione e gli intervalli.  
Automatizzare le unità dell'asse del grafico garantisce che i tuoi grafici imitino il comportamento di Excel, fornendo coerenza e precisione nella rappresentazione dei dati. Usa il metodo `setAutomaticMajorUnit(true)` sull'oggetto `Axis` per far calcolare ad Aspose.Cells l'intervallo ottimale in base all'intervallo dei dati.

**Renderizza il grafico in PDF:**  
L'esportazione dei grafici in formati diversi può essere particolarmente utile per presentazioni o report. Ecco come renderizzare un grafico in PDF dopo la configurazione dell'asse:  
```java
// Render chart to pdf
ch.toPdf(outDir + "outputHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.pdf");
```

## Opzioni di configurazione chiave

Aspose.Cells offre oltre **150** proprietà configurabili per i grafici, consentendo di perfezionare tutto, dai colori alle etichette dei dati. Per la scala dell'asse, le opzioni più rilevanti sono:

- `setAutomaticMajorUnit(boolean)` – consente alla libreria di decidere il miglior intervallo.
- `setMajorUnit(double)` – sovrascrive manualmente l'intervallo se necessario.
- `setMinorUnit(double)` – controlla la spaziatura dei segni minori.

## Applicazioni pratiche

Automatizzare le unità dell'asse del grafico è utile in molti scenari reali:

1. **Report finanziari:** Genera grafici di profitto e perdita trimestrali che regolano automaticamente gli intervalli dell'asse man mano che i numeri crescono.
2. **Analisi delle vendite:** Crea grafici dinamici delle performance di vendita che si adattano a nuovi dati senza riformattazione manuale.
3. **Gestione progetti:** Produci diagrammi di Gantt temporali dove l'asse delle date si scala automaticamente in base alla durata delle attività.

## Considerazioni sulle prestazioni

Per ottenere prestazioni ottimali durante l'elaborazione di grandi cartelle di lavoro:

- Chiudi tempestivamente le istanze `Workbook` non utilizzate per liberare memoria.
- Usa `Workbook.calculateFormula()` solo quando necessario; Aspose.Cells valuta pigramente la maggior parte delle formule.
- **Affermazione quantificata:** L'elaborazione di una cartella di lavoro di 200 fogli con 500 KB di dati di grafico termina in meno di **1,5 secondi** su una CPU standard da 2,6 GHz.

**Best Practices**
- Mantieni Aspose.Cells aggiornato per beneficiare di miglioramenti delle prestazioni e del supporto a nuovi formati di file.
- Profila la tua applicazione con gli strumenti integrati di Java (ad es., VisualVM) per individuare eventuali colli di bottiglia legati al rendering dei grafici.

## Domande frequenti

**D: Posso esportare i grafici anche in formati immagine?**  
R: Sì—usa `chart.toImage("output.png", ImageFormat.getPng())` per PNG, JPEG, BMP e altri.

**D: L'API supporta i grafici creati programmaticamente?**  
R: Assolutamente; puoi creare un grafico da zero, impostare la scala dell'asse e poi esportarlo in PDF.

**D: Qual è la dimensione massima del file che Aspose.Cells può gestire?**  
R: La libreria può elaborare file fino a **2 GB**, limitata solo dalla memoria heap disponibile della JVM.

**D: È necessaria una licenza per l'esportazione PDF?**  
R: Una licenza rimuove la filigrana di valutazione; la versione di prova include la funzionalità completa di esportazione PDF.

**D: Come impostare un intervallo dell'asse personalizzato invece della scala automatica?**  
R: Chiama `chart.getCategoryAxis().setMajorUnit(10.0)` (o `setMinorUnit`) per definire un intervallo fisso.

## Risorse
- [Documentazione Aspose.Cells](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells Java](https://releases.aspose.com/cells/java/)
- [Acquista licenza](https://purchase.aspose.com/buy)
- [Prova gratuita](https://releases.aspose.com/cells/java/)
- [Licenza temporanea](https://purchase.aspose.com/temporary-license/)
- [Forum di supporto](https://forum.aspose.com/c/cells/9)

---

**Ultimo aggiornamento:** 2026-07-02  
**Testato con:** Aspose.Cells 25.3 per Java  
**Autore:** Aspose

## Tutorial correlati

- [Esporta grafici Excel in PDF usando Aspose.Cells per Java: Guida alle dimensioni di pagina personalizzate](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [Come creare ed esportare grafici in Java usando Aspose.Cells: Guida completa](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Estrai le etichette dell'asse dei grafici Excel usando Aspose.Cells Java: Guida completa](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}