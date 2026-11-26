---
category: general
date: 2026-11-25
description: Esporta Excel in SVG con Aspose.Cells in Java – una guida passo passo
  per salvare Excel come SVG e creare un'immagine vettoriale.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: it
lastmod: 2026-11-25
og_description: Esporta Excel in SVG con Aspose.Cells in Java. Scopri come salvare
  Excel come SVG e generare immagini vettoriali di alta qualità in poche righe di
  codice.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Esporta Excel in SVG con Java – tutorial completo di Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Come esportare Excel in SVG usando Aspose.Cells in Java
url: /it/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Come esportare Excel in SVG con Aspose.Cells in Java

Se devi **esportare Excel in SVG**, questa guida ti mostra come farlo con Aspose.Cells per Java. Imparerai a **salvare Excel come SVG** e a generare un'immagine **vettoriale** di alta qualità in poche righe di codice.

Esportare una cartella di lavoro Excel in un file SVG ti consente di incorporare il foglio in pagine web, report o qualsiasi ambiente che preferisca grafiche scalabili. Il formato SVG conserva caratteri, colori e bordi delle celle senza la pixelatura tipica delle immagini raster.

## Prerequisiti

Prima di iniziare, assicurati di avere:

* Java 17 o versioni successive installate.  
* Una licenza attiva di Aspose.Cells per Java (o una chiave di valutazione temporanea).  
* Un progetto Maven o Gradle dove poter aggiungere la dipendenza di Aspose.Cells.

Aggiungi la libreria Aspose.Cells al tuo progetto:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Esporta Excel in SVG – passo‑per‑passo

Il processo consiste in tre semplici passaggi: caricare la cartella di lavoro, configurare le opzioni di esportazione SVG e salvare il risultato. Ogni passaggio è spiegato di seguito.

### Passo 1: Carica la cartella di lavoro contenente i dati

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Perché è importante:**  
`Workbook` è l'oggetto centrale in Aspose.Cells. Caricare il file una sola volta ti dà accesso a tutti i fogli, gli stili e gli oggetti incorporati, che l'esportatore SVG renderizzerà successivamente.

### Passo 2: Imposta le opzioni di esportazione immagine per SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Perché è importante:**  
`ImageOrPrintOptions` ti consente di controllare il formato di output. Selezionare `ImageFormat.SVG` garantisce che il risultato sia un **immagine vettoriale** anziché una bitmap. Abilitare `OnePagePerSheet` evita interruzioni di pagina all'interno di un foglio, cosa solitamente desiderata quando l'SVG verrà visualizzato in una vista web.

### Passo 3: Salva la cartella di lavoro come file SVG

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Perché è importante:**  
Il metodo `save` combina la cartella di lavoro caricata con le `exportOptions` configurate. La chiamata scrive un file SVG pienamente conforme che può essere aperto nei browser, in Inkscape o in qualsiasi editor che supporti i vettoriali.

## Esempio completo eseguibile

Unendo i tre passaggi ottieni un programma autonomo che puoi compilare ed eseguire subito:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Output previsto**

L'esecuzione del programma stampa:

```
Export complete: Excel saved as SVG.
```

Troverai `WithVariationSelectors.svg` in `C:/Output`. Aprendo il file in un browser vedrai il foglio di lavoro renderizzato come grafica scalabile, con testo, bordi e colori delle celle preservati.

## Varianti comuni e casi particolari

| Situazione | Regolazione consigliata |
|------------|--------------------------|
| **Foglio di lavoro multipli** | Scorri `workbook.getWorksheets()` e chiama `save` per ogni foglio, aggiungendo opzionalmente il nome del foglio al nome del file. |
| **Cartelle di lavoro di grandi dimensioni** | Incrementa `exportOptions.setRenderThreadCount(int)` per utilizzare il rendering parallelo, riducendo i tempi di conversione. |
| **DPI personalizzato** | Chiama `exportOptions.setHorizontalResolution(int)` e `exportOptions.setVerticalResolution(int)` per controllare la scala del viewBox dell'SVG. |
| **Incorporamento dei font** | Imposta `exportOptions.setExportFontAsSVG(true)` per includere le definizioni dei font direttamente nell'SVG, garantendo la fedeltà visiva su macchine senza i font originali. |
| **File protetti da password** | Fornisci la password al momento del caricamento: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Consigli professionali

* **Evita il fallback raster** – Se un foglio contiene grafici complessi, verifica che compaiano come elementi vettoriali nell'SVG. In caso contrario, abilita `exportOptions.setExportChartAsSVG(true)`.  
* **Prestazioni** – Per conversioni in batch, riutilizza un'unica istanza di `ImageOrPrintOptions` invece di crearne una nuova per ogni file.  
* **Test** – Convalida l'SVG generato con un validatore online (ad es., W3C SVG Validator) per individuare eventuali markup malformati in anticipo.

## Verifica della conversione

Puoi confermare programmaticamente che il file di output sia effettivamente un SVG:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

La presenza dell'elemento radice `<svg>` indica un'operazione di **convert Excel to SVG** riuscita.

## Conclusione

Questo tutorial ha dimostrato come **esportare Excel in SVG** usando Aspose.Cells per Java. Caricando la cartella di lavoro, configurando `ImageOrPrintOptions` per SVG e chiamando `save`, puoi **salvare Excel come SVG** e ottenere una conversione pulita da **Excel a immagine vettoriale**. Da qui potrai incorporare l'SVG nelle pagine web, includerlo nella documentazione o elaborarlo ulteriormente con qualsiasi strumento di grafica vettoriale.

### Cosa esplorare dopo

* **Esporta Excel come PNG o JPEG** – modifica `exportOptions.setImageFormat(ImageFormat.PNG)` per ottenere output raster.  
* **Converti Excel in PDF** – usa `PdfSaveOptions` per documenti stampabili.  
* **Elaborazione batch** – combina il codice sopra con un watcher del file system per **convertire automaticamente Excel in SVG** per ogni nuova cartella di lavoro in una cartella.

Sentiti libero di sperimentare con le opzioni e lascia che la flessibilità di Aspose.Cells trasformi i tuoi dati Excel in qualsiasi formato visivo tu necessiti. Buon coding!

## Cosa dovresti imparare dopo?

I tutorial seguenti trattano argomenti strettamente correlati che si basano sulle tecniche dimostrate in questa guida. Ogni risorsa include esempi di codice completi e funzionanti con spiegazioni passo‑per‑passo per aiutarti a padroneggiare ulteriori funzionalità dell'API e a esplorare approcci alternativi di implementazione nei tuoi progetti.

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel to SVG – Step‑by‑Step Java Guide](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}