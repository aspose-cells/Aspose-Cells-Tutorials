---
category: general
date: 2026-10-10
description: Scopri come esportare un intervallo di Excel come immagine in Java usando
  Aspose.Cells. La guida copre anche l'esportazione di celle selezionate come immagine
  e il salvataggio del foglio di lavoro Excel come immagine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: it
lastmod: 2026-10-10
og_description: Esporta un intervallo di Excel come immagine in Java con una soluzione
  passo‑passo. Include l’esportazione delle celle selezionate come immagine e il salvataggio
  del foglio di lavoro Excel come immagine.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Esporta un intervallo di Excel come immagine in Java – guida completa di
  Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Come esportare un intervallo Excel come immagine in Java con Aspose.Cells
url: /it/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare un intervallo di Excel come immagine in Java con Aspose.Cells

Se hai bisogno di **esportare un intervallo di Excel come immagine**, questo tutorial ti guida attraverso una soluzione Java completa usando la libreria Aspose.Cells. Imparerai anche come **esportare celle selezionate come immagine** e come **salvare un foglio di lavoro Excel come immagine** per scopi di reportistica o documentazione.

Esportare una parte di una cartella di lavoro in un'immagine elimina la necessità di strumenti di screenshot di terze parti e garantisce risultati pixel‑perfect. Alla fine di questa guida avrai un metodo riutilizzabile che scrive un PNG (o qualsiasi formato supportato) direttamente su disco, pronto per l'inclusione in PDF, email o pagine web.

## Prerequisiti

* Java 17 o versioni successive installate.
* Maven 3.8+ (o un altro strumento di build che possa gestire le dipendenze Maven).
* Una licenza Aspose.Cells per Java (la valutazione gratuita funziona ma aggiunge una filigrana).
* Un file Excel di esempio (`input.xlsx`) posizionato in una directory nota.

Le sezioni seguenti presumono che tu sia a tuo agio con lo sviluppo Java di base e la configurazione di un progetto Maven.

## Passo 1: Aggiungere Aspose.Cells al tuo progetto

Aggiungi la dipendenza Maven di Aspose.Cells al tuo `pom.xml`. Questa libreria fornisce le classi `Workbook`, `Worksheet` e `ImageOrPrintOptions` utilizzate nell'esempio di codice.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Suggerimento professionale:** Mantieni il numero di versione aggiornato; le versioni più recenti aggiungono supporto a nuovi formati e miglioramenti delle prestazioni.

## Passo 2: Creare un metodo di utilità per esportare un intervallo

Incapsulare la logica di esportazione in un metodo rende più semplice il riutilizzo tra progetti e la gestione di casi particolari come celle unite o righe nascoste.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Perché questo metodo è importante

* **Separazione delle responsabilità:** Caricamento, configurazione delle opzioni ed esportazione sono chiaramente separate.
* **Flessibilità:** Puoi cambiare il formato dell'immagine o il DPI senza modificare la logica di base.
* **Gestione degli errori:** Lanciare `Exception` permette al chiamante di decidere se registrare, riprovare o abortire.

## Passo 3: Chiamare il metodo con parametri reali

Di seguito è riportato un metodo `main` minimale che dimostra come **esportare celle selezionate come immagine** e anche come **salvare un foglio di lavoro Excel come immagine** utilizzando l'intervallo completo del foglio.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Output previsto

Eseguendo il programma vengono creati due file PNG:

* `range.png` – un'immagine che contiene solo le celle **A1:G20**.
* `full_sheet.png` – un'immagine dell'intera area utilizzata del primo foglio di lavoro, effettivamente **salvando il foglio di lavoro Excel come immagine**.

Puoi aprire i file con qualsiasi visualizzatore di immagini per verificare che il layout visivo corrisponda alla visualizzazione di Excel, includendo bordi delle celle, colori e celle unite.

## Passo 4: Gestire casi particolari comuni

### 1. Celle unite

Aspose.Cells preserva automaticamente l'aspetto delle celle unite, ma se hai bisogno di controllare il rendering, imposta `options.setOnePagePerSheet(true)` per forzare l'intero foglio su una singola pagina prima dell'esportazione.

### 2. Righe o colonne nascoste

Per impostazione predefinita, le righe/colonne nascoste non vengono renderizzate. Per includerle, abilita:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Intervalli grandi e consumo di memoria

Esportare intervalli molto grandi può consumare molta memoria. Se incontri `OutOfMemoryError`, considera:

* Ridurre il DPI (`options.setHorizontalResolution(150)`).
* Esportare l'intervallo in blocchi più piccoli e unire le immagini con una libreria grafica.

## Passo 5: Verificare il risultato programmaticamente (opzionale)

Se il tuo processo a valle deve confermare che l'immagine è stata generata correttamente, puoi caricare il PNG usando `javax.imageio.ImageIO` e controllare le sue dimensioni:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Una larghezza e altezza diverse da zero indicano un'esportazione riuscita.

## Conclusione

Ora sai come **esportare un intervallo di Excel come immagine** in Java, come **esportare celle selezionate come immagine** e come **salvare un foglio di lavoro Excel come immagine** usando Aspose.Cells. Il metodo riutilizzabile `exportRangeAsImage` astrae la complessità, ti permette di controllare la qualità dell'immagine e funziona con qualsiasi indice di foglio o intervallo di celle.

I prossimi passi che potresti esplorare:

* Converti il PNG in PDF con Aspose.PDF per la reportistica.
* Elabora in batch più cartelle di lavoro in una directory.
* Integra l'esportazione dell'immagine in un endpoint REST Spring Boot così i client possono richiedere immagini su richiesta.

Sentiti libero di sperimentare con diversi formati immagine (`ImageFormat.JPEG`, `ImageFormat.BMP`) e impostazioni DPI per soddisfare i requisiti visivi del tuo progetto. Buon coding!

## Cosa dovresti imparare dopo?

I seguenti tutorial coprono argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare funzionalità API aggiuntive ed esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}