---
category: general
date: 2026-10-07
description: Scopri come creare PNG da un intervallo ed esportare i dati come PNG
  in Java. Questa guida ti mostra come salvare l'immagine di un intervallo Excel utilizzando
  Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: it
lastmod: 2026-10-07
og_description: Crea PNG da un intervallo in Java ed esporta i dati come PNG con Aspose.Cells.
  Segui questo tutorial completo per salvare istantaneamente l'immagine dell'intervallo
  di Excel.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Crea PNG da un intervallo in Java – guida passo‑passo Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Come creare PNG da un intervallo in Java con Aspose.Cells
url: /it/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come creare PNG da un intervallo in Java con Aspose.Cells

Se hai bisogno di **creare PNG da un intervallo** in una cartella di lavoro Excel, questo tutorial ti mostra esattamente come farlo. Alla fine della guida sarai in grado di **esportare dati come PNG**, salvare un'immagine di un intervallo Excel e riutilizzare il file in report o pagine web.

Vedrai un programma Java completo e eseguibile che carica una cartella di lavoro, seleziona le celle desiderate, le rende come PNG e salva il risultato su disco. Non sono necessari strumenti esterni—Aspose.Cells gestisce tutto internamente.

## Cosa copre questo tutorial

* Prerequisiti e configurazione Maven per Aspose.Cells
* Caricamento di una cartella di lavoro che contiene una tabella pivot o qualsiasi intervallo di dati
* Definizione dell'esatto intervallo di celle da convertire
* Configurazione delle opzioni immagine per l'output PNG
* Rendering dell'intervallo e salvataggio del file PNG
* Problemi comuni e consigli per immagini di alta qualità

Dopo aver completato questi passaggi sarai in grado di **convertire un foglio di lavoro in PNG** per qualsiasi intervallo, sia esso una tabella semplice o un grafico pivot complesso.

## Prerequisiti

* Java 17 o successiva (il codice compila con JDK 11+)
* Maven 3.6+ (o Gradle se preferisci)
* Aspose.Cells per Java 23.12 o più recente – aggiungi la dipendenza mostrata di seguito
* Un file Excel esistente (`PivotWithStyle.xlsx`) che contiene l'intervallo che vuoi catturare

> **Consiglio professionale:** Se non disponi di una licenza, puoi richiedere una chiave di valutazione temporanea da Aspose. La libreria funziona in modalità valutazione senza configurazioni aggiuntive.

### Dipendenza Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Passo 1: Carica la cartella di lavoro che contiene l'intervallo target

La prima operazione è aprire il file Excel. Aspose.Cells legge il file in memoria senza richiedere Microsoft Office.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Perché è importante*: Caricare la cartella di lavoro ti dà accesso a fogli, celle e proprietà di impostazione pagina necessarie per il rendering.

## Passo 2: Accedi al foglio di lavoro che contiene l'intervallo

La maggior parte delle cartelle di lavoro ha un foglio predefinito all'indice 0, ma puoi anche usare il nome del foglio.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Se i tuoi dati si trovano su un foglio diverso, sostituisci `0` con l'indice appropriato o usa `workbook.getWorksheets().get("SheetName")`.

## Passo 3: Definisci l'intervallo di celle che desideri convertire

Puoi specificare qualsiasi area rettangolare usando la notazione A1. In questo esempio catturiamo `A1:D15`, che potrebbe essere una tabella pivot o un blocco di dati regolare.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Caso limite*: Quando l'intervallo include celle unite, Aspose.Cells espande automaticamente l'immagine per includere l'area unita.

## Passo 4: Prepara le opzioni immagine PNG

`ImageOrPrintOptions` ti consente di controllare formato, risoluzione e altri dettagli di rendering. Impostare il formato di salvataggio su PNG garantisce qualità senza perdita.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Aumentare i DPI è utile quando le celle di origine contengono caratteri piccoli o grafici dettagliati.

## Passo 5: Limita l'area di rendering all'intervallo selezionato

Assegnando l'intervallo come area di stampa, Aspose.Cells renderizza solo quelle celle e ignora il resto del foglio.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Se salti questo passaggio, l'intero foglio di lavoro verrà rasterizzato, il che può sprecare memoria e produrre un'immagine più grande.

## Passo 6: Renderizza l'intervallo e aggiungi l'immagine al foglio di lavoro (opzionale)

Se vuoi incorporare il PNG generato nuovamente nella cartella di lavoro (per scopi di anteprima), puoi aggiungerlo come immagine. Questo passaggio è opzionale per scenari di puro esportazione.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Perché potresti farlo*: Alcuni flussi di lavoro richiedono che l'immagine faccia parte della cartella di lavoro prima della distribuzione, ad esempio per creare un report stampabile che mescola celle native e immagini.

## Passo 7: Salva il file PNG su disco

Infine, scrivi l'immagine su un file. Il metodo `save` rispetta il formato specificato in `imageOptions`.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Quando il programma termina, `PivotImage.png` conterrà uno snapshot pixel‑perfect delle celle `A1:D15`.

### Output previsto

* Un file chiamato `PivotImage.png` situato in `YOUR_DIRECTORY`.
* L'immagine mostra esattamente il layout, i caratteri, i colori e i bordi dell'intervallo selezionato.
* Se l'intervallo di origine contiene una tabella pivot, l'immagine renderizzata include lo stesso stile e i valori calcolati visualizzati in Excel.

## Gestione di scenari comuni

### Esportazione di un intervallo non contiguo

Aspose.Cells non renderizza intervalli disgiunti in un'unica immagine. Per esportare più aree, crea immagini separate per ciascun intervallo e combinile successivamente con una libreria di elaborazione immagini (ad es., ImageIO).

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Salvataggio di un foglio di lavoro grande come PNG

Renderizzare un intero foglio che si estende per migliaia di righe può consumare molta memoria. Mitiga il problema:

* Riducendo i DPI (`imageOptions.setResolution(72)`) per un file più piccolo.
* Usando `setPageCount` per limitare il numero di pagine renderizzate.
* Esportando una pagina stampabile alla volta tramite `worksheet.getPageSetup().setPrintArea(...)`.

### Preservare le formule delle celle

Un'immagine PNG è un formato raster; le formule non vengono conservate. Se i consumatori successivi hanno bisogno dei dati grezzi, esporta anche l'intervallo come CSV o JSON usando `Range.exportDataTable()`.

## Esempio completo e eseguibile

Di seguito trovi la classe Java completa che puoi copiare‑incollare nel tuo IDE. Sostituisci `YOUR_DIRECTORY` con un percorso assoluto o relativo sulla tua macchina.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Esegui il programma con `mvn compile exec:java` (o lo strumento di build che preferisci). Dopo l'esecuzione, apri `PivotImage.png` per verificare il risultato.

## Conclusione

Ora sai come **creare PNG da un intervallo** in Java usando Aspose.Cells, **esportare dati come PNG** e **salvare l'immagine di un intervallo Excel** per qualsiasi scenario di reporting o condivisione. I passaggi—caricamento della cartella di lavoro, definizione dell'intervallo, configurazione delle opzioni immagine, impostazione dell'area di stampa e salvataggio del file—coprono l'intero flusso di lavoro per **convertire un foglio di lavoro in PNG** e **salvare le celle come PNG**.

### Prossimi passi

* Sperimenta con valori di `Resolution` diversi per bilanciare qualità e dimensione del file.
* Usa `ImageOrPrintOptions.setTransparent(true)` se ti serve un PNG con sfondo trasparente.
* Combina più immagini di intervalli in un unico PDF usando `PdfSaveOptions` per report multi‑pagina.
* Esplora l'esportazione verso altri formati raster (JPEG, BMP) cambiando `setSaveFormat`.

Sentiti libero di adattare questo modello a grafici, tabelle o interi fogli di lavoro. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci di implementazione alternativi nei tuoi progetti.

- [Come esportare un foglio di lavoro Excel in PNG usando Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convertire Excel in PNG usando Aspose.Cells per Java: Guida passo‑passo](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Creare un intervallo unito in Excel usando Aspose.Cells Java: Guida completa](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}