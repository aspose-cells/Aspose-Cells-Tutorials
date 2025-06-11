---
"date": "2025-04-08"
"description": "Impara a creare e personalizzare grafici a torta usando Aspose.Cells per Java. Una guida passo passo con esempi di codice per sviluppatori."
"title": "Padroneggiare Aspose.Cells&#58; creare e personalizzare grafici a torta in Java"
"url": "/it/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Padroneggiare Aspose.Cells: creare e personalizzare grafici a torta in Java

## Introduzione
Creare grafici visivamente accattivanti è un requisito comune quando si visualizzano dati in Excel. Che si tratti di presentare informazioni demografiche o di analizzare le tendenze di mercato, i grafici a torta offrono un modo chiaro per rappresentare dati proporzionali. Tuttavia, la configurazione di questi grafici a livello di codice può essere complessa. Questo tutorial vi guiderà nella creazione e personalizzazione di un grafico a torta Aspose.Cells utilizzando Java, semplificando il processo per gli sviluppatori.

**Cosa imparerai:**
- Imposta il tuo ambiente con Aspose.Cells per Java.
- Crea una nuova cartella di lavoro e accedi alle celle del foglio di lavoro.
- Inserire i dati in celle specifiche per preparare la creazione del grafico.
- Genera un grafico a torta da questi dati.
- Personalizza l'aspetto del tuo grafico a torta, inclusi colori, titoli e legende.

Prima di iniziare, assicurati di avere una conoscenza di base della programmazione Java e della gestione delle dipendenze di Maven o Gradle. Prepariamo il nostro ambiente!

## Prerequisiti
Per seguire questo tutorial, avrai bisogno di:
- **Kit di sviluppo Java (JDK)**: Versione 8 o superiore.
- **Ambiente di sviluppo integrato (IDE)**: Come IntelliJ IDEA o Eclipse.
- **Gestione delle dipendenze**: Utilizza Maven o Gradle per gestire le tue dipendenze.

### Librerie e dipendenze richieste
Assicurati di includere Aspose.Cells per Java nel tuo progetto utilizzando Maven o Gradle.

**Esperto**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Fasi di acquisizione della licenza
Aspose.Cells per Java è una libreria commerciale, ma puoi iniziare con una prova gratuita o richiedere una licenza temporanea. Visita [pagina di acquisto](https://purchase.aspose.com/buy) per esplorare le opzioni di licenza.

## Impostazione di Aspose.Cells per Java
Innanzitutto, assicurati che l'ambiente del progetto includa le librerie necessarie aggiungendole tramite Maven o Gradle, come mostrato sopra. Una volta incluse, puoi inizializzare Aspose.Cells:

```java
import com.aspose.cells.Workbook;

// Inizializza una nuova istanza della cartella di lavoro
Workbook workbook = new Workbook();
```

## Guida all'implementazione

### Creare e configurare una cartella di lavoro
La creazione di una cartella di lavoro è il primo passaggio in cui imposterai i tuoi dati.

#### Importa librerie
Assicurati che queste importazioni siano incluse nella parte superiore del tuo file:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Passaggio 1: creare un'istanza della cartella di lavoro
```java
// Crea un'istanza vuota della cartella di lavoro con cui lavorare.
Workbook workbook = new Workbook();
```
Questo passaggio inizializza il file Excel a livello di programmazione, consentendo di manipolarlo utilizzando le funzionalità di Aspose.Cells.

### Accedi o modifica le celle del foglio di lavoro
Successivamente, inserisci i dati nelle celle del foglio di lavoro che verranno utilizzati per il grafico a torta.

#### Passaggio 2: accedere a un foglio di lavoro e alle sue celle
```java
// Accedi al primo foglio di lavoro nella cartella di lavoro.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Inserire i valori campione utilizzati per un grafico a torta in celle specifiche.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Inserire i valori percentuali per un grafico a torta in celle specifiche.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
Qui puoi popolare il foglio di lavoro con i dati che rappresenteranno i diversi segmenti di un grafico a torta.

### Crea un grafico a torta

#### Passaggio 3: aggiungere un grafico a torta al foglio di lavoro
```java
// Crea un grafico a torta nel foglio di lavoro.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
Questo passaggio aggiunge un nuovo grafico a torta al foglio di lavoro nelle posizioni e nelle dimensioni specificate.

### Configurare serie e dati di grafici a torta

#### Passaggio 4: impostare la serie per il grafico
```java
// Configurare l'intervallo di dati della serie per il grafico.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Collega il titolo del grafico a torta a una cella contenente il testo del titolo.
pie.getTitle().setLinkedSource("D2");
```
Questo codice collega l'intervallo di dati e imposta la serie per il grafico a torta.

### Configurare l'aspetto della legenda e del titolo del grafico

#### Passaggio 5: personalizzare la legenda e il titolo del grafico
```java
// Imposta la posizione della legenda nella parte inferiore del grafico.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Imposta le proprietà del carattere per il titolo del grafico.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
La personalizzazione dell'aspetto migliora la leggibilità e l'attrattiva visiva.

### Personalizza i colori delle serie di grafici

#### Passaggio 6: modifica i colori dei segmenti della torta
```java
import com.aspose.cells.Color;

// Accedi e personalizza i colori dei singoli segmenti del grafico a torta.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
Queste impostazioni personalizzano il grafico in modo che si adatti a schemi di colori specifici.

### Adatta automaticamente colonne e salva cartella di lavoro

#### Passaggio 7: regolare la larghezza delle colonne e salvare il file
```java
// Adatta automaticamente tutte le colonne.
worksheet.autoFitColumns();

// Definire il percorso segnaposto della directory di output per il salvataggio della cartella di lavoro.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Salvare la cartella di lavoro modificata in un file Excel nella directory specificata.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
Infine, adatta automaticamente le colonne e salva la cartella di lavoro.

## Applicazioni pratiche
1. **Analisi demografica**: Utilizzare grafici a torta per visualizzare la distribuzione della popolazione in diversi paesi o regioni.
2. **Rapporti sulla quota di mercato**: Illustrare le quote di mercato di diverse aziende in un settore.
3. **Assegnazione del bilancio**: Visualizza come vengono allocati i budget tra i vari reparti all'interno di un'organizzazione.

Queste applicazioni dimostrano la versatilità e l'utilità di Aspose.Cells in scenari reali.

## Considerazioni sulle prestazioni
Per ottimizzare le prestazioni quando si utilizza Aspose.Cells:
- Ridurre al minimo l'utilizzo della memoria eliminando gli oggetti non più necessari.
- Utilizzare strutture dati efficienti per elaborare set di dati di grandi dimensioni.
- Profila la tua applicazione per identificare i colli di bottiglia.

Il rispetto delle best practice garantisce applicazioni fluide e reattive.

## Conclusione
Questo tutorial ti ha illustrato i passaggi per creare e personalizzare un grafico a torta utilizzando Aspose.Cells in Java. Con queste conoscenze, ora puoi applicare queste tecniche a diverse attività di visualizzazione dati nei tuoi progetti. Per ulteriori approfondimenti, considera l'approfondimento di altri tipi di grafico e delle opzioni di personalizzazione avanzate disponibili con Aspose.Cells.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}