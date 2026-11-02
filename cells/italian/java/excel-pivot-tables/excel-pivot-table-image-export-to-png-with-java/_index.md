---
category: general
date: 2026-07-03
description: Esporta un’immagine di tabella pivot di Excel usando Java. Scopri come
  impostare il formato immagine PNG con Aspose.Cells passo dopo passo.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: it
og_description: Esportazione di immagini da una tabella pivot di Excel in Java spiegata.
  Segui questo tutorial per impostare rapidamente e in modo affidabile il formato
  immagine PNG.
og_title: immagine della tabella pivot di Excel – Guida Java per l'esportazione in
  PNG
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'immagine della tabella pivot di Excel: esporta in PNG con Java'
url: /it/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – Esporta una tabella pivot come PNG in Java

Hai mai avuto bisogno di trasformare un **excel pivot table image** in un PNG pronto per la condivisione ma non sapevi da dove iniziare? Non sei solo. In molte pipeline di reporting la tabella pivot è la protagonista, ma il resto del team vuole solo un'immagine statica. La buona notizia? Con poche righe di Java e Aspose.Cells puoi **set image format png** e ottenere esattamente ciò che ti serve.

In questa guida percorreremo l’intero processo: caricare un workbook, recuperare la prima tabella pivot, configurare le opzioni di esportazione e infine scrivere un file PNG nitido su disco. Alla fine avrai uno snippet riutilizzabile da inserire in qualsiasi progetto Java.

## Cosa imparerai

- Come caricare un workbook Excel dal file system.
- Come individuare una specifica tabella pivot in un foglio di lavoro.
- I passaggi esatti per **set image format png** per l’immagine esportata.
- Problemi comuni (tabelle pivot multiple, set di dati grandi) e come evitarli.
- Una classe Java pronta all’uso che puoi copiare‑incollare.

### Prerequisiti

- Java 8 o versioni successive installate.
- Libreria Aspose.Cells per Java (l’ultima versione al 2026‑07‑03).
- Un file Excel (`input.xlsx`) che contenga almeno una tabella pivot.
- Familiarità di base con Maven o Gradle per la gestione delle dipendenze.

---

## Passo 1: Aggiungi Aspose.Cells al tuo progetto

Prima di tutto, assicurati che il JAR di Aspose.Cells sia nel tuo classpath. Se usi Maven, inserisci questo nel tuo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Per Gradle, è altrettanto semplice:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Aspose offre una chiave di valutazione gratuita di 30 giorni. Registrati sul loro sito, poi aggiungi `License.setLicense("Aspose.Cells.lic");` all’inizio del tuo programma per sbloccare tutte le funzionalità.

## Passo 2: Carica il workbook e accedi alla tabella pivot

Ora apriremo il file Excel e recupereremo la prima tabella pivot. Il codice qui sotto fa esattamente questo, ed è deliberatamente difensivo: se il workbook non ha fogli o il foglio non contiene una tabella pivot lanceremo un’eccezione chiara.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Perché questi passaggi sono importanti

- **Loading the workbook** ci dà accesso alle strutture dati sottostanti; Aspose.Cells astrae l’analisi a basso livello di OpenXML.  
- **Accessing the worksheet** è necessario perché le tabelle pivot sono legate a un foglio specifico. Se hai più fogli, puoi iterare su `wb.getWorksheets()` e scegliere quello che contiene la pivot desiderata.  
- **Retrieving the pivot table** è il cuore dell’operazione. `ws.getPivotTables().get(0)` recupera la prima, ma puoi anche cercare per nome con `ws.getPivotTables().get("MyPivot")`.  
- **Setting image format png** (la keyword secondaria) indica ad Aspose.Cells di renderizzare l’output come PNG senza perdita. Questo formato preserva linee nitide e testo, ideale per i report.  
- **Exporting with `toImage`** scrive il file in una sola chiamata, gestendo automaticamente paginazione e scaling.

## Passo 3: Verifica l'output

Dopo aver eseguito il programma, vai nella cartella `YOUR_DIRECTORY` e dovresti vedere `pivot.png`. Aprilo con qualsiasi visualizzatore di immagini—nota le linee della griglia nitide e il layout esatto che vedi in Excel. Se l’immagine appare sfocata, aumenta il DPI in `imgOpt.setResolution()`; 300‑600 funziona bene per risorse di stampa di alta qualità.

![excel pivot table image exported as PNG](excel-pivot-table-image.png "excel pivot table image exported as PNG")

*Testo alternativo dell'immagine:* **excel pivot table image exported as PNG**

## Gestione di più tabelle pivot

E se il tuo foglio contiene più di una tabella pivot? Lo snippet sopra prende la prima, ma puoi iterare:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Questo ciclo produrrà `pivot_0.png`, `pivot_1.png`, ecc., ciascuno rappresentante una diversa tabella pivot. Ricorda di **set image format png** una sola volta prima del ciclo; la stessa istanza di `ImageOrPrintOptions` può essere riutilizzata.

## Casi limite e consigli

| Situazione | Cosa controllare | Correzione suggerita |
|------------|------------------|----------------------|
| **Large pivot (many rows/columns)** | Il PNG può diventare molto grande, causando pressione sulla memoria. | Usa `imgOpt.setOnePagePerSheet(false)` per suddividere su più pagine, oppure riduci il DPI. |
| **Hidden rows/columns** | Aspose rispetta la visibilità; i dati nascosti non appariranno. | Rendi visibili programmaticamente con `ws.showRows(start, count, true)`. |
| **Custom styles (fonts, colors)** | Alcuni font aziendali potrebbero non essere renderizzati se non installati sul server. | Incorpora il font nella JVM o usa font di sistema tramite `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)`. |
| **Different output format needed later** | Potresti volere JPEG o BMP. | Cambia `imgOpt.setImageFormat(ImageFormat.JPEG)`—lo stesso codice funziona, basta un valore enum diverso. |

## Esempio completo (copia‑incolla)

Di seguito trovi l’intera classe, pronta per la compilazione. Incollala in `PivotTableToPng.java`, aggiusta i percorsi e esegui `javac PivotTableToPng.java && java PivotTableToPng`.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Eseguilo e avrai un **excel pivot table image** salvato come file PNG—esattamente ciò che la guida prometteva.

---

## Conclusione

Abbiamo appena coperto tutto ciò che ti serve per **export an excel pivot table image** usando Java, e ti abbiamo mostrato esattamente come **set image format png** con Aspose.Cells. Dal caricamento del workbook alla gestione dei casi limite, la soluzione è compatta, affidabile e pronta per la produzione.

Qual è il prossimo passo? Prova a esportare più pivot in batch, sperimenta impostazioni DPI diverse per risorse pronte alla stampa, o passa al formato JPEG per immagini ottimizzate per il web. Potresti anche esplorare l’incorporamento del PNG in un report PDF—Aspose.PDF lo rende un gioco da ragazzi.

Hai una variante nel tuo flusso di lavoro o un ostacolo? Lascia un commento e risolveremo insieme. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità aggiuntive dell’API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Esporta il workbook Excel come immagine usando Aspose.Cells per Java: Guida passo‑passo](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Come aggiornare la fonte della tabella pivot Excel con Aspose.Cells per Java: Guida completa](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Come creare un grafico Excel con linea di tendenza ed esportarlo come immagine usando Aspose.Cells per Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}