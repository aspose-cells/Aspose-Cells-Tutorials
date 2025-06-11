---
"date": "2025-04-07"
"description": "Scopri come creare e personalizzare grafici a torta in Excel con Aspose.Cells per Java. Segui questa guida passo passo per migliorare le tue competenze di visualizzazione dei dati."
"title": "Creare grafici a torta in Excel utilizzando Aspose.Cells per Java&#58; una guida completa"
"url": "/it/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Creare grafici a torta in Excel utilizzando Aspose.Cells per Java
## Introduzione
Creare grafici a torta accattivanti e informativi in Excel può trasformare dati grezzi in informazioni preziose, consentendo di prendere decisioni aziendali consapevoli in modo rapido. Hai difficoltà con le funzionalità integrate di Microsoft Excel o cerchi una soluzione scalabile che si integri perfettamente con le tue applicazioni Java? Aspose.Cells per Java è qui per aiutarti.

Questo tutorial ti guiderà nella creazione e personalizzazione di grafici a torta in file Excel utilizzando Aspose.Cells per Java. Scopri come aggiungere dati in modo efficiente, configurare gli elementi dei grafici e finalizzare la tua cartella di lavoro, il tutto con facilità e precisione.

**Cosa imparerai:**
- Impostazione e utilizzo di Aspose.Cells per Java
- Creazione di una nuova cartella di lavoro e suo popolamento con dati campione
- Aggiungere e personalizzare grafici a torta in un foglio di lavoro Excel
- Best practice per la configurazione e l'ottimizzazione dei grafici

Cominciamo col parlare dei prerequisiti.
## Prerequisiti
Prima di iniziare, assicurati di avere quanto segue:
### Librerie, versioni e dipendenze richieste
Assicurati che Aspose.Cells per Java versione 25.3 o successiva sia incluso nel tuo progetto utilizzando Maven o Gradle.
**Esperto:**
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
### Requisiti di configurazione dell'ambiente
- Un Java Development Kit (JDK) installato sul tuo sistema.
- Un ambiente di sviluppo integrato (IDE) come IntelliJ IDEA, Eclipse o NetBeans.
### Prerequisiti di conoscenza
Sarà utile una conoscenza di base della programmazione Java e la familiarità con le strutture dei file Excel.
## Impostazione di Aspose.Cells per Java
Aspose.Cells è una potente libreria che consente agli sviluppatori di creare, modificare e visualizzare fogli di calcolo Excel in applicazioni Java. Ecco come configurarla:
1. **Installazione**: Aggiungere la dipendenza Maven o Gradle come mostrato sopra.
2. **Acquisizione della licenza**:
   - Ottieni una licenza di prova gratuita per i test iniziali da [Prova gratuita di Aspose](https://releases.aspose.com/cells/java/).
   - Richiedi una licenza temporanea per testare tutte le funzionalità senza limitazioni tramite [Licenza temporanea](https://purchase.aspose.com/temporary-license/).
3. **Inizializzazione di base**: Inizia creando un'istanza di `Workbook` classe, che rappresenta il file Excel.
```java
import com.aspose.cells.Workbook;
// Crea e inizializza una nuova cartella di lavoro
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## Guida all'implementazione
Ora implementiamo passo dopo passo ciascuna funzionalità per creare una cartella di lavoro di Excel con un grafico a torta.
### 1. Creazione e inizializzazione della cartella di lavoro
**Panoramica**: Iniziamo inizializzando il nostro `Workbook` oggetto e accedendo al suo primo foglio di lavoro in cui aggiungeremo dati e grafici.
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// Crea una nuova istanza della cartella di lavoro
Workbook workbook = new Workbook();
// Accedi al primo foglio di lavoro nella cartella di lavoro
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2. Aggiunta di dati campione alle celle
**Panoramica**: Compila il foglio di lavoro con dati campione che verranno rappresentati nel grafico a torta.
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// Aggiungere i nomi dei paesi nella colonna A
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// Continua per gli altri Paesi...
// Aggiungere i dati di vendita corrispondenti nella colonna B
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// Continua per il resto dei dati...
```
### 3. Aggiunta di un grafico a torta al foglio di lavoro
**Panoramica**Inserisci un grafico a torta nel foglio di lavoro utilizzando intervalli di dati predefiniti.
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// Aggiungi un grafico a torta nella posizione e dimensione specificate
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4. Configurazione della serie di grafici
**Panoramica**: Definisci l'intervallo di dati per i dati di vendita e di categoria (nomi dei paesi) per garantire che il grafico a torta rappresenti accuratamente il tuo set di dati.
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// Imposta i dati di vendita come origine dati del grafico
serieses.add("B1:B8", true);
// Specificare i dati della categoria (nomi dei paesi)
serieses.setCategoryData("A1:A8");
// Abilita colori diversi per ogni fetta della torta
serieses.setColorVaried(true);

// Visualizzare una tabella dati sul grafico per chiarezza
chart.setShowDataTable(true);
```
### 5. Impostazione del titolo e dello stile del grafico
**Panoramica**: Personalizza il titolo del grafico per migliorarne la leggibilità e la presentazione.
```java
import com.aspose.cells.Color;

// Imposta il titolo del grafico con le opzioni di stile
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. Configurazione delle etichette dati per le serie di grafici
**Panoramica**: Aggiungere etichette dati a ogni fetta della torta, fornendo una chiara ripartizione dei valori.
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // Posizionare le etichette all'interno della base di ogni fetta di torta
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // Configurare le opzioni di visualizzazione delle etichette
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7. Salvataggio della cartella di lavoro
**Panoramica**Completa il tuo file Excel con tutti i dati e i grafici salvati sul disco.
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// Salvare la cartella di lavoro in un file Excel
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## Applicazioni pratiche
- **Analisi aziendale**: Utilizzare grafici a torta nei report sulle vendite per visualizzare la quota di mercato o la distribuzione dei ricavi tra le regioni.
- **Strumenti educativi**: Crea moduli di apprendimento interattivi che visualizzano la distribuzione dei dati statistici.
- **Gestione del progetto**: Rappresentare visivamente l'allocazione delle risorse e l'utilizzo del budget alle parti interessate.
## Considerazioni sulle prestazioni
Per ottimizzare le prestazioni:
- Riduci al minimo l'utilizzo della memoria gestendo in modo efficiente le dimensioni della cartella di lavoro.
- Se si gestiscono set di dati estesi, utilizzare le funzionalità di Aspose.Cells, come lo streaming di file di grandi dimensioni.
- Seguire le best practice di Java per la gestione della memoria, assicurandosi che le risorse vengano rilasciate correttamente dopo l'uso.
## Conclusione
Seguendo questa guida, hai imparato a creare, configurare e personalizzare grafici a torta in Excel utilizzando Aspose.Cells per Java. Questa potente libreria consente agli sviluppatori di integrare perfettamente funzionalità avanzate di fogli di calcolo nelle loro applicazioni Java.
Per approfondire ulteriormente, valuta la possibilità di approfondire altri tipi di grafici o di ampliare le tue capacità di manipolazione dei dati con le funzionalità aggiuntive offerte da Aspose.Cells.
## Sezione FAQ
1. **Posso usare Aspose.Cells gratuitamente?**
   - Sì, è disponibile una prova gratuita. Per accedere a tutte le funzionalità senza limitazioni, è possibile richiedere una licenza temporanea.
2. **È possibile creare altri tipi di grafici utilizzando Aspose.Cells?**
   - Assolutamente! Puoi creare grafici a barre, grafici a linee e altro ancora regolando il `ChartType`.
3. **Come posso gestire grandi set di dati in Excel con Java?**
   - Utilizzare tecniche di caricamento dati efficienti e valutare lo streaming per file di grandi dimensioni.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}